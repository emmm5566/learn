# docker

## 安装
```
# linux安装
sudo curl -fsSL https://get.docker.com| bash -s docker --mirror Aliyun

# 启动
sudo service docker start
```

***

## 常见问题

### 问题1：Docker Hub 拉取镜像失败的网络问题
```
# 编辑 Docker 的配置文件
sudo vim /etc/docker/daemon.json
# 添加镜像
{ "registry-mirrors": ["https://do.nark.eu.org", "https://dc.j8.work", "https://docker.m.daocloud.io", "https://dockerproxy.com", "https://docker.mirrors.ustc.edu.cn", "https://docker.nju.edu.cn"]  }
```


***

参考：
https://github.com/tech-shrimp/docker_installer
https://www.bilibili.com/video/BV1THKyzBER6
https://docs.qq.com/aio/DSXd3a1RmaFRTZXBP?p=LANRIebmVFAEoiub08h5ob

官方：
https://hub.docker.com
