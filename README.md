# 96Boards Carbon Basic Multi Thread Example

This example demonstrates spawning of multiple threads using K_THREAD_DEFINE.

# Table of Contents
- [1) Hardware requirements](#1-hardware-requirements)
- [2) Software](#2-software)
   - [2.1) Build Environment Setup](#21-build-environment-setup)
- [3) Overview](#3-overview)
- [4) Building and Running](#4-building-and-running)
- [5) Conclusion](#4-conclusion)

# 1. Hardware requirements:

1. [96Boards Carbon IE](https://www.96boards.org/product/carbon/)

# 2. Software

## 2.1 Build Environment Setup

- Follow the official Zephyr documentation to setup build environment
	- [Linux](http://docs.zephyrproject.org/getting_started/installation_linux.html)
	- [macOS](http://docs.zephyrproject.org/getting_started/installation_mac.html)
	- [Windows](http://docs.zephyrproject.org/getting_started/installation_mac.html)

# 3. Overview

The example works by spawning  three threads. The first two threads control a
separate LED. Both of these LEDs (USR1 and USR2) have their individual loop
control and timing logic defined by separate functions.

The third thread, uart_out(), sends out messages on the UART using printk().

- blink1() controls the USR1 LED that has a 100ms sleep cycle
- blink2() controls the USR2 LED that has a 1000ms sleep cycle

Each thread is then defined at compile time using K_THREAD_DEFINE.

This example is available in the upstream Zephyr Source: https://github.com/zephyrproject-rtos/zephyr/tree/master/samples/basic/threads

# 4. Building and Running

- **Compile**
```shell
$ cd zephyr_base
$ source zephyr-env.sh
$ cd samples/basic/threads
$ make
```

- **Flashing via OTG**
	- Connect the micro-USB cable to the USB OTG Carbon port and to your computer. The board should power ON. Force the board into DFU mode by keeping the BOOT0 switch pressed while pressing and releasing the RST switch
	- You should see following confirmation on your Linux host:
	```shell
	$ dmesg
	usb 1-2.1: new full-speed USB device number 14 using xhci_hcd
	usb 1-2.1: New USB device found, idVendor=0483, idProduct=df11
	usb 1-2.1: New USB device strings: Mfr=1, Product=2, SerialNumber=3
	usb 1-2.1: Product: STM32 BOOTLOADER
	usb 1-2.1: Manufacturer: STMicroelectronics
	usb 1-2.1: SerialNumber: 3574364C3034
	```
	- Flash
	```shell
	$ sudo make flash
	```

- **Running**
	- Push the RST button
	- You will be able to see USR1 and USR2 LEDs Flashing
	- To see the UART output
		- Connect the micro-USB cable to the USB UART (FTDI) port and to your computer. Run your favorite terminal program to listen for output.
		```shell
		minicom -D <tty_device> -b 115200
		```
		- Replace <tty_device> with the port where the board 96Boards Carbon can be found. For example, under Linux, /dev/ttyUSB0. The -b option sets baud rate. Press the Reset button and you should see the the following message in your terminal

# 5. Conclusion

K_THREAD_DEFINE function provides a simple way to do multi-threaded programming on an MCU on the Zephyr RTOS. However, K_THREAD_DEFINE also provides extreme combustibility and control as described in the official documentation for Kernel Threads API: http://docs.zephyrproject.org/api/kernel_api.html#threads  
