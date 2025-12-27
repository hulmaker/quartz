This is a testing device
in `/opt/icsystems.ai/icmonitor/.env-client` there is 
```
# Disables sensor restarting when footfall is not running
DISABLE_FOOTFALL_CHECK=true
```
this prevents cyclic restarting when footfall is not running

`footfall64-iclab`

- ssh -p 1422 icsapl@212.47.16.33
- 192.168.0.190
- -p 1422

for password contact [[#Responsible person]]

# benchmarking
In order to have relevant measurements, when footfall is running, call:
`sudo systemctl stop footfall`

[[onnxruntime NN benchmarking]]

# Responsible person
[[PROJECTS/iC/wiki/Personal/Filip Naiser]], [[PROJECTS/iC/wiki/Personal/Martin Vadlejch]]