# 参数-动作

## 参数通信

### 1. 参数

参数是节点的一个配置值，可以认为参数是一个节点的设置

参数值类型：
```
bool 和bool[]，布尔类型，用来表示开关
int64 和int64[]，整型
float64 和float64[]，浮点型
string 和string[]，字符串
byte[]，字节数组
```

### 2. param指令

```
# 列出节点参数
ros2 param list
ros2 param list [节点名]

# 获取参数值
ros2 param get <节点名> <参数名>

# 设置参数值
ros2 param set <节点名> <参数名> <新值>

# 保存参数到文件（被保存成/节点名.yaml）
ros2 param dump <节点名> [文件路径]

# 从文件加载参数
ros2 param load <节点名> <文件路径>

# 带参数节点运行
ros2 run <package_name> <executable_name> --ros-args --params-file <file_name>
```

### 3. 参数通信的实现

原理：ROS2的参数操作其实就是通过**服务通信**方式实现的，获取参数列表，set和get操作就是操作相应的服务

ROS2日志级别：
DEBUG开发调试，INFO常规运行信息，WARN警告，ERROR错误，FATAL致命错误
```
# 在运行任意节点时候可以通过CLI传递日志级别配置
ros2 run package-name node-name --ros-args --log-level debug

# rqt
Plugins → Logging → Console
Plugins → Configuration → Parameter Reconfigure
```

CSDN@鱼香ROS： https://blog.csdn.net/qq_27865227/article/details/131552341

***

## 动作通信

### 1. action组成

（1）Action的三大组成部分：
- **目标**：即Action客户端告诉服务端要做什么，服务端针对该目标要有**响应**。解决了不能确认服务端接收并处理目标问题。
- **反馈**：即Action服务端告诉客户端此时做的**进度**如何（类似与工作汇报）。解决执行过程中没有反馈问题。
- **结果**：即Action服务端最终告诉客户端其执行**结果**，结果最后返回，用于表示任务最终执行情况。

（2）action可以实现异步的双向通信

（3）Action由话题和服务共同构建（一个Action = 三个服务 + 两个话题）： 
- 三个服务 —— 1.目标传递服务 2.结果传递服务 3.取消执行服务  
- 两个话题 —— 1.反馈话题（服务发布，客户端订阅） 2.状态话题（服务端发布，客户端订阅）
![[action_structure.png]]

### 2. action指令

```
# 列出所有动作（-t 可看到action的类型）
ros2 action list [--details]

# 查看动作信息
ros2 action info <动作名>

# 发送动作目标
ros2 action send_goal <动作名> <类型> <目标参数> [--feedback]

# 查看参数格式
ros2 interface show <动作类型>
```

### 3. 动作通信的实现

```
// 依赖
--dependencies rclcpp_action

// 接口
# 请求（目标Goal）
float32 theta
---
# 响应（结果Result）
float32 delta
---
# 反馈（Feedback）
float32 remaining

```

CSDN@鱼香ROS：
https://blog.csdn.net/qq_27865227/article/details/131552561
https://blog.csdn.net/qq_27865227/article/details/131552630