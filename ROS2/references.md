# ROS2参考资料

## ROS2学习资料

参考：
（1）csdn@鱼香ROS，bilibili@鱼香ROS机器人
（2）bilibili@赵虚左 
（3）菜鸟教程 https://www.runoob.com/?frm=msidevs.net&tg=%CB%F7oE
（4）API https://www.apiref.com/
	API-cpp https://www.apiref.com/cpp-zh/cpp/

官方：
（1）ROS2-Humble Documentation https://docs.ros.org/en/humble/
	ROS2接口 https://docs.ros2.org/latest/api/
（2）colcon文档 https://colcon.readthedocs.io/en/released/index.html
（3）c++ https://cppreference.com/

***

## 遇到的问题和tips

### 1. source /opt/ros/humble/setup.bash
每打开新的终端，执行ros2相关命令之前一定要source，
不管是编译还是简单查看，不管是用colcon还是g++、make、cmake
`source /opt/ros/humble/setup.bash 或 source /opt/ros/humble/setup.zsh`

或直接修改全局环境（永久）
```
vim ~/.bashrc 或 ~/.zshrc
# 在最后一行加上
source /opt/ros/humble/setup.bash 或 source /opt/ros/humble/setup.zsh
```

### 2. vscode中包含rclcpp头文件报错
问题：vscode中`#include"rclcpp/rclcpp.hpp"`显示红色的波浪线
解决方法：包含rclcpp头文件时，如果vscode报错也没关系，是vscode没找到但不影响正常编译，vscode只是编辑器而不是编译器
（1）c_cpp_properties.json中加"includePath":/opt/ros/humble/include/**
（2）点击`#include"rclcpp/rclcpp.hpp"`红色波浪线下的黄色灯泡`Edit "includePath" setting`，在includePath中加`/opt/ros/humble/include/**`