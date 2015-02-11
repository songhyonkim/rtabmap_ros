rtabmap_ros
===========

RTAB-Map's ROS package.

For more information, demos and tutorials about this package, visit the [rtabmap_ros](http://wiki.ros.org/rtabmap_ros) page on the ROS wiki.

For the RTAB-Map libraries and standalone application, visit the [RTAB-Map's home page](http://introlab.github.io/rtabmap) or the [RTAB-Map's wiki](https://github.com/introlab/rtabmap/wiki).

## Installation 

### ROS distribution 
RTAB-Map is released as binaries in the ROS distribution.
 * Indigo
  ```
$ sudo apt-get install ros-indigo-rtabmap-ros
```
 * Hydro
  ```
$ sudo apt-get install ros-hydro-rtabmap-ros
```

**Note for Hydro: there are some issues on the actual version released (0.7.3) on ROS, visit [issues](https://github.com/introlab/rtabmap_ros/issues).**

### Build from source
This section shows how to install RTAB-Map ros-pkg on **ROS Hydro** (Catkin build). RTAB-Map works only with the PCL 1.7, which is the default version installed with ROS Hydro (**Fuerte and Groovy are not supported**).
 * **Note for ROS Indigo**: If you want SURF/SIFT, you have to build OpenCV from source to have access to **nonfree module**. See [issue 8](https://code.google.com/p/rtabmap/issues/detail?id=8&can=1) for more details.

 * The next instructions assume that you have setup your ROS workspace using this [tutorial](http://wiki.ros.org/catkin/Tutorials/create_a_workspace). The workspace path is `~/catkin_ws` and your `~/.bashrc` contains:
 
  ```
source /opt/ros/hydro/setup.bash
source ~/catkin_ws/devel/setup.bash
```

 1. First, you need to install the RTAB-Map standalone libraries (**don't checkout in the Catkin workspace**).
 
 ```
$ git clone https://github.com/introlab/rtabmap.git rtabmap
$ cd rtabmap/build
$ cmake -DCMAKE_INSTALL_PREFIX=~/catkin_ws/devel ..  [<---double dots included]
$ make -j4
$ make install
```

 2. Now install the RTAB-Map ros-pkg in your src folder of your Catkin workspace.
 
 ```
$ cd ~/catkin_ws
$ git clone https://github.com/introlab/rtabmap_ros.git src/rtabmap_ros
$ catkin_make
```

#### Update to new version 

```
$ cd rtabmap
$ git pull origin master
$ cd build
$ make
$ make install

$ roscd rtabmap_ros
$ git pull origin master
$ cd ~/catkin_ws
$ catkin_make
```

#### Mapping 

```
$ roscore
```

```
$ roslaunch kobuki_node minimal.launch
```

```
$ roslaunch kobuki_keyop safe_keyop.launch
```

```
$ roslaunch openni_launch openni.launch depth_registration:=true
```

```
$ rosrun depthimage_to_laserscan depthimage_to_laserscan image:=/camera/depth_registered/image_raw
```

```
$ roslaunch rtabmap_ros rgbd_mapping_kobuki.launch
```

