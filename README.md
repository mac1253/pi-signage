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


----------------------------------------------------------------------------------------------

### Setting up Kiosk mode

3.
```bash
sudo nano ~/.config/lxsession/LXDE-pi/autostart
```

4. 
This screen should match the below...
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

5. On another computers terminal type this command into a terminal (use your own Pi's IP address)
```bash
ssh pi@192.0.0.0
```
6. It will ask for a password. Enter the Pi password and you will be connected!
*(default password is 'raspberry' without quotes and default username is Pi)*
