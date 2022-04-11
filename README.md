# Mapping-Localization-Planning-Learning
参考任乾大神的深蓝学院多传感器融合定位课程和知乎文章；从SLAM的mapping到localization，再到planning的学习过程和记录。

## Preparation

[建图-定位和障碍物检测的研究分析](https://github.com/goldqiu/Mapping-Localization-Planning-Learning/blob/main/建图-定位和障碍物检测的研究分析.md)

## SLAM

### Mapping

[here](https://github.com/goldqiu/Mapping-Localization-Planning-Learning/tree/main/SLAM/Mapping)

#### 参考博客

##### 开源框架测试

[goldqiu：一：Tixiao Shan最新力作LVI-SAM(Lio-SAM+Vins-Mono)，基于视觉-激光-惯导里程计的SLAM框架，环境搭建和跑通过程](https://zhuanlan.zhihu.com/p/369154727)

[goldqiu：二.激光SLAM框架学习之A-LOAM框架---介绍及其演示](https://zhuanlan.zhihu.com/p/423077984)

[goldqiu：八.激光SLAM框架学习之LeGO-LOAM框架---框架介绍和运行演示](https://zhuanlan.zhihu.com/p/427840280)

[goldqiu：十一.激光惯导LIO-SLAM框架学习之LIO-SAM框架---框架介绍和运行演示](https://zhuanlan.zhihu.com/p/433113761)

[goldqiu：十二.激光SLAM框架学习之livox-loam框架安装和跑数据集](https://zhuanlan.zhihu.com/p/432520314)

[goldqiu：二十二.香港大学火星实验室R3LIVE框架跑官方数据集](https://zhuanlan.zhihu.com/p/456548828)

##### 实车测试

[goldqiu：七.激光SLAM框架学习之A-LOAM框架---速腾Robosense-16线雷达室内建图](https://zhuanlan.zhihu.com/p/427334685)

[goldqiu：九.激光SLAM框架学习之LeGO-LOAM框架---速腾Robosense-16线雷达室外建图和其他框架对比、录包和保存数据](https://zhuanlan.zhihu.com/p/428105632)

[goldqiu：十三.激光SLAM框架学习之livox-Mid-70雷达使用和实时室外跑框架](https://zhuanlan.zhihu.com/p/434685990)

[goldqiu：十六.激光和惯导LIO-SLAM框架学习之配置自用传感器实时室外跑LIO-SAM框架](https://zhuanlan.zhihu.com/p/434718863)

[goldqiu：十八.多个SLAM框架（A-LOAM、Lego-loam、LIO-SAM、livox-loam）室外测试效果粗略对比分析](https://zhuanlan.zhihu.com/p/441386977)

[goldqiu：二十四-香港大学火星实验室FAST-LIO2框架跑官方数据集](https://zhuanlan.zhihu.com/p/481546652)

##### 标定

[goldqiu：十四.激光和惯导LIO-SLAM框架学习之惯导内参标定](https://zhuanlan.zhihu.com/p/434710744)

[goldqiu：十五.激光和惯导LIO-SLAM框架学习之惯导与雷达外参标定（1）](https://zhuanlan.zhihu.com/p/434718435)

[goldqiu：二十.激光、视觉和惯导LVIO-SLAM框架学习之相机内参标定](https://zhuanlan.zhihu.com/p/446297673)

[goldqiu：二十一.激光、视觉和惯导LVIO-SLAM框架学习之相机与雷达外参标定（1）](https://zhuanlan.zhihu.com/p/446297974)

##### 开源框架学习

[goldqiu：三.激光SLAM框架学习之A-LOAM框架---项目工程代码介绍---1.项目文件介绍（除主要源码部分）](https://zhuanlan.zhihu.com/p/423245638)

[goldqiu：四.激光SLAM框架学习之A-LOAM框架---项目工程代码介绍---2.scanRegistration.cpp--前端雷达处理和特征提取](https://zhuanlan.zhihu.com/p/423300393)

[goldqiu：五.激光SLAM框架学习之A-LOAM框架---项目工程代码介绍---3.laserOdometry.cpp--前端雷达里程计和位姿粗估计](https://zhuanlan.zhihu.com/p/423323274)

[goldqiu：六.激光SLAM框架学习之A-LOAM框架---项目工程代码介绍---4.laserMapping.cpp--后端建图和帧位姿精估计（优化）](https://zhuanlan.zhihu.com/p/423348129)

[goldqiu：十.激光SLAM框架学习之LeGO-LOAM框架---算法原理和改进、项目工程代码](https://zhuanlan.zhihu.com/p/429096191)

[goldqiu：十七.激光和惯导LIO-SLAM框架学习之IMU和IMU预积分](https://zhuanlan.zhihu.com/p/437378667)

[goldqiu：十九.激光和惯导LIO-SLAM框架学习之项目工程代码介绍---代码框架和一些文件解释](https://zhuanlan.zhihu.com/p/444858817)

[goldqiu：二十三.激光和惯导LIO-SLAM框架学习之LIO-SAM项目工程代码介绍---基础知识](https://zhuanlan.zhihu.com/p/445862584)https://zhuanlan.zhihu.com/p/481546652)

### Localization

[here](https://github.com/goldqiu/Mapping-Localization-Planning-Learning/tree/main/SLAM/Localization)

#### 参考博客

[goldqiu：二十五.SLAM中Mapping和Localization区别和思考](https://zhuanlan.zhihu.com/p/494959811)

[goldqiu：一.全局定位--开源定位框架LIO-SAM_based_relocalization实录数据集测试](https://zhuanlan.zhihu.com/p/494961228)

[goldqiu：二.全局定位--开源定位框架livox-relocalization实录数据集测试](https://zhuanlan.zhihu.com/p/496006244)

#### Preparation

[定位前言](https://github.com/goldqiu/Mapping-Localization-Planning-Learning/tree/main/SLAM/Localization/定位前言.md)

## Planning

[here](https://github.com/goldqiu/Mapping-Localization-Planning-Learning/tree/main/Planning)

### Gazebo二维路径规划仿真

#### 参考博客

[goldqiu：一.路径规划---二维路径规划仿真实现-gmapping+amcl+map_server+move_base](https://zhuanlan.zhihu.com/p/455852721)

[goldqiu：二.路径规划---二维路径规划实车实现---gmapping+amcl+map_server+move_base](https://zhuanlan.zhihu.com/p/457770455)

#### 工程

[Gazebo_simulation](https://github.com/goldqiu/Mapping-Localization-Planning-Learning/tree/main/Planning/Gazebo_simulation)

