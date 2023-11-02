Downloaded VM Workstation Pro 17

Downloaded ISO from [archlinux.org](https://archlinux.org/download/)

    Using qBittorenter to download it

I edited the .vmx file by adding in **firmware="efi"**

Verified the boot mode by typing in **cat /sys/firmware/efi/fw_platform_size**

**ip link** and **ping archlinux.org** to ensure that we were connected to the internet

**timedatectl** to make sure the time was properly updated

fdisked into /dev/sda and added two partitions **/dev/sda1** (boot) with 500M and **/dev/sda2** (remainder) with the remaining 19.5G
    **+500M**
created file systems for both of them **mkfs.ext4 /dev/** plus each individual sda

    NOTE: instead had to unmount with **umount** and did mkfs.fat -F32 /dev/sda1

mounted remainder **mount /dev/sda2 /mnt**. Made dircetory and mounted boot **mkdir /mnt/boot** then **mount /dev/sda1 /mnt/boot**

    NOTE: instead i mkdir /mnt/boot/efi and mounted with mount /dev/sda1 /mnt/boot/efi

Would occasionlly check **lsblk** to ensure everything was properly in its place

pacstrap **pacstrap /mnt base base-devel linux linux-firmware vim**

    NOTE: had to add this in for it to work pacman -Sy efibootmgr

**genfstab -U /mnt >> /mnt/etc/fstab** to generate fstab file

**arch-chroot /mnt** to get into arch manager

**pacman -S networkmanager grub** to install something to get access to internet?

    pacman -S efibootmgr

**systemctl enable NetworkManager** so this will start internet on boot

**vim /etc/default/grub** uncomment grub_disable_os_prober=false
    esc to commandline, i to insert, :x! to save, :q! to quit

**grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB** installs bootloader

**grub-mkconfig -o /boot/grub/grub.cfg** makes grub config file

**passwd** to update password

**vim /etc/locale.gen** comments out our local lang

**locale-gen** generates locales

**vim /etc/locale.conf** getting proper language
    type in **LANG=en-US.UTF-8**

**vim /etc/hostname** changes name of host
    named it archbox

**ln -sf /usr/share/zoneinfo/America/Chicago /etc/localtime** changes time

exit out of chroot

**umount -R /mnt** unmounts drives

reboot

Arch Linux is now installed!

Now for distro, I am installing plasma with **pacman -S plasma-meta kde-applications**

**Systemctl enable sddm** allows DE to start on boot

reboot

had to **useradd** to get a user because it was blank

**sudo pacman -S openssh** install ssh

**sudo pacman -S nano** install nano

**sudo pacman -S git** install git

**EDITOR=nano visudo** change editor

uncommented the "%wheel ALL=(ALL) ALL" so we can do below code

created Codi and Ayden user, changed passwords, and gave both sudo with **usermod -aG wheel** + plus each individual user

Change shell:
    **sudo pacman -S zsh** and **sudo pacman -S zsh-completions**

    chsh -l to see installed shells

    chsh -s /usr/bin/zsh to change default shell

Color code:
    preferences in LXTerminal
    Changed setting there

Browser:
    Preinstalled on Plasma (Falkon)

Aliases:
    **alias c='clear'**
    **alias codi='echo The best Professor!"** #Not a suckup I swear
    **alias imtired='echo same bro'**

issues?
    couldnt install bootloader - fixed with turning boot drive into EFI
    DE wouldnt open - fixed with creating a folder with useraddch Installation Guide.md…]()
