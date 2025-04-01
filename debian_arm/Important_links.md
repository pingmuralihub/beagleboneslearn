# Beagle bone related flash scripts availble in this link
https://github.com/rcn-ee/repos
https://github.com/rcn-ee/repos/blob/master/bb-beagle-flasher/suite/bullseye/debian/beagle-flasher


# sync command usage with clear explaination
https://phoenixnap.com/kb/linux-sync

# usb and eth not working to working solution
https://forum.beagleboard.org/t/usb-and-ethernet-interfaces-are-not-visible-to-me/36157/6

# Beaglebone software images -> you can download the image based on the board ie. beaglebone black or beaglebone ai
https://www.beagleboard.org/distros

# Course Repository 
https://github.com/niekiran/EmbeddedLinuxBBB


# Angstrom Demo images for BBB
http://downloads.angstrom-distribution.org/demo/beaglebone/

# Uboot Source code 
https://ftp.denx.de/pub/u-boot/


# TI AM335x Driver guide
ALL the kernel driver related info is available in the following link
https://software-dl.ti.com/processor-sdk-linux/esd/docs/latest/linux/Foundational_Components_Kernel_Drivers.html


http://processors.wiki.ti.com/index.php/AM335x_LCD_Controller_Driver%27s_Guide
http://processors.wiki.ti.com/index.php/AM335x_Touchscreen_Driver%27s_Guide
http://processors.wiki.ti.com/index.php/AM335x_McSPI_Driver%27s_Guide
http://processors.wiki.ti.com/index.php/AM335x_MMC/SD_Driver%27s_Guide
http://processors.wiki.ti.com/index.php/AM335X_DCAN_Driver_Guide
http://processors.wiki.ti.com/index.php/AM335x_ADC_Driver%27s_Guide


arc/arm/kernel
head.s

        /*
         * The following calls CPU specific code in a position independent
         * manner.  See arch/arm/mm/proc-*.S for details.  r10 = base of
         * xxx_proc_info structure selected by __lookup_processor_type
         * above.
         *
         * The processor init function will be called with:
         *  r1 - machine type
         *  r2 - boot data (atags/dt) pointer
         *  r4 - translation table base (low word)
         *  r5 - translation table base (high word, if LPAE)
         *  r8 - translation table base 1 (pfn if LPAE)
         *  r9 - cpuid
         *  r13 - virtual address for __enable_mmu -> __turn_mmu_on
         *
         * On return, the CPU will be ready for the MMU to be turned on,
         * r0 will hold the CPU control register value, r1, r2, r4, and
         * r9 will be preserved.  r5 will also be preserved if LPAE.
         */



