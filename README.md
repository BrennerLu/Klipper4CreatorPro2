# Klipper4CreatorPro2
My shot at klipperising the FlashForge Creator Pro 2 3D-printer. My goal is a working printer without the need of swapping the mainboard

# Current State

Will never be implemented:
original Screen (seems fully proprietary, touch screens on MCUs are afaik not currently supported by Klipper)

To-Do:
Actually define build volume
get the second extruder working
create Slicer profile
get a screen alternative

Done:
All axis, except one extruder, are moving
Homing works
All fans are individually speed controllable
RGB-LEDs inside the chamber are working
Bed heater and thermistor are working
Both hotends and thermocouples are working

# Flashing
I replaced the original bootloader with the [CanBoot Bootloader by Arksine](https://github.com/Arksine/CanBoot) since I bricked the original software earlier by experimenting with an ST-Link. There are no protections in place for the STM32! It could be possible to flash Klipper with the original bootloader, but I am unable to try it.

# Compiling Klipper
I used the [Klipper-Fork by dockterj](https://github.com/dockterj/klipper) as base for my klipper install, since it implements the ADC-Chip ADS1118 into klipper. This IC measures the Type-K-Thermocouple at each of the extruders and sends the values via SPI to the MCU and isn't supported in the main branch of klipper.

I used following settings for compiling the firmware:
| Micro-controller Architecture | STMicroelectronics STM32 |
| Processor model | STM32F407 |
| Bootloader offset | 32KiB bootloader |
| Clock Reference | 8 MHz |
|Communication Interface | USB on PA11/PA12 |

I flashed the firmware via USB Serial

# Reverse engineering
To write the printer.cfg, I needed to know the pinout of the microcontroller. So I took the time and traced every single connection of the 144 pin microcontroller :D Known problems: one extruder isn't extruding
Documents are found in Klipper4CreatorPro2/reverseEngineering

# printer.cfg

I am currently working on the printer configuration. Axis are moving, but the end positions aren't really there. There is some work left to do. Since it's pretty work in progress, I won't make the printer.cfg public just yet.
