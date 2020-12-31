# lenovo-yoga-920-hackintosh
Files for installing MacOS on Lenovo Yoga 920

### What Doesn't Work
* Fingerprint Sensor
* Many of the function buttons (paper display, refresh, airplane mode, lock, switch display, disable camera only sometimes works)
* Sleep is not fully working*
* ThunderBolt**
* 4K 60Hz***
* Battery Status (the patch provided in the Catalina guide never worked for me on Catalina or on Big Sur now. I believe we need to follow the patching guide.)
* Possibly other things
### What Works
* 4K display
* Trackpad (with full MacOS trackpad gestures)
* Touchscreen (with gestures as well curtesy of VoodooI2C.
* Audio (Realtek ALC298 detected)
* USB (as far as I've determined)
* NVMe
* WiFi with Broadcom BCM4352 (I swapped my wireless card out for a DW1520)
* Camera
* Apple iServices (iMessage, Facetime, iCloud--as long as you update your SMBIOS as described below)

*Regarding sleep, it appears that MacOS stops writing system logs, but the keyboard backlight and fan seem to be on. Also, the laptop is a bit warm. This will need further troubleshooting.

**I have not attempted to get Thunderbolt working. I believe we may need an updated patch. Although, we can probably reuse SSDTs found in the Cadtalina guide.

***Lilu.kext does not support 4K 60Hz displays related to user patching being disabled? So we are restricted to 48Hz for the time being. It sucks, but Big Sur VP9 support is nice, so it makes up for it for me. No disrespect for the maintainers/supporters of Lilu, but it's a bit annoying.

Please note, features I have not included do not have SSDT or other easy ACPI patches. I am strongly against DSDT patches, as they break with BIOS changes, are extremely fragile, and can break sleep, Apple iServices etc. No part of this guide requires DSDT patching.
### Installation

1. I used Install Disk Creator to download the Big Sur 11.1 update and write it to a USB.
 1. Please make sure the USB is formatted as GPT
1. I mounted the EFI partition on the USB with an, old, but highly useful tool called EFI MountainShow (or you could just use diskutil via command line as well)
1. Copy the EFI partition I provided to the EFI partition you mounted
1. Update the SMBIOS in the EFI > OC > config.plist with new BSN, Serial, and SmUUID
 1. I use Clover Configuator to generate these instead of the recommended GenSMBIOS script as it's quicker
 1. I recommend using PlistEdit Pro to edit the plist. Please note, SMBIOS information can be found at Root > PlatformInfo > Generic
1. Boot USB and follow installation
1. Once booted into MacOS open terminal and run

```
sudo pmset autopoweroff 0
sudo pmset powernap 0
sudo pmset standby 0
sudo pmset proximitywake 0
```

1. Finally, mount the EFI partition on the USB and on your system disk. Copy the EFI (or at least just BOOT and OC) to your EFI partition on your system disk.


After this, everything should be set. Please note, there ARE things to fix, but this should serve as a good starting spot for most folks, who don't mind the shortcomings currently described in the "What Doesn't Work" section. Enjoy!

### Resources

I would like to thank the following people whom helped me directly or by reusing content of their's I found (which I hope is alright):

[bakgds](https://www.tonymacx86.com/members/bakgds.2070721/)
[qxuchn](https://www.tonymacx86.com/members/qxuchn.2207934/)
[dortania's ​OpenCore guide](https://dortania.github.io/)
[Rehabman](https://www.tonymacx86.com/members/rehabman.429483/)

And so many more
