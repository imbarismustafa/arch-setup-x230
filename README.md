# arch-setup-x230
Arch Linux Setup for Lenovo Thinkpad X230

### Backlight Control
inside
```/etc/default/grub```
append 
```GRUB_CMDLINE_LINUX_DEFAULT```
with this paraneter
```acpi_osi='!Windows 2012'```
then regenerate the config file with:
```grub-mkconfig -o /boot/grub/grub.cfg```

### Brave Video Acceleration
install ```libva-intel-driver``` and launch brave with ``` --use-gl=desktop``` and ```--ignore-gpu-blacklist```

### Touchpad
in ```/etc/X11/xorg.conf.d/50-synaptics.conf```
add the following:

```
Section "InputClass"
        Identifier "touchpad"
        MatchProduct "SynPS/2 Synaptics TouchPad"
        # MatchTag "lenovo_x230_all"
        Driver "synaptics"
        # fix touchpad resolution
        Option "VertResolution" "100"
        Option "HorizResolution" "65"
        # disable synaptics driver pointer acceleration
        Option "MinSpeed" "1"
        Option "MaxSpeed" "1"
        # tweak the X-server pointer acceleration
        Option "AccelerationProfile" "2"
        Option "AdaptiveDeceleration" "16"
        Option "ConstantDeceleration" "16"
        Option "VelocityScale" "20"
        Option "AccelerationNumerator" "30"
        Option "AccelerationDenominator" "10"
        Option "AccelerationThreshold" "10"
	# Disable two fingers right mouse click
	Option "TapButton2" "0"
        Option "HorizHysteresis" "100"
        Option "VertHysteresis" "100"
        # fix touchpad scroll speed
        Option "VertScrollDelta" "500"
        Option "HorizScrollDelta" "500"
EndSection
```

### Power Saving
in ```/etc/default/tlp```
add the following:

```
START_CHARGE_THRESH_BAT0=67
STOP_CHARGE_THRESH_BAT0=100
```

### Charge thresholds
install ```tpacpi-bar```

```
# echo 40 > /sys/class/power_supply/BAT0/charge_start_threshold
# echo 80 > /sys/class/power_supply/BAT0/charge_stop_threshold
```

### Fan control
install AUR ```thinkfan``` and configure ```/etc/thinkfan.conf``` with:

```
tp_fan /proc/acpi/ibm/fan
hwmon /sys/class/thermal/thermal_zone0/temp

(0, 0,  60)
(1, 53, 65)
(2, 55, 66)
(3, 57, 68)
(4, 61, 70)
(5, 64, 71)
(7, 68, 32767)
```

### Kernel
in ```/etc/mkinitcpio.conf```, add ```MODULES="i915"```. Regenerate initram image with ```sudo mkinitcpio -p linux```.
### Dual Screen
` xrandr --output LVDS-1 --auto --output HDMI-1 --above LVDS-1`

