---
title: archlinux
date: 2022-03-05 22:54:41
categories:
- guide
version:
---

## get started

## Install

```bash
# stop reflector
systemctl stop reflector.service

# make sure it boot from efi
ls /sys/firmware/efi/efivars

# make network work

# update system time
timedatectl set-ntp true # sync with network time
timedatectl status

# add local mirror to the list
vim /etc/pacman.d/mirrorlist

# disk partition
# to see how devices are partitioned
lsblk
# to partition given device, replace [x] with char(SATA) or num(NVME)
cfdisk /dev/sd[x]
# operations in cfdisk, make sure you have
# 1. partition 200M with EFI system type
# 2. partition >= 60% of your memory with Linux swap type
# 3. partition with Linux filesystem
# Press Write button and input yes(not y)
# use lsblk to check

# format partition
mkswap /dev/sdxn
## deal with btrfs
## this structure of btrfs is fit for Timeshift to backup system
mkfs.btrfs -L myArch /dev/sdxn
mount -t btrfs -o compress=zstd /dev/sdxn /mnt
btrfs subvolume create /mnt/@
btrfs subvolume create /mnt/@home
## to check
btrfs subvolume list -p /mnt
## umount
umount /mnt
## fin
# mount new system
mount -t btrfs -o subvol=/@,compress=zstd /dev/sdxn /mnt
mkdir /mnt/home
mount -t btrfs -o subvol=/@home,compress=zstd /dev/sdxn /mnt/home
mkdir -p /mnt/boot/efi
mount /dev/sdxn /mnt/boot/efi
swapon /dev/sdxn
# to check, -h means output human readable unit
df -h
free -h

# Install basic system
pacstrap /mnt base base-devel linux
# for real machine, also
pacstrap /mnt linux-firmware
# for virtual machine, for their managing tools compile
pacstrap /mnt linux-headers
# usaully use
pacstrap /mnt dhcpcd networkmanager vim sudo zsh zsh-completions

# fstab
genfstab -U /mnt > /mnt/etc/fstab
# check
cat /mnt/etc/fstab

# holy step!
arch-chroot /mnt

vim /etc/hostname
vim /etc/hosts
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
# sync system time to hardware time
hwclock --systohc
# edit locale, un comment what you need(en_US.UTF-8 zh_CN.UTF-8)
vim /etc/locale.gen
locale-gen
echo 'LANG=en_US.UTF-8'  > /etc/locale.conf
passwd root
pacman -S intel-ucode # Intel
pacman -S amd-ucode # AMD

pacman -S grub efibootmgr os-prober

grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=ARCH

# I usually set GRUB_CMDLINE_LINUX_DEFAULT="loglevel=5 nowatchdog"
# add GRUB_DISABLE_OS_PROBER=false to boot win10
vim /etc/default/grub
grub-mkconfig -o /boot/grub/grub.cfg

# go back
exit
# umount
umount -R /mnt
# remember after this unplug installation medium
reboot 
```