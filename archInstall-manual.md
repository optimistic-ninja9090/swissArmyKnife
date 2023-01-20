Download Arch : https://archlinux.org/download/

*Flash into USB*

VERIFY INTERNET ACCESS
```ip addr show```
```ping archlinux.org -c 5```

WIFI FIX
```iwctl```
> ```device list``` //Displays wireless interfaces
> ```station wlan0 scan``` //Triggers wifi card
> ```station wlan0 get-networks``` //Displays available wifi networks
> ```station wlan0 connect <wirelessDevice name>``` //Connects the desired wifi
ctrl+d to exit

SYNCING THE TIME
```timedatectl set-ntp true```
```timedatectl status```

DISK SETUP (UEFI METHOD) 
```cfdisk```
> don't fuck with the windows partitions (only if there are any windows partitions :-p)
> make LINUX FILESYSTEM & an EFI (500M efi)
> write and quit

formatting the partitions
> ```mkfs.ext4 /dev/<disk>``` //linux fs
> ```mkfs.fat -F32 /dev/<disk>``` //efi

mounting
> ```mount /dev/<lfs> /mnt```
> ```mkdir /mnt/boot```
> ```mount /dev/<efi> /mnt/boot```

INSTALL ARCH
```pacstrap -i /mnt base```

CONFIGURE INSTALLATION
```arch-chroot /mnt```
> ```pacman -S linux-lts linux-lts-headers```
> ```pacman -S neovim nano base-devel openssh networkmanager wpa_supplicant wireless_tools netctl dialog```
> ```systemctl enable NetworkManager``` //initiates nm
> ```pacman -S lvm2```
> ```nvim /etc/mkinitcpio.conf``` (look for HOOKS which is not commented, add 'lvm2' after 'block')
> ```mkinitcpio -p linux-lts\
> ```nvim /etc/locale.gen``` (India)
> ```locale.gen```
> ```passwd``` (root)
> ```useradd -m -g user -G wheel <userName>```
> ```passwd <userName>``` (user)
> ```EDITOR=nvim visudo``` (uncomment second line)

GRUB
```pacman -S grub efibootmgr dosftools os-probel mtools```
```grub-install --target=x86_64-efi --bootloader-id=grub_uefi --recheck```
```cp /usr/share/local/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo




