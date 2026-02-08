# safe-rm
"Solving the issue of accidental file deletion with `rm` on Linux."

***

## 1. 直接使用trash-cli

安装trash-cli
```
# 直接安装
sudo apt update
sudo apt install trash-cli

# 或者安装完整套件（包括 GUI 工具）
sudo apt install trash-cli trashapp
```

基础命令
```
# 删除文件或文件夹到回收站
trash-put filename.txt 或 trash file
trash-put -r directory/ 或 trash folder

# 列出回收站内容
trash-list
trash-list | grep 

# 恢复文件
trash-restore

# 清空回收站
trash-empty

# 删除特定时间的文件
trash-empty 7   # 删除7天前的文件

# 永久删除回收站中特定文件
trash-rm file1.txt

# 帮助命令
trash --help
```

***

## 2. 将rm改为\rm

```
vim ~/.bashrc 或 vim ~/.zshrc
# 创建一个别名，重写rm命令，当使用rm时输出警告
alias rm='echo "Warning: This is a dangerous command, and this action is irreversible! If you absolutely need to proceed, please use \rm." && /bin/rm'
# 通过\rm执行原始的rm命令，绕过警告
alias \rm='/bin/rm'
# 重新加载配置
source ~/.bashrc 或 source ~/.zshrc
```

***

## 3. 恢复rm删除的文件

***

参考：
（1） https://blog.csdn.net/atkstjstsktdtdmg/article/details/147481540
（2） https://blog.csdn.net/bandaoyu/article/details/102578311
（3） https://blog.csdn.net/semillon/article/details/6414729
（4） https://github.com/andreafrancia/trash-cli.git

