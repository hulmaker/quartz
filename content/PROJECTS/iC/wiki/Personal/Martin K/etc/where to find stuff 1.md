footfall
	- logs
		- ls -l /opt/icsystems.ai/footfall_logs/ | tail
			-  cat /opt/icsystems.ai/footfall_logs/THE_LOG_NAME | head -n 40
		- cat /opt/icsystems.ai/footfall_logs/2023-01-03_13h45m18s_compute_detections_for_single_dataset.log | head -n 40


VTs generating / ff-eval
-------------

**tail -- continuous logs**

`tail -f /epsilon/VTs/1.21.51-visu//2023-02-27_17h24m31s_run_group_of_visual_tests.log`




old footfall (1.XX) but with support for abs paths -- backcompatibility:
---------------------
branch:

`old_rework_for_automatization`



old footfall (1.22.19) with support THAT ACTUALLY WORKS -- fixed some bug in trakcing:
------------------------

`1.22.19_restructure`



recipes on clickup -- aneb try your luck
-------------------------

search/tag:

recipes - martin



**monitoring**

cd `/Users/martinkoucky/icsystemsai/icmonitor/dev`

`make frontend`


a u tamtoho nahore (..)

`make start`