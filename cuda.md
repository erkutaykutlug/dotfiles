## CUDA installation guide:
http://docs.nvidia.com/cuda/cuda-installation-guide-linux/#axzz4VZnqTJ2A
```
$ lspci | grep -i nvidia
$ uname -m && cat /etc/*release
$ gcc --version
```

## Install LINUX headers
```
$ sudo apt install linux-headers-$(uname -r)
```

## Download and install CUDA 8.0
For GTX 1080 Ti, select No to install NVidia driver 376.
```
$ wget https://developer.nvidia.com/compute/cuda/8.0/Prod2/local_installers/cuda_8.0.61_375.26_linux-run
$ sudo sh cuda_8.0.61_375.26_linux-run
```

For GTX 1080 Ti, you need to install NVidia driver 381.09 manually
```
$ sudo add-apt-repository ppa:graphics-drivers/ppa
$ sudo apt update
$ sudo apt -y install nvidia-381
```

If the installation fails, remove X lock in /tmp.

## Disable Nouveau if a command below displays anything:
```
$ lsmod | grep nouveau
```

Create a file at /etc/modprobe.d/blacklist-nouveau.conf with the following # contents:
```
blacklist nouveau
options nouveau modeset=0
```
Then regenerate the kernel initramfs:
```
$ sudo update-initramfs -u
```

## Install cuDNN 5.1
Download cuDNN from https://developer.nvidia.com/cudnn
```
$ sudo cp include/cudnn.h /usr/local/cuda/include
$ sudo cp -P lib64/libcudnn* /usr/local/cuda/lib64/
$ sudo chmod a+r /usr/local/cuda/include/cudnn.h
$ sudo chmod a+r /usr/local/cuda/lib64/libcudnn*
```

## Install NVIDIA CUDA Profile Tools
```
$ sudo apt install libcupti-dev
```

## Install TensorFlow
```
$ sudo pip install -U tensorflow-gpu
```

## Install Keras
```
$ sudo pip install keras
```

## Install GpuStat
```
$ sudo pip install gpustat
```

## Install OpenCV2
From http://leoybkim.com/wiki/installing-opencv-2.4.13-on-ubunto-16.04/
```
$ sudo apt update
$ sudo apt install -y checkinstall libopencv-dev libgtk2.0-dev pkg-config libavcodec-dev libpng12-dev libavformat-dev libswscale-dev yasm libxine2 libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev libv4l-dev libqt4-dev libmp3lame-dev libopencore-amrnb-dev libopencore-amrwb-dev libtheora-dev libvorbis-dev libxvidcore-dev x264 v4l-utils
$ sudo apt install -y libtbb2 libtbb-dev libjpeg-dev libpng-dev libtiff5-dev libjasper-dev libdc1394-22-dev

$ wget https://github.com/opencv/opencv/archive/2.4.13.2.tar.gz
$ tar xzvf 2.4.13.2.tar.gz && cd opencv-2.4.13.2
$ mkdir release && cd release
$ cmake -G "Unix Makefiles" -DCMAKE_CXX_COMPILER=/usr/bin/g++ CMAKE_C_COMPILER=/usr/bin/gcc -DCMAKE_BUILD_TYPE=RELEASE -DCMAKE_INSTALL_PREFIX=/usr/local -DWITH_TBB=ON -DBUILD_NEW_PYTHON_SUPPORT=ON -DWITH_V4L=ON -DINSTALL_C_EXAMPLES=ON -DINSTALL_PYTHON_EXAMPLES=ON -DBUILD_EXAMPLES=ON -DWITH_QT=ON -DWITH_OPENGL=ON -DBUILD_FAT_JAVA_LIB=ON -DINSTALL_TO_MANGLED_PATHS=ON -DINSTALL_CREATE_DISTRIB=ON -DINSTALL_TESTS=ON -DENABLE_FAST_MATH=ON -DWITH_IMAGEIO=ON -DBUILD_SHARED_LIBS=OFF -DWITH_GSTREAMER=ON ..
$ make all -j
$ sudo make install && sudo checkinstall
```