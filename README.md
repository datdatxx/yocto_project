


git clone https://github.com/agherzan/meta-raspberrypi.git
cd meta-raspberrypi/
git checkout scarthgap


git clone https://git.yoctoproject.org/poky
cd poky
git checkout scarthgap
less meta-poky/conf/distro/poky.conf


cd ..
git clone https://git.openembedded.org/meta-openembedded
cd meta-openembedded/
git checkout scarthgap

Configure Build

### We start by creating a build environment (to give us access to tools like “bitbake”). Note that the oe-init-build-env script will create an initial “build-rpi” folder and automatically change directories to it.

/// README.md meta-raspberrypi
cd /yocto
source poky/oe-init-build-env rpi-build
cd rpi-build

### You can view the layers that will be included in the build with the following:
bitbake-layers show-layers

dat@dat-Lenovo-Legion-5-15ARH05:~/embedded_workspace/yocto/rpi-build$ bitbake-layers show-layers
NOTE: Starting bitbake server...
layer                 path                                                                    priority
========================================================================================================
core                  /home/dat/embedded_workspace/yocto/poky/meta                            5
yocto                 /home/dat/embedded_workspace/yocto/poky/meta-poky                       5
yoctobsp              /home/dat/embedded_workspace/yocto/poky/meta-yocto-bsp                  5


### You should only have the default poky layers to start. We need to edit bblayers.conf in our build to add the necessary STM32MP BSP and dependency layers:

vi conf/bblayers.conf

BBLAYERS ?= " \
  /home/dat/embedded_workspace/yocto/poky/meta \
  /home/dat/embedded_workspace/yocto/poky/meta-poky \
  /home/dat/embedded_workspace/yocto/poky/meta-yocto-bsp \
  /home/dat/embedded_workspace/yocto/meta-raspberrypi \
  /home/dat/embedded_workspace/yocto/meta-openembedded/meta-oe \
  /home/dat/embedded_workspace/yocto/meta-openembedded/meta-python \
  "


cd ..
cd meta-raspberrypi/conf/machine/
less raspberrypi3-64.conf 