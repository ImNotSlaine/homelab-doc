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

* Burned Debian image with Balena Etcher in SD card.  
* Configured static IP and hostname.  
* Installed Klipper, Moonraker and Mainsail via KIAUH (see KIAUH installation guide).  
* Created klipper.bin  
	* Run `make menuconfig` in klipper directory.  
	* Select processor model STM32F103.  
	* Select 28KiB bootloader.  
	* Select Communication interface Serial on USART1 (PA10/PA9).  
	* Save configuration and run `make`.
* Save klipper.bin to another SD card.
* Run new firmware in the 3D printer.

### Configuration

printer.cfg from [0xD34D](https://github.com/0xD34D/ender3-v3-se-klipper-config/blob/main/printer-creality-ender3-v3-se-2023.cfg) on GitHub.  
	Added `[include mainsail.cfg]` at the start of the config file.  

## ClusterPi (Cluster with K3s)

* 3 x OrangePi Zero 3 (4GB RAM)
  * Debian Bookworm Server from orangepi (edited afterward)
  * K3s
* 3 x SD cards 64GB

### K3s Apps

* Longhorn
* Jellyfin
* NginxProxyManager
* PiHole - DNS Server

### Initial installation

* Burned Debian image with Balena Etcher in SD cards.
  * Changed the default orangepi repositories with the original Debian repo.
  * Edited the /etc/apt/sources.list to:

```
deb https://deb.debian.org/debian/ trixie contrib main non-free non-free-firmware
# deb-src https://deb.debian.org/debian/ trixie contrib main non-free non-free-firmware

deb https://deb.debian.org/debian/ trixie-updates contrib main non-free non-free-firmware
# deb-src https://deb.debian.org/debian/ trixie-updates contrib main non-free non-free-firmware

deb https://deb.debian.org/debian/ trixie-proposed-updates contrib main non-free non-free-firmware
# deb-src https://deb.debian.org/debian/ trixie-proposed-updates contrib main non-free non-free-firmware

deb https://deb.debian.org/debian/ trixie-backports contrib main non-free non-free-firmware
# deb-src https://deb.debian.org/debian/ trixie-backports contrib main non-free non-free-firmware

deb https://security.debian.org/debian-security/ trixie-security contrib main non-free non-free-firmware
# deb-src https://security.debian.org/debian-security/ trixie-security contrib main non-free non-free-firmware
```

* Run `sudo apt update` to update repositories.
  * Configured static IPs and hostname.
  * Run `sudo apt full-upgrade` for update from Bookworm to Trixie.
  * Run `sudo apt autoremove` to delete unused dependencies.
* Use GParted Live in external device to partition the SDs for later Longhorn implementation.
