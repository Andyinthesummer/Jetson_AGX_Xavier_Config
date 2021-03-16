# Opencv Installation

## Eigen
[eigen主页](https://eigen.tuxfamily.org/index.php?title=Main_Page)

```bash
## remove v3.4
sudo apt-get purge libeigen3-dev
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

## Opencv Version
```bash
## check opencv vversion
pkg-config opencv --modversion
# opencv4
pkg-config opencv4 --modversion
## check opencv libs installed
pkg-config opencv --lib
## check installation path
sudo find / -iname "*opencv*"
```

使用Sdk manager中的JetPack4.4安装的opencv的版本是4.1.1,使用上述命令即可以查看得到.可以选择卸载opencv4,彻底删除可以通过find命令找到opencv4安装路径和文件夹,手动删除
> sudo apt-get purge libopencv*

## Opencv Instalaion
在Xavier安装opencv3.4,可以参考[Build OpenCV 3.4 on NVIDIA Jetson AGX Xavier Developer Kit](https://www.jetsonhacks.com/2018/11/08/build-opencv-3-4-on-nvidia-jetson-agx-xavier-developer-kit/)进行安装,主要步骤如下:
```bash
$ git clone https://github.com/jetsonhacks/buildOpenCVXavier.git 
$ cd buildOpenCVXavier 
$ git checkout v1.0 
$ vim buildOpenCV.sh 
## 下载结束部分添加exit 0，只用来安装依赖库和下载opencv
$ cd ~/opencv
$ git clone https://github.com/opencv/opencv_contrib.git
$ git checout 3.4.3
```



**Note:**
1. 可以修改shell安装脚本,进行个性化安装,如可以修改安装路径`INSTALL_DIR=/usr/local`(autoware默认安装在`/usr/`路径下),是否下载额外的测试例程`DOWNLOAD_OPENCV_EXTRAS=NO`(不用下),如果opencv源码自己手动下载(git clone可能会比较慢),脚本中如下语句可以注释掉,避免重复执行:
    > cd $OPENCV_SOURCE_DIR    
    > git clone https://github.com/opencv/opencv.git    
    > cd opencv    
    > git checkout -b v${OPENCV_VERSION} ${OPENCV_VERSION}    

2. **opencv_contrib**也可以手动下载,放在opencv文件夹下,编译后安装,具体参考[opencv_contrib 安装](https://blog.csdn.net/JackSparrow_sjl/article/details/81911855),注意安装路径`-D CMAKE_INSTALL_PREFIX=/usr/local`,同时注意指定opencv_contrib的文件路径,例如`-D OPENCV_EXTRA_MODULES_PATH= ../opencv_contrib`,可以在上面openv的cmake编译规则修改,不要直接引用该博客的编译规则

**Ref.** 

1. [Build OpenCV 3.4 on NVIDIA Jetson AGX Xavier Developer Kit](https://www.jetsonhacks.com/2018/11/08/build-opencv-3-4-on-nvidia-jetson-agx-xavier-developer-kit/)

2. [opencv_contrib 安装](https://blog.csdn.net/JackSparrow_sjl/article/details/81911855)

3. [opencv_contrib github](https://github.com/opencv/opencv_contrib)


**Tips:**
1. 软连接sudo ln -s source_file target_file