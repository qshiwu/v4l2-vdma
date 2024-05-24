v4l2-vdma - an experimental repo based on [v4l2loopback](https://github.com/umlaeute/v4l2loopback)
==============================================================

# Prepration
sudo apt-get update
sudo apt-get install build-essential linux-headers-$(uname -r)
sudo apt-get install libv4l-dev v4l-utils
sudo usermod -aG video $USER
sudo apt-get install ffmpeg


# Build
```
make
sudo make install
```

# v4l2ctl
```
v4l2-ctl --device=/dev/video0 --all
```

# v4l2loopback
```
sudo modprobe v4l2loopback exclusive_caps=1
sudo modprobe v4l2loopback video_nr=10 card_label="v4l2loopback" exclusive_caps=1
```
## v4l2loopback example
```
sudo rmmod v4l2loopback
sudo modprobe v4l2loopback video_nr=10 card_label="v4l2loopback" exclusive_caps=1
cd examples
wget http://trace.eas.asu.edu/yuv/akiyo/akiyo_qcif.7z
7z x akiyo_qcif.7z
make yuv420_infiniteloop
./yuv420_infiniteloop /dev/video10 akiyo_qcif.yuv 176 144 30
ffplay /dev/video10
```

# ffmpeg / ffplay
ffplay devicename


# Gstreamer
```
gst-launch-1.0 v4l2src device=/dev/video0 ! xvimagesink
```

```
gst-launch-1.0 -v videotestsrc pattern=snow ! "video/x-raw,width=640,height=480,framerate=25/1,format=UYVY" ! v4l2sink device=/dev/video0
```

```
ffmpeg -re -f lavfi -i "movie=my_video_file.mp4" -f v4l2 /dev/video0
```


