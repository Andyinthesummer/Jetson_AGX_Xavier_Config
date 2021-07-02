## 双系统安装教程

### ubuntu镜像制作
1. 下载ISO镜像文件
   可以从[ubuntu官方网站](https://ubuntu.com/)，也可以从国内镜像源网站下载，如：[中科大源](http://mirrors.ustc.edu.cn/ubuntu-releases/)或者[阿里云源](http://mirrors.aliyun.com/ubuntu-releases/)。
   i386 - 32位（Intel制定的标准）
   amd  - 64位（AMD制定的标准）
2. 下载并安装[UltraISO](https://cn.ultraiso.net/)软件制作U盘启动
   * 文件->打开ISO文件
   * 启动->写入硬盘硬盘映像，写入方式一般可以选择USB-HDD+

### ubuntu系统安装

**1.** 使用DiskGenius清除原ubuntu系统使用的几个分区(包括EFI分区)，注意不要删除Windows的EFI分区，参考[博客](https://blog.csdn.net/guikunchen/article/details/88077330)去除引导项

**2.** F2进入BIOS，设置U盘开机启动

**3.** 开始安装参考[博客](https://www.cnblogs.com/masbay/p/10844857.html)进行分区设置，然后选择对应的引导器    

   * /efi: 分配启动引导空间，一般200MB到500MB即可    
    512MB+逻辑分区+空间起始位置+EFI文件系统    
    *这里一定要选择EFI文件系统，不要选择/boot，下面选择启动设备要用到它*
   * /swap: 分配交换空间，分配与自己内存相仿的大小    
   如8000MB+逻辑分区+空间起始位置+交换空间
   * / :分配根目录空间，用于装系统30GB左右    
   50000MB+主分区+空间起始位置+Ext4日志文件系统+/    
   * /home: 分配/home目录空间，这里用于存放用户文件    
   剩余所有空间+逻辑分区+空间起始位置+Ext4日志文件系统+/home    

### 安装完成后任务项
* 修改源 tuna/ustc/aliyun...
* NVIDIA-MX250驱动安装
  - [驱动安装](https://zhuanlan.zhihu.com/p/105135151?utm_source=qq)
  - [cuda-9.0安装](https://blog.csdn.net/wqwqqwqw1231/article/details/101776245)    
*注意安装cuda时不要安装opengl，否则可能开不了机*
* chromium安装
```bash
sudo add-apt-repository ppa:a-v-shkop/chromium
sudo apt-get upate
sudo apt-get install chromium-browser

## uninstall firefox
dpkg --get-selections  |grep firefox
sudo apt-get purge firefox firefox-locale-en firefox-locale-zh-hans
```
* 中文输入法安装（谷歌输入法）--*[参考博客](https://blog.csdn.net/a1015392344/article/details/99350608)*
```bash
## 安装中文输入法的支持
sudo apt-get install language-pack-zh-hans
## 安装谷歌输入法
sudo apt-get install fcitx-googlepinyin
## 打开设置中的语言设置，键盘输入方法改为fcitx
## 重启系统
sudo reboot
## 打开终端，输入命令：fcitx-configtool， 打开fcitx设置，来添加google输入法。点击 + 号来添加
## 取消勾选“”Only show current language“”, 拖动滚动条，找到Google Pinyin，点击OK，添加完成。
```
* opencv安装 -- *[参考博客](https://blog.csdn.net/echoamor/article/details/83022352)*
  采用cmake-gui进行编译安装，能更好的进行编译参数设置
* eigen 3.3.7安装--*DCMAKE_INSTALL_PREFIX=/usr*
  
* pcl1.9安装    
  安装目录*DCMAKE_INSTALL_PREFIX=/usr*，可以通过cmake-gui来显式设置    
  注意版本问题：*cuda9.0 对应pcl1.9.1*，否则可能报错    
  注意安装依赖库时eigen的版本，不用安装以免覆盖3.3.7

* github密钥设置
* google账户
* vimrc
