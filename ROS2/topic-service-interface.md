ROS2提供了四种通信方式：
- 话题-Topics
- 服务-Services
- 动作-Action
- 参数-Parameters

# 话题—服务—接口

## 话题通信

### 1. 话题工具

```
# RQT工具之rqt_graph
rqt_graph  #启动
Plugins->Introspection->Node Graph #GUL/RQT操作
ros2 run rqt_graph rqt_graph

ros2 topic -h #-h即--help
```

### 2. topic指令

```
# 启动发布者/订阅者
ros2 run pkg_name node_name

# 查看topic帮助文档
ros2 topic -h #-h即--help

# 列出所有话题
ros2 topic list  # 列出所有话题  
ros2 topic list -t  # 列出所有话题+消息类型

# 查看话题信息
ros2 topic info <话题名>

# 打印实时话题内容
ros2 topic echo <话题名>

# 查看话题的消息类型
ros2 topic type <话题名>

# 手动发布话题消息
ros2 topic pub <话题名> <消息类型> <消息内容> 

# 查看话题发布频率
ros2 topic hz <话题名>

# 查看话题带宽占用
ros2 topic bw <话题名>

# 查看消息类型
ros2 interface show <消息接口>
```

### 3. 话题通信的实现

- 话题：n个发布者 —— n个订阅者，单向通信
- 同一个话题，所有的发布者和接收者必须使用相同消息接口
- 为了防止错过消息，通常先启动订阅者再启动发布者

CSDN@鱼香ROS： https://blog.csdn.net/qq_27865227/article/details/131407311

***

## 服务通信

### 1. service指令

```
# 启动服务端/客户端
ros2 run pkg_name node_name

# 列出所有服务
ros2 service list

# 查看服务详细信息
ros2 service info <服务名>

# 手动调用服务
ros2 service call <服务名> <服务类型> <请求内容>

# 查看服务接口类型
ros2 service type <服务名>

# 查找使用某一接口/某类型的服务
ros2 service find <服务类型>
```

### 2. 服务通信的实现

- 服务：1个服务端 （响应）—— n个客户端（请求），双向通信
- 为了减少客户端等待时间，通常先运行服务端再运行客户端

CSDN@鱼香ROS： https://blog.csdn.net/qq_27865227/article/details/131407468

***

## interface接口

### 1. interface指令

```
# 列出所有接口（msg/srv/action）
ros2 interface list

# 查看接口结构定义
ros2 interface show <接口类型>

# 列出指定包的所有接口
ros2 interface package <包名>

# 生成接口的 Protobuf 格式
ros2 interface proto <接口类型>
```

### 2. 接口形式

接口是一种用来统一的规范

接口格式：
- 话题：xxx.msg，`包名/msg/消息名`
- 服务：xxx.srv，`包名/srv/服务名`
- 动作：xxx.action，`包名/action/动作名`

接口数据类型：
```
# 基础类型（同时后面加上[]可形成数组）
bool
byte
char
float32,float64
int8,uint8
int16,uint16
int32,uint32
int64,uint64
string

# 包类型（在已有的接口类型上进行包含）
uint32 id
string image_name
sensor_msgs/Image（可以多层套娃）
```

### 3. 自定义接口实践

定义接口（示例）
```
// example_ros2_interfaces/srv
// 服务接口 MoveRobot.srv
# 前进后退的距离(请求，客户端发送)
float32 distance
---
# 当前的位置（响应，服务端返回）
float32 pose

// example_ros2_interfaces/msg
// 话题接口 基础类型 RobotStatus.msg
uint32 STATUS_MOVEING = 1
uint32 STATUS_STOP = 1
uint32  status
float32 pose
// 话题接口 混合包装类型 RobotPose.msg
uint32 STATUS_MOVEING = 1
uint32 STATUS_STOP = 2
uint32  status
geometry_msgs/Pose pose

// example_ros2_interfaces/action
// 动作接口 MyRobot.action
# 目标（Goal）：客户端发送的机器人移动目标 
float32 target # 目标坐标
--- 
# 结果（Result）：服务端完成任务后返回的最终结果 
bool success # 是否成功到达目标
--- 
# 反馈（Feedback）：服务端实时发送的移动进度 
float32 current # 当前坐标
```

创建接口功能包编接口
```
ros2 pkg create example_ros2_interfaces --build-type ament_cmake --dependencies rosidl_default_generators 
# 注意功能包类型必须为：ament_cmake
# 自己创建并编译自定义接口文件时依赖rosidl_default_generators必须添加，使用其他包已生成好的接口无需添加
```

编译自定义接口功能包
```
1. 在CMakeLists.txt中，添加rosidl_generate_interfaces。
2. 在packages.xml中，添加<member_of_group>rosidl_interface_packages</member_of_group>。
```
注意：区分generators和generate

ament_cmake类型功能包导入接口
```
1. 在CMakeLists.txt中，添加find_packages和ament_target_dependencies。
2. 在packages.xml中，添加depend标签并将消息接口写入。
3. 在代码中，添加#include"消息功能包/xxx/xxx.hpp"。
```

- 实例
CSDN@鱼香ROS： 
https://blog.csdn.net/qq_27865227/article/details/131407530
https://blog.csdn.net/qq_27865227/article/details/131407551