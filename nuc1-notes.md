# OpenBSD on a Intel NUC NUC7i5BNK

This file contains my notes on my journey to get something useful running OpenBSD on a Intel NUC that i got my hands on.

## Installation

Was easy and straightforward. I used the latest OpenBSD 7.6 release. All settings were default.
Before the installation i updated the BIOS (now only available from Asus, since Intel sold the NUC division to Asus).
Also i disabled everything in the BIOS that was not needed for a headless server.
I added a RTC wakeup time to the BIOS, so the NUC will wake up every day at 3:00 AM. Futhermore i set the NUC to power on when power is restored after a power failure.

### Hardware

Details on the system can be found on a [hardware probe of my NUC on bsd-hardware.info](https://bsd-hardware.info/?probe=4ebc19b4f9).

Installation by:

```sh
# go superuser
do su -
# install the latest release
pkg_add hw-probe
# and run it
hw-probe -all -upload
```

### Software installed

```sh
su
# Editor of my choice (nano), midnight commander, git
pkg_add nano mc git
```

## Get some monitoring

Next step will be to get some monitoring on the system.
