---
id: installation
title: Installing RatOS
sidebar_label: Installation
sidebar_position: 1
---

# Installation

## Raspberry Pi Installation

:::warning USE PROPER AUTHENTIC SD CARDS
There are multiple examples of bad quality sd cards causing boot and corruption issues. It's highly recommended to get SanDisk Ultra U1 A1 cards (16GB or larger) from an official source to ensure long life and reliable operation of your Raspberry Pi.
:::

Download the newest release (download the RatOS-\*.img.xz file under the assets dropdown) of [RatOS on github](https://github.com/Rat-Os/RatOS/releases/latest).
Then use [Balena Etcher](https://www.balena.io/etcher/) to write that image to the SD card that goes into your raspberry pi (16GB or larger).

Note: this will destroy all data on the card!

:::info
For Raspberry Pis with 1gb or less memory, it's recommended to use the 32-bit (`rpi32`) version of the image. 64-bit (`rpi64`) causes too high memory usage in some situations.
:::

<a class="button button--primary" href="https://github.com/Rat-Os/RatOS/releases/latest">Download RatOS</a>

### WIFI or Ethernet

When the RatOS image has been written to the SD card, insert the SD card into the Raspberry Pi and turn on the Pi. After a few minutes the raspberry pi will host a hotspot called "RatOS", join this hotspot on your phone or a PC/Laptop with wifi, the password is "raspberry". When connected, open [http://RatOS.local/configure](http://RatOS.local/configure) or [http://192.168.50.1/configure](http://192.168.50.1/configure) and follow the steps presented there to setup wifi and your printers hostname.

Alternatively, if you're using a pi with Ethernet, you can use an ethernet cable instead.

:::danger Internet Connection is required on first run!
There's currently a limitation in RatOS that **requires internet access** on first run. Klipper cannot compile it's c_helper functions without being connected to the internet.
If you proceed through board flashing without the pi connected to the internet, you'll get an error saying your board is not responsive, even after it's been flashed succesfully.

After succesfull flashing and detection in the configurator, an internet connection is nolonger required for operation, nor subsequent flashing.
:::

## Preparing your control board

:::info
It is heavily recommended that you flash your board and make sure it is detected in the configurator **before** you plug in your stepper drivers and start connecting your wiring.

It may be required for you to use an SD Card to initially flash your board. If this is required, then be sure to use a good quality SD card that is no more than 32GB in size. Additionally, it should be formatted with either FAT16 (sometimes just called FAT), or FAT32 with a cluster size of 8kb or 4kb
:::

After completing the wifi setup wizard, wait a couple of minutes, then open [http://RatOS.local/configure?step=1](http://RatOS.local/configure?step=1) in your browser (or whatever hostname you chose during setup). Complete the wizard to flash your control board and optionally a toolboard. When you've done that successfully, the configurator will lead you to Mainsail, which we'll now use to update RatOS and related packages to the latest version.

:::info Troubleshooting
If you cannot connect to http://RatOS.local/ but the RatOS hotspot doesn't show up, try looking up the IP of your pi on your routers admin interface and use that instead. Eg: http://192.168.0.123/.
:::

## Mainsail

Mainsail is the control interface for your printer. Mainsail is a web application that talks to Klipper through Moonraker (the Klipper API). Mainsail is what you'll be using to start prints, monitor progress, configure klipper and much more. Mainsail is what you see when you open [http://RatOS.local/](http://RatOS.local/)

![Mainsail](/img/mainsail.jpg)

:::info
To learn more about mainsail, [read the mainsail documentation](https://docs.mainsail.xyz/).
:::

## Updating

Go to the `MACHINE` tab in Mainsail. You'll see a sheet with the title "Update Manager", if you're familiar with Fluidd or Mainsail, you'll notice a new entry called `RatOS`. This `RatOS` package will update all the config files in the config folder, improvements, support for hotends, macros, extruders, new boards etc, will be coming to your printer this way in the future. **Be sure to keep this up to date, especially if you update klipper or moonraker**. Always update the RatOS package first, before updating anything else. This is important because Klipper and Moonraker sometimes make changes that require manual system or configuration changes which RatOS will try to do for you.

Go ahead an update all the packages to their latest versions, start with RatOS, then click `Update All Components`. When you update klipper, RatOS will attempt to flash your board automatically. If this fails (which should be rare), you can always go back to the [http://RatOS.local/configure?step=1](http://RatOS.local/configure?step=1) to flash your board if necessary. If you get a klipper error mentioning mcu and host versions, this means you need to flash your board.

In general, it's advisable to keep all your packages up to date, but if you're happy with how your printer works and there's nothing interesting for you in the updates, it's perfectly fine to delay updating until a later time. Klipper is a continually evolving project, that also means that bugs _do happen_. In the rare circumstance that bugs are introduced, they're usually fixed very quickly, but if you have a bunch of important prints coming up, maybe delay the updates untill afterwards.

Now it's time to start wiring. Find your board under "Supported Boards" in the docs menu to the left, and return to the next step below when you've completed your wiring.

## Setup

With the board flashed and everything wired up, you can now proceed to the [configuration guide](/docs/configuration).
