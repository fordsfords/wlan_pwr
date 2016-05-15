# wlan_pwr
CHIP script to improve wireless performance and reliability by turning off power management.

## License

I want there to be NO barriers to using this code, so I am releasing it to the public domain.  But "public domain" does not have an internationally agreed upon definition, so I use CC0:

Copyright 2016 Steven Ford http://geeky-boy.com and licensed
"public domain" style under
[CC0](http://creativecommons.org/publicdomain/zero/1.0/): 
![CC0](https://licensebuttons.net/p/zero/1.0/88x31.png "CC0")

To the extent possible under law, the contributors to this project have
waived all copyright and related or neighboring rights to this work.
In other words, you can use this code for any purpose without any
restrictions.  This work is published from: United States.  The project home
is https://github.com/fordsfords/wlan_pwr/tree/gh-pages

To contact me, Steve Ford, project owner, you can find my email address
at http://geeky-boy.com.  Can't see it?  Keep looking.

## Introduction

The [CHIP](http://getchip.com/) single-board computer has built-in WIFI hardware.
Linux can put the WIFI hardware into different power modes, presumably to reduce electrical consumption.
But many have reported problems with CHIP's WIFI, especially performance, and occasionally reliability.
I have seen CHIP unable to complete an "apt-get update" with power management turned on.

Fortunately, it is easy to turn off the power management with a simple command:
    sudo iwconfig wlan0 power off

Unfortunately, with CHIP's current OS, that setting is not remembered across reboots.  So the next
time you boot CHIP, power management will be back on.

The "wlan_pwr" script is designed to be run during system startup, and turns power management off
as the interface is brought up.

You can find wlan_pwr on github.  See:

* User documentation (this README): https://github.com/fordsfords/wlan_pwr/tree/gh-pages

Note: the "gh-pages" branch is considered to be the current stable release.  The "master" branch is the development cutting edge.

## Quick Start

These instructions assume you are in a shell prompt on CHIP.

1. Get the prerequisit Linux package.

        sudo apt-get install wireless-tools

2. Verify that power management is turned on:

        /sbin/iwconfig wlan0

    You should see the line:

        Power Management:on

3. Get the shell script file onto CHIP and reboot:

        sudo wget -O/etc/network/if-up.d/wlan_pwr http://fordsfords.github.io/wlan_pwr/wlan_pwr
        sudo chmod +x /etc/network/if-up.d/wlan_pwr
        sudo shutdown -r now

4. Test the package.  Wait for CHIP to finish booting, and log back in.  Then:

        /sbin/iwconfig wlan0

    You should see the line:

        Power Management:off

## Release Notes

* 15-May-2016

    Initial release.
