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

- **Ambient temperature and air condition monitoring**

![image](https://github.com/Mandywualmighty/Auto-following-Suitcase-Application/blob/master/doc/screenshots/Temperature%20and%20PM2.5%20monitoring.png   "Temperature and PM2.5 monitoring" )

- **obstacle avoiding**

![image](https://github.com/Mandywualmighty/Auto-following-Suitcase-Application/blob/master/doc/screenshots/obstacle%20avoiding.gif   "obstacle avoiding")

- **Auto-following** 

![image](https://github.com/Mandywualmighty/Auto-following-Suitcase-Application/blob/master/doc/screenshots/Auto%20following.gif "Auto-following")

- **Auto-alarm** (The device will sound the alarm when the distance between one and suitcase is longer than 4 meters, and call the mobile phone when it is longer than 5.5 meters)

![image](https://github.com/Mandywualmighty/Auto-following-Suitcase-Application/blob/master/doc/screenshots/Auto-alarm.gif)


### System Architecture

![image](https://github.com/Mandywualmighty/Auto-following-Suitcase-Application/blob/master/doc/screenshots/System%20architecture.png  "System architecture")

## Hardware and Software Setup
### Required Hardware
- 1 DesignWare ARC EM Starter Kit(EMSK)
- 1 Digilent PMOD TMP2
- 1 Dust Sensor(ZPH01)
- 1 Display Screen(OLED)
- 1 Buzzer
- 1 GPRS Module(SIM900A)
- 2 Motor Driver Module(TB6612FNG)
- 4 Positioning Module(DWM1000)
- 4 Wheel
- 4 Motor
- 1 SD Card
- 3 Ultrasonic Sensor(HCSR04)

The list of hardware is shown in the picture following. 

![image](https://github.com/Mandywualmighty/Auto-following-Suitcase-Application/blob/master/doc/screenshots/hardware.png)

### Required Software
- Metaware or ARC GNU Toolset
- Serial port terminal, such as putty, tera-term or minicom

### Hardware Connection
1. The EMSK implement **Auto-folowing** smart device, it will process the data returned by positioning module and ultrasonic sensor,and send instructions to motor driver module.It can also monitor temperature and dust concentration of air,we can view these data on OLED. 
   - Connect **Positioning module** to **J1**(Using UART interface), connect **Motor driver module** to **J3** and **J6**,connect **Ultrasonic sensor** to **J1** and **J3**.
   - Connect **PMOD TMP2** to **J4**(Using IIC interface), connect **ZPH01** to **J5**(Using uart interface),connect **OLED** and **GPRS** to **J2**(Using IIC interface),connect **Buzzer** to **J6**.
2. Configure your EMSKs with proper core configuration.

## User Manual
### Before Running This Application
Download source code of **Auto-following Suitcase** from github.

The hardware resources are allocated as following table.

|  Hardware Resource  |            Function                                           |
| ------------------- | ------------------------------------------------------------- |
|  PMOD TMP2          |        Temperature sensor                                     |
|  ZPH01              |        Dust sensor                                            |
|  OLED               |        Display screen                                         |
|  SIM900A            |        Send messages or call                                  |
|  TB6612FNG          |        Motor driver module                                    |
|  HCSR04             |        Dust sensor                                            |
|  OLED               |        Ultrasonic sensor                                      |
|  DWM1000            |        Positioning module                                     |

- Modify mux.c (/board/emsk/common/emsk_init.c)
```
line 107: change 
	set_pmod_mux(PM1_UR_UART_0 | PM1_LR_SPI_S	\
				| PM2_I2C_HRI		\
				| PM3_GPIO_AC		\
				| PM4_I2C_GPIO_D	\
				| PM5_UR_SPI_M1 | PM5_LR_GPIO_A	\
				| PM6_UR_SPI_M0 | PM6_LR_GPIO_A );
 to 
	set_pmod_mux(mux_regs, PM1_UR_UART_0 | PM1_LR_GPIO_A	\
				| PM2_I2C_HRI			\
				| PM3_GPIO_AC			\
				| PM4_I2C_GPIO_D		\
				| PM5_UR_GPIO_C | PM5_LR_SPI_M2	\
				| PM6_UR_GPIO_C | PM6_LR_GPIO_A );
```
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

[Link](https://v.youku.com/v_show/id_XMzYyOTY0MjcwMA==.html?x&sharefrom=android&sharekey=47f57584b11aa1e3916e149dc1b044aa0)

[40]: http://embarc.org/embarc_osp/doc/embARC_Document/html/page_example.html   " embARC Example User Guide"
