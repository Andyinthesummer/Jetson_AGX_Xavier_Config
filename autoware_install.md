# Autoware Installation

Install autoware from source by following the [source build](https://gitlab.com/autowarefoundation/autoware.ai/autoware/-/wikis/Source-Build)

### Key Steps
* Flash the xavier with sdkmaneger
* Remove opencv4 and install 3.2.0(default in 18.04)
```bash
## remove opencv4
$ sudo apt-get purge libopencv*
##
$ sudo vim /etc/apt/sources.list.d/nvidia-l4t-apt-source.list
## remove the apt source of jetson
## deb https://repo.download.nvidia.com/jetson/common r32.5 main
## deb https://repo.download.nvidia.com/jetson/t194 r32.5 main
$ sudo apt-get update
## install opencv 3.2.0 default instead of opencv4
$ sudo apt-get install libopencv-dev
```
* Version of eigen must be greater than 3.3.7
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
*Note:* you can care about version of eigen after you install ros and dependcies of autoware, but before compile the autoware.

* Install ros and compile autoware

**Ref.**
1. [Autoware Installation Wiki](https://gitlab.com/autowarefoundation/autoware.ai/autoware/-/wikis/Installation)


Autoware Project has been moved to Github: https://github.com/Autoware-AI/autoware.ai

View source code according to [autoware.ai.repos](https://github.com/Autoware-AI/autoware.ai/blob/master/autoware.ai.repos) file.





### Issues
1. CUDA version
support 10.0
10.2 in Jetson AGX Xavier

2. Opencv version


