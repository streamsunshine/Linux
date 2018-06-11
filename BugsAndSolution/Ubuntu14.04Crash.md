# System Crash

在安装udev后，并没有达到自己的目的，所以决定卸载udev，使用命令sudo apt-get remove udev后，系统崩溃，无法启动。提示缺少/sbin/init文件。

## 崩溃原因猜想

首先说明卸载指令
* apt-get remove 移除软件并保留配置文件
* apt-get remove --purge 卸载并删除配置文件
* apt-get autoremove 将自动卸载所有自动安装且不再使用的软件包（可能删除一些系统必要的包，慎重）

所以指令应该没问题，怀疑因为udev是系统组件，所以导致系统卸载了一些依赖关系，进而系统无法启动。

### 解决步骤及结果

1、采用了网上一篇[ubuntu16.04使用sudo apt-get autoremove导致系统崩溃的解决办法](https://blog.csdn.net/TAB_YLS/article/details/79422631)选择其中的修复grub，结果重新安装了grub，导致我的grub的操作系统选择界面也崩溃了（我安装的win7和ubuntu14.04的双系统），grub只能命令行。  
这个方法不一定不行，可以考虑使用boot-repair的磁盘修复模式也许好使。

2、接下来解决grub命令行的问题，找到的解决方案中要求使用root指令，但是grub2之后的版本已经不支持了，找到的[解决方案](https://www.linuxidc.com/Linux/2014-10/108238.htm)是
* ls //找到当前有哪些磁盘，结果类似(hd0,msdos0)...
* cat (hd0.msdos0) //或者ls (hd0,msdos0),依次查看，哪个是ubuntu的启动盘
* linux /boot/vmlinuz* ro root=/dev/sda1 //*为内核版本号，可使用tab补全
* initrd /initrd.img
* boot
成功启动，如果系统可以正常运行，执行
* sudo update-grub
* sudo grub-install /dev/sda
恢复。

我们这里ubuntu系统仍然没有恢复。

3、依据网上的方案，制作同版本14.04的启动盘，设置从U盘启动，选择try ubuntu，然后挂载崩溃系统的文件系统，除了/home目录外，使用cp命令将u盘中根文件系统的内容复制到崩溃系统的中。重新启动系统。此时恢复了命令行模式的系统登录。但是图形界面工作不正常，输入用户名和密码后，崩溃重新进入到登录界面。

4、网上需要重新安装GPU驱动，但是重新安装后仍然没有恢复，由于现在并不影响使用，暂时不进行进一步的修复。
存放几个链接在这里
https://www.jianshu.com/p/34236a9c4a2f
https://blog.csdn.net/u014682691/article/details/80605201
https://blog.csdn.net/liuyan20062010/article/details/78582940
http://www.mamicode.com/info-detail-1434964.html


