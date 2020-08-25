# esp32cam-ready
https://github.com/rzeldent/esp32cam-ready
#
https://github.com/circuitrocks/ESP32-RTSP
#
https://forums.developer.nvidia.com/t/sainsmart-imx219-not-recognized/126293/6
#
https://developer.ridgerun.com/wiki/index.php?title=NVIDIA_Jetson_ISP_Control#Custom_ISP_Configuration
#
https://github.com/RidgeRun/NVIDIA-Jetson-IMX477-RPIV3
#
http://www.davidhunt.ie/raspberry-pi-zero-with-pi-camera-as-usb-webcam/
#

Fix pink tint
https://medium.com/@jonathantse/fix-pink-tint-on-jetson-nano-wide-angle-camera-a8ce5fbd797f

Here is how you could use the fix:
Download the tuning profile
wget https://www.waveshare.com/w/upload/e/eb/Camera_overrides.tar.gz
tar zxvf Camera_overrides.tar.gz 
Copy it to the directory
sudo cp camera_overrides.isp /var/nvidia/nvcam/settings/
sudo chmod 664 /var/nvidia/nvcam/settings/camera_overrides.isp
sudo chown root:root /var/nvidia/nvcam/settings/camera_overrides.isp


#https://www.arducam.com/docs/camera-for-jetson-nano/fix-red-tint-with-isp-tuning/
Power on Jetson Nano and open the Terminal (Ctrl+ALT+T)

Test camera with the command:

DISPLAY=:0.0 gst-launch-1.0 nvarguscamerasrc ! 'video/x-raw(memory:NVMM), width=3280, height=2464, format=(string)NV12, framerate=(fraction)20/1' ! nvoverlaysink -e
If you find that the image captured is red. You can try to download .isp file and installed:

wget https://www.arducam.com/downloads/Jetson/Camera_overrides.tar.gz
tar zxvf Camera_overrides.tar.gz
sudo cp camera_overrides.isp /var/nvidia/nvcam/settings/
sudo chmod 664 /var/nvidia/nvcam/settings/camera_overrides.isp
sudo chown root:root /var/nvidia/nvcam/settings/camera_overrides.isp
