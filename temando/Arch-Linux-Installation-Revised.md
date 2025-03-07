[Go Back](/temando/)

## Installation
As usual the *wiki* has it all, so follow it [Arch Wiki](https://wiki.archlinux.org/title/Installation_guide)
The following notes are just for me to remember when installing *Arch*
1. Increase terminal font size `setfont ter-132b` change "`132`" for a lower value to make the font smaller to set the font to default only run `setfont`
2. Run `lsblk` to get the name of the disk you will be using, usually it is most of the time `nvme0n1` 
3. Create the needed partitions by using `fdisk` 
	1. **Note:** *This partition assumes that I am going to be installing only Arch, not dual booting at all, for dual booting. I might need to create a another EFI partition, never use the EFI partition windows/macos creates*

```
gdisk /dev/nvme0n1 # run `lsblk` to see what label your drive obtained

p # Shows which partition there are
d # Deletes partitions
t # Changes the typr of partitiong
w # Saves all changes

d # run it until all parition have been deleted

# Efi partition
n
ENTER
ENTER
+1G

L
Look up "efi"
ef00 # This should be the output unless otherwise

# Boot partition
n
ENTER
ENTER
+2G

L
Look up "boot"
ef02 # This should be the output unless otherwise


# Disk partition
n
ENTER
ENTER
ENTER # Since this partition will using what remains of the disk

L
Look up "luks"
8309 # This should be the output to set the partition as a LUKS partition type

Finally, type "w" to save all changes to the disk
Press "Y" to confirm the changes
```

4. **Encrypting disk LVM** as of now, I been using **LVM** and it has been working fine
	1. Run `cryptsetup luksFormat /dev/nvme0n1p2 # Change drive label accordantly`
	2. Enter a secure passwd `12345678 wink wink`
	3. Now, open the `luks` encrypted drive, exec `cryptsetup open --type luks /dev/nvme0n1p2 lvm` Note: Call the drive whichever you want "lvm" is just an example
5. **LVM Creation** 
	1. Run `pvcreate /dev/mapper/lvm`
	2. Now create the volume group `vgcreate volgroup0 /dev/mapper/lvm`
	3. Create 2 Logical Volumes
		1. `lvcreate -n swap -L 20G -C y volgroup0` adjust as needed
		2. `lvcreate -L 100GB volgroup0 -n lv_root` adjust size as needed
		3. `lvcreate -l 100%FREE volgroup0 -n lv_home` the rest of the FREE Space will be assigned to `lv_home`
	4. Format the EFI and Boot partition in this case `nvme0n1p1` as FAT32
		1. Run `mkfs.fat -F 32 /dev/nvme0n1p1` to format the EFI partition
		2. Run `mkfs.ext4 /dev/nvme0n1p2` to format the Boot partition
	5. Last run the following command to activate `dm_mod` and enable all volumes
		1. `modprobe dm_mod`
		2. `vgscan`
		3. `vgchange -ay`
	6. Format both `lv` as `btrfs` by running the following commands
		1. `mkfs.btrfs -L root /dev/volgroup0/lv_root`
		2. `mkfs.btrfs -L home /dev/volgroup0/lv_home`
	7. Last but not least, format `swap` partition
		1. `mkswap /dev/volgroup0/swap`
	8. Mount everything as follows
		1. `swapon /dev/volgroup0/swap` to mount the `swap` memory partition
		2. `mount /dev/volgroup0/lv_root /mnt` to mount the `root` partition
		3. `mkdir -p /mnt/{home,boot}` to create `home` and `boot` folders
		4. `mount /dev/nvme0n1p2 /mnt/boot` to mount the `boot` partition, this will be obviously different on each system, make sure to mount the right partitions
		5. `mount /dev/volgroup0/lv_home /mnt/home` to mount the `home` partition
		6. Last but not least, make a `efi` folder within `/mnt/boot`
		7. `mkdir /mnt/boot/efi` to be able to mount the `efi` partition
		8. `mount /dev/nvme0n1p1 /mnt/boot/efi` to mount the `efi` partition
	9.  Install **bootstrap** apps and kernel
```
pacstrap -K /mnt base base-devel linux linux-lts linux-headers linux-lts-headers linux-firmware git lvm2 networkmanager openssh os-prober sudo grub efibootmgr vim neovim nano man zsh ranger tmux bash 
```
**Note:** This will take sometime to complete
6. Generate **fstab**
	1. `genfstab -U /mnt >> /mnt/etc/fstab`
	2. Check the output of `fstab` `cat /mnt/etc/fstab`
7. Switch to my new system
	1. `arch-chroot /mnt`
8. Set up time zone
	1. `ln -sf /usr/share/zoneinfo/America/Los_Angeles /etc/localtime`
	2. `hwclock --systohc` This syncs the time to the hardware clock
9. Edit `/etc/locale.gen` and uncomment `en_US.UTF-8 UTF-8`
	1. then, run `locale-gen`
10. Create `local.conf` in `/etc/locale.conf`
	1. Run `nvim /etc/locale.conf` and enter `LANG=en_US.UTF-8`
11. Create `hostname` name it something like `Arch`
	1. `nvim /etc/hostname` input `Arch` 
12. Edit `/etc/mkinitcpio.conf` and run/input the following
```
nvim /etc/mkinitcpio.conf
Add "encrypt lvm2" in between "block and filesystems"

# Generate Kernel Ramdisks, run each kernel you installed
mkinitcpio -p linux
mkinitcpio -p linux-lts
```
13. Set up GRUB
	1. Get the `disk UUID` by running `blkid /dev/nvme0n1p2` the drive label will be different or the same, write/save the `UUID` (This is case sensitive, be careful)
		1. **NOTE: Double check the drive's UUID, do not use the root drive UUID you need to use the partition**
	2. Edit `/etc/default/grub` and add the following right after `GRUB_CMDLINE_LINUX_DEFAULT="loglevel-3 quiet`
	3. `cryptdevice=UUID=Disk_UUID:volgroup0` the "UUID" we got in step 1
14. Install GRUB
	1. `grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=GRUB`
		1. *Note: you might need to remount `/dev/sda2` efi partition and even make the /boot/efi folder as well*
	2. `grub-mkconfig -o /boot/grub/grub.cfg` This generates the config file for GRUB
15. Enable NTP
	1. `nvim /etc/systemd/timesyncd.conf` and set the following
	2. `NTP=0.arch.pool.ntp.org 1.arch.pool.ntp.org 2.arch.pool.ntp.org 3.arch.pool.ntp.org`
	3. `FallbackNTP=0.pool.ntp.org 1.pool.ntp.org`
	4. Now, enable the systemd-timesyncd service `systemctl enable systemd-timesyncd.service`
16. Run the following at the end for good measure, this regenerate all linux images
	1. `mkinitcpio -p linux`
	2. `mkinitcpio -p linux-lts`
17. Lastly, enable some essential systems
```
# Install display manager
pacman -S sddm
# Install Microcode updates for CPU
pacman -S intel-ucode # For Intel CPUs
pacman -S amd-ucode   # For AMD CPUs

# One liner
pacman -S sddm intel-ucode

# Change root passwd and add usr
passwd # This will change root passwd

# -m creates a home dir, -G add the user to the Wheel group (admid group)
useradd -mG wheel -s /bin/zsh toniiz
passwd toniiz # Add passwd for "toniiz"

# Uncomment the wheel line, save file and exit it
visudo

# Enable Network Manager and Display Manager
systemctl enable NetworkManager sddm

# Also regenerate grub config file
grub-mkconfig -o /boot/grub/grub.cfg
```
18. Finally, exit from `chroot` unmount all and reboot
	1. Run `exit` once
	2. `umount -R /mnt` unmounts all mounted volumes
	3. `reboot`
	4. DONE!