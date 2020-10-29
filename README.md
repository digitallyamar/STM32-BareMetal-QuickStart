# STM32-BareMetal-QuickStart

## What is this?
This is a repo containing STM32 baremetal bootloader code with C runtime environment. You can use this repo as a kick start template to start writing bare metal applications on top of it.

## How to use?
	- Clone the repo.

	- Switch to the STM32-BareMetal-QuickStart directory.

	- Run "make" to get a "STM32_BareMetal.bin" binary file in the "build" output directory.

	- Flash this file to your STM32 board using st-flash utility.
		- st-flash write STM32_BareMetal.bin 0x08000000

	- Debug Method 1: Using st-util
		- On terminal 1, run the command:
			- st-util
		- On terminal 2, run the command:
			- arm-none-eabi-gdb build/STM32_BareMetal.elf
			- In gdb, connect to the board using command:
				- target extended localhost:4242

	- Debug Method 2: Using openocd
		- On terminal 1, run the command:
			- openocd -f interface/stlink-v2.cfg -f target/stm32f4x.cfg
		- On terminal 2, run the command:
			- arm-none-eabi-gdb --nx -ex 'set remotetimeout unlimited' -ex 'set confirm off' -ex 'target remote 127.0.0.1:3333' -ex 'monitor reset halt' -ex 'monitor flash write_image erase build/STM32_BareMetal.bin 0x08000000' -ex 'monitor reset halt' build/STM32_BareMetal.elf
			- In gdb, connect to the board using command:
				- monitor reset halt
