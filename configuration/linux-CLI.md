# Linux常用命令

- GUI（Graphical User Interface）图形用户界面
- CLI（Command-Line Interface）命令行界面了

## ubuntu安装

### 更新
`sudo apt update `

### 安装
#### 1. apt
Debian系统的系统（Debian，Ubuntu，Deepin，Raspbian等）都可以使用apt命令安装软件
```
sudo apt install 软件包 -y
或 sudo apt-get install 软件包
```
-y ： 默认yes
```
# apt命令用法：
    更新软件列表：apt update -y
    搜索软件: apt search 关键字
    显示软件包详情：apt show 软件包名
    安装软件：apt install 软件包名
    升级指定软件：apt upgrade 软件包名
    升级所有可以升级的软件：apt upgrade
    卸载软件：apt remove 软件包名
    卸载软件并移除软件依赖：apt autoremove 软件包名
    卸载软件并删除配置文件：apt remove 软件包名 --purge
```
#### 2. snap
```
# snap命令用法：
	搜索软件包：snap find 关键字
    显示软件包详情：snap info 软件包名
    安装软件包：snap install 软件包名
    升级指定软件：snap refresh 软件包名
    升级所有可以升级的软件：snap refresh
    卸载软件：snap remove 软件包
```
#### 3. dpkg
在官网提供deb后缀的软件包下载
`sudo dpkg -i 文件名.deb`

### 自动修复依赖
```
sudo apt --fix-broken install -y 
或 sudo apt install -f -y 
```

***

## Linux常用指令

菜鸟教程 https://www.runoob.com/w3cnote/linux-common-command-2.html

| 命令 | 英文全称 | 核心用途 | 基本语法 |
|---|---|---|---|
| **系统基础类** | - | - | - |
| sudo | superuser do | 普通用户临时获取 root 超级管理员权限 | `sudo [选项] <command>` |
| su | switch user | 切换用户身份 | `su [选项] [用户名]` |
| exit | 无（内置命令） | 退出当前终端/用户环境 | `exit` |
| clear | 无（内置命令） | 清空终端屏幕输出 | `clear` |
| history | 无（内置命令） | 查看终端执行过的历史命令 | `history [选项]` |
| reboot | 无（系统命令） | 重启系统 | `sudo reboot` |
| shutdown | 无（系统命令） | 关闭/定时关闭系统 | `sudo shutdown [选项] [时间]` |
| man | manual | 查看命令官方帮助文档 | `man [选项] <command>` |
| which | 无（工具命令） | 查看命令的绝对执行路径 | `which <command>` |
| **文件目录类** | - | - | - |
| ls | list | 列出目录下文件/子目录 | `ls [选项] [目录/文件]` |
| cd | change directory | 切换工作目录 | `cd [目标目录]` |
| pwd | print working directory | 查看当前所在的绝对工作目录 | `pwd` |
| mkdir | make directory | 创建新目录 | `mkdir [选项] <目录名>` |
| rm | remove | 删除文件/目录 | `rm [选项] <文件/目录>` |
| cp | copy | 复制文件/目录 | `cp [选项] <源文件/目录> <目标路径>` |
| mv | move | 移动/重命名文件/目录 | `mv [选项] <源文件/目录> <目标路径/新名称>` |
| touch | 无（系统命令） | 创建空文件/更新文件时间戳 | `touch <文件名>` |
| cat | concatenate | 查看小文件完整内容/拼接文件 | `cat [选项] <文件>` |
| head | 无（工具命令） | 查看文件开头内容 | `head [选项] <文件>` |
| tail | 无（工具命令） | 查看文件结尾内容/实时监控日志 | `tail [选项] <文件>` |
| find | 无（工具命令） | 按条件查找文件/目录 | `find [路径] [选项] [匹配规则]` |
| grep | global regular expression print | 按关键词过滤文本内容 | `grep [选项] <关键词> <文件>` |
| tar | tape archive | 压缩/解压文件 | `tar [选项] <压缩包名> <文件/目录>` |
| zip | 无（工具命令） | 压缩文件为 ZIP 格式 | `zip [选项] <压缩包名> <文件/目录>` |
| unzip | 无（工具命令） | 解压 ZIP 格式文件 | `unzip [选项] <压缩包名>` |
| **权限管理类** | - | - | - |
| chmod | change mode | 修改文件/目录访问权限 | `chmod [选项] <权限> <文件/目录>` |
| chown | change owner | 修改文件/目录所有者 | `chown [选项] <所有者:组> <文件/目录>` |
| chgrp | change group | 修改文件/目录所属用户组 | `chgrp [选项] <用户组> <文件/目录>` |
| **包管理类（Ubuntu）** | - | - | - |
| apt | advanced package tool | 系统包管理器（安装/更新/卸载） | `sudo apt [选项] <操作> <软件包>` |
| apt-get | advanced package tool get | apt 底层命令（脚本常用） | `sudo apt-get [选项] <操作> <软件包>` |
| apt-cache | advanced package tool cache | 搜索/查询软件包信息 | `apt-cache [选项] <操作> <关键词>` |
| dpkg | Debian package | 安装本地 DEB 包 | `sudo dpkg [选项] <包文件>` |
| snap | Snappy（Snap Package Manager） | 跨发行版包管理器 | `sudo snap [选项] <操作> <软件包>` |
| **进程服务类** | - | - | - |
| ps | process status | 查看运行进程 | `ps [选项]` |
| top | table of processes | 实时监控进程/系统资源 | `top [选项]` |
| kill | 无（系统命令） | 终止进程 | `kill [选项] <进程ID>` |
| pkill | process kill | 按进程名终止进程 | `pkill [选项] <进程名>` |
| systemctl | system control | 管理系统服务 | `sudo systemctl [选项] <操作> <服务名>` |
| nohup | no hang up | 后台运行命令（断开终端不中断） | `nohup <命令> &` |
| jobs | 无（内置命令） | 查看后台运行的任务 | `jobs [选项]` |
| fg | foreground | 将后台任务调至前台 | `fg [任务ID]` |
| bg | background | 将前台任务放至后台 | `bg [任务ID]` |
| **系统硬件类** | - | - | - |
| uname | unix name | 查看系统内核/架构信息 | `uname [选项]` |
| lsb_release | linux standard base release | 查看 Ubuntu 系统版本 | `lsb_release [选项]` |
| df | disk free | 查看磁盘空间使用情况 | `df [选项]` |
| du | disk usage | 查看文件/目录磁盘占用 | `du [选项] <文件/目录>` |
| free | 无（工具命令） | 查看内存/交换分区使用情况 | `free [选项]` |
| lscpu | list cpu | 查看 CPU 硬件信息 | `lscpu` |
| nvidia-smi | nvidia system management interface | 查看 NVIDIA 显卡/显存/驱动信息 | `nvidia-smi` |
| nvcc | nvidia cuda compiler | 查看 CUDA 版本 | `nvcc -V` |
| **网络操作类** | - | - | - |
| ip | ip route | 查看/配置网卡信息 | `ip [选项] <操作>` |
| ping | 无（网络工具） | 测试网络连通性 | `ping [选项] <目标IP/域名>` |
| wget | web get | 从网络下载文件 | `wget [选项] <URL>` |
| curl | command line url tool | 测试网络接口/下载文件 | `curl [选项] <URL>` |
| ss | socket statistics | 查看网络端口占用 | `ss [选项]` |
| scp | secure copy | 跨服务器安全复制文件/目录 | `scp [选项] <源> <目标>` |
| rsync | remote sync | 本地/远程文件增量同步 | `rsync [选项] <源> <目标>` |
| ssh | secure shell | 远程登录服务器 | `ssh [选项] <用户名@服务器IP>` |

