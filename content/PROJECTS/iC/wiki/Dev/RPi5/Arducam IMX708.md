[ArduCam Documentation](https://docs.arducam.com/Raspberry-Pi-Camera/Native-camera/12MP-IMX708/#arducam-fixed-focus-imx708-camera-module)

```bash
sudo nano /boot/firmware/config.txt 
#Find the line: camera_auto_detect=1, update it to:
camera_auto_detect=0
#Find the line: [all], add the following item under it:
dtoverlay=imx708
# If you want to enable the camera kit on the cam0 port of Pi5, please refer to the following modifications:
#dtoverlay=imx708,cam0
#Save and reboot.
```