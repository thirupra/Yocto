# Yocto

Build Linux Image for Raspberry Pi board using Yocto Project




Raspberry pi is a very popular development board for IoT and Industrial projects.it comes in many different versions like Raspberry pi 4, Raspberry Pi 3, and Raspberry 2, etc. Yocto is an open-source project which provides a build framework and metadata to help to create a custom image for your target board also it supports the raspberry pi BSP layer.
Follow the below steps to build the image for your Raspberry pi board using Yocto Project.

Prerequisite


Download Poky
Download Raspberry pi meta layer
Setup build environment
Set machine name in local.conf and add raspberrypi layer in bblayer.conf
Start bitbake to build the image
Flash SD card
Boot

Prerequisite

Need Ubuntu-based Host system with a minimum 50 GB free space with internet connection.
Install the below package on the host machine which supports the Yocto Project.

# Install the below required package on your host machine

sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib build-essential chrpath socat cpio python python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping libsdl1.2-dev xterm


if it doesnt work use below 3 commands
Install Python 3:
sudo apt-get install python3

Install additional dependencies:
sudo apt-get install python3-pip python3-pexpect

Proceed with the rest of your installation:
sudo apt-get install gawk wget git diffstat unzip texinfo gcc-multilib build-essential chrpath socat cpio python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping libsdl1.2-dev xterm

Download Poky

Poky is the Yocto reference distribution.it contains all the basic meta layers
Every 6 months, Yocto Project releases a new version of poky. so we clone dunfell latest stable version of poky.

# Clone the poky with the below command. 

$ git clone git://git.yoctoproject.org/poky -b dunfell



Download Raspberry pi meta layer

You will need a BSP layer to support the Raspberry Pi boards. so Yocto Project is providing a meta-raspberrypi layer that contains information related to raspberry pi boards that are required during the build.
Download meta-raspberrypi layer from the poky directory

$ cd poky

# clone raspberrypi layer using below command

$ git clone https://git.yoctoproject.org/meta-raspberrypi/ -b dunfell


Setup build environment
initialize the oe-init-build-env script with the below command from the poky directory and it will auto-create the build directory. Now your current working directory would be the build directory.

# Setup the environment

$source oe-init-build-env


csg@csg-global:~/yocto/poky$ source oe-init-build-env
mkdir: cannot create directory ‘/home/csg/yocto/poky/build’: Permission denied
Error: The builddir (/home/csg/yocto/poky/build) does not exist!
Run the following command to change the ownership of the yocto/poky directory (and its contents) to the csg user and group:
sudo chown -R csg:csg ~/yocto/poky
ls -ld ~/yocto/poky
drwxr-xr-x 13 csg csg 4096 Apr  9 16:29 /home/csg/yocto/poky




Set machine name in local.conf and add the raspberry pi layer in bblayer.conf
local.conf file is used for user configuration and we are building the image for raspberry pi 4 (64-bit variants) then machine name should raspberrypi4-64 and comment other machine names in local.conf
You can set machine name based on your raspberry pi boards


Example:
For raspberry pi 3
machine ?= "raspberrypi3"
For raspberry pi 2
machine ?= "raspberrypi2"

To generate an SD card image file, we need to set the IMAGE_FSTYPE variable.

# For raspberry pi 4 machine name 
machine ?= " raspberrr4-64"

# For SD card image
MAGE_FSTYPES = "tar.xz ext3 rpi-sdimg"



Now, We have to add the meta-raspberrypi layer in the build/conf/bblayers.conf file. This file store information of all meta-layer path which used by the bitbake
In my case meta-raspberrypi layer path is /home/tutorialadda/yocto/poky/meta-raspberrypi

 

Start bitbake to build the image
We are ready to start the bitbake to build the image.core-minimal-image recipe provides the minimal bootable image for the Raspberry pi boards.
Bitbake will take several hours to complete the build process. it depends on your internet speed and CPU performance.
Generated image present at the tmp/deploy/images/raspberrypi4-64/ directory.

# Run bitbake 
$ bitbake core-image-minimal



Flash SD card
After completing the build process bitbake will generate the core-image-minimal-raspberrypi4-64.rpi-sdimg file at tmp/deploy/images/raspberrypi4-64/ directory

Now just plug the SD card into your host machine and follow the below steps

To check the SD card partition run sudo fdisk -l and replace x with your sd card partition id.

$ sudo umount /dev/sdx

# Flash SD card with the generated image

$ sudo dd if=tmp/deploy/images/raspberrypi4-64/core-image-minimal-raspberrypi4-64.rpi-sdimg of=/dev/sdx

$ sudo umount /dev/sdx

Boot

Insert SD card into raspberry pi and start on the board.

root is the username and password is not required






#The commands below are the ones I tried.

Build Linux Image for Raspberry Pi board using Yocto Project




Raspberry pi is a very popular development board for IoT and Industrial projects.it comes in many different versions like Raspberry pi 4, Raspberry Pi 3, and Raspberry 2, etc. Yocto is an open-source project which provides a build framework and metadata to help to create a custom image for your target board also it supports the raspberry pi BSP layer.
Follow the below steps to build the image for your Raspberry pi board using Yocto Project.

Prerequisite


Download Poky
Download Raspberry pi meta layer
Setup build environment
Set machine name in local.conf and add raspberrypi layer in bblayer.conf
Start bitbake to build the image
Flash SD card
Boot

