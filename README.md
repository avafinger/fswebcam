# fswebcam 
fswebcam - Small and simple webcam software for *nix.

Created by Philip Heron <phil@sanslogic.co.uk>
http://www.sanslogic.co.uk/fswebcam/

This is the program used to generate images for a webcam. It captures a number
of frames from any V4L or V4L2 compatible device, averages them to reduce noise
and draws the details on it using the GD Graphics Library which also handles
compressing the image to PNG or JPEG.

## INSTALLING

Run the following commands in the source folder to build and install fswebcam:

    ./configure --prefix=/usr --disable-v4l1 --enable-32bit-buffer
    make
    sudo make install

It's only requirements are that the GD library be installed with JPEG, PNG
and FreeType support.

## Install Dependencies

    sudo apt-get install libgd-dev libjpeg-dev libpng-dev libfreetype6-dev

## Run samples:

    fswebcam --Vflip 1 -r 1600x1200 -p YUV420P - > cam640x480_2.jpg
    fswebcam --Hflip 1 -r 640x480 -p YUV420P - > cam640x480_1.jpg
    fswebcam --exposure 4 -r 640x480 -p YUV420P - > cam640x480_3.jpg

** Don't forget to update your GC2035 driver to get better results

## Rockchip platform support

**IMX-415 camera sensor:**

 	fswebcam  --displayfps 1 -S 90 -d /dev/video11 -r 3864x2192 -p UYVY  - > 3864x2192.jpg


## Mainline Kernel support

In order to use fswebcam in your Distro running a mainline kernel version you need to play with **media-ctl** and **v4l2-ctl** before you grab the files.

* Install v4l2 utils

        sudo apt-get install v4l-utils
        
* Find your camera sensor

        v4l2-ctl --list-devices
        cedrus (platform:cedrus):
          /dev/video1
        
        sun6i-csi (platform:csi):
          /dev/video0

