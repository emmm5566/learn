# Vscode配置多目录C++

## vscode打开
```
code + 文件路径	#打开文件 
code + 文件夹路径	#打开文件夹，加载整个目录作为工作区 
code . 或 code ./	#打开当前终端所在的目录

code -n 文件/文件夹	#强制新建一个VSCode窗口打开（避免和现有窗口合并）
code -r 文件/文件夹	#强制复用当前VSCode窗口打开（节省窗口空间）
code --diff 文件1 文件2	#用VSCode对比两个文件的差异（适合排查代码修改）
```

***

## g++配置运行
### 1. task.json 
```
{
	"version": "2.0.0",
	"tasks": [
		{
			"type": "cppbuild",
			"label": "C/C++: g++ build active file",
			"command": "/usr/bin/g++",
			"args": [
				"-fdiagnostics-color=always",
				"-g",
				// "${file}",
				// "-o",
				// "${fileDirname}/${fileBasenameNoExtension}"

				// 修改args参数
				"-I", //include包含
				"${workspaceFolder}/include", //添加头文件包含
				"${workspaceFolder}/src/*.cpp", //指定要编译的所有源文件
				"-o", //output命名
				"${workspaceFolder}/bin/${fileBasenameNoExtension}" //指定了生成的可执行文件的输出路径和名称，${fileBasenameNoExtension}表示当前文件的基本名称（没有扩展名）
			],
			"options": {
				//"cwd": "${fileDirname}"
				"cwd": "${workspaceFolder}" //任务的工作目录为工作区的根目录
			},
			"problemMatcher": [
				"$gcc"
			],
			"group": {
				"kind": "build",
				"isDefault": true
			},
			"detail": "compiler: /usr/bin/g++"
		}
	]
}



// Terminal -> Configure Default Build Task -> C/C++: g++ build active file

//task.json 文件用于配置任务（Tasks），通常用于构建、运行、测试等操作
//通常，task.json 文件用于配置构建任务，例如使用 CMake 构建项目、使用 Makefile 构建项目、运行测试等
```

### 2.launch.json
```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) Launch",
            "type": "cppdbg",
            "request": "launch",
            //"program": "enter program name, for example ${workspaceFolder}/a.out",
            // 更改启动路径，刚才在task.json文件中将执行文件生成在了bin文件目录下
            "program": "${workspaceFolder}/bin/main",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                },
                {
                    "description": "Set Disassembly Flavor to Intel",
                    "text": "-gdb-set disassembly-flavor intel",
                    "ignoreFailures": true
                }
            ],

            // 执行前先执行task进行编译, 确保launch最新代码结果，也可以不加
            "preLaunchTask": "C/C++: g++ build active file"
        }

    ]
}



// Run -> Add Configuration -> C++(GDB/LLDB) -> Add Configuration: (gdb) Launch

//launch.json 文件用于配置调试器（Debugger）的启动配置
//通常，launch.json 文件用于配置如何启动和调试你的代码，例如调试 C++ 程序、Node.js 应用程序、Python 脚本等

//总的来说，task.json 用于配置任务，而 launch.json 用于配置调试器启动配置
```

### 3. c_cpp_properties.json
CTRL + SHIFT + P 输入命令 : C/C++: Edit configurations (UI)，在Include path中添加：${workspaceFolder}/include
```
{
    "configurations": [
        {
            "name": "Linux",
            "includePath": [
                "${workspaceFolder}/**",
                "${workspaceFolder}/include"  //添加头文件包含
            ],
            "defines": [],
            "compilerPath": "/usr/bin/gcc",
            "cStandard": "c17",
            "cppStandard": "gnu++17",
            "intelliSenseMode": "linux-gcc-x64"
        }
    ],
    "version": 4
}
```

### 4.运行
```
//编译运行：ctrl + shift + b 进行build
//调试运行：f5 启动调试器
```

***

## CMake配置运行
```
# 手动编译
 mkdir build && cd build
 cmake .. 
 make
 ./main

# 使用CMake Tools
# CMake图标 -> PROJECT STATUS
# （1）文件夹Folder后的小铅笔，配置项目信息
# （2）配置Configure：先选中后2项模式(GCC,Debug)，后点击带有箭头的图标
# （3）生成Build：生成可执行文件
```


***

## vscode调试
- 设置断点：点击行号左侧空白处，会出现一个红点，表示断点已设置；
	运行到断点，才能调试VARIABLES和WATCH

- Continue(f5) 继续运行
	Step Over(f10) 单步执行
	Step Into(f11) 进入函数
	Step Out(shift+f11) 跳出函数
	Restart(ctrl+shift+f5) 重启调试
	Stop Shift+F5 停止调试

***

## vscode常用快捷键

```
Tab/Shift Tab  #缩进/自动补全
ctrl + c/v/x  #复制/粘贴/剪切
ctrl + shift + c/v  #终端复制/粘贴
ctrl + Z  #撤销
ctrl + S  #保存

ctrl + ,  #设置
ctrl + k + t  #选择主题 
ctrl + 鼠标滚轮  #调整字体大小(ctrl+, -> Mouse Wheel Zoom)
ctrl + +/-  #全界面缩放
ctrl + shift + 5  #打开新终端
ctrl + f  #文本查找
ctrl + h  #文本替换
ctrl + \  #分屏
ctrl + /  #注释 或 取消注释
ctrl + k + c/u  #注释/取消注释
ctrl + shift + b  #编译运行
f5  #调试运行
f10  #单步执行
f11  #进入函数
f12  #跳转到定义
```

***

## 遇到的问题和tips

### 1. 关闭copilot：
ctrl+shift+p 打开设置
输入 preferences: open usr settings
查找copilot，关闭Github>Copilot>Editor:Enable Auto Completions

***

参考：
（1） https://blog.csdn.net/qq_51482778/article/details/137018621
（2） https://blog.csdn.net/riversuer/article/details/145934761
（3） https://blog.csdn.net/Mr_Wuuuuuu/article/details/135903835