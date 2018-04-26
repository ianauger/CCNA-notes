# Chapter 8: Managing Cisco Devices

## The Configuration Register
* 16 bit number which determines startup behaviors
* Read as series of 4-bit nibbles - individual bits 15-0 from left to right
  * 0-3: Boot field
  * 6: if set, ignore NVRAM on startup
  * 7: OEM bit enabled
  * 8: Diable break on startup
  * 10: On startup, IP broadcast with all 0s
  * 5, 11-12: adjust console line speed
  * 13: boot default ROM if netboot fails
  * 14: IP broadcasts don't have net numbers
  * 15: enable diagnostic messages, ignore NVRAM
* Boot field:
  * 00: ROMMON mode
  * 01: Boot mini-IOS
  * 02-F: USe boot commands specified in NVRAM
* Config register can be used via sh ver
* 0x2102 is the normal settings
* From config mode, config-register changes current setting -- will be retained across reboots

## Boot system commands
* Let you change boot behaviors
* i.e.: boot system <location> lets you set a target to load IOS from
* Can stack directives -- i.e., try FTP, then TFTP, then boot from flash &c

## Password recovery
* Need to change bit 6 in the config register to disable loading startup-config from NVRAM
* Sequence:
  1. Issue break command during startup -- ctrl-break
  2. Change config register in ROMMON: confreg 0x2142
  3. Type I for initialize or reset, skip setup when prompted and enable privledged mode
  4. Copy startup config to running config
  5. Enter config mode, change enable password
  6. Change config register to 0x2102
  7. Copy run start to commit config and reload
  
## Backing up/restoring/upgrading IOS
* Recommended before upgrading in case it breaks something (duh)
* copy command used
  * If TFTP server used, it must be on same subnet as one of the router's ethernet interfaces, if using another router must ensure enough space in flash memory.
  * e.g. copy flash tftp, then follow prompts.
* show flash shows contents of flash and space available
* show ver has some of the same information, as well as the running IOS image
* same copy command also used to get new image on router

## Cisco IOS File System
* Can work with onboard memory using CLI using commands similar to DOS/UNIX
* Uses URLs -- e.g. "flash:/" shows root directory, "tftp://" for TFTP servers
* Commands:
  * dir
  * copy
  * move
  * show file
  * delete
  * erase/format
  * cd/pwd
  * mkdir/rmdir

## Licensing
* Router ships with more features than are enabled -- need to get licenses for subets of features
* Also have trial licensing to demo features and see if they are needs-suiting
* Default license is IPBase
* Addons:
  * Data (MPLS, ATM, multiprotocol support)
  * Unified Communications (VoIP)
  * Security (IOS firewall, IPS, IPSec, 3DES, VPN)
* Adding licenses
  * First find UDI - combination of unique product ID and S/N - show license udi
  * Get license either via Cisco License Manager or Cisco Product License Portal
  * Once you have PAK (product activation key), combine it with UDI to get license file
  * Copy license to router
  * From enable mode:
    * license install <license file on file system>
    * reload
* Right-to-Use trial activation
  * Add module using license boot module <router series> technology-package <package>
* Checking licenses:
  * show licenses shows which licenses are enabled, type, state, and period left
  * show license feature shows licenses and simple yes/no stats
  * show version shows basic technology packages 
* Backing up licenses
  * license save <dest>, usually flash
  * disable license: no license boot module...
  * license clear <package
  * reload
