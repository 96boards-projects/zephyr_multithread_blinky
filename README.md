# 96Boards Carbon Basic Multi Thread Example
## Overview

This example demonstrates spawning of multiple threads using K_THREAD_DEFINE.

The example works by spawning  three threads. The first two threads control a
separate LED. Both of these LEDs (USR1 and USR2) have their individual loop
control and timing logic defined by separate functions.

The third thread, uart_out(), sends out messages on the UART using printk().

- blink1() controls the USR1 LED that has a 100ms sleep cycle
- blink2() controls the USR2 LED that has a 1000ms sleep cycle

Each thread is then defined at compile time using K_THREAD_DEFINE.

This example is available in the upstream Zephyr Source: https://github.com/zephyrproject-rtos/zephyr/tree/master/samples/basic/threads 
***

## Building

### COMPILE
```shell
$ cd zephyr_base
$ source zephyr-env.sh
$ cd samples/basic/threads
$ make
```

### Flashing via OTG
```shell
$ sudo make flash
```
