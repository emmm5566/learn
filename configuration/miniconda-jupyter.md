# miniconda和Jupyter

## 安装miniconda
```
# 下载miniconda安装脚本
https://www.anaconda.com/download
# 给安装脚本添加执行权限
chmod +x ~/Downloads/miniconda.sh
# 运行安装脚本
bash ~/Downloads/miniconda.sh
#关闭当前终端，重新打开一个新终端，让 Miniconda 的环境变量配置生效。
source ~/.bashrc 或 source ~/.zshrc
# 验证
conda --version
```

***

## miniconda常用命令

### 一、环境管理命令
```
# 查看所有已创建的 conda 环境
conda env list
conda info --envs

# 创建新环境（指定环境名+Python版本，示例：环境名myenv，Python3.10）
conda create -n myenv python=3.10

# 激活指定环境（进入环境）
conda activate myenv

# 退出当前环境（通用，base/自定义环境均适用）
conda deactivate

# 删除指定环境（谨慎操作，删除环境及所有依赖包）
conda remove -n myenv --all

# 复制已有环境（备份/复用）
conda create -n myenv_copy --clone myenv
```

### 二、包管理命令
```
# 安装单个包（当前激活环境）
conda install numpy

# 安装指定版本包
conda install pandas=2.0.0

# 批量安装多个包
conda install numpy pandas matplotlib

# 卸载单个包
conda uninstall numpy

# 批量卸载多个包
conda remove numpy pandas

# 查看当前环境所有已安装包
conda list

# 查看指定包的版本信息
conda list numpy

# 更新单个包
conda update numpy

# 更新当前环境所有包
conda update --all

# 更新 Miniconda 自身
conda update conda

# 搜索包的可用版本
conda search numpy
```

### 三、配置与其他常用命令
```
# 查看 Miniconda 版本
conda --version
conda -V

# 查看 conda 详细信息（版本、环境路径、配置等）
conda info

# 清理所有无用缓存（释放磁盘空间）
conda clean -a

# 仅清理未使用的包缓存
conda clean -p

# 查看当前 conda 配置
conda config --show
```

### 四、退出 base 环境
1. 临时退出当前终端的 base 环境
`conda deactivate`
2. 永久关闭终端启动时自动激活 base
```
# 关闭自动激活
conda config --set auto_activate_base false

# 恢复自动激活（如需）
conda config --set auto_activate_base true
```

***

## 卸载miniconda
```
# 删除 Miniconda 安装目录
rm -rf ~/miniconda3

# 清理环境变量配置
# 编辑 .bashrc 文件，删除末尾的 conda 初始化代码
nano ~/.bashrc
或 删除 ~/.zshrc 末尾的 conda 初始化代码
nano ~/.zshrc

# 重新加载配置
source ~/.bashrc 或 source ~/.zshrc
```

***

## Jupyter

- 在网页运行python的工具

```
# 安装python3-pip
sudo apt update && sudo apt install -y python3-pip
pip3 --version
# 安装Jupyter
pip3 install jupyter -i https://pypi.tuna.tsinghua.edu.cn/simple

# 启动jupyter notebook
jupyter-notebook

# shift + enter 运行 / Disable Debugger
```

***

## 常见问题

### 问题1：提示 “conda: command not found”
说明初始化未生效，手动执行初始化命令：
```
# 临时激活 conda 基础环境
source ~/miniconda3/bin/activate
# 专门为 Zsh 初始化 conda（关键）
conda init 或 conda init zsh
# 重新加载配置
source ~/.bashrc 或 source ~/.zshrc
```

### 问题2：command not found: jupyter-notebook
```
# 修复PATH
nano ~/.zshrc  # 编辑 zsh 配置文件  
export PATH="$HOME/.local/bin:$PATH"  # 在文件末尾添加以下内容（复制粘贴）  
# 保存退出：按 Ctrl+O → 回车 → Ctrl+X 
source ~/.zshrc  # 刷新配置
```