## Pre-requistes
- PYNQv2.5 https://github.com/Xilinx/PYNQ/releases
- DNNDK 3.1 https://www.xilinx.com/products/design-tools/ai-inference/ai-developer-hub.html#edge
- rootfs.tar [rootfs.tar](https://pan.baidu.com/s/1hTtdL0vds3gAUVLqbQkGLA) (pass code: t8ep)

Before we get down to business, please reference [PYNQ Getting Started](https://pynq.readthedocs.io/en/v2.5.1/getting_started.html) to setup your board.

## Install Dependencies
```
sudo apt update
sudo apt upgrade -y
sudo apt install libgoogle-glog-dev -y
sudo apt remove libopencv-dev -y 
# DNNDK C++ requires opencv 3.1, 3.3, 3.4, however the one provided by ubuntu18.04 is opencv 3.2
sudo apt install python-pip -y
# DNNDK3.1 provides Python2.7 based APIs, which is not compatible with jupyter notebook.
# We have to install ipykernel manually to enable Python2.7 in jupyter notebook.
sudo pip install ipykernel matplotlib==2.2.0 pillow
```

## Install DNNDK
- Unzip dnndk3.1
- Copy xilinx_dnndk_3.1/ZedBoard to PYNQ-Z2
- Copy xilinx_dnndk_3.1/common to PYNQ-Z2
- Copy rootfs.tar to PYNQ-Z2, OpenCV3.3 libraries are included in it, which is compiled by Petalinux2018.3 with OpenCV enabled in rootfs.
```
mkdir rootfs
tar -xvf rootfs.tar -C rootfs
mkdir -p /usr/local/lib
mkdir -p /usr/local/bin

# copy libopencv*.3.3 to /usr/lib
sudo cp -r rootfs/usr/include/openc* /usr/include
sudo cp -d rootfs/usr/lib/libopencv* /usr/lib
sudo cp -d rootfs/usr/lib/libwebp* /usr/lib
sudo cp rootfs/usr/lib/pkgconfig/opencv.pc /usr/lib/pkgconfig

cd Zedboard
sudo chmod +x install.sh
sudo ./install.sh
sudo reboot
```


## Pre-built Image
You can also directly download the [pre-built image](https://pan.baidu.com/s/1aqCYu1U0zqCZYBk6LjJuUA)  (passcode:9997) to try out the jupyter notebook with image.

