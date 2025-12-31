# Homelab Documentation

* KlipperPi (3D Printer)

## KlipperPi (3D Printer)

* OrangePi Zero 3 (1GB RAM)  
  * Debian Bookworm Server from orangepi (local copy)  
  * Klipper via [KIAUH](https://github.com/dw-0/kiauh)  
* Ender 3 V3 SE  
  * Firmware via KIAUH (local klipper.bin)  
* SD card 16GB (for the OrangePi)  
* SD card 8GB (for the 3D printer)

### Initial installation

Burned Debian image with Balena Etcher in SD card.  
Configured static IP and hostname.  
Installed Klipper, Moonraker and Mainsail via KIAUH (see KIAUH installation guide).  
Created klipper.bin  
>Run ´make menuconfig´ in klipper directory.  
>Select processor model STM32F103.  
>Select 28KiB bootloader.  
>Select Communication interface Serial on USART1 (PA10/PA9).  
>Save configuration and run ´make´.  
Save klipper.bin to another SD card.  
Run new firmware in the 3D printer.

### Configuration

printer.cfg from [0xD34D](https://github.com/0xD34D/ender3-v3-se-klipper-config/blob/main/printer-creality-ender3-v3-se-2023.cfg) on GitHub.  
	Added \[include mainsail.cfg\] at the start of the config file.  
