# Automate Green CLI

**Automate Green CLI is a modified version of the Particle CLI.  It has been modified to work with Particle-based Automate Green devices.  A simple Find and Replace was performed to updated the names, so the README may not be correct.**

The Automate Green CLI is a powerful tool for interacting with your devices and the Automate Green Cloud.  The CLI uses [node.js](http://nodejs.org/) and can run on Windows, Mac OS X, and Linux fairly easily.  It's also [open source](https://github.com/automategreen/automategreen-cli) so you can edit and change it, and even send in your changes as [pull requests](https://help.github.com/articles/using-pull-requests) if you want to share!

## Known Issues
* The Wireless Photon Setup Wizard will only automatically switch networks on OS X. Users of other operating systems will need to manually connect their computer to the Photon's Wi-Fi. You will be prompted during the wizard when this is required.

## Installing

  First, make sure you have [node.js](http://nodejs.org/) installed!

  Next, open a command prompt or terminal, and install by typing:

```sh
$ npm install -g automategreen-cli
$ automategreen cloud login
```

  *Note!*  If you have problems running this, make sure you using Terminal / the Command Prompt as an Administator, or try using ```sudo```

```sh
$ sudo npm install -g automategreen-cli
```


## Install (advanced)

To use the local flash and key features you'll need to install [DFU-util](http://DFU-util.sourceforge.net/) and [openssl](http://www.openssl.org/).  They are freely available and open-source, and there are installers and binaries for most major platforms as well.

Here are some great tutorials on the community for full installs:

[Installing on Ubuntu](https://community.automategreen.io/t/how-to-install-spark-cli-on-ubuntu-12-04/3474)

[Installing on Windows](https://community.automategreen.io/t/tutorial-spark-cli-on-windows-06-may-2014/3112)

### Installing on Mac OS X:
Rather than installing these packages from source, and instead of using MacPorts, it is relatively straightforward to use [Homebrew](http://brew.sh) to install ```dfu-util``` and ```openssl```. Once you have installed `brew` the basic command is ```brew install dfu-util openssl```.

## Upgrading

To upgrade Automate Green-CLI, enter the following command:

```sh
$ npm update -g automategreen-cli
```


## Running from source (advanced)

To grab the CLI source and play with it locally

```sh
git clone git@github.com:spark/automategreen-cli.git
cd automategreen-cli
npm install
node app.js help
```

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->
## Table of Contents

- [Getting Started](#getting-started)
  - [automategreen setup](#automategreen-setup)
  - [automategreen help](#automategreen-help)
- [Updating Firmware](#updating-firmware)
  - [Photon/P1/Electron](#photonp1electron)
    - [automategreen update](#automategreen-update)
  - [Core](#core)
    - [Apply the CC3000 patch](#apply-the-cc3000-patch)
    - [Performing a "Deep update"](#performing-a-deep-update)
- [Command Reference](#command-reference)
  - [automategreen setup wifi](#automategreen-setup-wifi)
  - [automategreen login](#automategreen-login)
  - [automategreen logout](#automategreen-logout)
  - [automategreen list](#automategreen-list)
  - [automategreen device add](#automategreen-device-add)
  - [automategreen device rename](#automategreen-device-rename)
  - [automategreen device remove](#automategreen-device-remove)
  - [automategreen flash](#automategreen-flash)
    - [Flashing a directory](#flashing-a-directory)
    - [Flashing one or more source files](#flashing-one-or-more-source-files)
    - [Flashing a known app](#flashing-a-known-app)
    - [Compiling remotely and Flashing locally](#compiling-remotely-and-flashing-locally)
  - [automategreen compile](#automategreen-compile)
    - [compiling a directory](#compiling-a-directory)
    - [example automategreen.include](#example-automategreeninclude)
    - [example automategreen.ignore](#example-automategreenignore)
    - [Compiling one or more source files](#compiling-one-or-more-source-files)
    - [Compiling in a directory containing project files](#compiling-in-a-directory-containing-project-files)
  - [automategreen call](#automategreen-call)
  - [automategreen get](#automategreen-get)
  - [automategreen monitor](#automategreen-monitor)
  - [automategreen identify](#automategreen-identify)
  - [automategreen subscribe](#automategreen-subscribe)
  - [automategreen publish](#automategreen-publish)
  - [automategreen serial list](#automategreen-serial-list)
  - [automategreen serial monitor](#automategreen-serial-monitor)
  - [automategreen serial flash](#automategreen-serial-flash)
  - [automategreen keys doctor](#automategreen-keys-doctor)
  - [automategreen keys new](#automategreen-keys-new)
  - [automategreen keys load](#automategreen-keys-load)
  - [automategreen keys save](#automategreen-keys-save)
  - [automategreen keys send](#automategreen-keys-send)
  - [automategreen keys server](#automategreen-keys-server)
    - [Encoding a server address and port](#encoding-a-server-address-and-port)
  - [automategreen keys address](#automategreen-keys-address)
  - [automategreen keys protocol](#automategreen-keys-protocol)
  - [automategreen config](#automategreen-config)
  - [automategreen binary inspect file.bin](#automategreen-binary-inspect-filebin)
  - [automategreen webhook](#automategreen-webhook)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Getting Started

  These next two commands are all you need to get started setting up an account, claiming a device, and discovering new features.

### automategreen setup

  Guides you through creating a new account, and claiming your device!

```sh
$ automategreen setup
```

### automategreen help

  Shows you what commands are available, and how to use them.  You can also give the name of a command for detailed help.

```sh
$ automategreen help
$ automategreen help keys
```

## Updating Firmware

### Photon/P1/Electron

#### automategreen update

If you wish to easily update the system firmware running on your device to a later version, you can use the `automategreen update` command. For the exact version it will update to, check the version of the files in the [updates folder](https://github.com/automategreen/automategreen-cli/tree/master/updates).

1. Make sure you have [DFU-util](http://dfu-util.sourceforge.net/) installed.
1. Connect your device via USB, and put it into [DFU mode](https://docs.automategreen.io/guide/getting-started/modes/#dfu-mode-device-firmware-upgrade-).
1. Run `automategreen update`.

### Core

#### Apply the CC3000 patch

The easiest way to apply the CC3000 patch is to flash the known "cc3000" firmware followed by the "tinker" firmware over USB.

1. Make sure you have [DFU-util](http://dfu-util.sourceforge.net/) installed
1. Connect your Core via USB, and place it into DFU mode by holding both buttons, and releasing reset, keep holding mode until your Core flashes yellow.
1. Run `automategreen flash --usb cc3000`. This will run a special firmware program that will update the firmware running inside the CC3000 WiFi module.
When it's done running, your Core will be blinking yellow in DFU-mode, you'll need to flash regular firmware like Tinker
to get connected and developing again.
1. Run `automategreen flash --usb tinker`. This will flash a new version of Tinker to your Core and return to a blinking blue "listening" state, where
you can:
1. Run `automategreen setup` or `automategreen setup wifi` to provide your network credentials to get connected again.

#### Performing a "Deep update"

Any Core shipped before Summer 2014 would benefit from having this update applied at least once. It improves the Core's performance on very busy networks, and helps fix other minor issues. This update now ships with the CLI so you can apply it to Cores that are unable to get online otherwise.

1. Make sure you have [DFU-util](http://dfu-util.sourceforge.net/) installed
1. Connect your Core via usb, and place it into DFU mode by holding both buttons, and releasing RESET, keep holding MODE until your Core flashes yellow.
1. Run ```automategreen flash --usb deep_update_2014_06```
1. Your Core should reboot and try to connect to any previously saved wifi networks, and then update itself again.

## Command Reference

### automategreen setup wifi

Helpful shortcut for adding another wifi network to a device connected over USB.  Make sure your device is connected via a USB cable, and is slow blinking blue [listening mode](http://docs.automategreen.io/guide/getting-started/modes/#listening-mode)

```sh
$ automategreen setup wifi
```

### automategreen login

Login and save an access token for interacting with your account on the Automate Green Cloud.

```sh
$ automategreen login
```

### automategreen logout

Logout and optionally revoke the access token for your CLI session.

```sh
$ automategreen logout
```

### automategreen list

Generates a list of what devices you own, and displays information about their status, including what variables and functions are available

```sh
$ automategreen list

Checking with the cloud...
Retrieving devices... (this might take a few seconds)
my_device_name (0123456789abcdef01234567) 0 variables, and 4 functions
  Functions:
    int digitalwrite(string)
    int digitalread(string)
    int analogwrite(string)
    int analogread(string)

```

### automategreen device add

Adds a new device to your account

```sh
$ automategreen device add 0123456789abcdef01234567
Claiming device 0123456789abcdef01234567
Successfully claimed device 0123456789abcdef01234567
```

### automategreen device rename

Assigns a new name to a device you've claimed

```sh
$ automategreen device rename 0123456789abcdef01234567 "pirate frosting"
```

### automategreen device remove

Removes a device from your account so someone else can claim it.

```sh
$ automategreen device remove 0123456789abcdef01234567
Are you sure?  Please Type yes to continue: yes
releasing device 0123456789abcdef01234567
server said  { ok: true }
Okay!
```

### automategreen flash

Sends a firmware binary, a source file, or a directory of source files, or a known app to your device.

Note!  When sending source code, the cloud compiles ```.ino``` and ```.cpp``` files differently.  For ```.ino``` files, the cloud will apply a pre-processor.  It will add missing function declarations, and it will inject an ```#include "
  application.h"``` line at the top of your files if it is missing.

If you want to build a library that can be used for both Arduino and Automate Green, here's a useful code snippet:

```cpp
#if defined(ARDUINO) && ARDUINO >= 100
#include "Arduino.h"
#elif defined(SPARK)
#include "application.h"
#endif
```

#### Flashing a directory

You can setup a directory of source files and libraries for your project, and the CLI will use those when compiling remotely.  You can also create ```automategreen.include``` and / or a ```automategreen.ignore``` file in that directory that will tell the CLI specifically which files to use or ignore.

```sh
$ automategreen flash deviceName my_project
```

#### Flashing one or more source files

You can include any number of individual source files after the device Name, and the CLI will include them while flashing your app.


```sh
$ automategreen flash deviceName app.ino library1.cpp library1.h
```

#### Flashing a known app

You can easily reset a device back to a previous existing app with a quick command. Three app names are reserved right now: "tinker", "voodoo", and "cc3000".  Tinker is the original firmware that ships with the device, and cc3000 will patch the wifi module on your Core. Voodoo is a build of [VoodooSpark](http://voodoospark.me/) to allow local wireless firmata control of a device.

```sh
$ automategreen flash deviceName tinker
$ automategreen flash deviceName cc3000
$ automategreen flash deviceName voodoo

```

You can also update the factory reset version using the `--factory` flag, over USB with `--usb`, or over serial using `--serial`.

```sh
$ automategreen flash --factory tinker
$ automategreen flash --usb tinker
$ automategreen flash --serial tinker
```

#### Compiling remotely and Flashing locally

To work locally, but use the cloud compiler, simply use the compile command, and then the local flash command after.  Make sure you connect your device via USB and place it into [DFU mode](https://docs.automategreen.io/guide/getting-started/modes/#dfu-mode-device-firmware-upgrade-).

```sh
$ automategreen compile device_type my_project_folder --saveTo firmware.bin
OR
$ automategreen compile device_type app.ino library1.cpp library1.h --saveTo firmware.bin

$ automategreen flash --usb firmware.bin
OR
$ automategreen flash --serial firmware.bin
```


### automategreen compile

Compiles one or more source file, or a directory of source files, and downloads a firmware binary. This is device specific and must be passed as an argument during compilation.

The devices available are:

- photon (alias is 'p')
- core (alias is 'c')

eg. `automategreen compile photon xxx` OR `automategreen compile p xxxx` both targets the photon

Note!  The cloud compiles ```.ino``` and ```.cpp``` files differently.  For ```.ino``` files, the cloud will apply a pre-processor.  It will add missing function declarations, and it will inject an ```#include "
application.h"``` line at the top of your files if it is missing.

If you want to build a library that can be used for both Arduino and Automate Green, here's a useful code snippet:

```cpp
#if defined(ARDUINO) && ARDUINO >= 100
#include "Arduino.h"
#elif defined(SPARK)
#include "application.h"
#endif
```

#### compiling a directory

You can setup a directory of source files and libraries for your project, and the CLI will use those when compiling remotely.  You can also create ```automategreen.include``` and / or a ```automategreen.ignore``` file in that directory that will tell the CLI specifically which files to use or ignore.  Those files are just plain text with one line per filename

```sh
$ automategreen compile device_type my_project_folder
```

#### example automategreen.include
```text
application.cpp
library1.h
library1.cpp
```

#### example automategreen.ignore
```text
.ds_store
logo.png
old_version.cpp
```

#### Compiling one or more source files

You can include any number of individual source files after the device id, and the CLI will include them while compiling your app.


```sh
$ automategreen compile device_type app.ino library1.cpp library1.h
```

#### Compiling in a directory containing project files

This will push all the files in a directory that the command line is currently 'cd' in for compilation.

```sh
$ automategreen compile device_type .
```

### automategreen call

Calls a function on one of your devices, use ```automategreen list``` to see which devices are online, and what functions are available.

```sh
$ automategreen call deviceName digitalwrite "D7,HIGH"
1
```

### automategreen get

Retrieves a variable value from one of your devices, use ```automategreen list``` to see which devices are online, and what variables are available.

```sh
$ automategreen get deviceName temperature
72.1
```

### automategreen monitor

Pulls the value of a variable at a set interval, and optionally display a timestamp

* Minimum delay for now is 500 (there is a check anyway if you keyed anything less)
* hitting ```CTRL + C``` in the console will exit the monitoring

```sh
$ automategreen monitor deviceName temperature 5000
$ automategreen monitor deviceName temperature 5000 --time
$ automategreen monitor all temperature 5000
$ automategreen monitor all temperature 5000 --time
$ automategreen monitor all temperature 5000 --time > my_temperatures.csv
```

### automategreen identify

Retrieves your device id when the device is connected via USB and in listening mode (flashing blue).

```sh
$ automategreen identify
$ automategreen identify 1
$ automategreen identify COM3
$ automategreen identify /dev/cu.usbmodem12345

$ automategreen identify
0123456789abcdef01234567
```

### automategreen subscribe

Subscribes to published events on the cloud, and pipes them to the console.  Special device name "mine" will subscribe to events from just your devices.

```sh
$ automategreen subscribe
$ automategreen subscribe mine
$ automategreen subscribe eventName
$ automategreen subscribe eventName mine
$ automategreen subscribe eventName deviceName
$ automategreen subscribe eventName 0123456789abcdef01234567
```

### automategreen publish

Allows a message to be published via the CLI without using a physical Automate Green device. This is particularly useful when you are testing your firmware against an actual `published` event.

There is a `--private` flag that allows you to `publish` events to devices subscribing to events with the `MY_DEVICES` option.

```sh
$ automategreen publish eventName
$ automategreen publish eventName --private
$ automategreen publish eventName someData
$ automategreen publish eventName someData --private
```

### automategreen serial list

Shows currently connected devices acting as serial devices over USB.

```sh
$ automategreen serial list
```


### automategreen serial monitor

Starts listening to the specified serial device, and echoes to the terminal.

```sh
$ automategreen serial monitor
$ automategreen serial monitor 1
$ automategreen serial monitor COM3
$ automategreen serial monitor /dev/cu.usbmodem12345
```

### automategreen serial flash

Flash a firmware binary over serial using the YMODEM protocol.

```sh
$ automategreen serial flash firmware.bin
```

### automategreen keys doctor

Helps you update your keys, or recover your device when the keys on the server are out of sync with the keys on your device.  The ```automategreen keys``` tools requires both DFU-util, and openssl to be installed.

Connect your device in [DFU mode](https://docs.automategreen.io/guide/getting-started/modes/#dfu-mode-device-firmware-upgrade-), and run this command to replace the unique cryptographic keys on your device.  Automatically attempts to send the new public key to the cloud as well.

```sh
$ automategreen keys doctor your_device_id
```

There have been reports of the new public key not being sent to the cloud, in which case ```automategreen keys send``` will need to be run manually.

### automategreen keys new

Generates a new public / private keypair that can be used on a device.

```sh
$ automategreen keys new
running openssl genrsa -out device.pem 1024
running openssl rsa -in device.pem -pubout -out device.pub.pem
running openssl rsa -in device.pem -outform DER -out device.der
New Key Created!

$ automategreen keys new mykey
running openssl genrsa -out mykey.pem 1024
running openssl rsa -in mykey.pem -pubout -out mykey.pub.pem
running openssl rsa -in mykey.pem -outform DER -out mykey.der
New Key Created!
```

### automategreen keys load

Copies a ```.DER``` formatted private key onto your device's external flash.  Make sure your device is connected and in [DFU mode](https://docs.automategreen.io/guide/getting-started/modes/#dfu-mode-device-firmware-upgrade-).  The `automategreen keys` tools requires both DFU-util, and openssl to be installed.  Make sure any key you load is sent to the cloud with `automategreen keys send device.pub.pem`

```sh
$ automategreen keys load device.der
...
Saved!
```

### automategreen keys save

Copies a ```.DER``` formatted private key from your device's external flash to your computer.  Make sure your device is connected and in [DFU mode](https://docs.automategreen.io/guide/getting-started/modes/#dfu-mode-device-firmware-upgrade-).  The ```automategreen keys``` tools requires both DFU-util, and openssl to be installed.

```sh
$ automategreen keys save name_of_file
...
Saved!
```

### automategreen keys send

Sends a device's public key to the cloud for use in opening an encrypted session with your device.  Please make sure your device has the corresponding private key loaded using the ```automategreen keys load``` command.

```sh
$ automategreen keys send 0123456789abcdef01234567 device.pub.pem
submitting public key succeeded!
```

### automategreen keys server

Switches the server public key stored on the device's external flash. This command is important when changing which server your device is connecting to, and the server public key helps protect your connection. Your device will stay in DFU mode after this command, so that you can load new firmware to connect to your server. By default this will only change the server key associated with the default protocol for a device. If you wish to change a specific protocol, add `--protocol tcp` or `--protocol udp` to the end of your command.


```sh
$ automategreen keys server my_server.der
$ automategreen keys server my_server.der --protocol udp
```

#### Encoding a server address and port

When using the local cloud you can ask the CLI to encode the IP or dns address into your key to control where your device will connect. You may also specify a port number to be included.

```sh
$ automategreen keys server my_server.pub.pem 192.168.1.10
$ automategreen keys server my_server.der 192.168.1.10 9000
$ automategreen keys server my_server.der 192.168.1.10 9000 --protocol udp
```

### automategreen keys address

Reads and displays the server address, port, and protocol from a device.

```sh
$ automategreen keys address

tcp://device.spark.io:5683
```

### automategreen keys protocol

Changes the transport protocol used to communicate with the cloud. Available options are `tcp` and `udp` for Electrons (if you are running at least firmware version 0.4.8).

```sh
$ automategreen keys protocol tcp
$ automategreen keys protocol udp
```

### automategreen config

The config command lets you create groups of settings and quickly switch to a profile by calling `automategreen config profile-name`. This is especially useful for switching to your local server or between other environments.

Calling `automategreen config automategreen` will switch **Automate Green-Cli** back to the Automate Green Cloud API server.

```sh
$ automategreen config profile-name
$ automategreen config automategreen
$ automategreen config local apiUrl http://localhost:8080  //creates a new profile with name "local" and saves the IP-address parameter
$ automategreen config useSudoForDfu true
```

Calling `automategreen config identify` will output your current config settings.

```sh
$ automategreen config identify
Current profile: automategreen
Using API: https://api.automategreen.io
Access token: 01234567890abcdef01234567890abcdef012345
```

### automategreen binary inspect file.bin

Describe binary generated by compile.

```sh
$ automategreen binary inspect file.bin
file.bin
 CRC is ok (06276dc6)
 Compiled for photon
 This is a system module number 2 at version 6
 It depends on a system module number 1 at version 6
```

### automategreen webhook

Registers your webhook with the Automate Green Cloud. Creates a postback to the given url when your event is sent.

```sh
$ automategreen webhook list
$ automategreen webhook delete WEBHOOK_ID
$ automategreen webhook create example.json #run this command in the directory containing example.json
$ automategreen webhook GET <your_event_name> http://<website.you.are.trying.to.contact
```

For `$ automategreen webhook GET <your_event_name> http://<website.you.are.trying.to.contact`, you can retrieve the response using:

```sh
void setup(){
Automate Green.subscribe("hook-response/<event_name>", handlerFunction, MY_DEVICES);
}

void handlerFunction(const char *name, const char *data) {
  // Important note!  -- Right now the response comes in 512 byte chunks.  
  // This code assumes we're getting the response in large chunks, and this
  // assumption breaks down if a line happens to be split across response chunks
  
  process the data received here....
}
```
More examples and information about **webhooks** can be found here: https://docs.automategreen.io/guide/tools-and-features/webhooks/
