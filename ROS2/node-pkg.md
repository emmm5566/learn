# 节点和功能包

## 节点
```
# 运行节点
# 启动 <package_name>包下的 <executable_name>中的节点
ros2 run <package_name> <executable_name>

# 查看节点列表
ros2 node list

# 查看节点信息
ros2 node info <node_name>

# 重映射节点名称
ros2 run turtlesim turtlesim_node --ros-args --remap __node:=my_turtle

# 运行节点时设置参数
ros2 run example_parameters_rclcpp parameters_basic --ros-args -p rcl_log_level:=10
```

***

## 功能包

功能包安装获取
```
# 会自动放置到系统目录，不用再次手动
sudo apt install ros-<version>-package_name
```

功能包pkg指令
```
# 与功能包相关的指令 ros2 pkg
create       Create a new ROS2 package
executables  Output a list of package specific executables
list         Output a list of available packages
prefix       Output the prefix path of a package
xml          Output the XML of the package manifest or a specific tag

# 创建功能包
# –build-type 用来指定该包的编译类型，一共有三个可选项ament_python、ament_cmake、cmake
# –dependencies 指的是这个功能包的依赖
# package_name 在前在后都可以
ros2 pkg create --help
ros2 pkg create <package-name> --build-type {cmake,ament_cmake,ament_python}  --dependencies <依赖名字> --license Apache-2.0
ros2 pkg create [-h] [--package-format {2,3}]
                       [--description DESCRIPTION] [--license LICENSE]
                       [--destination-directory DESTINATION_DIRECTORY]
                       [--build-type {cmake,ament_cmake,ament_python}]
                       [--dependencies DEPENDENCIES [DEPENDENCIES ...]]
                       [--maintainer-email MAINTAINER_EMAIL]
                       [--maintainer-name MAINTAINER_NAME]
                       [--node-name NODE_NAME] [--library-name LIBRARY_NAME]
                       package_name

# 列出可执行文件
ros2 pkg executables  #列出所有
ros2 pkg executables <package-name>  #列出package-name功能包的所有可执行文件

# 列出所有的包
ros2 pkg list

# 输出某个包所在路径的前缀
ros2 pkg prefix <package-name>

# 列出包的清单描述文件
ros2 pkg xml <package-name>
```

***

## 编译

- 在widows平台下，静态链接库是.lib文件，动态库文件是.dll文件
- 在linux平台下，静态链接库是.a文件，动态链接库是.so文件

使用colcon编译
```
# 创建
mkdir -p ws/src/ && cd ws/src  # 创建工作空间
ros2 pkg create pkg_name --build-type ament_cmake --dependencies rclcpp --license Apache-2.0  # 创建功能包 
touch pkg_name/src/node_name.cpp  # 创建节点

# 编译
# 注意：若移动文件要删除build,install,log重新编译
source /opt/ros/humble/setup.zsh 或 source /opt/ros/humble/setup.bash
colcon build --packages-select pkg_name  # 在工作空间下,package[s]
source install/setup.bash 或 source install/setup.zsh
ros2 run pkg_name node_name



# 创建带节点的功能包示例
ros2 pkg create 
  --build-type ament_cmake \
  --dependencies rclcpp std_msgs \
  --node-name my_node \
  --license Apache-2.0 \
  my_cpp_package \
```

colcon build参数
```
# 构建指令
--packages-select，仅生成单个包（或选定的包）。
--packages-up-to，构建选定的包，包括其依赖项。
--packages-above，整个工作区，然后对其中一个包进行了更改。此指令将重构此包以及（递归地）依赖于此包的所有包。
注意：是package[s]，package后面有s

# 指定构建后安装的目录
--build-base 和 --install-base，指定构建目录和安装目录

# 合并构建目录
--merge-install，使用作为所有软件包的安装前缀，把所有包的文件合并到同一目录，环境变量只加1条路径。

# 符号链接安装
--symlink-install，不把文拷贝到install目录，而是通过创建符号链接的方式。

# 错误时继续安装
--continue-on-error，当发生错误的时候继续进行编译。

# CMake参数
--cmake-args，将任意参数传递给CMake。与其他选项匹配的参数必须以空格为前缀。

# 控制构建线程
--executor EXECUTOR，用于处理所有作业的执行程序。默认值是根据所有可用执行程序扩展的优先级选择的。要查看完整列表，请调用 colcon extensions colcon_core.executor --verbose。
    sequential [colcon-core]，一次处理一个包。
    parallel [colcon-parallel-executor]，处理多个作业平行。
–parallel-workers NUMBER，要并行处理的最大作业数。默认值为 os.cpu_count() 给出的逻辑 CPU 内核数。

# 开启构建日志
--log-level，设置日志级别，比如--log-level info。
```



