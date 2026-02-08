# ROS2常用工具

## 1. RQT

- rqt：ROS Qt-based GUI Toolkit（基于Qt框架的ROS图形化工具套件），是 ROS（ROS1/ROS2）官方的图形化可视化、调试、监控工具集 
- Qt ：一款跨平台、C++ 编写的图形用户界面（GUI）开发框架，用于快速开发桌面、嵌入式、移动设备的可视化程序

```
# 安装
# zsh会优先把*当作"路径通配符"去匹配本地文件,把通配符*用单引号/双引号括起来，告诉zsh这是给apt用的通配符，而非本地路径匹配
sudo apt install 'ros-humble-rqt*' -y

# 启动
# 通用启动 
ros2 run rqt_gui rqt_gui 或 rqt
# 常用快捷启动
ros2 run rqt_tf_tree rqt_tf_tree # TF 坐标树 
ros2 run rqt_plot rqt_plot # 数据绘图 
ros2 run rqt_graph rqt_graph # 节点-话题拓扑图
ros2 run rqt_console rqt_console # 日志查看
# 图形化操作
Plugins插件->Introspection内省->Node Graph  #查看节点和节点之间的关系
Plugins->Topic->Message Publisher  #可以图形化发布话题数据
Plugins->Service->Service Caller  #图形化调用服务工具
Plugins->Visualization->Image View  #看图像话题数据的Image View
Plugins->Visualization->MatPlot  #话题数据图形化工具MqtPlot(我的绘图/自定义绘图插件)，可以用来调PID(Proportional–Integral–Derivative,机器人闭环控制算法)
Plugins->Configuration->Dynamic Reconfigure
```

## 2. CLI

`对应的指令 -h  #获取使用方法`

## 3. rosbag2

rosbag2：用于记录话题的数据
```
# 记录
ros2 bag record /topic-name
ros2 bag record topic-name1  topic-name2  #记录多个话题
ros2 bag record -a  #记录所有话题

# -o name 自定义输出文件的名字
ros2 bag record -o file-name topic-name
# -s 存储格式

# 查看录制出话题的信息
ros2 bag info bag-file

# 播放 
ros2 bag play xxx.db3
ros2 topic echo /chatter  #查看数据
# -r 倍速播放
ros2 bag play rosbag2_2021_10_03-15_31_41_0.db3 -r 10  #十倍速播放
# -l 循环播放
ros2 bag play rosbag2_2021_10_03-15_31_41_0.db3  -l
# 播放单个话题
ros2 bag play rosbag2_2021_10_03-15_31_41_0.db3 --topics /chatter

Ctrl + C  #打断录制
ws/rosbag2_xxxxxx.db3  #文件存储位置
```

## 4. RVIZ2

数据可视化工具
```
# 启动
rviz2
ros2 run rviz2 rviz2

# Displays窗口底下Add添加插件
# 鼠标左键、鼠标右键、按下滚轮拖动 可以修改视角

# ctrl + s 保存为默认配置（只能有一个）
# ctrl + shift + s 保存当前rviz2设置，生成.rviz配置文件
rviz2 -d /path/rviz_tf.rviz  #以rviz_tf.rviz配置打开rviz2

```

***

## 常见问题

### 问题1：RVIZ2 报错 `Frame [map] does not exist`
解决方法：Displays->Global Options->Fixed Frame，直接点击map修改成一个存在的坐标系