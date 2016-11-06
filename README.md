# rtl8812AU
This repository contains drivers for the rtl8812AU and rtl8821AU/rtl8811AU chipsets.

It started out because I found a newer driver then I found elsewhere, namely version 4.3.8.
But since then I found even newer versions released by Realtek and decided to use/update those too.  
If you find a newer version then I have, I'd appreciate it if you would share it.

Currently there are the following branches, named after the initial Realtek driver version.
- [version 4.3.8](https://github.com/diederikdehaas/rtl8812AU/tree/driver-4.3.8)
- [version 4.3.14](https://github.com/diederikdehaas/rtl8812AU/tree/driver-4.3.14)
- [version 4.3.22-beta](https://github.com/diederikdehaas/rtl8812AU/tree/driver-4.3.22-beta)

The driver (versions) are primarily targetted at [Debian](https://www.debian.org) and [Raspbian](https://www.raspbian.org), but I have no reason to assume it won't work for other distrubutions. If fixes are needed for other distrubution with no negative effect on Debian or Raspbian, I'll gladly incorporate those into my repository.

I have currently successfully compiled the driver on Debian kernel 3.2, 3.16, 4.1-4.8 and on Raspbian with kernel 3.18, 4.1 and 4.4.

Installing

Installing the driver is simply a matter of copying the built module into the correct location and updating module dependencies using depmod:

$ sudo cp 8812au.ko /lib/modules/$(uname -r)/kernel/drivers/net/wireless
$ sudo depmod
The driver module should now be loaded automatically.

DKMS

Automatically rebuilds and installs on kernel updates. DKMS is in official sources of Ubuntu, for installation do:

$ sudo apt-get install build-essential dkms 
The driver source mus be copied to /usr/src/8812au-4.3.14

Then add it to DKMS:

$ sudo dkms add -m 8812au -v 4.3.14
$ sudo dkms build -m 8812au -v 4.3.14
$ sudo dkms install -m 8812au -v 4.3.14
Check with:

$ sudo dkms status
Eventually remove from DKMS with:

$ sudo dkms remove -m 8812au -v 4.3.14 --all
