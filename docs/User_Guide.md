# User Guide

**Early Disclaimer: CinePI-2K's [current release](https://github.com/schoolpost/CinePI/releases) is far from being considered stable, so use it at your own risk. Do not expect it to work flawlessly. Expect lots of bugs and dropped frames! This is just the nature of things, but hopefully through a collaborative effort, we'll get to a stable working version soon!**

## Installation

You find the current CinePI-2K release [here](https://github.com/schoolpost/CinePI/releases). The software is currently being distributed as a standalone operating system installation image for the Raspberry Pi (based on a modified [Raspberry Pi OS](https://www.raspberrypi.org/software/operating-systems/)). The source code will be made available in CinePI-2K's main GitHub repository. 

It is difficult to package CinePI as an installable "app" for existing Raspberry Pi operating system installations due to its particular dependencies on specific operating system/Linux kernel-level configurations. Releases and packaging will be assessed and revisited in the future. 

## Installation:
### Requirements:
 - Raspberry Pi 4 Model B with 4GB or more. Models with less RAM are untested. Currently, more RAM allows longer video takes, so the 8GB model is preferable.
 - Preferably an additional heat sink with cooling fans for the Raspberry Pi. These are being offered by various third-party manufacturers. It must leave access to the GPIO and camera ports.
 - Raspberry Pi High Quality Camera module
 - 8GB Micro SD card for the CinePI-2K operating system. (You can also use larger cards if 8GB are not available, but they won't offer any advantage.)
- Twin Dupont cable and a momentary push button. (These can be bought for a few dollars in any electronics supply store. If you don't want to solder, buy a push button with screw connectors.)
 - Fast external USB 3.x SSD drive to act as your camera's storage medium. Samsung's T5 drives are a proven solution. Other USB SSD drives (respectively USB housings for SATA or NVME SSDs) can be used if they support USB 3 and the UASP protocol. Make sure to connect the drive with the originally supplied USB cable, respectively with a USB 3 cable that reliably supports high transfer speeds. Slow media or wrong cables will result in dropped frames.

   The USB SSD disk can be formatted in **ExFAT** (universal file system for flash memory) / **EXT4** (Linux file system) / **NTFS** (Windows file system). EXT4 is recommended and performs currently the best, next best is ExFAT. NTFS is supported but not recommended due to ongoing development of the NTFS3 driver that is used in this release. 
   
   **Disks must be labeled "RAW" when being formatted. The CinePI-2K will not recognize disks without this label.** 
   
 - HDMI display/monitor, with a suitable cable to connect it to the Raspberry Pi's Micro HDMI port. A video field monitor (with focus peaking, zebras and punch-in focus) is recommended; budget models ($100-$200) are sufficient.
- For using the camera in the field, a USB power bank with power delivery (PD), or a comparable solution for mobile USB power (such as Blind Spot Gear's Power Junkie for Sony NP-F batteries if you want to use the same batteries for the camera and a video field monitor).
- For controlling the camera's settings (ISO, shutter angle, white balance), you need a smartphone app that talks to the CinePI-2K via Bluetooth using Blackmagic's Bluetooth camera control protocol originally developed for the Blackmagic Pocket 4K and 6K cameras. Existing iOS and Android apps for those cameras should be principally be able to control the CinePI-2K. The following iOS app has been tested and does work:

   - [Bluetooth+ for Blackmagic](https://apps.apple.com/us/app/bluetooth-for-blackmagic/id1376947780)
 
   The following Android app works principally, but not reliably:

  - [My Camera Controller](https://play.google.com/store/apps/details?id=com.taskdesigns786.android.mycameracontroller)

***
### Flashing
Download the zipped CinePI-2K image from the [release page](https://github.com/schoolpost/CinePI/releases) and unzip it.
You will need a disk flashing utility, such as these listed below:

 - [Etcher](https://www.balena.io/etcher/) (Windows, MacOS, Linux)
 - [Win32DiskImager](https://sourceforge.net/projects/win32diskimager/) (Windows)

Put your Micro SD card into an SD card reader connected to you computer (if necessary, using a full-size SD card adapter). Start the disk flashing utility, select the CinePI-2K image and flash it to the Micro SD card. 

***
### Configuration ( MUST READ ) 
CinePI-2K in its current form **heavily benefits from overclocking** above the base speed of the Raspberry Pi. The current release is configured with modest overclocking as its default. The overclocking settings can be changed in the **config.txt** file found in the boot partition of the CinePI-2K's Micro SD card (after you have successfully flashed it). 

**Use additional cooling and/or add a heatsink to your Raspberry Pi for best performance.** If possible, attempt to further push overclocking if your Raspberry Pi and cooling device allow it. Refer to online guides (such as [this one](https://magpi.raspberrypi.org/articles/how-to-overclock-raspberry-pi-4)) on how to properly  and safely overclock your Raspberry Pi. 

***
### Camera setup

For a visual installation guide, you can watch [this video](https://vimeo.com/517921653). Here are step-by-step instructions:

1. If available, mount your heat sink/cooler on the Raspberry Pi.

2. Attach your camera module with the ribbon band cable to the camera connector on the Raspberry Pi, as explained in the manual of the camera module. Use the tripod screw mount of the camera module to secure it on a tabletop micro tripod, clamp, magic arm or similar. 

3. Solder or screw the push button to the loose ends of the twin Dupont cable. Connect one cable with the Raspberry Pi's GPIO 4 and the other with Ground:

![Raspberry Pi 4b GPIO diagram](https://www.raspberrypi.org/documentation/usage/gpio/images/GPIO-Pinout-Diagram-2.png)

4. Screw your lens into the camera module. If you use a c-mount lens, keep the spacer ring on the camera module. If you use a CS mount (CCTV) lens, screw the spacer ring off the camera module. - In doubt, you can check later whether the lens will be able to focus to infinity, and remove or reattach the ring accordingly.

5. Put the Micro SD card that you flashed with the CinePI-2K software into the Raspberry Pi's Micro SD card slot.

6. Connect your HDMI monitor to the Raspberry Pi. (It doesn't matter to which of the two Micro HDMI ports.)

7. Optionally: connect your USB SSD drive to one of the Raspberry Pi's USB-A ports. (You can also do this later after CinePI-2K has booted.)


### First boot


- Switch on the monitor first. 

- Power up the Raspberry Pi by attaching it to USB power. 

- About 5-10 seconds later, you should be greeted with the CinePI-2K splash screen. Boot-up time can take another 30-60 seconds. Be patient. 

- After the Raspberry Pi has fully booted up, you should see a live view of what your camera can see. 

(The aim is optimize boot time in the future to under 10 seconds.)

#### Troubleshooting

If the camera image stays black even after waiting for a longer time, while you see the CinePI-2K's control display (showing ISO, shutter angle, system temperature etc.), make sure that the lens cap of your lens is off. 

If the image is still dark, point the camera to a light source, respectively a brighter lit scene, or increase ISO with the smartphone app (see section _Usage_). 

If your lens doesn't focus, but you only see a blurred-out image, either remove or (if you've already removed it) reattach the C-mount adapter screw mount ring that came with your Raspberry Pi's High Quality Camera module.

If the camera display is shifted and partly cut off, switch off the monitor and switch it on again (while leaving the CinePI-2K running).


***

### Usage

In addition to the live view you will see a number of other settings/parameters that are updated live according to state of the camera. 

 - The bottom left shows a live reading of the remaining / total disk space of your attached media. 
 - The bottom middle is live timecode indicator to show how long your recording is. 
 - The top right shows both the system temperature and CPU usage statistics. 

When you attach a USB 3.x SSD drive to the USB 3 slot of the Raspberry Pi, the disk will automatically be mounted and be ready for recording. (You will see the disk space in the bottom left being updated after your disk has been attached. If it indicates disk space that does not match the actual capacity of the drive you attached, then there might have been a mounting error. Re-attach the disk in this case.) 

To trigger recording, press the button (connected GPIO 4 and ground, as described in the section _Camera Preparation_). Video recordings can only be made onto an external disk attached via USB 3.x.

With the smartphone app (see section _Installation_), you can currently control the following parameters of the CinePI-2K:

 - Frame Rate ( 5-50fps @ 2028x1080 or 5-40fps @ 2028x1520 ) 
 - Shutter Angle
 - ISO
 - Resolution 

*** 

### Lens guide

[To be added.]

*** 

### Rigging

[Information on housings for the CinePI-2k will be added.]

If you use a heavy lens, such as a vintage c-mount zoom lens, support its weight with an extra holder underneath the lens barrel. You may consider putting the CinePI-2K on a video camera rig with 15mm/8inch rods and use a compatible lens support.

*** 

### Quirks

 - Bugs, bugs, bugs....(likely to be lots of other issues I've completely missed, please be ready to document/track these for them to be addressed.) 

***

### Developers

The source can be accessed straight from the Pi via SSH using the credentials:
-user: pi
-pwd: cinemapi


***
Hopefully you too will be able to get your own CinePI-2K up and running and capture some exceptional footage with this low-cost setup! (I would love to see the footage you capture so don't be afraid to share!) 

Track bugs in the issues section. I expect there will be lots at the start. 