Prerequisite

Need Ubuntu-based Host system with a minimum 50 GB free space with internet connection.
Install the below package on the host machine which supports the Yocto Project.

# Install the below required package on your host machine

sudo apt-get install gawk wget git-core diffstat unzip texinfo gcc-multilib build-essential chrpath socat cpio python python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping libsdl1.2-dev xterm


if it doesnt work use below 3 commands
Install Python 3:
sudo apt-get install python3

Install additional dependencies:
sudo apt-get install python3-pip python3-pexpect

Proceed with the rest of your installation:
sudo apt-get install gawk wget git diffstat unzip texinfo gcc-multilib build-essential chrpath socat cpio python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping libsdl1.2-dev xterm

Download Poky

Poky is the Yocto reference distribution.it contains all the basic meta layers
Every 6 months, Yocto Project releases a new version of poky. so we clone dunfell latest stable version of poky.

# Clone the poky with the below command. 

$ git clone git://git.yoctoproject.org/poky -b dunfell



Download Raspberry pi meta layer

You will need a BSP layer to support the Raspberry Pi boards. so Yocto Project is providing a meta-raspberrypi layer that contains information related to raspberry pi boards that are required during the build.
Download meta-raspberrypi layer from the poky directory

$ cd poky

# clone raspberrypi layer using below command

$ git clone https://git.yoctoproject.org/meta-raspberrypi/ -b dunfell


Setup build environment
initialize the oe-init-build-env script with the below command from the poky directory and it will auto-create the build directory. Now your current working directory would be the build directory.

# Setup the environment

$source oe-init-build-env


csg@csg-global:~/yocto/poky$ source oe-init-build-env
mkdir: cannot create directory ‘/home/csg/yocto/poky/build’: Permission denied
Error: The builddir (/home/csg/yocto/poky/build) does not exist!
Run the following command to change the ownership of the yocto/poky directory (and its contents) to the csg user and group:
sudo chown -R csg:csg ~/yocto/poky
ls -ld ~/yocto/poky
drwxr-xr-x 13 csg csg 4096 Apr  9 16:29 /home/csg/yocto/poky




Set machine name in local.conf and add the raspberry pi layer in bblayer.conf
local.conf file is used for user configuration and we are building the image for raspberry pi 4 (64-bit variants) then machine name should raspberrypi4-64 and comment other machine names in local.conf
You can set machine name based on your raspberry pi boards


Example:
For raspberry pi 3
machine ?= "raspberrypi3"
For raspberry pi 2
machine ?= "raspberrypi2"

To generate an SD card image file, we need to set the IMAGE_FSTYPE variable.

# For raspberry pi 4 machine name 
machine ?= " raspberrr4-64"

# For SD card image
MAGE_FSTYPES = "tar.xz ext3 rpi-sdimg"



Now, We have to add the meta-raspberrypi layer in the build/conf/bblayers.conf file. This file store information of all meta-layer path which used by the bitbake
In my case meta-raspberrypi layer path is /home/tutorialadda/yocto/poky/meta-raspberrypi

 

Start bitbake to build the image
We are ready to start the bitbake to build the image.core-minimal-image recipe provides the minimal bootable image for the Raspberry pi boards.
Bitbake will take several hours to complete the build process. it depends on your internet speed and CPU performance.
Generated image present at the tmp/deploy/images/raspberrypi4-64/ directory.

# Run bitbake 
$ bitbake core-image-minimal



Flash SD card
After completing the build process bitbake will generate the core-image-minimal-raspberrypi4-64.rpi-sdimg file at tmp/deploy/images/raspberrypi4-64/ directory

Now just plug the SD card into your host machine and follow the below steps

To check the SD card partition run sudo fdisk -l and replace x with your sd card partition id.

$ sudo umount /dev/sdx

# Flash SD card with the generated image

$ sudo dd if=tmp/deploy/images/raspberrypi4-64/core-image-minimal-raspberrypi4-64.rpi-sdimg of=/dev/sdx

$ sudo umount /dev/sdx

Boot

Insert SD card into raspberry pi and start on the board.

root is the username and password is not required

sudo dd if=tmp/deploy/images/raspberrypi4-64/core-image-full-cmdline-raspberrypi4-64.rpi-sdimg of=/dev/sda







lsof /dev/video0





for Raspberry 5 
![Screenshot from 2025-05-05 11-24-11](https://github.com/user-attachments/assets/3a88832b-034a-4147-97c7-7b517f241901)
![Screenshot from 2025-05-05 11-25-16](https://github.com/user-attachments/assets/ad47a06d-efed-4072-b373-3c4411636a2b)
![Screenshot from 2025-05-05 11-26-06](https://github.com/user-attachments/assets/92bc8d49-623c-4c24-800f-cf3b45882f3c)
![image](https://github.com/user-attachments/assets/607644b7-d72c-478e-afd7-00c770f21a49)





raspberry pi 64

![Screenshot from 2025-05-05 13-31-28](https://github.com/user-attachments/assets/4af96746-7a8d-4391-b128-e8ed66564b89)

![Screenshot from 2025-05-05 13-33-02](https://github.com/user-attachments/assets/3101aa25-b4fb-46cc-884b-6db0560ea928)



