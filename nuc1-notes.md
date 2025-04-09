# OpenBSD on a Intel NUC NUC7i5BNK

This file contains my notes on my journey to get something useful running OpenBSD on a Intel NUC that i got my hands on.

## Installation

Was easy and straightforward. I used the latest OpenBSD 7.6 release. All settings were default.
Before the installation i updated the BIOS (now only available from Asus, since Intel sold the NUC division to Asus).
Also i disabled everything in the BIOS that was not needed for a headless server.
I added a RTC wakeup time to the BIOS, so the NUC will wake up every day at 3:00 AM. Futhermore i set the NUC to power on when power is restored after a power failure.

### Network

I have a static IP address on my network, so i set the router to route the public ports 80 and 443 to the NUC.

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

## confiure doas

Howto from <https://docs.vultr.com/introduction-to-doas-on-openbsd>:

```sh
# add user to wheel group
usermod -G wheel haenno
# add doas to the wheel group
echo "permit persist :wheel" >> /etc/doas.conf
```

## Get some monitoring

Current temperature can be shown with `sysctl`:

```sh
nuc1# sysctl -a | grep "hw.sensors" | grep "degC"
hw.sensors.cpu0.temp0=42.00 degC
hw.sensors.pchtemp0.temp0=45.00 degC
```

## setup grafana and prometheus

Howto from <https://findelabs.com/post/grafana-prometheus-monitoring-openbsd/>

<https://ports.to/path/sysutils/loki,-promtail.html>

<https://www.tumfatig.net/2018/monitoring-openbsd-using-collectd-influxdb-and-grafana/>

## Get a webserver with SSL running

Howto from <https://www.openbsdhandbook.com/services/webserver/ssl/>.

Note: Example configs need to be copyied and a example index.html file needs to be created in a webroot directory.

```sh
cp -p /etc/examples/acme-client.conf /etc/
cp -p /etc/examples/httpd.conf /etc/
mkdir /var/www/htdocs/haenno.de
nano /var/www/htdocs/haenno.de/index.html
```

Credit also to: <https://obsd.solutions/en/blog/2022/03/04/openbsd-acme-client-70-for-letsencrypt-certificates/index.html>

## python on openbsd

 pkg_add py3-virtualenv
 python3 -mvenv /path/to/venv  # to create
 . /path/to/venv/bin/activate  # to use

## Commands Cheatsheet

Last logs: ``tail -f /var/log/daemon``