* List the formats available

        v4l2-ctl -d 0 --list-formats --list-ctrls

        User Controls

                               contrast 0x00980901 (int)    : min=0 max=255 step=1 default=0 value=0 flags=slider
                             saturation 0x00980902 (int)    : min=0 max=255 step=1 default=64 value=64 flags=slider
                                    hue 0x00980903 (int)    : min=0 max=359 step=1 default=0 value=0 flags=slider
                white_balance_automatic 0x0098090c (bool)   : default=1 value=1 flags=update
                            red_balance 0x0098090e (int)    : min=0 max=4095 step=1 default=0 value=0 flags=inactive, slider
                           blue_balance 0x0098090f (int)    : min=0 max=4095 step=1 default=0 value=0 flags=inactive, slider
                               exposure 0x00980911 (int)    : min=0 max=65535 step=1 default=0 value=590 flags=inactive, volatile
                         gain_automatic 0x00980912 (bool)   : default=1 value=1 flags=update
                                   gain 0x00980913 (int)    : min=0 max=1023 step=1 default=0 value=23 flags=inactive, volatile
                        horizontal_flip 0x00980914 (bool)   : default=0 value=0
                          vertical_flip 0x00980915 (bool)   : default=0 value=0
                   power_line_frequency 0x00980918 (menu)   : min=0 max=3 default=1 value=1

        Camera Controls

                          auto_exposure 0x009a0901 (menu)   : min=0 max=1 default=0 value=0 flags=update

        Image Processing Controls

                             pixel_rate 0x009f0902 (int64)  : min=0 max=2147483647 step=1 default=61430400 value=61430400 flags=read-only
                           test_pattern 0x009f0903 (menu)   : min=0 max=4 default=0 value=0
        ioctl: VIDIOC_ENUM_FMT
          Index       : 0
          Type        : Video Capture
          Pixel Format: 'BA81'
          Name        : 8-bit Bayer BGBG/GRGR

          Index       : 1
          Type        : Video Capture
          Pixel Format: 'GBRG'
          Name        : 8-bit Bayer GBGB/RGRG

          Index       : 2
          Type        : Video Capture
          Pixel Format: 'GRBG'
          Name        : 8-bit Bayer GRGR/BGBG

          Index       : 3
          Type        : Video Capture
          Pixel Format: 'RGGB'
          Name        : 8-bit Bayer RGRG/GBGB

          Index       : 4
          Type        : Video Capture
          Pixel Format: 'BG10'
          Name        : 10-bit Bayer BGBG/GRGR

          Index       : 5
          Type        : Video Capture
          Pixel Format: 'GB10'
          Name        : 10-bit Bayer GBGB/RGRG

          Index       : 6
          Type        : Video Capture
          Pixel Format: 'BA10'
          Name        : 10-bit Bayer GRGR/BGBG

          Index       : 7
          Type        : Video Capture
          Pixel Format: 'RG10'
          Name        : 10-bit Bayer RGRG/GBGB

          Index       : 8
          Type        : Video Capture
          Pixel Format: 'BG12'
          Name        : 12-bit Bayer BGBG/GRGR

          Index       : 9
          Type        : Video Capture
          Pixel Format: 'GB12'
          Name        : 12-bit Bayer GBGB/RGRG

          Index       : 10
          Type        : Video Capture
          Pixel Format: 'BA12'
          Name        : 12-bit Bayer GRGR/BGBG

          Index       : 11
          Type        : Video Capture
          Pixel Format: 'RG12'
          Name        : 12-bit Bayer RGRG/GBGB

          Index       : 12
          Type        : Video Capture
          Pixel Format: 'YUYV'
          Name        : YUYV 4:2:2

          Index       : 13
          Type        : Video Capture
          Pixel Format: 'YVYU'
          Name        : YVYU 4:2:2

          Index       : 14
          Type        : Video Capture
          Pixel Format: 'UYVY'
          Name        : UYVY 4:2:2

          Index       : 15
          Type        : Video Capture
          Pixel Format: 'VYUY'
          Name        : VYUY 4:2:2

          Index       : 16
          Type        : Video Capture
          Pixel Format: 'HM12'
          Name        : YUV 4:2:0 (16x16 Macroblocks)

          Index       : 17
          Type        : Video Capture
          Pixel Format: 'NV12'
          Name        : Y/CbCr 4:2:0

          Index       : 18
          Type        : Video Capture
          Pixel Format: 'NV21'
          Name        : Y/CrCb 4:2:0

          Index       : 19
          Type        : Video Capture
          Pixel Format: 'YU12'
          Name        : Planar YUV 4:2:0

          Index       : 20
          Type        : Video Capture
          Pixel Format: 'YV12'
          Name        : Planar YVU 4:2:0

          Index       : 21
          Type        : Video Capture
          Pixel Format: 'NV16'
          Name        : Y/CbCr 4:2:2

          Index       : 22
          Type        : Video Capture
          Pixel Format: 'NV61'
          Name        : Y/CrCb 4:2:2

          Index       : 23
          Type        : Video Capture
          Pixel Format: '422P'
          Name        : Planar YUV 4:2:2

          Index       : 24
          Type        : Video Capture
          Pixel Format: 'RGBP'
          Name        : 16-bit RGB 5-6-5

          Index       : 25
          Type        : Video Capture
          Pixel Format: 'RGBR'
          Name        : 16-bit RGB 5-6-5 BE

          Index       : 26
          Type        : Video Capture
          Pixel Format: 'JPEG' (compressed)
          Name        : JFIF JPEG
          
* find the info and topology

          media-ctl --device /dev/media1 -p
          Media controller API version 5.7.9

          Media device information
          ------------------------
          driver          sun6i-csi
          model           Allwinner Video Capture Device
          serial          
          bus info        
          hw revision     0x0
          driver version  5.7.9

          Device topology
          - entity 1: sun6i-csi (1 pad, 1 link)
                      type Node subtype V4L flags 0
                      device node name /dev/video0
            pad0: Sink
              <- "ov5640 2-003c":0 [ENABLED,IMMUTABLE]

          - entity 5: ov5640 2-003c (1 pad, 1 link)
                      type V4L2 subdev subtype Sensor flags 0
                      device node name /dev/v4l-subdev0
            pad0: Source
              [fmt:UYVY8_2X8/640x480@1/30 field:none colorspace:srgb xfer:srgb ycbcr:601 quantization:full-range]
              -> "sun6i-csi":0 [ENABLED,IMMUTABLE]


* Grab files from OV5640 using the **fswebcam**

        media-ctl --device /dev/media1 --set-v4l2 '"ov5640 2-003c":0[fmt:YUYV8_2X8/1280x720]'
        ./fswebcam --displayfps 1 -S 30 -d /dev/video0 -r 1280x720 -p YUV420P - > /tmp/cam_640x480_yuv420p.jpg

![640x480](https://github.com/avafinger/fswebcam/raw/mainline-kernel/nanopi-air/cam_640x480_yuv420p.jpg)
