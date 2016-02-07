# HP-Chromebook-Fixes
Fixes for linux mint on the HP Chromebook 14 Falco

To use this, you'll have to copy each file from the place they are in the repository to your install. E.g. copy /etc/rc.local in the repository to your /etc/rc.local.

After that, you'll have to execute the following commands:
```sudo chmod +x /etc/pm/sleep.d/05_sound
```sudo update-grub
```sudo update-grub

The following files will fix suspend:
* /etc/rc.local
* /etc/default/grub
* /etc/pm/sleep.d/05_sound

The general notion is that before suspend, the drivers need to tell the components explicitly to be turned off, and then turned on again on resume.

I'm grateful for this helpful blogpost: https://philipalban.wordpress.com/2014/04/25/fixing-suspend-in-xubuntu-on-the-acer-c720-a-simplified-guide/

The following file fixes the mouse, adds a bit of sensitivity:
* /etc/X11/xorg.conf.d/50-cros-touchpad.conf

You may also be interested in this wiki page https://wiki.archlinux.org/index.php/HP_Chromebook_14.
