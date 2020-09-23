## Usefull Tools

### Jetson-Stats
[jetson-stats](https://github.com/rbonghi/jetson_stats#jtop) is a package to monitoring and control your NVIDIA Jetson [Xavier NX, Nano, AGX Xavier, TX1, TX2] Works with all NVIDIA Jetson ecosystem.

The detail instruction is shown in [github repository](https://github.com/rbonghi/jetson_stats). Here some basic operations will be introduced.

#### Install
```bash
## install pip, if you need
sudo apt-get install python-pip
## or install pip3, if you need 
sudo apt-get install python3-pip
## install jetson-stats with pip 
sudo -H pip install jetson-stats
## or install jetson-stats with pip3
sudo -H pip3 install jetson-stats
## you can update the tool 
sudo -H pip install -U jetson-stats
```

After installation, just `sudo reboot` your jetson device.

#### Basic Usage

```console
nvidia@jetson-xavier:~/$ jtop
nvidia@jetson-xavier:~/$ jtson_release -v
```

#### Control jetson in your python script with jtop library
You can run jtop in your python script and control the jetson,  include  Tegrastats, NVP Model, Fan, Status board (i.g. Model version, Jetpack, … )), [read here](https://github.com/rbonghi/jetson_stats/wiki/library) for detail.


### VS-Code

Xavier是arm架构,和x86架构vs安装包不同
#### github源
Ref [Jetson Xavier Nano Lesson 2](https://v.qq.com/x/page/e097699jzox.html) and [Jetson Nano Lesson 37](https://www.youtube.com/watch?v=ZcmgUY6j_bI&ab_channel=PaulMcWhorter).
```bash
$ sudo apt-get install curl
$ curl -L https://github.com/toolboc/vscode/releases/download/1.32.3/code-oss_1.32.3-arm64.deb -o code-oss_1.32.3-arm64.deb
sudo dpkg -i code-oss_1.32.3-arm64.deb
```
然后打开code-oss即可使用.

#### packagecloud源
1. 进入网站 https://packagecloud.io/headmelted/codebuilds, 点击Packsges

2. 查看安装包列表,选择需要的版本(后缀带有arm64(aarch64))，点击查看wget命令,复制下载安装包,使用dpkg进行安装
    ```bash
    # example
    $ wget --content-disposition https://packagecloud.io/headmelted/codebuilds/packages/debian/stretch/code-oss_1.32.0-1550644676_arm64.deb/download.deb
    $ sudo dpkg -i code-oss_1.32.0-1550644676_arm64.deb
    ```