***

## Linux常用路径/查找命令
```
一、当前路径 & 目录切换
pwd                # 显示当前绝对路径
cd 目标路径        # 切换目录
cd ./make          # 进入同名文件夹（避坑写法）
cd ..              # 返回上一级
cd ~               # 回到家目录

二、文件 / 目录查找
find . -name "*.cpp"                # 当前目录找指定文件
find / -name "setup.zsh" 2>/dev/null  # 全局查找(屏蔽错误)
locate 文件名                       # 快速全局查找(先 sudo updatedb)
ls -l 路径                          # 查看目录详情
ls -R 路径                          # 递归查看子目录

三、可执行命令定位
which ros2           # 查找命令可执行路径
which python3
whereis ros2         # 查命令+手册+源码路径

四、IP / 网络地址
ip addr              # 查看网卡与IP
hostname -I          # 快速输出本机IP
ping IP/域名         # 网络连通测试

五、路径环境辅助
echo $PATH           # 查看系统可执行路径
realpath 文件/目录   # 输出绝对路径
```

***

## 常用快捷键

```
# ubuntu

## 窗口管理
Super  #应用列表，super键即win键（系统键）
Super + ←/→/↑/↓  #窗口贴边
Super + Tab  #切换窗口
PrtSc  #截图
Alt + F4  #关闭当前窗口
Ctrl + F4  #关闭当前页面
Alt + 空格  #窗口操作选择(Alt + 空格 -> Always on Top  #置顶)

## 终端操作 
Ctrl + Shift + T  #新建终端
Ctrl + Shift + C/V  #终端复制/粘贴
Ctrl + L  #清空终端 
Ctrl + D  #退出终端 
Tab  #自动补全
↑/↓  #查看调用上/下一条命令

## 文件管理
Ctrl + C/V/X  #复制/粘贴/剪切 
Ctrl + Z  #撤销
Ctrl + S  #保存
Ctrl + N  #新建文件夹 
Ctrl + F  #搜索文件 
Ctrl + H  #显示隐藏文件
F2  #重命名
Delete  #移至回收站 
```

***

## 常见问题

### 1. ubuntu死机
按住 Alt + PrtSc的同时，缓慢依次按下(每个键间隔 1-2 s) R E I S U B