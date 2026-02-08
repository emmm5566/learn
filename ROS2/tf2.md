# TF坐标变换

## 1. 命令

- TF - TransForm 坐标变换，tf2是ROS2的坐标变换工具
- 欧拉角：yaw偏航角-rz，pitch俯仰角-ry，roll滚转角-rx（弧度制）

```
# tf2_ros 功能包
# static_transform_publisher  静态坐标变换发布

# 查看帮助文件
ros2 run tf2_ros static_transform_publisher -h

# 发布坐标变换
ros2 run tf2_ros static_transform_publisher 
--x X --y Y --z Z  #平移translation
--qx QX --qy QY --qz QZ --qw QW  #四元数quaternion rotation
--roll ROLL --pitch PITCH --yaw YAW  #欧拉角quaternion rotation
--frame-id FRAME_ID --child-frame-id CHILD_FRAME_ID  #<父坐标系> <子坐标系>
# 也可以省略提示符直接写参数
ros2 run tf2_ros static_transform_publisher --x 0.3 --y 0.0 --z 0.0 --roll 0.0 --pitch 0.0 --yaw 3.14 --frame-id base --child-frame-id point
ros2 run tf2_ros static_transform_publisher 0.3 0 0 0 0 3.14 base point

# 查询坐标系之间的关系（子坐标系相对于父坐标系的变换）
ros2 run tf2_ros tf2_echo <父坐标系> <子坐标系>
```

## 2. 可视化工具

```
# mrpt
sudo apt install mrpt-apps -y
3d-rotation-converter

# rqt-tf-tree
sudo apt install ros-humble-rqt-tf-tree
# rqt -> Plugins -> Visualization -> TF Tree

# view_frames  
ros2 run tf2_tools view_frames 
# 在目录下生成 frames.pdf

# tf2_monitor
ros2 run tf2_ros tf2_monitor
```

## 3. C++发布TF

原理
- 静态：发布 /tf_static 话题
- 动态：不断发布 /tf 话题
```
ros2 ropic list
ros2 topic echo /tf_static
```

相关代码
```
// 依赖  --dependencies rclcpp tf2_ros geometry_msgs tf2_geometry_msgs

#include "rclcpp/rclcpp.hpp"
#include "geometry_msgs/msg/transform_stamped.hpp" //提供消息接口
#include "tf2/LinearMath/Quaternion.h" //提供tf2::Quaternion类
#include "tf2_geometry_msgs/tf2_geometry_msgs.hpp" //消息类型转换函数
#include <tf2/utils.h> //简化TF操作
#include "tf2_ros/static_transform_broadcaster.h" //静态坐标广播类
#include <tf2_ros/transform_broadcaster.h> //坐标广播类

//声明&初始化发布者
//静态
std::shared_ptr<tf2_ros::StaticTransformBroadcaster> broadcaster_;
this->broadcaster_ = std::make_shared<tf2_ros::StaticTransformBroadcaster>(this);
//动态
std::unique_ptr<tf2_ros::TransformBroadcaster> tf_broadcaster_;
tf_broadcaster_ = std::make_unique<tf2_ros::TransformBroadcaster>(this);

//发布
geometry_msgs::msg::TransformStamped transform;
transform.header.stamp = this->get_clock()->now(); //时间戳
transform.header.frame_id = "map"; //父坐标系
transform.child_frame_id = "base_link"; //子坐标系
// Fill in transform.transform.translation
transform.transform.translation.x = 0.0; //平移量
transform.transform.translation.y = 0.0;
transform.transform.translation.z =0.0;
// Fill in transform.transform.rotation
auto quat = tf2::Quaternion();
quat.setRPY(0.0;, 0.0, 0.0); //弧度制欧拉角转四元数
transform.transform.rotation = tf2::toMsg(quat); //转成消息接口类型
////transform.transform.rotation.x = 0.0;
////transform.transform.rotation.y = 0.0;
////transform.transform.rotation.z = 0.0;
////transform.transform.rotation.w = 0.0;
tf_broadcaster_->sendTransform(transform);

//静态：发布一次
//动态：使用定时器周期性发布
```

## 4. 查询TF关系

原理：订阅话题 /tf /tf_static 收集所有坐标系关系，进行计算
```
#include "tf2_ros/buffer.h" //提供Buffer
#include "tf2/utils.h" //提供getEulerYPR()

//用buffer收集
buffer_ = std::make_shared<tf2_ros::Buffer>(this->get_clock());
listener_ = std::make_shared<tf2_ros::TransformListener>(*buffer_, this);

//用buffer->lookupTransform查询(目标坐标系, 源坐标系, 当前时刻, 超时时间)
const auto transform = buffer_->lookupTransform(
	"base_link", "target_point", this->get_clock()->now(),
	rclcpp::Duration::from_seconds(1.0f));
```