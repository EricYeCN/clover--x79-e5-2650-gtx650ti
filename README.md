# clover--x79-e5-2650-gtx650ti（安装macOS-High-Sierra-10.13.2-(17C88)）

主板朗宁X79-e5-2650-gtx650ti（安装macOS-High-Sierra-10.13.2-(17C88)）

# 黑苹果 四叶草 for 朗宁 X79 

压缩包里有两个文件夹，台式机启动的EFI（只有config.list）；U盘安装用的EFI。

安装盘用黑果小兵的，链接：https://blog.daliansky.net/macOS-High-Sierra-10.13.2-(17C88)-official-version-and-Clover-4333-original-image.html

我的邮箱是：ye_bin@sina.com大家可以一起交流


# 硬件详情

主板: 朗宁  X79 V2.46 ATX

CPU：E5-2650 V1 

显卡：GTX650TI

内存：16GB DDR3 1333

声卡：ALC892

网卡：Rtl8168/8111/8112


# macOS兼容性:

10.10 Yosemite: 未测试.

10.11 El Capitan: 未测试.

10.12 macOS Sierra: 未测试.

10.13.4 macOS High Sierra: 良好.

10.14.5 macOS Mojave: 安装到启动三次进入系统之前，提示“找不到安装资源

10.15 beta macOS Catalina: 未测试..



#  安装黑苹果全过程(我的PC是win10+macOS10.13.2)

我的PC三年前已安装macOS10.10.5和windows双系统当时某宝花费100+RMB，目的是可以用上FCPX进行视频编辑，可是随着FCPX升级10.10.5已经不支持最新版的软件了。新年，举国stay home的时候决定安装新版的macOS。<br>

找到了黑果小兵的部落阁https://blog.daliansky.net
内容比较全有最新的原版镜像。有各种安装帮助文档。<br>
## 先看看 黑苹果支持的显卡列表https://blog.daliansky.net/Mojave-Hardware-Support-List.html
<br>我的显卡是GTX650TI,列表中有显示有可能花屏或闪屏，有安装10.10.5的成功经验，我想我可以试试。

##  再看看  

Hackintosh黑苹果长期维护机型整理清单 https://blog.daliansky.net/Hackintosh-long-term-maintenance-model-checklist.html

找到适合（或接近）自已PC的EFI，下载备用。<br>
一个8G以上的U盘;还要用一个U盘PE启动盘。
DiskGenius(分区工具)；http://www.diskgenius.cn/download.php<br>
MacOS镜像写入工具balenaEtcher-Portable https://mac.softpedia.com/get/Utilities/Etcher.shtml<br>
EasyUEF(系统引导编辑工具) http://www.ddooo.com/softdown/134088.htm<br>

## 下载MacOS镜像
macOS 10.13.2 https://blog.daliansky.net/macOS-High-Sierra-10.13.2-(17C88)-official-version-and-Clover-4333-original-image.html<br>
### 此处我下载了各种版本，10.15.X,10.14.X，10.13.6这些我的PC都安装不成功，只有10.13.2成功。

用balenaEtcher-Portable刻录到U盘，注意执行balenaEtcher-Portable要用鼠标右键管理员模式<br>

用U盘PE启动盘启动，先用ghost备份win10到机械硬盘，再用其中的DiskGenius进行分区（***分区有风险 ）* ，我的240G固态按分为500m EFI,200m MRB，120G ntfs，将备份的ghost文件恢复到120G分区,剩下的空间需要在win10中我的电脑 ，右键，管理，磁盘管理 ，进行分区，新建简单卷，不给盘符，不格式化为RAW格式。<br>

启动win10，插入写好MacOS镜像的U盘，删除U盘的 EFI分区中clover目录中的内容， 将下载好的clover目录中的内容复制到U盘对应位置<br>


### 进入BIOS <BR>

关闭串口 (Serial Port)

禁用 USB ECHI

开启 USB XHCI

禁用 intel虚拟技术

硬盘模式设置为AHCI，关闭Secure Boot，关闭intel虚拟技术,UEFI Boot设置为 Enabled,在BOOT菜单中选择UEFI:+U盘名称， 启动。<BR>
选中 Boot macOS Install from macOS Hight Sierra 按空格 ，移到 -v参数按空格选中。这处过程出错最多，大多是显卡无法驱动或BIOS设置错，请自行百度。<br>

### 安装提示安装macOS 应用程序副本已损坏，不能用来安装macOS的解决方法

该错误会经常出现于旧版中，根源是苹果的安装镜像中的证书过期导致的。解决方法如下：
实用工具-终端，输入命令：date 0201010116，回车后关闭终端，可继续安装进程；
安装过程中全程断开网络

### 抹盘时提示"MediaKit报告设备上的空间不足以执行请求的操作"的原因及解决方法

出现该提示最根本的原因就是你之前的磁盘分区中ESP分区的尺寸小于200MB

### 解决方法

Windows下使用diskgenius删除掉MSR分区,将多出来的分区合并到ESP,正好凑成200MB,以满足安装macOS的基本需求.
macOS下可以直接使用磁盘工具进行抹盘,它会自动生成一个200MB的EFI分区,当然前提条件是你需要先备份好磁盘里的数据,否则会造成全盘数据的丢失,请谨慎操作.

### 安装中出现的IOConsoleUsers: time(0) 0->0, lin 0, llk 1, IOConsoleUsers: gIOScreenLockState 3, hs 0, bs 0, nov 0, sm 0x0错误的临时解决方法

最常见的安装过程中出现的一个错误是：<br>
IOConsoleUsers: time(0) 0->0, lin 0, llk 1,<br>
IOConsoleUsers: gIOScreenLockState 3, hs 0, bs 0, nov 0, sm 0x0<br>
***原因是系统 无法识别出你的显卡驱动，临时的解决方法是：<br>

取消勾选Inject Intel<br>
或者将platform-id修改为0x12345678<br>
不知道如何操作的请移步Clover使用教程 https://blog.daliansky.net/clover-user-manual.html <br>
其实就是EFI不匹配你的显卡，找个适合的EFI即可。<br>





# 资助

我花费了一些时间和精力在上面，如果此项目帮助到了您，欢迎来资助我继续完善它。

微信支付后还有个 留言 功能。如果只是在付款时填写“求助”而没有再留言，我是联系不上你的喔，下面单独填写的“手机号”我并不能看得见。我的邮箱是ye_bin@sina.com。

注意：这不是有偿协助，我的时间非常有限，共勉！


![Image text](https://github.com/EricYeCN/clover--x79-e5-2650-gtx650ti/blob/ffbce0f4692d243d1d41212f0413672a216c2d36/temp.jpg)
