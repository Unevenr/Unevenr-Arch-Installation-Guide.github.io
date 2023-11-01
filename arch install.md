Downloaded VM Workstation Pro 17

Downloaded ISO from [archlinux.org](https://archlinux.org/download/)

    Using qBittorenter to download it

I edited the .vmx file by adding in **firmware="efi"**

Verified the boot mode by typing in **cat /sys/firmware/efi/fw_platform_size**

Used **ip link** and **ping archlinux.org** to ensure that we were connected to the internet

Typed **timedatectl** to make sure the time was properly updated

Typed **fdisk -l** to...
10:59

fdisked into /dev/sda and added two partitions **/dev/sda1** (boot) with 500M and **/dev/sda2** (remainder) with the remaining 19.5G
    **+500M**
created file systems for both of them **mkfs.ext4 /dev/** plus each individual sda

    NOTE: instead had to unmount with **umount** and did **mkfs.fat -F32 /dev/sda1**
    UPDATE: used **mkfs.fat -F32** for both this time

mounted remainder **mount /dev/sda2 /mnt**. Made dircetory and mounted boot **mkdir /mnt/boot** then **mount /dev/sda1 /mnt/boot**

    NOTE: instead i **mkdir /mnt/boot/efi**  and mounted with **mount /dev/sda1 /mnt/boot/efi**

Would occasionlly check **lsblk** to ensure everything was properly in its place

used pacstrap **pacstrap /mnt base base-devel linux linux-firmware vim**

    NOTE: had to add this in for it to work **pacman -Sy efibootmgr** 

used **genfstab -U /mnt >> /mnt/etc/fstab** to generate fstab file?

used **arch-chroot /mnt /bin/bash** to get into arch manager?

used **pacman -S networkmanager grub** to install something to get access to internet?

    used **pacman -S efibootmgr**

**systemctl enable NetworkManager** so this will start internet on boot

**vim /etc/default/grub** uncomment grub_disable_os_prober=false
    esc to commandline, i to insert, :x! to save, :q! to quit

**grub-install --target=x86_64-efi --efi-directory=/boot --bootloader-id=GRUB**

**grub-mkconfig -o /boot/grub/grub.cfg**
(no file or)

**passwd** to update password

**vim /etc/locale.gen** comments out our local lang

**locale-gen** generates locales

**vim /etc/locale.conf**
    type in **LANG=en-US.UTF-8**

**vim /etc/hostname**
    named it archbox

**ln -sf /usr/share/zoneinfo/America/Chicago /etc/localtime**
exit out of chroot

**umount -R /mnt**

reboot

Arch Linux is now installed!

Now for distro, I am installing plasma with **pacman -S plasma-meta kde-applications**

**Systemctl enable sddm**

reboot

had to **useradd** to get a user because it was blank

sudo pacman -S openssh

had do sudo pacman -S nano

sudo pacman -S xorg-xinit
nano .xintric

sudo pacman -S git

EDITOR=nano visudo

uncommentedthe "%wheel ALL=(ALL) ALL"

created Codi and Ayden user, changed passwords, and gave both sudo with **usermod -aG wheel** + plus each individual user

Change shell:
    **sudo pacman -S zsh** and **sudo pacman -S zsh-completions**

    chsh -l to see installed shells

    chsh -s /usr/bin/zsh to change default shell

Color code:
preferences in LXTerminal
Changed setting there

Browser:

arafad


github repo
setting
    pages

use Majaro

1) Add color coding to the terminal (like you see in the archiso during installation).

2) Set the system to boot into the GUI desktop environment.

3) Add a few aliases to .bashrc or .zshrc. Need some ideas for good Linux aliases? Check here.