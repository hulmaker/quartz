

```bash
# Check which credentials your code is using
gcloud config list

# Check credentialed accounts
gcloud auth list

# set auth application-default
gcloud auth application-default login

# change account
gcloud config set account hulmakerik@gmail.com
gcloud config set account erik.hulmak@eyen.se

# set project
gcloud config set project <project>

# secret
gcloud secrets versions access latest --secret=""

# a lot of usefull info about instances
gcloud compute instances describe <VM_NAME> --zone=<ZONE>
gcloud compute instances describe <VM_NAME> --zone=<ZONE> --format="value(serviceAccounts.email)"
```

# RailState
```bash
# eyen config set
gcloud config set account erik.hulmak@eyen.se && gcloud config set project named-purpose-220220

# projects
gcloud config set project railstate-development
gcloud config set project named-purpose-220220

# eyen - tohle nevim co je, pry prime pripojeni na gcloud
gcloud compute ssh ssh-reverse-tunnel-01 --zone=us-central1-c -- -p 9211

# copy detection event from cloud storage to local folder (change the location)
gsutil -m cp -r ‘gs://cv-pipeline-uploads/locations/na/us/ca/marathon/marathon/2025/2/3/detected_events/*’ .
```

# getxr.ai
```bash
loud config set account hulmakerik@gmail.com && gcloud config set project xrai-prod && gcloud auth application-default login
```

# AI Teacher
```bash
# ai-teacher config set
gcloud config set account hulmakerik@gmail.com && gcloud config set project ai-teacher-441210

# ai-teacher compute
gcloud compute ssh ai-teacher-1

# secret test
gcloud secrets versions access latest --secret="gemini-api-key"

# The VM instance has scopes that are less permissive that the service account roles. Running this commnad adds scopes for accessing the full cloud-platform
gcloud compute instances stop ai-teacher-1 --zone=us-central1-c
gcloud compute instances set-service-account ai-teacher-1 --zone=us-central1-c --service-account=1000668196687-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/cloud-platform
gcloud compute instances start ai-teacher-1 --zone=us-central1-c
```

# Personal
```bash
# personal automations connect
gcloud config set account hulmakerik@gmail.com && gcloud config set project personal-446120

gcloud compute ssh instance-20250105-232646
gcloud compute ssh --zone "us-east1-d" "instance-20250105-232646" --project "personal-446120"

# access secret
gcloud secrets versions access latest --secret="google-oauth-client-credentials" --project "personal-446120"
```


