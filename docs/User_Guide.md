# User Guide

**Early Disclaimer: CinePI-2K's [current release](https://github.com/schoolpost/CinePI/releases) is far from being considered stable, so use it at your own risk. Do not expect it to work flawlessly. Expect lots of bugs and dropped frames! This is just the nature of things, but hopefully through a collaborative effort, we'll get to a stable working version soon!**

## Installation

You find the current CinePI-2K release [here](https://github.com/schoolpost/CinePI/releases). The software is currently being distributed as a standalone operating system installation image for the Raspberry Pi (based on a modified [Raspberry Pi OS](https://www.raspberrypi.org/software/operating-systems/)). The source code will be made available in CinePI-2K's main GitHub repository. 

It is difficult to package CinePI as an installable "app" for existing Raspberry Pi operating system installations due to its particular dependencies on specific operating system/Linux kernel-level configurations. Releases and packaging will be assessed and revisited in the future. 

### Installation Requirements:
 - Raspberry Pi 4 Model B with 4GB or more. Models with less RAM are untested. Currently, more RAM allows longer video takes, so the 8GB model is preferable.
 - Preferably an additional heat sink with cooling fans for the Raspberry Pi. These are being offered by various third-party manufacturers. It must leave access to the GPIO and camera ports.
 - Raspberry Pi High Quality Camera module
 - 8GB Micro SD card for the CinePI-2K operating system. (You can also use larger cards if 8GB are not available, but they won't offer any advantage.)
- Twin Dupont cable and a momentary push button. (These can be bought for a few dollars in any electronics supply store. When the CinePi isn't built into a protective camera housing, a push button with screw connectors for the cables will be more robust than a push button that requires soldering the cables to it.) You can also skip the push button and simply leave the two blank cable ends available to the camera operator, who would then have to briefly short-circuit them in order to trigger recording.
 - A fast external USB 3.x SSD drive to act as your camera's storage medium. Samsung's T5 drives are a proven solution. Other USB SSD drives (respectively USB housings for SATA or NVME SSDs) can be used if they support USB 3 and the UASP protocol. Make sure to connect the drive to one the Raspberry Pi's USB 3 ports (the ones with the blue socket) using the USB cable included with the drive, or a USB 3 cable that reliably supports high transfer speeds. Slow media or wrong cables will result in dropped frames.

   The USB SSD disk can be formatted in **ExFAT** (universal file system for flash memory) / **EXT4** (Linux file system) / **NTFS** (Windows file system). EXT4 is recommended and performs currently the best, next best is ExFAT. NTFS is supported but not recommended due to ongoing development of the NTFS3 driver that is used in this release. 
   
   **Disks must be labeled "RAW" when being formatted. The CinePI-2K will not recognize disks without this label.** 
   
 - HDMI display/monitor, with a suitable cable to connect it to the Raspberry Pi's Micro HDMI port. A video field monitor (with focus peaking, zebras and punch-in focus) is highly recommended; budget models ($100-$200) are sufficient.
- For using the camera in the field, a USB power bank with power delivery (PD), or a comparable solution for mobile USB power (such as [Blind Spot Gear's Power Junkie](https://www.blindspotgear.com/power-junkie) for Sony NP-F batteries if you want to use the same batteries for the camera and a video field monitor).
- For controlling the camera's settings (ISO, shutter angle, white balance), you need a smartphone app that talks to the CinePI-2K via Bluetooth using Blackmagic's Bluetooth camera control protocol originally developed for the Blackmagic Pocket 4K and 6K cameras. Existing iOS and Android apps for those cameras should be principally be able to control the CinePI-2K. The following iOS app has been tested and does work:

   - [Bluetooth+ for Blackmagic](https://apps.apple.com/us/app/bluetooth-for-blackmagic/id1376947780)
 
   The following Android app works principally:

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

3. Solder or screw the push button to the loose ends of the twin Dupont cable, or leave the loose ends available to the camera operator. Connect one cable with the Raspberry Pi's GPIO 4 and the other with Ground. A GPIO diagram can be found [here](https://www.raspberrypi.org/documentation/usage/gpio/) in the documentation of the Raspberry Pi project.

4. Screw your lens into the camera module. If you use a c-mount lens, keep the 5mm spacer ring on the camera module. If you use a CS mount (CCTV) lens, screw the spacer ring off the camera module. - In doubt, you can check later whether the lens will be able to focus to infinity, and remove or reattach the ring accordingly.

5. Put the Micro SD card that you flashed with the CinePI-2K software into the Raspberry Pi's Micro SD card slot.

6. Connect your HDMI monitor to the Raspberry Pi. (It doesn't matter to which of the two Micro HDMI ports.)

7. Optionally: connect your USB SSD drive to one of the Raspberry Pi's USB-A ports. (You can also do this later after CinePI-2K has booted.)


### First boot

- Switch on the monitor first. 

- Power up the Raspberry Pi by attaching it to USB power. 

- About 5-10 seconds later, you should be greeted with the CinePI-2K splash screen. Boot-up time can take another 30-60 seconds. Be patient. 

- After the Raspberry Pi has fully booted up, you should see a live view of what your camera can see. 

(The aim is optimize boot time in the future to under 10 seconds.)

### Troubleshooting

- If the camera image stays black even after waiting for a longer time, while you see the CinePI-2K's control display (showing ISO, shutter angle, system temperature etc.), make sure that the lens cap of your lens is off. 

- If the image is still dark, point the camera to a light source, respectively a brighter lit scene, or increase ISO with the smartphone app (see section _Usage_). 

- If your lens doesn't focus, but you only see a blurred-out image, either remove or (if you've already removed it) reattach the C-mount adapter screw mount ring that came with your Raspberry Pi's High Quality Camera module.

- If the camera display is shifted and partly cut off, switch off the monitor and switch it on again (while leaving the CinePI-2K running).


***

## Usage

In addition to the live view you will see a number of other settings/parameters that are updated live according to state of the camera. 

 - The bottom left shows a live reading of the remaining / total disk space of your attached media. 
 - The bottom middle is live timecode indicator to show how long your recording is. 
 - The top right shows both the system temperature and CPU usage statistics. 

When you attach a USB 3.x SSD drive to the USB 3 slot of the Raspberry Pi, the disk will automatically be mounted and be ready for recording. (You will see the disk space in the bottom left being updated after your disk has been attached. If it indicates disk space that does not match the actual capacity of the drive you attached, then there might have been a mounting error. Re-attach the disk in this case.) 

To trigger recording, press the button or - if you didn't install a button - briefly short-circuit the two cable ends (connected to GPIO 4 and ground, as described in the section _Camera Preparation_). Video recordings can only be made onto an external disk attached via USB 3.x.

With the smartphone app (see section _Installation_), you can currently control the following parameters of the CinePI-2K:

 - Frame Rate ( 5-50fps @ 2028x1080 or 5-40fps @ 2028x1520 ) 
 - Shutter Angle
 - ISO
 - Resolution 

*** 

## Lens guide

### CS mount vs. c-mount

The Raspberry High Quality Camera module supports two types of lenses: 

1. CS mount (a standard for CCTV cameras)
2. c-mount (an older standard for 8mm and 16mm film cameras as well as for CCTV video cameras). 

Both are screw mounts with identical diameters and mechanics. C-mount and CS mount lenses are indistinguishable from each other unless they have been labeled. The only difference between the two mounts is that CS mount has a shorter flange focal distance (i.e. a shorter distance between lens and sensor) of 12.526 mm than c-mount (17.526 mm). The black adapter ring included with the Raspberry Pi's High Quality Camera module serves as a 5mm spacer to make c-mount lenses fit the camera and have them correctly focus to infinity.

The Raspberry Pi Foundation sells inexpensive 6mm and 16mm CS mount lenses for the High Quality Camera module, which act as wide-angle and moderate tele lenses respectively. On internet marketplaces, you can easily find other CS mount and c-mount lenses, including vintage c-mount lenses for 8mm and 16mm cameras. As a rule of thumb, modern CS mount lenses will give your footage a high contrast video look, old c-mount lenses a softer and more filmic look. (Note: vintage film camera lenses can be pricey collectibles. It often makes more sense to look for defect old film cameras that include suitable - removable - lenses.)

Modern, high-resolution lenses are also more likely to provoke aliasing and moiré artefacts on the CinePi's recorded footage while lower-resolution vintage soften the image and thus prevent moiré.

### Sensor coverage and focal lengths

The Raspberry Pi High Quality Camera module uses a 1/2.3" sensor with a size of 7.564 * 5.476 mm. This means that CCTV lenses made for 1/2" sensors will cover the camera image without vignetting (i.e. without black corners). 

In analog film terminology, the CinePi's sensor size of 7.564 * 5.476 mm sit right in between Super 8 (5.79 * 4,01 mm) and 16mm (10.26 * 7.49 mm) and is best comparable to Pathé's 9.5mm film format (8.2 * 6.15 mm).

16mm c-mount film lenses will therefore always cover the CinePi sensor without issues. According to our experience, Super 8 c-mount zooms can vignette at wide-angle settings. Adapted d-mount 8mm prime lenses (see next section) however tend to cover the sensor. (This also includes Kern's c-mount lenses for the Bolex H8 camera. They have a shorter flange focal distance than standard c-mount and can screwed on the CinePI without the c-mount spacer ring.)

Here's an overview of focal lengths for the CinePi, in comparison to common focal lengths for 35mm stills/full frame cameras:

|	| super wide-angle | standard wide-angle | slight wide-angle | normal   | portrait tele | standard tele | super tele |
|---------------------|---------------------|---------------------|---------------------|-------------------|----------|---------------|---------------|
| CinePi | 5 mm | 6 mm             | 7 mm           |  10.5 mm | 18 mm      | 21 mm         | 38mm
| 35mm full frame photo camera (for comparison) | 24 mm	| 28 mm               | 35 mm             | 50 mm    | 85 mm         | 100 mm        | 180 mm


### Adapting other lens mounts

D-mount lenses for Regular 8mm cameras (i.e. the older, 8mm reel-to-reel format with an image size of 4.5 * 3.3 mm that preceded Super 8) can be used on the CinePi with the help of a d-mount to c-mount adapter ring (manufactured by [Fotodiox](https://fotodioxpro.com/products/d-c-p)). Since d-mount has almost the same flange focal distance as CS mount (12.29 mm vs. 12.526 mm), such an adapted lens can be directly screwed onto the camera.

In the past, a number of lens mount adapters for common 35mm photo camera bayonets (Leica, Nikon F, M42, Minolta etc.) to c-mount were produced. These adapters can be used for mounting older manual photo camera lenses to the CinePi. However, the typical focal lengths of these lenses will make turn them into extreme tele focal lengths on the camera.

### Flange focal distance / back focus calibration

The thin, black, jagged metal rotating ring behind the lens mount is for fine-tuning the flange focal distance (respectively back focus) of any lens screwed onto the High Quality Camera module. This is a very useful feature of the camera module and particularly important for using 8 and 16mm parfocal film camera zoom lenses with the CinePi. Parfocality means that a zoom lens stays in focus when being zoomed in and out. (Most photo camera and cheaper CCTV zoom lenses aren't parfocal and lose focus while zooming.) 

The best way to calibrate the back focus for a lens is to set its focus to infinity, point it at a far away object (such as a landmark on the horizon) and turn the back focus adjustment ring until the lens perfectly reaches infinity focus. 

To set correct back focus for a parfocal zoom lens, the lens should first be calibrated to infnity as described above, then be focused onto a nearby object (in ca. 1-2m meters distance), zoomed in and out while fine-tuning back focus until the object stays in focus. 

*** 

## Rigging

[Information on housings for the CinePI-2k will be added.]

If you use a heavy lens, such as a vintage c-mount zoom lens, support its weight with an extra holder underneath the lens barrel. You may consider putting the CinePI-2K on a video camera rig with 15mm/8inch rods and use a compatible lens support.

*** 

## Quirks

 - Bugs, bugs, bugs....(likely to be lots of other issues I've completely missed, please be ready to document/track these for them to be addressed.) 

***

## Developers

The source can be accessed straight from the Pi via SSH using the credentials:
-user: pi
-pwd: cinemapi


***
Hopefully you too will be able to get your own CinePI-2K up and running and capture some exceptional footage with this low-cost setup! (I would love to see the footage you capture so don't be afraid to share!) 

Track bugs in the issues section. I expect there will be lots at the start. 


