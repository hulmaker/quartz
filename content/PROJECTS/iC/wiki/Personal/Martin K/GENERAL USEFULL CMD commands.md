
to get correct DATASETS_PATH -- this is needed in many scripts across iC, but might not be needed in the future:

`export DATASETS_PATH=/data/footfall/datasets/

RUNNING FOOTFALL THE OLD WAY
----------------------

commands needed to run footfall the old way:

`export DATASETS_PATH=/data/footfall/datasets/;export CACHE_PATH=/epsilon/TRACKING_CHECKPOINTS/$commit/;export PROPOSER_CACHE_PATH=/epsilon/TRACKING_CHECKPOINTS/$commit/proposer;export PYTHONPATH=src;conda activate footfall;`


maybe this as well sometimes:

`export PYTHONPATH=./src`


https://app.clickup.com/18311012/v/dc/hetv4-6707/hetv4-1447
