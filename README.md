# splash-pi
Raspberry splash screen template

##  download the template and customize

### At your workstation, run:
```
# change the boot screen text message in the BOOT_MSG variable before running the sed command

git clone https://github.com/524c/splash-pi
cd splash-pi
BOOT_MSG="V1.0 xxx 2021"
sed -i -E "s/__BOOT_MSG__/$BOOT_MSG/" splash-pi.script

# replace the splash.png file with your custom image
# copy the new theme 'splash-pi' to the rpi home folder
```


## on your rpi, run:
```
sudo mkdir -p /usr/share/plymouth/themes/splash-pi
sudo cp -rf ~/splash-pi /usr/share/plymouth/themes/
sudo ln -s /usr/share/plymouth/themes/splash-pi/splash-pi.plymouth /etc/alternatives/default.plymouth
sudo ln -s /usr/share/plymouth/themes/splash-pi/splash-pi.plymouth /usr/share/plymouth/themes/default.plymouth
```

### enable splash screen in /boot/cmdline.txt (minimum required)
```
console=tty3 splash plymouth.ignore-serial-consoles logo.nologo
```

### /boot/cmdline.txt full example
```
console=serial0,115200 consoleblank=1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline fsck.repair=yes rootwait loglevel=3 vt.global_cursor_default=0 noatime nodiratime ipv6.disable=1 quiet console=tty3 splash plymouth.ignore-serial-consoles logo.nologo
```

to disable the rainbow boot image, comment the line disable_splash in /boot/config.txt
```
# disable_splash=1
```

After a reboot, the new splash screen and text message will be displayed.
