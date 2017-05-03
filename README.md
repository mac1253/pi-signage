# pi-signage
This guide will transform your raspberry pi into a perfect signage device

### Check everything up to date

1. 
```bash
sudo apt-get update && sudo apt-get upgrade -y
```
2. 
```bash
sudo apt-get install chromium-browser x11-xserver-utils unclutter
```

### Setting up Kiosk mode

3.
```bash
sudo nano ~/.config/lxsession/LXDE-pi/autostart
```

4. This screen should match the below...
```bash
lxpanel --profile LXDE-pi
@pcmanfm --desktop --profile LXDE-pi
#@xscreensaver -no-splash
@point-rpi
@xset s off
@xset -dpms
@xset s noblank
@sed -i 's/"exited_cleanly": false/"exited_cleanly": true/' ~/.config/chromium-browser/Default/Preferences
@chromium-browser --noerrdialogs --disable-infobars --kiosk http://www.whateverwebsitey.com --incognito
```
5. 
Now press [Ctrl]-[O] then [Enter] and then [Ctrl]-[X] to save and then exit the document.

6. 
```bash
Sudo reboot
```
if you need to exit locally ALT+F4 **or** CTRL + W on a keyboard will exit Chromium



### Setting up SSH

1. Launch Raspberry Pi Configuration from the Preferences menu

2. Navigate to the Interfaces tab

3. Select Enabled next to SSH

4. Click OK

5. Next, In terminal type 
```bash
route -ne
```

6. take the first IP address  under the column Gateway and write it down.

7. Now in the terminal type. It will list the DNS ip next to the words nameserver,  Write it down.
```bash
cat /etc/resolv.conf
```

8. Open up this file in the terminal
```bash
sudo nano /etc/dhcpcd.conf
```

9. In that file, add this to the end of the file *Replace the values with your written down values.*
```bash
#Custom static IP address for eth0.
static ip_address=192.168.0.25
interface eth0
static domain_name_servers=192.168.0.1
static routers=192.168.0.1
```

10. On another computers terminal type this command into a terminal (use your own Pi's IP address)
```bash
ssh pi@192.0.0.0
```
11. It will ask for a password. Enter the Pi password and you will be connected!
*(default password is 'raspberry' without quotes and default username is Pi)*

### Auto refreshing the pi and changing URL
1. Install  xdotool
```bash
sudo apt-get install xdotool
```

2. After the download is finished, open the autostart file
```bash
sudo nano sudo nano ~/.config/lxsession/LXDE-pi/autostart
```

3.  At the bottom of the file add this
```bash
@lxterminal --command watch -n25 "xdotool search --class chromium key ctrl+R"
```
*-n25 referes to the number of seconds when it refreshes, change it to fit your needs*
This switches the tabs and refreshes the site every 25 seconds.
