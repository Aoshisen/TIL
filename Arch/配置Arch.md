# 配置Arch Linux



## 常用软件

 1.浏览器 ：google-chrome firefox

2.下载工具：motrix

3.yay git zsh 

4.开发：visual-studio-code-bin

5.字体：**noto-fonts** **noto-fonts-cjk noto-fonts-emoji** [adobe-source-han-serif-cn-fonts](https://archlinux.org/packages/?name=adobe-source-han-serif-cn-fonts)  [wqy-zenhei](https://archlinux.org/packages/?name=wqy-zenhei)  archlinuxcn/nerd-fonts-complete

6..输入法： fcitx fcitx-libpinyin fcitx-table-other fcitx-table-extra fcitx-qt5 fcitx-configtool

7.Typora

8.create_ap

9.截图工具：deepin-screenshot

10.生产力工具 utools screenkey

11.游戏 steam （需要启用mutilib）需要安装 steam-fonts

然后为了性能需要安装nvidia 

````bash
sudo pacman -S bumblebee
sudo pacman -S nvidia
sudo systemctl enable bumblebeed.service
sudo pacman -S virtualgl
optirun  glxspheres64 #测试性能
````

然后再安装 primusrun

vblank_mode=0 primusrun %command%

vblank_mode=0 primusrun %command% -language schinese -international -perfectworld



12.通信工具 teamviewer

````bash
sudo systemctl enable teamviewerd.service
````

13.视频推流：obs-studio

14.图形处理：inkscape gimp

15.图形查看工具  Gwenview









### Kde插件

panon lanuchpad-plasma  Netspeed-Widget



### yay换源

```bash
yay --aururl "https://aur.tuna.tsinghua.edu.cn" --save
```



### 连接到github

```bash
ssh-keygen -t rsa -C "1041370212@qq.com"
```



### **配置终端**

改变终端为zsh

````bash
chsh -s /bin/zsh #在konsole里面可以不需要这个操作直接在设置里面更改就行了
````



```bash
git clone git://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh    # 下载oh-my-zsh
```



```bash
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc 
#下载好了就有一个模板了，然后复制到家目录就好了
```

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
# 下载一些常用的插件 autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/z	sh-syntax-highlighting
#自动高亮
```

```bash
vim ~/.zshrc #在pulgin那一个括号里面加上这两个插件的名称
```

**终极美化powerline10K**

https://github.com/romkatv/powerlevel10k#oh-my-zsh

```bash
git clone --depth=1 https://gitee.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
#下载powerlne10K
```

```bash
vim ~/.zshrc
# ZSH_THEME="powerlevel10k/powerlevel10k"  将主题设置为powerline10K
```

需要下载一些字体才能正常显示完成

- [MesloLGS NF Regular.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS NF Regular.ttf)

- [MesloLGS NF Bold.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS NF Bold.ttf)

- [MesloLGS NF Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS NF Italic.ttf)

- [MesloLGS NF Bold Italic.ttf](https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS NF Bold Italic.ttf)

- 上面的字体下载不了，所以采用下面的方法，也可以试一试yay nerd-fonts

  ```bash
  git clone https://github.com/ryanoasis/nerd-fonts.git --depth 1
  cd nerd-fonts
  ./install.sh
  ```
  
  

### **系统美化**

kde plasma 样式

WhiteSur-dark 

窗口装饰也是WhiteSur

图标：sudo pacman -S papirus-icon-theme

壁纸：https://wall.alphacoders.com/by_sub_category.php?id=193044&name=%E8%B5%9B%E5%8D%9A%E6%9C%8B%E5%85%8B+%E5%A3%81%E7%BA%B8&lang=Chinese



### **开机自启动的应用**

1. latte dock 
2. fcitx
3. utools
4. screenkey

### **开机启动小键盘**

转到“*系统设置”>“输入设备”>“键盘”*，在“*硬件”*选项卡的“*等离子启动时*的*NumLock”*部分中，选择所需的NumLock行为。（这个会在输入密码之后打开数字键盘，而不是在开机后登陆界面就打开小键盘）

````
vim /etc/sddm.conf #因为我用的是kde桌面，所以会在sddm.conf.d里面读取配置所以这里可以直接编辑vim /etc/sddm.d/kde_settings.conf 
[General]
...
Numblock=on
````



```bash
yay gnome-system-monitor  #gnome家的好看多了

sudo pacman -Rsn ksysguard #系统自带但是删除不了
```



### **下载安装QQ等软件**

yay qq （linuxqq）（deepin-wine-tim）好像这个版本不需要下载什么xsettings就可以运行deepin-wine-tim了果断删除linuxqq

deepin.com.qq.office真香

但是后来这个也挂掉了，因为版本太低的原因后来用的是这个**com.qq.tim.spark 3.2.0.21856spark0-1** 也会有无法输入中文的现象，方法仿照下面的修改就行了，这个简直完美



```bash
/opt/deepinwine/apps/Deepin-TIM
/opt/apps/com.qq.tim.spark/files/run.sh

export XMODIFIERS="@im=fcitx"
export GTK_IM_MODULE="fcitx"
export QT_IM_MODULE="fcitx" #需要粘贴在最后一句话的前面不然没用
```



```bash
sudo pacman -S 	xsettingsd
cp /usr/bin/xsettingsd ~/.config/autostart-scripts/
```

````bash
sudo pacman-S wqy-microhei #这是deepin.com.qq.office需要的字体但是安装了好像也没什么用
````



yay wechat （wechat-uos-2:2.0.0-11451419）

