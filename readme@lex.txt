Build:
./configure --prefix=/usr --disable-v4l1 --enable-32bit-buffer
make
sudo make install

Dependencies:
sudo apt-get install libgd2-xpm-dev libjpeg-dev libpng-dev

Run:
fswebcam --Vflip 1 -r 1600x1200 -p YUV420P - > cam640x480_2.jpg
fswebcam --Hflip 1 -r 640x480 --fps 25 -p YUV420P - > cam640x480_1.jpg
fswebcam --exposure 4 -r 640x480 --fps 25 -p YUV420P - > cam640x480_1.jpg

