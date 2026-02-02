# Ubuntu安装

## 1.双系统
【Windows 10 和 Ubuntu 双系统的安装和卸载】 https://www.bilibili.com/video/BV1554y1n7zv/?share_source=copy_web&vd_source=3edb0252876833ef8605499dfd2a02a7
https://blog.csdn.net/kuwola/article/details/127618930?fromshare=blogdetail&sharetype=blogdetail&sharerId=127618930&sharerefer=PC&sharesource=emmm555&sharefrom=from_link

## 2.vim
sudo apt install vim

## 3.ROS2，docker，vscode，github桌面版，微信
wget http://fishros.com/install -O fishros && . fishros

## 4.QQ
https://im.qq.com/linuxqq/  x86版
uname -m 查看系统架构 

## 5.github桌面版
https://github.com/shiftkey/desktop/releases

## 6. joplin或obsidian
sudo snap install joplin-desktop 
https://obsidian.md/download

## 7.clash-erge或nekoray或v2rayN
https://nekoray123.com/
https://doc.6bc.net/

## 8.zsh，foxglove

***

## 检查安装与卸载

```
dpkg -l | grep 程序名字  #查找包名
dpkg -l | grep 程序名字 #检查是否安装成功
sudo rm -f /路径/安装包名字.deb  #删除损坏的安装包
sudo apt install -f -y #修复系统可能的安装残留

（一）删除主程序
# 1. 先查找系统中安装的包名（确认安装的版本）
dpkg -l | grep 包中包含的单词 
# 2. 彻底卸载（purge会删除程序+系统级配置）
sudo apt purge 安装包名 -y 
# 3. 清理卸载后残留的依赖包
sudo apt autoremove -y

（二）删除用户级配置文件
# 删除核心配置/缓存/日志（关键） 
rm -rf ~/.config/配置名字 
rm -rf ~/.cache/缓存名字 
rm -rf ~/.local/share/日志名字

（三）验证
# 检查是否还有进程
ps aux | grep -i 进程名字 | grep -v grep 
# 检查是否还有残留文件 
ls -al ~/.config | grep 配置名字 
ls -al /usr/bin | grep 进程名字 
```

