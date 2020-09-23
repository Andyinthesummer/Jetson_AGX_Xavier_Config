## ROS Installation

### 手动安装
#### Ubuntu镜像源
国内的镜像源速度快,包括阿里,网易,中科大,清华等,该篇[csdn blog](https://blog.csdn.net/xiangxianghehe/article/details/80112149)整理了常见的源,也可以参考具体的镜像云网站.

Example:
```bash
##中科大源
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-updates main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-backports main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-security main restricted universe multiverse
deb https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse
deb-src https://mirrors.ustc.edu.cn/ubuntu/ bionic-proposed main restricted universe multiverse

```

#### Arm镜像源

Arm源和x86源是不一样的,Xavier需要使用arm源,需要将源中`/ubuntu/`改为`/ubuntu-ports/`,如下例:
```bash
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu/ bionic main restricted universe multiverse
## 更改为
deb https://mirrors.tuna.tsinghua.edu.cn/ubuntu-ports/ bionic main restricted universe multiverse
```

#### 修改镜像源

```bash
##在修改源之前注意备份:
sudo cp /etc/apt/sources.list /etc/apt/sources.list.bak
##打开镜像文件修改源:
sudo vim /etc/apt/sources.list
```
#### 更新源
```bash
sudo apt-get update
sudo apt-get upgrade
```

------

下面安装步骤请参考[Ubuntu install of ROS Melodic](http://wiki.ros.org/melodic/Installation/Ubuntu) in ros wiki(1.2-1.6), 以下为简单步骤:
#### Setup your sources.list
```bash
sudo sh -c '. /etc/lsb-release && echo "deb http://mirrors.tuna.tsinghua.edu.cn/ros/ubuntu/ `lsb_release -cs` main" > /etc/apt/sources.list.d/ros-latest.list'
```
#### Set up your keys
```bash
sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654
```
#### Installation
```bash
sudo apt update
sudo apt install ros-melodic-desktop-full
```
#### Environment setup
```bash
echo "source /opt/ros/melodic/setup.bash" >> ~/.bashrc
source ~/.bashrc
```

#### Dependencies for building packages
```bash
sudo apt install python-rosdep python-rosinstall python-rosinstall-generator python-wstool build-essential
```
initialize rosdep
```bash
sudo rosdep init
rosdep update
```

### 使用脚本安装
参照[脚本仓库](https://github.com/jetsonhacks/installROSXavier),注意提前设置镜像源
```bash
$ git clone https://github.com/jetsonhacks/installROSXavier.git
$ cd installROSXavier
$ ./installROSXavier
```