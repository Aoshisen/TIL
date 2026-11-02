## 安装后的一些问题和解决的思路

**1.panon无法正常显示**

````bash
sudo pacman -S qt5-websockets \
    python-docopt python-numpy python-pyaudio python-cffi python-websockets 
````



**2.终端显示和输入中文**

```
vim /etc/locale.gen

```

```bash
sudo vim ~/.pam_environment

GTK_IM_MODULE DEFAULT=fcitx
QT_IM_MODULE  DEFAULT=fcitx
XMODIFIERS    DEFAULT=@im=fcitx  # 解决了终端不能输入中文的问题
```



**3.本地化设置**（在很多地方还是有英语，在终端里面是不可以显示中文的，所以需要通过本地化设置来改变这个问题）

官方地址：https://wiki.archlinux.org/index.php/Localization_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)/Simplified_Chinese_(%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87)

```bash
sudo vim /etc/locale.conf
   export LC_ALL=zh_CN.UTF-8  #这样做是可以的
   LANG=en_US.UTF-8 #官方推荐的
```

然后官方推荐的还可以在~/.xprofile 里面设置本地化

````bash
vim ~/.xprofile
   export LANG=zh_CN.UTF-8
export LANGUAGE=zh_CN:en_US
# 官方不推荐使用 export LC_ALL=zh_CN.UTF-8 但是这个是真的无脑我就是用的这个
````





