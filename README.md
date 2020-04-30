# FLOAM
## Fast Lidar Odometry and Mapping

## This work is an optimied version of A-LOAM and LOAM with the computational cost reduced by 3 times

This code is modified from [LOAM](https://github.com/laboshinl/loam_velodyne) and [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM) .

**Modifier:** [Wang Han](http://wanghan.pro), Nanyang Technological University

## 1. Modification
This includes some optimization on the original implementation

1. Analytic methods is used instead of auto differentiation. This is performed on se3
2. Use linear motion prediction model to estimate the initial pose
3. Laser odometry and laser mapping are merged 
4. A dynamic local map is used instead of global map, in order to save memory cost. Based on massive experiments, this only has slight influence on the performance. 

## 2. Evaluation
Computational efficiency evaluation (based on KITTI dataset):
Platform: Intel® Core™ i7-8700 CPU @ 3.20GHz 
ALOAM: 151ms per frame
ALOAM_Optimized: 59ms per frame

Localization error:
dataset      			ALOAM     	ALOAM_Optimized
KITTI sequence 00		0.55%		0.51%
KITTI sequence 02		3.93%		1.25%
KITTI sequence 05   	1.28%   	0.93%

<img src="https://github.com/wh200720041/FLOAM/img/kitti_example.gif"/>

## 3. Prerequisites
### 3.1 **Ubuntu** and **ROS**
Ubuntu 64-bit 18.04.
ROS Melodic. [ROS Installation](http://wiki.ros.org/ROS/Installation)

### 3.2. **Ceres Solver**
Follow [Ceres Installation](http://ceres-solver.org/installation.html).

### 3.3. **PCL**
Follow [PCL Installation](http://www.pointclouds.org/downloads/linux.html).

## 4. Build 
###4.1
Clone the repository and catkin_make:
```
    cd ~/catkin_ws/src
    git clone https://github.com/HKUST-Aerial-Robotics/A-LOAM.git
    cd ../
    catkin_make
    source ~/catkin_ws/devel/setup.bash
```
### 4.2 Run Example
Download [KITTI sequence 05](https://drive.google.com/open?id=18ilF7GZDg2tmT6sD5pd1RjqO0XJLn9Mv), unzip and copy the file 2011_09_30_0018.bag into src/aloam_optimized/dataset/. 
```
    roslaunch aloam_optimized aloam_optimized.launch
```

## 5. Test other sequence
To generate rosbag file of kitti dataset, you may use the tools provided by 
[kitti_to_rosbag](https://github.com/ethz-asl/kitti_to_rosbag) or [kitti2bag](https://github.com/tomas789/kitti2bag) 

## 6.Acknowledgements
Thanks for [A-LOAM](https://github.com/HKUST-Aerial-Robotics/A-LOAM) and LOAM(J. Zhang and S. Singh. LOAM: Lidar Odometry and Mapping in Real-time) and [LOAM_NOTED](https://github.com/cuitaixiang/LOAM_NOTED).
