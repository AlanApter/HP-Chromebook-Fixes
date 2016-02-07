# HP-Chromebook-Fixes
Fixes for linux mint on the HP Chromebook 14 Falco

These fixes are once you've managed to remove the write-protection on the bios, entered developer mode on your Chromebook, entered into the SeaBios slot, and installed Linux. If you haven't done that yet, you should follow these guides:
* Removing the write-protection - https://wiki.archlinux.org/index.php/HP_Chromebook_14#Locating_the_Write-Protect_Screw
* Entering developer mode - http://www.howtogeek.com/210817/how-to-enable-developer-mode-on-your-chromebook/
* To flash a new ROM, run John Lewis's script: https://johnlewis.ie/custom-chromebook-firmware/rom-download/. Make sure you have the right model, you've removed write [protection, and you know what you're doing. I think this step is optional, but I did it to remove the 'Chromebook missing or damaged OS screen' (next step).
* To enter the legacy Seabios slot, press Ctrl-L when the 'Chromebook missing or damaged OS' appears (it should appear if you've followed the steps above). If you've run John Lewis's script, this might not be necessary.
* If you can boot into Seabios, make sure you have a live USB with Linux Mint on it (I had some trouble with the file format of the USB stick, your mileage may vary).
* Initially live usb wouldn't work - it only got to the grub screen. I had to press tab, and change mem=1G to get it to load into the live USB (if you have the same problem, put this config before the double slash, not afterwards, as otherwise it'll limit your memory to one gigabyte, instead of the 4 gigabytes you should have. If you aren't sure if you did it wrong, type '''free -m''' once you've installed Linux Mint.

There's a version of Linux designed for Chromebooks called GalliumOS based off Ubuntu. They have the fixes in this repository, and some other tweaks. I haven't tried it, and I'm wary of the vague 'other optimisations'.

To use this, you'll have to copy each file from the place they are in the repository to your install. E.g. copy /etc/rc.local in the repository to your /etc/rc.local.

After that, you'll have to execute the following commands:
```
sudo chmod +x /etc/pm/sleep.d/05_sound

sudo update-grub

sudo update-grub2
```

The following files will fix suspend:
* /etc/rc.local
* /etc/default/grub
* /etc/pm/sleep.d/05_sound

The general notion is that before suspend, the drivers need to tell the components explicitly to be turned off, and then turned on again on resume.

I'm grateful for this helpful blogpost: https://philipalban.wordpress.com/2014/04/25/fixing-suspend-in-xubuntu-on-the-acer-c720-a-simplified-guide/

The following file fixes the mouse, adds a bit of sensitivity:
* /etc/X11/xorg.conf.d/50-cros-touchpad.conf
