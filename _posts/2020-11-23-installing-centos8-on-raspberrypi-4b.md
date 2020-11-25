---
title: Installation of CentOS 8 on RaspberryPi 4 B"
date: 2020-11-23 23:30:00 +0900
categories: RaspberryPi
---

## Prerequisite

* RaspberryPi 4
  * Hope I don't need to explain this
* micro SD Card
  * RaspberryPi 4 uses micro SD card as main storage
* SD Card writer
  * Needed for flashing CentOS image to the SD card
* HMDI to micro cable
  * RaspberryPi4 uses micro HDMI port for HDMI output. 
  * You'll need to see the screen of RaspberryPi4 until you finish step in this blog to connect to you RaspberryPi via ssh over the network.
* USB pluggable keyboard
  * A keyboard needs to be plugged in you RaspberryPi to type commands for the first boot configuration.

## Downloading centOS 8

First you will need to download CentOS 8 for Raspberry Pi. You can find the image from:
https://people.centos.org/pgreco/CentOS-Userland-8-stream-aarch64-RaspberryPI-Minimal-4/

Use this command to extract the xz file in Mac.
```shell
brew install xz
xz -d filename.xz
```

## Flashing the image to a SD card

The next step is to flash the OS to a SD card.

Thanks to Etcher you don't have to use command line interface for flashing SD card.
* Download Etcher: https://www.balena.io/etcher/

Flashing the CentOS 8 image to a SD card using Etcher should be pretty straightforward.


## The first boot
Slide the SD card into your RaspberryPi and plug USB-C for the power and micro HDMI for display.

### The first login
If everything went well, you'll see the prompt asking you the login user and password.
Use this default account for your first boot.
* localhost login: root
* password: centos

Let's change the password
```
passwd
```

### Configuring WiFi
Let's configure WiFi connection so that you can ssh into your RaspberryPi from your laptop.
I used these nmcli commands that comes with CentOS 8 for setting up wireless connection.

List all the network devices
```
nmcli d
```

To make sure wifi is turned on
```
nmcli r wifi on
```

List WiFi networks
```
nmcli d wifi list
```

To connect to a WiFi network
```
nmcli d wifi connect <network name> password <password>
```

To make sure the connection is established
```
nmcli d
```

Check the IP address
```
ifconfig
```

### Adding user

Add a user for better safety and avoid using root

```
useradd <username>
passwd <username>
usermod -aG wheel <username>
```

The last command adds your new account to `wheel` group that grants the account a special privileges, so you can skip it for normal users.

### SSH

Everything should be ready for now for remote ssh connection.

Test if you can connect to your RaspberryPi via SSH over the network.

```
ssh <username>@<ip_address>
```

## References
* http://reallyappreciate.com/raspberry-pi-4-8gb-model-with-centos-8/
* https://core.docs.ubuntu.com/en/stacks/network/network-manager/docs/configure-wifi-connections