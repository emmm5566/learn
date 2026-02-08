# zsh配置

## 安装zsh
```
sudo apt install zsh git wget
chsh -s /bin/zsh  # 将终端的默认shell改为zsh
```

## 安装oh-my-zsh
```
wget https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh -O - | sh
# 下载并安装GitHub上的zsh配置文件oh-my-zsh
```

## 安装常用插件（高亮和补全）
```
# zsh-autosuggestions是历史命令补全插件
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

# zsh-syntax-highlighting是命令高亮显示，可以判断命令有无
git clone https://gitee.com/Annihilater/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

```

## 配置 .zshrc
```
vim ~/.zshrc
# 找到以下行：
plugins=(git)
# 改为：
plugins=(git zsh-autosuggestions zsh-syntax-highlighting)
```

***

## 遇到的问题

## 遇到的问题

### 问题1：命令输入卡顿
```
# 编辑或创建 /etc/wsl.conf 文件：
sudo vim /etc/wsl.conf
# 添加以下内容：
[interop]
appendWindowsPath=false
# 在 PowerShell 中运行以下命令重启 WSL：
wsl --shutdown
```
参考：https://github.com/zdharma-continuum/fast-syntax-highlighting/issues/13#issuecomment-1080320354

### 问题2：加载环境
```
source /opt/ros/humble/setup.bash 改成 source /opt/ros/humble/setup.zsh
source install/setup.bash 改成 source install/setup.zsh
source ~/.bashrc 改成 source ~/.zshrc
```
