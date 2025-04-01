# 

-----------------------------------------------------------------

# First Step -> Run the following commands to install uboot or linux kernel module.

sudo apt-get update
sudo apt-get install build-essential lzop u-boot-tools net-tools bison flex libssl-dev libncurses5-dev libncursesw5-dev unzip chrpath xz-utils minicom wget git-core
sudo apt-get install libgmp-dev
sudo apt-get install libmpc-dev
sudo apt-get install liblz4-tool
sudo apt install gcc-arm-linux-gnueabihf

----------------------------------------------------------------------

# Second step -> clone the beagleboard git repo into your git source

Open the terminal and navigate to the source folder run the command.
git init
After initializing the Git repository, you can proceed to clone the repository by pasting the copied URL from Git and providing a name for
the cloned repository. Here is the command:
git clone https://github.com/beagleboard/linux.git
Execute the command 
git checkout 5.10.168-ti-rt-r76
to switch to the desired branch in the Git repository.
-----------------------------------------------------------------

*************************cross tool-chain installation and settings for linux host******************

STEP 1 : Download arm cross toolchain for your Host machine
https://releases.linaro.org/components/toolchain/binaries/7.5-2019.12/arm-linux-gnueabihf/

STEP 2 :  export  path of the cross compilation toolchain. 
1.Go to you home directory -> cd /home/murali/
2.Open .bashrc using vim or gedit text editor
3.Copy the below export command with path information to .bashrc file
export PATH=$PATH:<path_to_tool_chain_binaries>
4. Save and close
export PATH=$PATH:/home/murali/Desktop/beaglebone_black/linux_images/gcc-linaro-7.5.0-2019.12-x86_64_armeb-linux-gnueabihf/bin


or simply do
echo “export PATH=$PATH:<path_to_tool_chain_binaries>” >  ~/.bashrc
echo “export PATH=$PATH:/home/murali/Desktop/beaglebone_black/linux_images/gcc-linaro-7.5.0-2019.12-x86_64_armeb-linux-gnueabihf/bin” >  ~/.bashrc

5. after that type the following command
source .bashrc

6. Now type arm and press tab and it will show the all the arm cross compiler list


*********************************SD-card formater application **********************


Beaglebone software images -> you can download the image based on the board ie. beaglebone black or beaglebone ai
https://www.beagleboard.org/distros

install GParted Partition Editor application from the app center
GParted Partition Editor

Gparted works fine with VMware ubunt but it is not working when ubunt running as external hard drive 
after 2 days of headache and different approach found that disk is great in buit tool
   # Issue with Gpart:
    A. you can create fat16 boot primary partition but it is not showing in lsblk and cannot mount /media/murali/BOOT




Select the usb device of the sd card by using following command
sudo dmesg

Two partition only need 
1. BOOT 
2. ROOTFS



*************************U-boot Compilation ***************************************************
sudo apt update
sudo apt install gcc-arm-linux-gnueabihf

STEP 1: distclean : deletes all the previously compiled/generated object files. 

make CROSS_COMPILE=arm-linux-gnueabihf- distclean

STEP 2 : apply board default configuration for uboot

make CROSS_COMPILE=arm-linux-gnueabihf- am335x_boneblack_defconfig


STEP 3 : run menuconfig, if you want to do any settings other than default configuration . 

make CROSS_COMPILE=arm-linux-gnueabihf-  menuconfig


STEP 4 : compile 
/* This step installs all the generated .ko files in the default path of the computer (/lib/modules/<kernel_ver>) */​

make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- -j4  // -j4(4 core machine) will instruct the make tool to spawn 4 threads
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- -j8  // -j8(8 core machine) will instruct the make tool to spawn 8 threads


************************* linux compilation ***************************************************
STEP 1:
/*
 *removes all the temporary folder, object files, images generated during the previous build. 
 *This step also deletes the .config file if created previously 
 */

 make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- distclean

STEP 2:
/*creates a .config file by using default config file given by the vendor */

 make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- bb.org_defconfig (4.4)
for 4.11 use omap2plus_defconfig

STEP 3:
/*This step is optional. Run this command only if you want to change some kernel settings before compilation */ ​

 make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- menuconfig

STEP 4:
/*Kernel source code compilation. This stage creates a kernel image "uImage" also all the device tree source files will be compiled, and dtbs will be generated */ ​

 make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- uImage dtbs LOADADDR=0x80008000 -j4

STEP 5:
/*This step builds and generates in-tree loadable(M) kernel modules(.ko) */

 make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- -j4 modules

STEP 6:
/* This step installs all the generated .ko files in the default path of the computer (/lib/modules/<kernel_ver>) */​

 make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- INSTALL_MOD_PATH=<path of the RFS> modules_install


************************* Busy box compilation ***************************************************

STEP 1: download busybox 

STEP 2 : Apply default configuration
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- defconfig

STEP 3 : change default settings if you want 
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- menuconfig

STEP 4 : generate the busy box binary and minimal file system 
make ARCH=arm CROSS_COMPILE=arm-linux-gnueabihf- CONFIG_PREFIX=<install_path> install



*********************************build-root compilation ***********************************
1) download the build root package from 

https://buildroot.org/

2) configure the build root 


*******************************Dropbear compilation*************************************

1) Download Dropbear 

2) Configure Dropbear

./configure --host=arm-linux-gnueabihf --disable-zlib --prefix=/home/kiran/BBB_Workspace/dropbear CC=arm-linux-gnueabihf-gcc

3) compile the Dropbear as static 

make PROGRAMS="dropbear dropbearkey dbclient scp" STATIC=1

4) install dropbear generated binaries 
make PROGRAMS="dropbear dropbearkey dbclient scp" install


5) generate RSA and DSS keys 
dropbearkey -t dss -f dropbear_dss_host_key
dropbearkey -t rsa -f dropbear_rsa_host_key

6) run the dropbear 
# dropbear

7) make a SSh connection from pc 
ssh -l root 192.168.7.2





# use this command to install an openssh server on your ubuntu host 
sudo apt-get install openssh-server

















