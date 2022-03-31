# Localization

## 基于地图的定位：

纯里程计是建图的基础，但有累计误差，不能直接用于建图定位，所以我们需要做一些约束，比如回环检测，但回环检测只能减小一部分的累计误差。回环检测或者前端的帧间约束，对地图的一致性还是有影响的，怎么都还会有误差。

我们可以用先验信息，比如组合导航，组合导航有先验的位姿信息，包括姿态，但是先验位姿对于来回建图会有影响，如重影。；而只用RTK或GNSS也是一种方式，这时姿态靠其他方法来给出。

如果需要做高精的地图，那么需要对整个点云进行聚类，提取整个点云的三维特征（实际物体，比如杆，这有点像测绘里面的标定），然后进行后处理优化调整。

### 回环检测、全局定位：

![Localization-2](.\pic\Localization-2.jpg)



对于有初始相对位姿的情况，只需要做当前帧对历史帧对于初始帧的相对位姿匹配。

#### scan context



到历史点云去索引，三维的计算量太大。

三维降为两维，



点云切割：

按照圆环划分，按角度和半径切分，变为二维。

二维矩阵：行代表圆环

列代表扇形。

值为最高的点的高度值

思考：这里是不是可以进行高程划分



基于两个矩阵的匹配：即基于scan context

两个矩阵要差不多。



![1648521574(1)](L:\寒假备份\算法学习\slam融合定位学习\图片\1648521574(1).jpg)

两个矩阵的列向量相互内积为一，即两个矩阵近似是相等的。

d就反映了差异性，值小为差异性大。



但是有旋转变的特性。

朝向变了会有改变



要有旋转不变性:

有一个寻找距离最小的方法

通过切割列，计算当前帧和历史帧的距离最小的那个列对于的当前帧。

计算复杂度太大，如果地图特别大的情况下，因为需要计算二维的数组，进行当前帧和历史帧的匹配，

作者代码中降低计算复杂度的方法是:用同一列进行累加，匹配变成了一维。

降维，但是也会降低准确度， 

先用低维去缩小范围，大概确认在哪，然后二维是进行准确匹配。

缩小范围是跟gps确定范围是一样的意思。

找到了那一帧，帧确定了，位置就确定了，因为历史帧代表了位置，而列的平移量其实就是旋转。

确定了粗略位姿，可以用ICP和NDT的精确匹配。

作用：就是确认粗略的位姿。满足ICP和NDT的位姿要求



降低时间复杂度：

搜索范围同样也是当前帧为圆点，按圆来往外搜索。

统计圆环内是否有点，统计有点的数量，组成向量。

先进行数量的判断。

同样也是一维的方式，大致筛选哪些是值得去匹配的，即相似帧

然后相似帧中再用前面的一维方式，再过滤。

可以构建kdtree，然后进行查找，更加快。







涵盖2.5d信息的理解，我可以理解为二维数据的索引代表了二维平面信息，而值则为高度信息。（转换为高程就是每个值其实是有高度的）

需要考虑深度学习提取特征，考虑强化学习来得到位置。



##### SC-Lego-loam

按照当前帧的发散的圆去搜索历史帧（包括了相对位姿），历史帧要最早的。 这种是相对位姿已知，且偏差不大

找到了历史帧，做匹配的方式： 

当前帧到历史帧的匹配，是直接一帧的匹配，还是submap的匹配

或者是submap和submap的匹配。

计算量和精度的取舍。

粗略匹配上了后，就进行ICP或者NDT

进行scan to map的配准





相对位姿未知，偏差也比较大的情况下，就得到地图上搜索。

要得到航线的偏转、位置就是搜索到的帧。就是里程计的对应点	

将帧旋转到地图上，再进行NDT





来一个关键帧需要生成关键帧信息。scancontext

源码：

先计算半径和角度，根据此来划分区间，并对二维数组进行幅值。

生成kdtree（原理？），用向量，区别有点和无点

找最近邻，即和当前帧最近似的历史帧。

然后进行一维的比较，再进行二维的比较。

这里的比较是有环形数组的平移比较。

输出相差的位姿



每来一次关键帧进行生成scancontext相关信息。

##### Scan_context应用

Integrated with A-LOAM: [SC-A-LOAM](https://github.com/gisbi-kim/SC-A-LOAM)

Integrated with LeGO-LOAM: [SC-LeGO-LOAM](https://github.com/irapkaist/SC-LeGO-LOAM)

Integrated with LIO-SAM: [SC-LIO-SAM](https://github.com/gisbi-kim/SC-LIO-SAM)

Integrated with FAST-LIO2: [FAST_LIO_SLAM](https://github.com/gisbi-kim/FAST_LIO_SLAM)

Integrated with a basic ICP odometry: [PyICP-SLAM](https://github.com/gisbi-kim/PyICP-SLAM)

##### Scan_context相关论文

Scan Context: Egocentric Spatial Descriptor for Place Recognition Within 3D Point Cloud Map.(IROS-2018)

Scan Context++: Structural Place Recognition Robust to Rotation and Lateral Variations in Urban Environments.(T-RO-2021)

SSC: Semantic Scan Context for Large-Scale Place Recognition.(IROS-2021)

Intensity Scan Context: Coding Intensity and Geometry Relations for Loop Closure Detection.(ICRA-2020)

Global Place Recognition using An Improved Scan Context for LIDAR-based Localization System.(2021)

1-Day Learning, 1-Year Localization: Long-Term LiDAR Localization Using Scan Context Image.(2019)

DiSCo-SLAM: Distributed Scan Context-Enabled Multi-Robot LiDAR SLAM With Two-Stage Global-Local Graph Optimization.(2022)

#### 特征直方图

A fast, complete, point cloud based loop closure for LiDAR odometryand mapping

![Localization-1](.\pic\Localization-1.jpg)

感觉用在固态雷达会比较合适。

论文题目：A fast, complete, point cloud based loop closure for LiDAR odometryand mapping
应用案例：loam_livox
开源代码：https://github.com/hku-mars/loam_livox