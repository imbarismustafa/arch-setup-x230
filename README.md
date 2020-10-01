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

Source: https://bbs.archlinux.org/viewtopic.php?id=224485
