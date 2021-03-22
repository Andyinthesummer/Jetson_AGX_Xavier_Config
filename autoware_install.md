# Autoware Installation

Install autoware from source by following the [source build](https://gitlab.com/autowarefoundation/autoware.ai/autoware/-/wikis/Source-Build)

### Key Steps

1. Flash the xavier with sdkmaneger, ref. [Xavier configuration](xavier_configuration.md).

2. Remove opencv4 and install 3.2.0(default in 18.04)

```bash
## remove opencv4
$ sudo apt-get purge libopencv*
##
$ sudo vim /etc/apt/sources.list.d/nvidia-l4t-apt-source.list
## remove the apt source of jetson
## deb https://repo.download.nvidia.com/jetson/common r32.5 main
## deb https://repo.download.nvidia.com/jetson/t194 r32.5 main
$ sudo apt-get update
```

```bash
## install opencv 3.2.0 default instead of opencv4
$ sudo apt-get install libopencv-dev
```

*Note:*

* opencv 3.2.0 uncompiled with cuda(as shown in `$ jtop`)

* opencv compiled with cuda please ref. [Opencv installation](opencv_install.md)(version 3.4.3)

3. Version of eigen must be greater than 3.3.7

    ```bash
    ## remove v3.4
    sudo find /usr -iname *eigen*
    ## remove related directories and files
    ## example: sudo rm -rf .........
    ## install v3.3.7
    git clone https://gitlab.com/libeigen/eigen.git
    cd eigen
    git checout 3.3.7
    mkdir build
    ## install_dir_prex = /usr
    cmake-gui
    cd build
    make 
    sudo make install
    ```

    *Note:* you can care about version of eigen after you install ros packages and dependencies of autoware, but before compile the autoware.

4. Pcl(v1.8 default)  yaml-cp(0.5.2 default) and velodyne(1.5.2/ros-melodic default) will be installed auotomatically while independencies are installed.


5. Install ros melodic and compile autoware
    Ref. [ros_related](ros_related.md) && [autoware source build](https://github.com/Autoware-AI/autoware.ai/wiki/Source-Build).
    Take care about the version of eigen!

    Create a new script `compile.sh` :
    ```bash
    #!/bin/bash
    AUTOWARE_COMPILE_WITH_CUDA=1 colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release --packages-select op_global_planner

    ## --packages-ignore
    ## --packages-select

    ## op_planner 
    ## op_local_planner 
    ## lidar_sonar_obstacle_detector 
    ## lidar_euclidean_cluster_detect
    ## detected_objects_visualizer 

    ## Without CUDA Support
    ## colcon build --cmake-args -DCMAKE_BUILD_TYPE=Release
    ```


* 

**Ref.**
1. [Autoware Installation Wiki](https://gitlab.com/autowarefoundation/autoware.ai/autoware/-/wikis/Installation)


Autoware Project has been moved to Github: https://github.com/Autoware-AI/autoware.ai

View source code according to [autoware.ai.repos](https://github.com/Autoware-AI/autoware.ai/blob/master/autoware.ai.repos) file.





### Issues
1. CUDA version
support 10.0
10.2 in Jetson AGX Xavier

2. Opencv version


