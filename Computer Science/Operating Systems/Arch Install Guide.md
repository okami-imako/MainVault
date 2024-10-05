---
tags:
  - operating-system
  - arch
  - guide
relates to:
  - "[[Unix]]"
---
# Steps
## Prepare the usb stick
---
1) Download the iso from https://archlinux.org/download/
2) Flash the usb drive with the image (balena etcher)
3) Boot from the usb drive

## Disk Partitioning
---
1) Partition disks using `cfdisk`
Suggested partition table:
![[partition-table.png]]
2) Format the partitions
```bash
mkfs.ext4 /dev/root_partition
mkfs.fat -F 32 /dev/efi_system_partition
mkswap /dev/swap_partition
```
>run `lsblk` to verify everything
3) Mount the file system
```bash
mount /dev/root_partition /mnt
mount --mkdir /dev/efi_system_partition /mnt/boot
swapon /dev/swap_partition
```

## Setup
---
1) Install stuff
```bash
pacstrap -K /mnt base linux linux-firmware sof-firmware base-devel grub efibootmgr vim networkmanager amd-ucode zsh
```
2) Generate fstab file
```bash
genfstab /mnt > /mnt/etc/fstab
```
3) Chroot into the new system
```bash
arch-chroot /mnt
```
4) Setup time
```bash
ln -sf /usr/share/zoneinfo/Europe/Warsaw /etc/localtime
hwclock --systohc
```
5) Setup locale
    - Edit `/etc/locale.gen` file - uncomment `en_US.UTF-8 UTF-8`
    - Run `locale-gen`
    - Create `/etc/locale.conf` with `LANG=en_US.UTF-8`
6) Create hostname
Write hostname to `/etc/hostname`
7) Set the root password
```bash
passwd
```
8) Add user
```bash
adduser -m -G wheel -s /bin/zsh okami
passwd okami
```
Run `EDITOR=vim visudo` and uncomment `%wheel ALL=(ALL) ALL` line
9) Start NetworkManager
```bash
systemctl enable NetworkManager
```

## Grub Setup
---
1) Install os-prober
```bash
pacman -S os-prober
```
2) Enable os-prober
Edit `/etc/default/grub` and uncomment `GRUB_DISABLE_OS_PROBER=false` line in the end if the file
3) Finish setup
```bash
sudo grub-install --target=x86_64-efi --efi-directory=/boot --modules="tpm" --disable-shim-lock --recheck
sudo grub-mkconfig -o /boot/grub/grub.cfg
```

## Secure Boot
---
1) Install sbctl
```bash
sudo pacman -S sbctl
```
2) Restart and set Secure Boot to Setup mode
3) Verify you are in Setup mode
```bash
sbctl status
```
4) Create and enroll keys
```bash
sudo sbctl create-keys
sudo sbctl enroll-keys -m
```
5) Verify that the keys have been enrolled
```bash
sbctl status
```
6) Check which files need to be signed for secure boot to work
```bash
sudo sbctl verify
```
7) Sign all unsigned files
```bash
sudo sbctl sign -s /file/to/sign
```
8) You may get an error because of an issue with certain files being immutable. To make those files mutable, run the following command for each file then re-sign afterwards:
```bash
sudo chattr -i /file/to/sign
```
9) Verify that everything has been signed
```bash
sudo sbctl verify
```
10) Reboot, enable Secure Boot and verify that it is enabled
```bash
sbctl status
```

## Gnome
---
1) Install gnome and start gdm
```bash
sudo pacman -S gnome
sudo systemctl enable --now gdm
```

# Useful Links
1) [Comfy Install Guide](https://www.youtube.com/watch?v=68z11VAYMS8)
2) [Dreams of Autonomy Guide](https://www.youtube.com/watch?v=YC7NMbl4goo)
3) [Dualboot with Windows Guide](https://www.youtube.com/watch?v=dRoFme30qAY)
4) [Secure Boot Instructions](https://www.reddit.com/r/archlinux/comments/10pq74e/my_easy_method_for_setting_up_secure_boot_with/)