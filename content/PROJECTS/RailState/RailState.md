---
tags:
  - on/business
email: erik.hulmak@eyen.se
link: https://www.railstate.com/
company: RailState
---

[[_People#People - RailState]]

**Coding standards**:
`mypy program.py --config-file=.mypy.ini`
```bash
cd cv_pipeline
export PYTHONPATH=$(pwd):$(pwd)/external/shared-util-py/:$(pwd)/external

cd cv_pipeline-training
export PYTHONPATH="$(pwd):$(pwd)/external:$(pwd)/external/cv_pipeline:$(pwd)/external/cv_pipeline/external:$(pwd)/external/cv_pipeline/external/shared-util-py:$(pwd)/external/label_studio"

# run checks
python external/shared_cicd/check_modified_files.py --check "pylint"
python external/shared_cicd/check_modified_files.py --check "mypy --install-types --non-interactive"
```

**Merge**:
- run triggers: fe2e, cv-pipeline-faster-e2e, cv-pipeline-train-id-test
**Database**:
- links: [schema](https://github.com/RailState/server-db/blob/prod/schema/schema.png), [password for eyen_ro](https://docs.google.com/spreadsheets/d/1ALBaxQemTQq_Bgdetszrr4PJV642Xwtx0JFUCa16l3U/edit?gid=0#gid=0), [cloud-sql-proxy releases](https://github.com/GoogleCloudPlatform/cloud-sql-proxy/releases)
- client: beekeeper-studio
- proxy set in docker container
```bash
# run DEV sql-proxy in docker
./cloud-sql-proxy railstate-development:us-central1:railstate-dev-9 -a 0.0.0.0 -p 5432
# run PROD sql-proxy in docker
./cloud-sql-proxy named-purpose-220220:us-central1:hk-fact-01 -a 0.0.0.0 -p 5432
# run PROD sql-proxy on instance
cloud_sql_proxy -instances=named-purpose-220220:us-central1:hk-fact-01=tcp:5432

# connect to the prod database with psql:
PGPASSWORD=$(gcloud secrets versions access latest --secret=psql_eyen_ro_password) psql -h localhost -p 5432 -U eyen_ro -d train_observation_dev
```


**Deployment**:
- triggers
- query pro selekci devicu: `"((PROD & architecture=b) & currentState.sensorId between 200 and 220),b-0260"`  - produkcni devicy (devicy co nemaji DEV tag a jejich status je "deployed"), ale jen architekturu B a jen pro sensory s id mezi 200 a 220 (vcetne) a pak se k nim jeste prihodi b-0260.

**Task Notes**
- [[RS - 2024-11-01 - Duplicate Car Ids]]
- [[RS - 2024-11-18 Hazmat Stickiness]]
- [[RS asdf]]
sightingy z tohoto roku

# Annotation job
download `google_application_credentials`: [label_studio_service_account](https://console.cloud.google.com/security/secret-manager/secret/label_studio_service_account/versions?inv=1&invt=AbpYGQ&authuser=2&project=railstate-development)
copy your `label_studio_api_key` from: [label studio settings](https://labeling.development.railstate.com/user/account)
- [car features instructions](https://docs.google.com/document/d/1l7DrRrNtlx7fmWE_CATEGMcA-A6hewmibWdWAgUvMY8/edit?tab=t.0#heading=h.7sebe4xw5kdc)
- [hazmat instructions](https://docs.google.com/document/d/1yuI4efuFiXkpSO9J-1mSwtOUufCRiM8T/edit#heading=h.o7xoxvy2derq)
Send annotation request mails to:
```
TO: shankar@infosearchbpo.com, srinivasan@infosearchbpo.com
CC: ondrej, data-labeling@railstate.com
```
# Useful commands
**Dev project name**: `railstate-development`
**Prod project name**: `named-purpose-220220`


```bash
# Sign in
gcloud config set account erik.hulmak@eyen.se && gcloud config set project railstate-development && gcloud auth application-default login

# Get google secret:
gcloud secrets versions access latest --secret="SendGrid-API-key" --project="named-purpose-220220"

# Mount to device sshfs
sshfs -o ProxyJump=railstate-ssh-tunnel -p 10413 rs-ops@localhost:/ mnt

# See recent google builds
gcp-builds

# See the build logs
gcloud builds log BUILD_ID
```


# Compute Instances - TrainId/Panorama server
[Alerting Policies](https://console.cloud.google.com/monitoring/alerting/policies?pli=1&invt=AbzvSw&inv=1&authuser=2&project=named-purpose-220220) - you can see Train-id queue, pano queue, etc...
[Pub/Sub train id queue](https://console.cloud.google.com/monitoring/alerting/policies/16738530466614773647?pli=1&invt=AborSQ&inv=1&authuser=2&project=named-purpose-220220) - you don't want to go over 300 unacked messages
```bash
# connect to the TrainId instance
gcloud compute ssh cv-pipeline-01
# connect to the panorama instance
gcloud compute ssh cv-pipeline-07
# NOTE: cv-pipeline-08 also exists (not sure what's there)

# change the user
sudo su ubuntu
# connect to tmux
tmux a
# cv_pipeline repo here
cd /home/ubuntu/eyen-cv-pipeline
# logs are available here:
cd /home/ubuntu/pipeline_results_train_id
```

# Connect to device
Use either script: [device-ssh](https://github.com/RailState/device-infrastructure/blob/prod/deployment/device-ssh) (did not work last time), or connect manually
```bash
gcloud config set account erik.hulmak@eyen.se && gcloud config set project named-purpose-220220

# connect to the tunnel instance
gcloud compute ssh ssh-reverse-tunnel-01 -- -p 9211
# switch to user that opens tunnels to devices
sudo su incoming-ssh
# connect to the device - XXX is a seriove cislo
ssh -p 10XXX rs-ops@localhost
ssh -p 10413 rs-ops@localhost

# sshfs na slozku (musis byt pripojen pomoci device-ssh aby se otevrel port)
sshfs -o ProxyJump=railstate-ssh-tunnel -p 10413 rs-ops@localhost:/ _mnt

# rsync upload. (it's important to use ./event since event contains :)
export event="event_401_2025_05_03_13:33:59.267051"
rsync -P -ra -e 'ssh -p 10401' "./${event}" "rs-ops@localhost:/data/cv-pipeline/tag_train_detection/"

# download
rsync -P -ra -e 'ssh -p 10413' "rs-ops@localhost:'/tmp/tag_event_401_2025_09_26_05:05:18.858229_compressed'" "/tmp"
```
then you can clone `cv_pipeline` repo to `/data/git/repo`

## Logs from device
```bash
# service log (short term)
journalctl -u sensor_manager.service

# inspect syslog on device (long term, some exceptions can be there)
less /var/log/syslog

# logging on cloud (loaded from syslog using fluentbit some data might be missing if the log file overflows.)
https://cloudlogging.app.goo.gl/5zy7B1kgPNVGVLJh8
```
# connect to izar - tag reader UI
- open tunel with device-ssh command, port is device id
- run the command below, change the port to device id
`ssh -p 10413 rs-ops@localhost -L 44444:izar-2025c2.local:80`

Jak se pripojit k IZAR web-ui:  

- `device-ssh 413` v prvnim terminalu
- `ssh -p 10413 rs-ops@localhost -L 44444:izar-2025c2.local:80` v druhem terminalu
- browser [http://localhost:44444/](http://localhost:44444/)
    - user `web`
    - password `radio`

[grafana device dashboard](https://grafana.internal.railstate.com/d/pNxNhxJ4k/device-system-and-cv-stats?orgId=1&var-device_id=c-0413&from=now-12h&to=now)
```bash
# search for all lidar related messages in todays logs - make sure there are no "No available lidar measurements."
sudo journalctl -u sensor_manager_tag_reader.service --since "today" | grep lidar

# Hotfix exception that restarts the service when there are no lidar measurements
sudo journalctl -u sensor_manager_tag_reader.service --since "today" | grep "No valid distance"
```


# Downloading Images from LTE device (413)
```bash
event="tag_event_401_2025_10_16_05:21:33.663333"
outdir="/tmp/detection_event_preview"
target="${outdir}/${event}.zip"

cd /data/git/eyen-cv-pipeline
export PYTHONPATH=$(pwd):$(pwd)/external/shared-util-py/:$(pwd)/external
/usr/bin/python3 -m bin.generate_detection_event_preview \
	"/data/archive/DETECTION_EVENT/$event" "$outdir" \
	--skip=2 --quality=50 --width=1280
ls -lh $outdir

# on local machine
rsync -P -ra -e 'ssh -p 10413' "rs-ops@localhost:'$target'" "/tmp"
unzip "/tmp/${event}.zip" -d "/tmp/$event"
cd "/tmp/$event"
```

# Kotlin - server API
```bash
# Token si muzes stahnout v profile na UI
export TOKEN="eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJhcGkucmFpbHN0YXRlLmNvbSIsImlzcyI6InJhaWxzdGF0ZS5jb20iLCJ1aWQiOiJBRzRVUU1hN3RXVmNxbUFkZVlURk9PSGkySnMxIiwidGlkIjoidGVzdC10b2tlbiJ9.FyRZbklSAurm1wv4khyD2B3yWLx96BKSBTMDAUJJCpc"

curl -v -H "Authorization: Bearer $TOKEN" https:///api.railstate.com/api/v3/documentation/html?public=false > /tmp/api_documentation.html
# Na test api je adresa test.railstate.com
```


# Umler db Update
1. https://github.com/RailState/server-db/tree/prod/migrations/umler
2. patch umler_types and platform_counts in cv_pipeline: https://github.com/RailState/cv_pipeline/tree/dev/cv_pipeline/ocr/umler
3. run fe2e

# Testing new models (rs-prod)

1. `cv-pipeline/datastorage_requirements.txt` set correct model path.
2. Update triton server on `cv-pipeline-testing-triton`see [[PROJECTS/RailState/RailState#Deploy new model| Deploy new model - Update triton server]]

Then connect to `cv-pipeline-02` or `cv-pipeline-03`:
1. `gcloud compute ssh cv-pipeline-0X --project named-purpose-220220` , then `sudo su -- ubuntu`
2. Backup `cv_pipeline/configs/pano_pipeline_server_triton_on_06.json` and change `triton_url` to: `cv-pipeline-testing-triton.us-central1-c.c.named-purpose-220220.internal:8001`
3. In **tmux**: Stop and run the pano pipeline (either in the current branch or in yours, depending whether the changes are model-only)
4. running pano: `CLOUDPATHLIB_FILE_CACHE_MODE=cloudpath_object PYTHONPATH=$(pwd):$(pwd)/external/shared-util-py/:$(pwd)/external  PROMETHEUS_MULTIPROC_DIR=$(mktemp -d) python3 bin/process_panoramas_server_triton.py configs/pano_pipeline_server_triton_on_testing.json`
5. Write to cv-pipeline prod kde to testuju, nech to bezet a koukni na par sightingu
Keep it running for 20 minutes and then revert back. See few sightings in debug UI (filter by instance), if it's ok, run again and see numbers in grafana. Focus on aplus devices


# Deploy new model

**1. Preparation**: `cv-pipeline` merge
- update `cv_pipeline/verion.py`, and `cv_pipeline/datastorage_requirements`
- _if building deb packages_: you need to update their versions too, do it after you build them and then merge. No need to do it now.
- merge to **prod** with `merge commit` strategy (do not squash!)
- wait for `fe2e` to finish (you can build the apt package during that time)

**2. Deploy to CANARY**:
1. Message to `cv-pipeline-prod` on slack - maybe some wants to merge something or exclude some sensor from updating.
2. sensor manager deb: [cv_pipeline/deployment/README.md#cloud](https://github.com/RailState/cv_pipeline/blob/dev/deployment/README.md#cloud)
3. models deb: [cv_pipeline/deployment/README.md#updating-models-on-devices](https://github.com/RailState/cv_pipeline/blob/dev/deployment/README.md#updating-models-on-devices)
4. Follow the [device update handbook](https://docs.google.com/document/d/11xzIcmsP0SnBVD9Lh_ccrPVuordTBqb-_w3eWMoSdyA/edit?usp=sharing)
	- Run `update-devices` trigger on selected devices from CANARY
	- `_DEVICE_SET="CANARY ~ aplus-0167 ~ c-0456"`  a `_UPDATE_PLAYBOOK="update_device.yml"`
5. Only aplus devices run models on edge, if you want other devices to use the update model, you have to update the triton server

**3. Update Triton Server**
1. Connect to `cv-pipeline-06` or `cv-pipeline-testing-triton` (Where triton is hosted)
2. `sudo su -- ubuntu`, then `tmux a`
3. pull recent changes
4. `./utils/download_triton_repository.sh`
5. **Stop** `pano_pipeline` on `cv-pipeline-02`, `cv-pipeline-03` (or any cloud instances that are connect to your triton server)
6. Stop and re-run triton server: `sudo ./triton/run_triton_server.sh`
7. **Start** the `pano_pipeline` again on cloud instances with `CLOUDPATHLIB_FILE_CACHE_MODE=cloudpath_object PYTHONPATH=$(pwd):$(pwd)/external/shared-util-py/:$(pwd)/external  PROMETHEUS_MULTIPROC_DIR=$(mktemp -d) python3 bin/process_panoramas_server_triton.py configs/pano_pipeline_server_triton_on_06.json`
Don't forget to stop `cv-pipeline-testing-triton` when you are done

**4. Monitor Grafana**:
- [panorama-pipeline](https://grafana.internal.railstate.com/d/tqCRzwBVk/panorama-pipeline?orgId=1)
- [triton-inference-server](https://grafana.internal.railstate.com/d/slEY4dsZk/triton-inference-server?orgId=1&from=now-6h&to=now)

 

---

# Contacts:
- [glendoiron@railstate.com](mailto:glendoiron@railstate.com)
- [johnschmitter@railstate.com](mailto:johnschmitter@railstate.com)
- [danieldevoe@railstate.com](mailto:danieldevoe@railstate.com)


| Model B cost                                         |                                                           |        |
| ---------------------------------------------------- | --------------------------------------------------------- | ------ |
| Camera & Lens                                        | 3 MP resolution industrial camera. Motorized zoom lens    | $800   |
| Microprocessor                                       | Nvidia Xavier AXG -specialized high speed image processor | $699   |
| IR Illuminator                                       | Custom built 1400 W IR strobe - partly site-specific      | $605   |
| Solid State Drive                                    | 1 TB high speed industrial solid state drive              | $150   |
| Weatherproof enclosure, fittings and mounting plates | Polycarbonate case IP65, pre-milled holes                 | $180   |
| Thermoelectric Cooler                                | Peltier cooler of 100-225 BTU/h (30-67W)                  | $200   |
| Balance                                              | LIDAR,Cabling, mounting hardware, power supply            | $773   |
| Cell Modem                                           | Teltonika                                                 | $150   |
| Approximate total                                    |                                                           | $3,557 |