> [论坛](http://www.hipschina.com/)里这两天讨论这个蛮多，看了会gacotte的readme，整理如下：



## 一、开启PAE模式：


### a、XP系统：修改Boot.ini增加/PAE参数，比如把：
- multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional" /noexecute=optin /fastdetect
- 变成：multi(0)disk(0)rdisk(0)partition(1)\WINDOWS="Microsoft Windows XP Professional" /noexecute=optin /fastdetect /PAE
### b、win7系统：打开CMD，在cmd中输入bcdedit /set pae forceenable再确认启用PAE模式

## 二、ramdisk部分：

-  1：下载ramdisk： [http://www.jensscheffler.de/site ... 4096.5_200811130.7z](http://www.jensscheffler.de/sites/default/files/Gavotte_RAMDisk_1.0.4096.5_200811130.7z)
-  2：先导入注册表ram4g.reg，再运行ramdisk.exe，点击“Install Ramdisk”安装驱动
-  3：Disk Size选择内存盘大小，Driver Letter选择盘符【我喜欢用B，4中将以B为例】，Media Type选择Fixed Media，按OK确认。切记此时不要做其他内存盘任何操作
-  4：运行FORMAT /FS:NTFS /Q /V:RamDisk B:转成NTFS模式，再运行CHKDSK /L:2048 B:更改NTFS日志大小，再预设TEMP文件夹MKDIR B:\TEMP，再去Gavotte_RAMDisk文件夹内运行rdutil B: registry保存内存盘目录结构等设置到注册表（批处理很方便-_-!!!）
-  5：重启，重启后设置浏览器临时文件夹到B:\\temp ，如果需要修改系统环境变量的temp建议也设置到该子目录别用根目录。

## 三、其他：

- 1：放虚拟内存文件到内存盘，这是一个好主意，不过意义不大，除非你能逆天到有足够内存虚拟一个4G的内存盘。
-  2：开启PAE模式失败的，可以查看下是不是硬件不支持。运行everest，如图：

`Gmeek-html<img src=https://cdn.jsdelivr.net/gh/chaizia/pic/img/20241213141124244.png>`

<!-- ##{"timestamp":1316917536}## -->