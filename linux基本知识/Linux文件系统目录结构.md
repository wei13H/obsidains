/bin文件包含基本的命令，ls，cp之类的
/sbin包含了系统命令，modprobe ，hwclock，ifconfig等系统命令。
/dev设备文件储存目录，应用程序通过这些控制设备。
/etc
系统配置文件的所在地，一些服务器的配置文件也在这里，如用户账号及密码配置文件。busybox 的启动脚本也存放在该目录。
/lib
系统库文件存放目录，如LDD6410 包含libc-2.6.1.so、libpthread-2.6.1.so、libthread_db-1.0.so 等
/mnt
/mnt 这个目录一般是用于存放挂载储存设备的挂载目录的，比如有cdrom 等目录。可以
参看/etc/fstab 的定义。有时我们可以把让系统开机自动挂载文件系统，把挂载点放在这里也
是可以的。
/opt
opt 是“可选”的意思，有些软件包会被安装在这里，例如，在LDD6410 的文件系统中，
Qt/Embedded 就存放在该目录。
98）
8．/proc
操作系统运行时，进程及内核信息（比如CPU、硬盘分区、内存信息等）存放在这里。/proc
目录为伪文件系统proc 的挂载目录，proc 并不是真正的文件系统，它存在于内存之中。
9．/tmp
有时用户运行程序的时候，会产生临时文件，/tmp 就用来存放临时文件的。
10．/usr
这个是系统存放程序的目录，比如用户命令、用户库等。LDD6410 的usr 包括bin、sbin、lib
三个子目录。usr/bin 中包含diff、which、who、rx、cmp 等，usr/sbin 中包含chroot、flash_eraseall、
inetd 等，usr/lib 中包含libjpeg.so.62.0.0 等。
11．/var
var 表示的是变化的意思，这个目录的内容经常变动，如/var 的/var/log 目录被用来存放系统
日志。
12．/sys
Linux 2.6 内核所支持的sysfs 文件系统被映射在此目录。Linux 设备驱动模型中的总线、驱动
和设备都可以在sysfs 文件系统中找到对应的节点。当内核检测到在系统中出现了新设备后，内核
会在sysfs 文件系统中为该新设备生成一项新的记录。