## xavier image clone and recovery

Flash the system and ref. [xavier_configuration](xavier_configuration.md).

@RECORD

&emsp;&emsp;Check the version of jetpack in xavier: `head n -1 /etc/nv_tegra_release` .

* JetPack4.4.1 has been adopted in sg.
* JetPack4.5.1 has been adopted in cy.

**KEY STEPS**

**1.** 连接Xavier与主机。可以直接使用usb-typc线缆连接，直接分配192.168.55.1字段IP。

**2.** ssh登录Xavier
```bash
## 标记系统为只读
$ sudo echo "u" | sudo dd of=/proc/sysrq-trigger
## 通过DD方式备份系统
$ sudo dd if=/dev/mmcblk0p1 | ssh andy@192.168.55.100 dd of=/home/andy/xavier-image.raw
## 30064771072 bytes (30 GB, 28 GiB) copied, 283.565 s, 106 MB/s
```
**3.** 转化生成的raw到稀疏的img，加快刷机
```bash
## 切换到相应的Jetpack版本bootloader下
$ cd /home/andy/nvidia/nvidia_sdk/JetPack_4.5.1_Linux_JETSON_AGX_XAVIER/Linux_for_Tegra/bootloader
## 转换
$ sudo ./mksparse -v --fillpattern=0 /home/andy/xavier-image.raw system-new.img
## 备份原来的system.img，并将system-new.img更改为system.img
$ mv system.img system-old.img
$ mv system-new.img system.img
```
**4.** 使用usb-typc线缆连接主机和新的xavier设备,将Xavier切换到recovery模式(设备上有三个按钮，按住中间的按钮，再按开机按钮，然后同时放开两个按钮)
```bash
$ cd /home/andy/nvidia/nvidia_sdk/JetPack_4.5.1_Linux_JETSON_AGX_XAVIER/Linux_for_Tegra/
$ sudo ./flash.sh -r jetson-xavier mmcblk0p1
## *** The target t186ref has been flashed successfully. ***
## Reset the board to boot from internal eMMC.
```

**Ref. :**
* https://forums.developer.nvidia.com/t/xavier-cloning/65159/12
* https://forums.developer.nvidia.com/t/duplicate-clone-xavier-filesystem/71211
* https://www.cnblogs.com/gloria-zhang/p/12837212.html
* https://blog.csdn.net/yiyayi1/article/details/105007545/
* https://forums.developer.nvidia.com/t/compile-custom-image-of-jetson-xavier-agx-to-sdk-manager/163800/3
