# esp32cam with tasmota, rtsp

https://cgomesu.com/blog/Esp32cam-tasmota-webcam-server/#flashing-tasmota32-webcam-server

download:
```
wget \
https://ota.tasmota.com/tasmota32/tasmota32-webcam.bin \
  https://github.com/arendst/Tasmota-firmware/raw/main/static/esp32/boot_app0.bin \
  https://github.com/arendst/Tasmota-firmware/raw/main/static/esp32/bootloader_dout_40m.bin \
  https://github.com/arendst/Tasmota-firmware/raw/main/static/esp32/partitions.bin
```

```
python -m esptool –-chip esp32 erase_flash

python -m esptool --chip esp32 --port COM7 write_flash -z 0x1000 esp32-20190113-v1.9.4-779g5064df207.bin

esptool.py --port $ESP_PORT erase_flash
```

```
esptool --chip esp32 \
  --port COM6 \
  --before default_reset \
  --after hard_reset \
  write_flash -z \
  --flash_mode dout \
  --flash_freq 40m \
  --flash_size detect \
  0x1000 bootloader_dout_40m.bin \
  0x8000 partitions.bin \
  0xe000 boot_app0.bin \
  0x10000 tasmota32-webcam.bin
```

template:
https://templates.blakadder.com/ai-thinker_ESP32-CAM.html

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
#
#
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

## ESP32CAM MQTT !!
https://github.com/botabotlab/ESP32CAM-MQTT

## OPENCV gestream grab
We also were unable to close the gstreamer pipeline started with the following command:

stream = cv2.VideoCapture("nvarguscamerasrc ! video/x-raw(memory:NVMM), width=1280, "
                                       "height=720, framerate=30/1, format=NV12 ! nvvidconv ! "
                                       "video/x-raw, format=BGRx, width=640, height=360 ! "
                                       "videoconvert ! video/x-raw, format=BGR ! appsink")
However, adding the following line worked:

stream = cv2.VideoCapture("nvarguscamerasrc ! video/x-raw(memory:NVMM), width=1280, "
                                       "height=720, framerate=30/1, format=NV12 ! nvvidconv ! "
                                       "video/x-raw, format=BGRx, width=640, height=360 ! "
                                       "videoconvert ! video/x-raw, format=BGR ! appsink "
                                       "wait-on-eos=false drop=true max-buffers=60 -e -vvv")
For more information, see https://github.com/InES-HPMM/linux-l4t/issues/5 6

https://forums.developer.nvidia.com/t/how-to-close-gstreamer-pipeline-in-python/74753/15

--------------
## QR, francefu   https://www.facebook.com/francefu
https://github.com/fustyles/Arduino/blob/master/ESP32-CAM_QRCode_Recognition/ESP32-CAM_QRCode_Recognition.ino

## esp-32 camera rtsp / dimkas
binary  https://github.com/dimkas/ESP32_RTSP_Cam/blob/master/ESP32_RTSP_cam.bin  <br>
https://github.com/dimkas/ESP32_RTSP_Cam  <br>

## ESPcam ai thinker
https://github.com/raphaelbs/esp32-cam-ai-thinker
## Espcam32 revisited
https://github.com/easytarget/esp32-cam-webserver <br>
https://hackaday.io/project/168563-7-esp32-cam-example-expanded

