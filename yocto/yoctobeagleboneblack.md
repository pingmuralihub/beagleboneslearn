

# Initially windows 11 as host machine, ubuntu 24.06 installed in vmware workstation, laptop is old configuration(Intel® Core™ i7-4700MQ CPU @ 2.40GHz × 8,  8Gb ram). While working with debian arm linux system get slow didn't impact work but yocto bitbake command execution time Laptop hanged. So i've decided to install ubutu as host machine in external usb hard drive.  

1. installed ubuntu 24.06 latest one, followed instruction as per the link "https://github.com/Munawar-git/YoctoTutorials/blob/master/00_Yocto_Intro/00-Yocto-Intro.md" following 
original command "sudo apt install  ..." not worked,tested indiduallay, found the not working command   
    sudo apt install gawk wget git diffstat unzip texinfo gcc build-essential chrpath socat cpio python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping python3-git python3-jinja2     libegl1-mesa libsdl1.2-dev pylint3 xterm python3-subunit mesa-common-dev zstd liblz4-tool
  
    libegl1-mesa is changed to libegl1-mesa-dev 
  
    pylint3 is no longer available
  
    working command and tested by murali
    sudo apt install gawk wget git diffstat unzip texinfo gcc build-essential chrpath socat cpio python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping python3-git python3-jinja2   libegl1-mesa-dev libsdl1.2-dev xterm python3-subunit mesa-common-dev zstd liblz4-tool

2. With ubuntu 24.06 latest one,after the "bitbake core-image-full-cmdline " command laptop restarts unexpectedly and the restart happened for 7 times. Then checked the "https://github.com/Munawar-git/YoctoTutorials/blob/master/00_Yocto_Intro/00-Yocto-Intro.md" weblink, they have used Ubuntu 18.04 (LTS). 

3. So installed 18.04, followed instruction as per the link "https://github.com/Munawar-git/YoctoTutorials/blob/master/00_Yocto_Intro/00-Yocto-Intro.md", it also didn't work as per the link
   a. vs code is hanged during execution of  "bitbake core-image-full-cmdline " 
   b. After execution of  "bitbake core-image-full-cmdline ", the output is stopped at 62% for 20times almost 2 days wasted.
   c. Then installed  Ubuntu 22.04 

4. After installing Ubuntu 22.04, followed instruction as per the link "https://github.com/Munawar-git/YoctoTutorials/blob/master/00_Yocto_Intro/00-Yocto-Intro.md",
    a. After execution of  "bitbake core-image-full-cmdline ", the output is not generated due to some warnings, tried 6 times with same 4 error message and almost wasted 2 days.
    b. Gone through several weblink, changed local.conf, uncomment the following lines and then it produced output with 3 warnings 
        BB_HASHSERVE_UPSTREAM = "hashserv.yoctoproject.org:8686"
        PACKAGE_CLASSES ?= "package_rpm package_deb package_ipk"

.











------------------------------------------------


