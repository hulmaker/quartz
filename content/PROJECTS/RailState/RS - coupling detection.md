
![[Recording 20250823170000.m4a]]

![[Recording 20250823170007.m4a]]
```bash
export NEPTUNE_API_TOKEN="eyJhcGlfYWRkcmVzcyI6Imh0dHBzOi8vYXBwLm5lcHR1bmUuYWkiLCJhcGlfdXJsIjoiaHR0cHM6Ly9hcHAubmVwdHVuZS5haSIsImFwaV9rZXkiOiIzOGNhMDMxYS03NmUyLTQ0NDQtYjQ4ZC1lODg4NTY1YWRmMjkifQ=="

./launch_training_instance.sh "configs/learn_car-features_mini.json" "feature/sc-57620/update-scripts-car-separator"

```

Doc resources:
- [startup script](https://cloud.google.com/compute/docs/instances/startup-scripts)
- [image manual baking](https://cloud.google.com/compute/docs/images/image-management-best-practices#manual_baking)

## Create instance

1. create the instance.
```
export INSTANCE_NAME=car-features-training-manual
export ZONE=us-central1-a
export PROJECT=railstate-development

gcloud compute instances create $INSTANCE_NAME \
	--project $PROJECT --zone=$ZONE \
    --metadata=startup-script='' \
    --machine-type=n1-standard-4 \
    --image="projects/deeplearning-platform-release/global/images/common-cu124-v20241224" \
    --accelerator=type=nvidia-tesla-t4,count=1 \
    --max-run-duration=2d \
    --instance-termination-action=STOP \
    --maintenance-policy=TERMINATE \
    --boot-disk-size=300GB \
    --service-account=training-instance@railstate-development.iam.gserviceaccount.com \
    --scopes=cloud-platform,logging-write,monitoring-write
```
2. Connect with ssh: `gcloud compute ssh --zone "$ZONE" "$INSTANCE_NAME" --project "$PROJECT"`
3. copy the ssh key: `gcloud secrets versions access latest --secret="cloudbuild_github_ssh_key" | pbcopy` and replace <SSH_KEY> in startup.sh
4. Copy the script to instance `gcloud compute scp "startup.sh" "$INSTANCE_NAME":~/ --zone="$ZONE" --project="$PROJECT"`
5. Connect to the instance with ssh `gcloud compute ssh --zone "$ZONE" "$INSTANCE_NAME" --project "$PROJECT"`
6. Run the script as root `sudo sh startup.sh`
7. Stop the instance: `gcloud compute instances stop INSTANCE_NAME --zone=ZONE --project=PROJECT_ID`
8. delete the instance but keep the disk to create an image later
```
gcloud compute instances delete "$INSTANCE_NAME" \
  --zone="$ZONE" \
  --project="$PROJECT" \
  --keep-disks=boot \
  --quiet
```
9. Create image from the source disk
```
export IMAGE_NAME="gpu-custom-image-manual"

# Delete the image if it exists first
gcloud compute images delete $IMAGE_NAME --project=$PROJECT --quiet

gcloud compute images create "$IMAGE_NAME" \
  --project="$PROJECT" \
  --source-disk="$INSTANCE_NAME" \
  --source-disk-zone="$ZONE" \
  --family="custom-gpu-images"
```
10. Delete the source disk: `gcloud compute disks delete "$INSTANCE_NAME" --zone="$ZONE" --project="$PROJECT" --quiet`
11. Run the launch script with updated image-name

**IMPORTANT**: STOP the instance

**NOTE**: the launch script does not work, but If I run all these commands manually it works.
Also set neptune api key and project in the config: project "erik.hulmak/car-feature-detector"


### Neptune
NEPTUNE_API_TOKEN: ...
project: erik.hulmak/car_feature_detector

### Additional packages we need to install before running on localhost
```bash
# Additional dependencies, install yolo
pip install openmim imagecorruptions albumentations==1.3.1
pip install torch==1.10.2 torchvision==0.11.3 -f https://download.pytorch.org/whl/cu118/torch_stable.html

mim install "mmengine>=0.6.0" "mmcv>=2.0.0rc4,<2.1.0" "mmdet>=3.0.0,<4.0.0" mmyolo
```

### random odkladiste
```bash
INSTANCE_NAME=car-features-training-manual
ZONE=us-central1-a
PROJECT=railstate-development
SCRIPT="run_training.sh"
BRANCH=$(git rev-parse --abbrev-ref HEAD)
CONFIG="configs/learn_couplings.json"

gcloud compute ssh $INSTANCE_NAME --project $PROJECT --zone=$ZONE 

gcloud storage buckets list
--impersonate-service-account=training-instance@railstate-development.iam.gserviceaccount.com

gcloud compute ssh $INSTANCE_NAME --project $PROJECT --zone=$ZONE --command="sudo -u ubuntu bash -c \"cd && cp /tmp/$SCRIPT . && chmod +x ~/$SCRIPT && tmux new-session -d -s training && tmux send-keys -t training '~/$SCRIPT  $CONFIG $BRANCH' C-m\""
```

## Tasks
- [x] Initial dataset with difficult samples
- [x] Articulated vehicular flatcars - how to find them
- [x] Make it possible to train car boxes and not couplings, or both at the same time
- [ ] experiment with augmentation - discover how it is done and adjust it as you see fit
- [x] e2e trigger - what it should do?
- [x] check if the model you trained yesterday exists
	- does not exist, failed with: Cannot find best model in -- probably needs more batches


`_process_annotation` v `dataset_adapter.py` dela:
- extract_annotation_results - to vytahne bboxy, ale nerozlisuje mezi from_name, takze jsou pomichane boxy pro coupling a pro car_box
- annotation_results_to_training_task - validuje, ze vsechny boxy jsou z jednoho from_name
	- misto toho by mohla byt jedna classification uloha per from_name
	- nebo by v configu bylo from_name a byl by filter jen na boxy z tohoto from_name. uloha by pak byla pouze na toto


```sql
-- select 1000 articulated vehicular flat cars
-- see Umler Appendix I for umet explanation
-- there are only cars with 2 platfoms, not more... (and it's string)
SELECT equipment_id, umet, a020 as unit_count
FROM third_party.umler
WHERE umet LIKE 'V%' AND a020 = '2'
ORDER BY RANDOM()
LIMIT 1000;

-- distinct vehicular cars we spotted in the last month or so
with recent_fcars as (
	select distinct ocr_umler_number from trains.car_sightings where car_type = 'Vehicular Flatcar' and detection_time > '2025-08-01';
),
multiplatfom_fcars as (
	SELECT equipment_id, umet, a020 as unit_count
	FROM third_party.umler
	WHERE umet LIKE 'V%' AND a020 = '2';
)
select * from recent_fcars as r
join multiplatform_fcars m on m.equipment_id = r.ocr_umler_number

select count(*) from trains.car_sightings where detection_time > '2025-08-01' and car_type = 'Vehicular Flatcar';

-- je 4286 articulated vehicular flat cars
SELECT count(*) FROM third_party.umler WHERE umet LIKE 'V%' AND a020 = '2';

select id, sighting_id, ocr_umler_number, car_type, detection_time from trains.car_sightings where ocr_umler_number in ('AOK 0000501623', 'NOKL0000798471', 'NOKL0000798438', 'FXE 0000518267', 'AOK 0000504534', 'AOK 0000504505', 'BTTX0000880194', 'AOK 0000502966', 'FXE 0000518240', 'BTTX0000880413', 'AOK 0000504588');
```

v server_db repo je script pro generovani csv filu pro stack cars
v datasetu warningy - zastoupeni intermodalu a simple
Blbosti kdyz `train_sightings.car_count_estimate <= 3`


training/car_feature_detector/configs/yolov8_m_car_features_template.py


typy caru co muzou mit vic platforem:
- mow
- vehicular stack car
- stack car
Jak je hledat pro separator dataset?
- v umler db jde podle car id najit pocet platforem.
- Pro takove cary si jde v car_sightings najit panorama_position - podle toho identifikovat framy co nas zajimaji
- Z tech framu najit ty kde bude nejspis coupling a includnout ho v datasetu



indices for building a dataset with hard cases:
- sightings with less than 3 cars
- warnings: W_CARS_LOST_DURING_CAR_SEPARATION

given list of sensors:
select 5 train sightings per sensor per:
	- nighttime TRUE/FALSE
	- intermodal/normal
