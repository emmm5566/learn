# git

## 安装git
```
# 安装git
sudo apt update
sudo apt install git
# 查看
git --version
```

***

## git配置
```
git config --global user.name "******" //英文名
git config --global user.email "********@***.com" //邮箱
ssh-keygen -t rsa -C "********@***.com" //邮箱同上

# 连敲三次回车
# 进入id_rsa.pub复制公钥
cd ~/.ssh
gedit id_rsa.pub //gedit或nano或vim

# 打开GitHub，进入你的设置中添加公钥 Settings -> SSH and GPG keys -> New SSH key
ssh -T git@github.com
```

***

## git使用

```
1. git clone <仓库地址SSH>   

2. git branch -a
	/*先看下当前在哪个分支（一般克隆后都在master/main分支），顺便复制一下要去的分支，按q退出*/
3. git checkout -b <分支名>      /*建立分支*/
4. git checkout <要去的分支名称>
5. git branch     /*再确认一下确实已经在自己的分支了*/

6. git pull --no-rebase origin <分支名字>  /*使用合并*/
7. git pull origin <分支名字>
	/*从项目分支拉取最新的代码到个人分支，然后再进行修改，保证每次修改都是修改的最新代码*/

8. git status         /*看看自己修改了哪些文件*/

9. git add .  /*添加当前目录下所有符合条件的文件*/
10. git add <修改了的文件或文件夹名称>

11. git commit -m "任务号 注释说明"   /*提交日志信息*/
12. git log /*查看日志*/

13. git push origin <分支名字>
	/*把已经提交的文件推送到远端仓库*/
```

***

## 问题
1.注意有没有上传，没有提交成功前一定不要切换分支，否则会导致文件混乱

***

参考：
cdsn：https://blog.csdn.net/Jason_Math/article/details/123940302
