# Four-quadrant photoelectric sensor of laser positioning
This application is designed to show how to develop a new **Four-quadrant photoelectric sensor of laser positioning** using embARC. The design of the new structure consists of a ingenious combination of four silicon photoelectric semiconductors and a three-dimensional cross-gap structure. The whole positioning process is that the sensor converts the optical signal of the 532 nm laser into a photo-voltage output signal, and controls the laser to move to the center line of the two quadrants of the sensor through a difference algorithm, which is to verify the function of the new four-quadrant sensor.This design is mainly suitable for finding the energy center of the Gaussian laser spot, and the laser automatically follows the target.

* [Introduction](#introduction)
	* [Function](#function)
	* [System Architecture](#system-architecture)
* [Hardware and Software Setup](#hardware-and-software-setup)
	* [Required Hardware](#required-hardware)
	* [Required Software](#required-software)
	* [Hardware Connection](#hardware-connection)
* [User Manual](#user-manual)
	* [Before Running This Application](#before-running-this-application)
	* [Run This Application](#run-this-application)
* [DemoVideo](#demovideo)

## Introduction
**A new four-quadrant photoelectric sensor of laser positioning**

### Function

- **Laser spot positioning of any two quadrant center line**


- **Convert the optical signal of the 532 nm laser into a photo-voltage signal**


- **Solve the inconsistency of each quadrant parameter brought by the photoelectric semiconductor process** 


### System Architecture

![image](https://github.come/18292051032/mbarc_applications-arc_design_contest-2019-XDU_Four-quadrant-photoelectric-sensor-of-laser-positio/project picture/Positioning system schematic.png)

## Hardware and Software Setup
### Required Hardware
- 1 DesignWare ARC EM Starter Kit(EMSK)
- 1 Four-quadrant photoelectric sensor(Homemade)
- 1 Motor
- 1 Screw slider(CBX1610X-500)
- 1 Motor Driver Module(M6600)
- 1 Laser(532 nm)
- 1 AD sampling module(PCF8591)
- 1 PC
- 3 DC-DC boost module
- 1 DC-DC buck module
- 3 MOS field effect transistor(IRFP250N)

The list of hardware is shown in the picture following. 

![image](https://github.come/18292051032/mbarc_applications-arc_design_contest-2019-XDU_Four-quadrant-photoelectric-sensor-of-laser-positio/project picture/Positioning system schematic.png)

The four-quadrant photoelectric sensor is made by ourselves and the physical picture are shown below.

![image](https://github.com/Mandywualmighty/Auto-following-Suitcase-Application/blob/master/doc/screenshots/hardware.png)

### Required Software
- Metaware or ARC GNU Toolset
- Serial port terminal, such as putty, tera-term or minicom

### Hardware Connection
1. The EMSK implement that the center of the laser spot is positioned on the center line of any two quadrants. It will process the photo-voltage output signal, which is converted by the four-quadrant sensor. And display it in real time on the PC and send the command to the motor drive module, in order to achieve motor movement and direction correction. 
   - Connect four-quadrant photoelectric sensor to AD sampling module, connect AD sampling module to **J2**(Using GPIO interface).
   - Connect Motor driver module to MOS field effect transistor. Connect MOS field effect transistor to DC-DC boost module. Connect DC-DC boost module to **J3**.The detailed hardware connection picture is shown below.
   
![image](https://github.com/Mandywualmighty/Auto-following-Suitcase-Application/blob/master/doc/screenshots/hardware.png)
 
2. Configure your EMSKs with proper core configuration.

## User Manual
### Before Running This Application
Download source code of **Auto-following Suitcase** from github.

The hardware resources are allocated as following table.

|  Hardware Resource                  |            Function                           |
| ------------------------------------| ----------------------------------------------|
|  Four-quadrant photoelectric sensor |        Positioning module                     |
|  CBX1610X-500                       |        Screw slider module                    |
|  M6600                              |        Motor driver module                    |
|  Laser(532nm)                       |        Launch 532nm light source              |
|  PCF8591                            |        Pass photo-voltage signal              |
|  DC-DC boost module                 |        Powering the motor drive module        |
|  DC-DC buck module                  |        Powering the laser                     |
|  IRFP250N                           |        Providing Pulse signal                 |

### Run This Application

Here take **EMSK2.2 - ARC EM7D** with GNU Toolset for example to show how to run this application.

#### Makefile

- Target options about EMSK and toolchain:

		BOARD ?= emsk
		BD_VER ?= 22
		CUR_CORE ?= arcem7d
		TOOLCHAIN ?= gnu

- The relative series of the root directory, here the path of the Makefile is 

		#
		# root dir of embARC
		#
		EMBARC_ROOT = ../../..
		MID_SEL = common u8glib


See [ embARC Example User Guide][40], **"Options to Hard-Code in the Application Makefile"** for more detailed information about **Makefile Options**.

#### Driver

Placing the drivers' source code in `driver` folder, you can see there are subfolders for ultasonic,GPRS,ZPH01,buzzer and temperature drivers.
Placing the C source file and header file in the corresponding subfolder.

|  folder/file        |            Function           |
| ------------------- | ------------------------------|
|  ultrasonic         |       ultrasonic driver       |
|  temperature        |       temperature driver      |
|  GPRS               |       GPRS driver             |
|  ZPH01              |       ZPH01 driver            |
|  buzzer             |       buzzer driver           |


# DemoVideo

[Link](https://v.youku.com/v_show/id_XNDI4Nzg1MDEwOA==.html?spm=a2h3j.8428770.3416059.1)

[40]: http://embarc.org/embarc_osp/doc/embARC_Document/html/page_example.html   " embARC Example User Guide"
