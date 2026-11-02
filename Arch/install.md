 # Arch Linux的安装 



###  1.分区

fdisk /dev/sda

/ dev/sda1  				+512M 			EFI SYSTEM       efi分区

/dev/sda2					+12G   			Linux Swap      交换分区

/dev/sda3  				 剩下所有          Linux root(x86-64)  根分区



fdisk /dev/sdb

/dev/sdb1                    所有                 Linux Home

## 1.1格式化分区

````bash
mkfs.fat -F32 /dev/sda1   #格式efi分区
````

````````bash
mkswap /dev/sda2       #格式化交换分区
swapon /dev/sda2       #挂载交换分区
````````

````````bash
mkfs.ext4 /dev/sda3
mkfs.ext4 /dev/sdb1
````````

## 1.2 挂载分区

````bash
mount /dev/sda3 /mnt            #挂载根分区，一定要注意这个必须是首先挂载的那个分区
````

````bash
mkdir /mnt/efi
mount /dev/sda1 /mnt/efi   #挂载efi分区
````

````bash
mkdir /mnt/home
mount /dev.sdb1 /mnt/home  #挂载home分区
````



## 2.1安装系统

````bash
pacstrap /mnt base linux linux-firmware    #安装最基本的应用到/mnt
````

`````bash
genfstab -U /mnt >> /mnt/etc/fstab         #生成对应的fstab文件
`````

## 2.2进入系统

````bash
arch-chroot /mnt
````

```bash
pacman -S vim
```

## 2.3网络配置

````bash
vim /etc/hostname
````

```bash
vim /etc/hosts
        127.0.0.1 localhost
        ::1 localhost
        127.0.0.1 ThunderGod.localdomain ThunderGod
```



### 2.4设置密码

```bash
passwd
```



### 2.5安装配置引导程序

```bash
pacman -S grub efibootmgr         #安装引导程序
```

````bash
grub -install --target=x86_64-efi --efi-directory=/efi --bootloader-id=grub #配置引导程序
````

```bash
grub-mkconfig -o /boot/grub/grub.cfg #生成配置文件
```

### 2.6安装联网工具

````bash
pacman -S networkmanager network-manager-applet wpa_supplicant wireless_tools opensssh base-devel linux-headers dialog os-prober mtools dosfstools
````

### 安装完成重启进入系统

````bash
exit
umount /mnt
reboot
````

### 3.系统配置

```bash
systemctl start NetworkManager
systemctl enable NetworkManager
```

### 3.2安装显卡驱动

````bash
pacman -S mesa vulkan-intel xf8-video-intel
````

### 3.3安装显示服务器

````bash
pacman -S xorg
````

### 3.4添加普通用户到用户组

```bash
useradd -m -G wheel aoshisen
passwd aoshisen
```

```bash
vim /etc/sudoers
```

### 3.5安装kde的启动器

```bash
pacman -S sddm
systemctl enable sddm
```

### 4.常用软件和Kde桌面的配置

````bash
pacman -S plasma-desktop konsole dolphin
````

重启就可以进入到系统了





