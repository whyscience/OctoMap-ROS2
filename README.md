# OctoMap-ROS2

This repository uses a part of the [octomap_mapping](https://github.com/OctoMap/octomap_mapping) `ros2` branch.  

**I recommend utilizing docker to easily configure your environment setting.**

## How to use  

### Requirements  
- [Docker](https://www.docker.com/)  
- [NVIDIA docker](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html)

Clone this repository. It doesn't matter if the path is not a ros2 workspace.   
```
git clone https://github.com/Taeyoung96/OctoMap-ROS2.git
```

### Make a docker image (For the docker user) 
```
cd docker
```
```
docker build -t octomap-ros2:latest .
```

### Environment setting  
- ROS2 humble
- PCL
- Eigen

### Make a docker container  

When you create a docker container, you need several options to use the GUI and share folders.

First, you should enter the command below in the local terminal to enable docker to communicate with Xserver on the host.

```
xhost +local:docker
```

After that, make your own container with the command below.  

```
sudo chmod -R 777 container_run.sh
```
```
./container_run.sh <container_name> <image_name:tag>
```

:warning: **You should change {container_name}, {docker image} to suit your environment.**  

For example,  
```
 ./container_run.sh octomap_ros2 octomap-ros2:latest
```

If you have successfully created the docker container, the terminal output will be similar to the below.  

**output** :  

```
Current working directory: /home/taeyoung/Desktop/FAST_LIO_ROS2
================Octomap server ROS2 Docker Env Ready================
root@taeyoung-cilab:~/ros2_ws#
```

### How to run  

You need to run the 3D Mapping package (ex. FAST_LIO_ROS2) at the same time.  

On `/ros2_ws` directory,
```
colcon build
```

```
source install/setup.bash
```

```
ros2 launch octomap_server octomap_yonsei-hall-4_mapping.launch.xml
```


#### Map save
```
ros2 run nav2_map_server map_saver_cli -f ~/ros2_ws/src/ --ros-args --remap map:=/projected_map
```

