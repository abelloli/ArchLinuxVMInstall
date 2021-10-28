Install iso and boot up VM. Verify that you have efi and then make sure you have an internet connection by pinging. Set up partitions, make sure you have an efi one, and then format them. Set up your sda1 and sda2 and install all the needed packages that will help you later on. If you don't instal packages here it makes other parts of the process a lot harder. Once you have everything set up, reboot the system and log back into the vm. **Install NetworkManager** Create the users for your system and then set up your network connection. Install your desired shell and then install a web browser. 


Code Used during install-


Boot Sequence:

Download ISO, Create VM 2GB Ram 20GB HDD
Boot up vm, Select Arch Linux install medium press enter

Verify Boot Mode:
#ls /sys/firmware/efi/efivars		make sure it finds the file

Connect to Internet:
#ping archlinux.org 		See if you are connected
Update System Clock:
#timedatectl set-ntp true
#timedatectl status		check service status

Partition the disks:
#fdisk -l 			list the devices
#cfdisk /dev/sda	Gives us the prompt to change (Make sure it says Free Space)GPT
Enter, 500M Size, Type EFI System
Free Space, enter, remaining space
Write

Format the Partitions:
#mkfs.fat -F32 /dev/sda1
#mkfs.ext4 /dev/sda2
Mount File System:
#mount /dev/sda2 /mnt
#mkdir /mnt/efi
#mount /dev/sda1 /mnt/efi

Install Packages:
#pacstrap /mnt base linux linux-firmware

Configure the System:
#genfstab -U /mnt >> /mnt/etc/fstab		Define UUID
#arch-chroot /mnt				Change root
#pacman -Syu vim nano
#nano /etc/locale.gen
Clear # from en_us.Utf-8
Ctrlx, y
#nano /etc/hostname
#nano /etc/hosts
127.0.0.1 	localhost
::1		localhost
127.0.1.1	austin
#passwd				root password

Add Users:
#useradd -G (groups) -m (user)	add user
passwd				set user password
#pacman -Syu netctl
#pacman -Syu dhcpcd
#pacman -Syu sudo
#EDITOR=nano visudo
Clear # %wheel
#pacman -Syu grub efibootmgr
#grub-install --target=x86_64-efi --efi-directory=/efi/ --bootloader-id=Arch
#grub-mkconfig -o /boot/grub/grub.cfg

Finishing Install:
exit
reboot

After Rebooting:
#sudo su
#sudo cd examples/ethernet-dhcp .
#sudo nano ethernet-dhcp
Clear # dhcp client
Ip a
2:
#sudo nano ethernet-dhcp 
Interface = 2
#sudo systemctl enable dhcpcd
#sudo systemctl start dhcpcd
#ping archlinux
#sudo pacman -Syu neofetch		data of vm
#neofetch
#useradd sal and codi
Add passwd sal and codi
Sudo passwd -e sal/codi	expire
#pacman -S xf86-video-intel
#pacman -S xorg
#pacman -S lxde
#systemctl enable lxdm

Install zhs:
#which $SHELL	    type
#sudo pacman -S zsh zsh-completions
#zsh
1, 1, 0, 2, 1, 3, 1, v, 0, 4, 0, 0
#nano .zshrc
Autoload -Uz promptinit
Promptinit
#source .zshrc
#prompt -l
#prompt fire
#sudo pacman -S curl git wget
#sh -c “$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)”
#upgrade_oh_my_zsh
#nano .zshrc

Plugins  (git archlinux)
ZSH_themes “gnzh”
#source .zshrc
#nano /etc/passwd			change sal and codi usr/bin/zsh

SSH:
#pacman -S openssh
#ssh -p 53997 acb4881@129.244.245.21

Color Coding:
In edit tab

Alias:
Alias c=’clear’
