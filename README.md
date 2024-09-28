# Ender 3 Octoprint Configuration Steps

## Requirements

- Raspberry Pi  
- Up to 2 Ender 3 printers - *don’t plug in the printers yet*  
- Micro or mini USB cables (depending on what model of Enders they are)  
- Up to 2 1080p cameras (optional) - *don’t plug in the cameras yet*  
- Micro SD card and Mac adapter

## Octopi Image

Originally taken from [Octopi Image Tutorial](https://all3dp.com/2/octoprint-setup-how-to-install-octopi-on-a-raspberry-pi/).

1. Download and install the Raspberry Pi Imager from the [Raspberry Pi Foundation](https://www.raspberrypi.org/software/).
2. Insert your SD card into your Macbook
3. Open the Raspberry Pi Imager and click on "Choose OS"
4. Then go to "Other specific-purpose OS > 3D printing > OctoPi". Choose the latest stable version.
5. Back on the main window, click "Choose Storage" and select your SD card
6. Click Next. Then, when asked, edit the settings for the installation:
   1. Set the hostname to `octopi\<octopi number\>` or the printer name (all lowercase)
   2. Set the login to the same name and use "cslab" as the password
   3. Set the wireless LAN information:  
      Note: things don’t seem to work well over wifi, ethernet is a better option
      1. SSID: CSlabWPA2
      2. Password: (ask a professor or another student for the password)
      3. Hidden: Check
      4. Region: US
   4. Enable SSH service
7. Click Ok/Yes/Write/whatever to have the image written to the SD card
8. Once done, insert the newly imaged Octoprint SD card into the Raspberry Pi and turn/plug it on/in

## Setup Octoprint Instances

1. Unplug all USB drives
2. SSH to the pi: ssh \<name\>@\<name\> (you must be on the CS lab network)
3. Once connected to the pi run this command (all one line):

```bash
wget -O octoprint-setup.sh "https://raw.githubusercontent.com/MoravianUniversity/octoprint-setup/refs/heads/main/octoprint-setup.sh" && bash octoprint-setup.sh && echo "Done!"
```

4. This script does the following:
   1. Sets up the printers and cameras by having you plug them in one at a time. They must stay plugged into the same ports since they don’t report serial numbers over USB.
   2. Completes a lot of other config including duplicating Octoprint instances and setting up nginx to make custom domain names for each printer. It reports the MAC address needed by proper networking.  
   *Note:* custom domain names can be tested by editing your personal `/etc/hosts` file to map the names to the Pi’s IP address. This only affects your laptop, nothing else. To make it work for others, need to have a professor submit an IT ticket.
5. Octoprint instances are on ports 5000 and 5001 using the original Raspberry Pi name:  
   http://\<name\>.cslab.moravian.edu:5000  
   http://\<name\>.cslab.moravian.edu:5001  

All octopi logins on the web interface have username octoprint and password cslab.

By modifying your personal `/etc/hosts` file (or after the networking edits are made globally), you can access with the new domain names without a port number.

After all installing is complete, disable Octolapse by going to the far right tab on the Octopi interface and deselecting enable. In order to use Octolapse you need special instructions at the beginning of your gcode files.  
