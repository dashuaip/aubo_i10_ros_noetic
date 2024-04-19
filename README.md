# aubo_i10_ros_noetic

安装前提：使用小鱼一键安装了 ros noetic 和 rosdepc

一键安装指令：
```
wget http://fishros.com/install -O fishros && . fishros
```
---
一、aubo package 安装

1.创建文件夹  
```mkdir -p ~/aubo_ws/src```

2.进入src目录   
```cd ~/aubo_ws/src/```

3.下载 ros package  
```git clone https://github.com/dashuaip/aubo_i10_ros_noetic.git```

或  

```git clone https://gitee.com/dashuaip/aubo_i10_ros_noetic.git```

4.安装依赖  
```sudo apt install ros-noetic-industrial-*```

5.安装依赖  
```sudo apt install ros-noetic-rviz-*```

6.安装依赖  
```sudo apt install ros-noetic-gazebo-*```

7.安装依赖  
```sudo apt install ros-noetic-moveit-*```

8.创建软链接  
```sudo ln -sf /usr/include/eigen3/Eigen/ /usr/include/Eigen```

9.创建软链接  
```sudo ln -sf /usr/include/eigen3/unsupported/ /usr/include/unsupported```

10.下载依赖库   
```wget http://archive.ubuntu.com/ubuntu/pool/main/p/protobuf/libprotobuf9v5_2.6.1-1.3_amd64.deb```

11.安装依赖库   
```sudo dpkg -i libprotobuf9v5_2.6.1-1.3_amd64.deb```

12.安装依赖   
```rosdepc install -y --from-paths . --ignore-src --rosdistro noetic -r```

13.回到工作空间目录  
```cd ~/aubo_ws```

14.编译，失败了就多输几次  
```catkin build```

15.注意***处修改成自己的用户名   
```echo "source /home/***/aubo_ws/devel/setup.bash" >> ~/.bashrc```

16.初始化  
```source ~/.bashrc```

---
二、aubo robot 启动

1.rviz  
想控制真实机械臂，就把 robot_ip 换成机械臂的IP地址  
```roslaunch aubo_i10_moveit_config moveit_planning_execution.launch robot_ip:=127.0.0.1```

2.gazebo  
```roslaunch aubo_gazebo aubo_i10_gazebo_control.launch```
