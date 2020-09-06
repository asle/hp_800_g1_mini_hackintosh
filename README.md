![HP 800 G1](https://github.com/asle/hp_800_g1_mini/blob/master/hp_800_g1.png?raw=true)

# HP 800 G1 mini Hackintosh - OpenCore
The HP 800 G1 Mini is a tiny PC and first gen. of the HP 800 mini series. Perfect for hackintoshing!

## About this guide
This is not a complete tutorial but based on the [OpenCore Vanilla Desktop Guide for Haswell](https://dortania.github.io/OpenCore-Install-Guide/config.plist/haswell.html). I reccommend reading the guide carefully to understand OpenCore. Or else you will not learn anything! My goal with this guide is to help you avoid all the errors you would encounter. The guide is great but every PC is different and this one was a bit quirky and needed some tweaking to work! I assume you already have made an OS X install-USB.

## Specs
* Intel i7-4785T @ 2.20GHz (35w) 4-core/8-thread
* 16GB (2x8) DDR3 1600MHz
* M.2 NVMe AHCI 128GB drive
* 2.5" SSD Samsung 860 EVO 500GB
* BCM94360NG(M.2) wifi/bt card
* 65w external power supply
* OpenCore 0.6.0

## What is working
* Mac OS X 10.15.6
* Sleep
* Wifi/Bluetooth with new Broadcom card
* Multi-monitor (2)
* iMessage, AppStore
* AirDrop, Handoff etc.
* Dual-boot OS X / Windows 10

## About mini-PCs and this machine
I am fascinated by these small, cute Mac Mini-like PCs and have had my hands on many different models from Lenovo, HP and Dell. You can get the first gen. models very cheap online (much cheaper than a slower Mac Mini) and they pack a lot of power considering their small size and price. They are all easy to upgrade with RAM, hard drives and CPU. That is not possible with a Mac Mini! What differs these machines are mainly:
* Different Intel gen. 4th, 6th, 7th, 8th etc.
* RAM speed and max capacity
* USB3 / USB-C and USB3 speeds
* Single or dual drive capacity 
* Heat and noise differences
___
The HP 800 G1 is the first gen. in this series. It features a Haswell low-power cpu, up to 16gb RAM and 2 drive slots, 1 x M.2 sata and 1 x 2.5".

## Pros HP 800 G1 
* The "T" cpu runs cool
* Easy to open (thumbscrew)
* Simple to swap to 3rd party wifi/bt card (the HP 800 G4 would not accept the same wifi/bt card)
* Can install 2 hard drives
* Easy to install 2.5" hard drive

## Cons HP 800 G1 
* The fan on this are a bit noisier than others I have tested even when temps are low
* The CPU heatsink must be removed to swap the M.2 drive. Thus new thermal paste must be applied
* The M.2 drive is NVMe but only SATA meaning not better speed than a 2.5" SSD. 

## Installation
* I installed Windows10 on the drive and used [SSDTIME](https://github.com/corpnewt/SSDTTime)to generate the SSDTs. I copied these over to the ACPI folder. I can not guarantee these are perfect for your PC but I suggest you do this on your own HP 800 G1 to be sure.
* Copy over my EFI folder to the EFI partition
* Edit config.plist to enter new serialse UUID etc.

## USB port mapping
I have enclosed the USBports.kext derived from hackintool. It should work on your PC of this model.

## config.plist changes
I had a lot of different errors mostly related to "com.apple.AppleFSCompressionTypeDataLess load succeeded" and kernel panics. Coming from Clover I found the equivalent to 
"usb fixusbownership" which is "ReleaseUsbOwnership -> YES" in OpenCore. This seemed to fix those problems. And to be honest I don't remember all changes I did. You will see the [OC sanity checker](https://opencore.slowgeek.com/) complain about those changes :-)

## Wifi - Bluetooth
I am using the BCM94360NG from FENVI. This requires no extra kexts to work as it is recognized as a native card.

![BCM94360NG](https://github.com/asle/hp_800_g1_mini/blob/master/BCM94360NG.jpg?raw=true)

I also tested with a Dell 1820A wifi/bt card that is much cheaper and am using it in some other Hackintoshes. To make it work you have to add the airport* and brcm* kexts in the **Kexts_off** folder.  I do not reccomend these cards as some work and some don't. I had one left over and this must have been bad because I suddenly got kernel panics and all kinds of different boot errors. After many hours I removed the 1820A and everything was ok again! That is why I suggest to use the extra money on the BCM94360NG. It just works. I am not sure about the **AirportBrcmFixup.kext** since it only renames the wifi card to AirportExtreme. I did not see any speed difference with it. Have to test more.

