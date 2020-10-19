# N1-Rom
斐讯 N1 盒子玩法很多，心血来潮，收集一下斐讯 N1 盒子 ROM 固件及遥控器。

斐讯 N1 盒子 ROM 固件收集
webpad 大神官改精简斐讯天天链 N1 官改 v2.2 线刷包
最后更新于 2018-9-22，很大可能以后不再更新。特点是：稳定简单流畅不卡，投屏也好用，功能比较强大，是电视盒子一族的不二选择，固件上安装的 Kodi 能完美读取中英双语特效字幕。只能线刷。

帖子：地址 · 固件备用下载地址（解压密码1024）

相关资料：N1 降级 Webpad 刷小钢炮系统+Docker 安装 OpenWrt 旁路由

附：N1 救砖方法
原文。亲测适用小钢炮刷回 WEBPAD 2.2 官改。

准备工作：

N1机子一台，机子是正常使用install.sh安装armbian到EMMC的，又想恢复成原来的安卓固件，系统崩溃了也没关系
准备好WEBPAD大的2.2线刷包
USB_Burning_Tool 刷机工具
USB 公对公线一条
开始刷机：

先把USB对公线链接到电脑USB口与N1的第二个口（靠HDMI口），N1不要通电
打开USB_Burning_Tool，导入固件WEBPAD大的2.2的线刷包，验证通过后，出现开始字样
勾选擦除FLASH，不要勾选擦除bootloader，USB_Burning_Tool点击开始运行刷机，3秒钟内速度让N1通电。
USB_Burning_Tool开始正常识别N1线刷模式，刷机开始。
烧录完成后，拔电重启，N1恢复了原来的样子，可以正常ADB连接，进入线刷，重新安装ARMBIAN。
荒野无灯 - 小钢炮
荒野无灯小钢炮（NDM）系统官网：http://nanodm.net

下载地址：http://rom.nanodm.net/N1/

固件带 qBittorrent、Transmission、Aria2、Filemanager、Gerbera、Jellyfin 和 Syncthing，还有 Docker……可以折腾 OpenWrt 当旁路由……

更多资料可参考：N1 降级 Webpad 刷小钢炮系统+Docker 安装 OpenWrt 旁路由

Armbian
Armbian 是轻量级的 Debian 系统和为 ARM 开发板专门发行并重新编译的 Debian 系统(Ubuntu 派生自 Debian)。

下载：N1-ARMBIAN-5.77（带 dtb 文件，解压密码 1024）

相关资料：斐讯N1 – 完美刷机Armbian教程

xiangsm - Armbian-5.77 on N1, so far so good

flippy - OpenWRT 支持写入EMMC
flippy - OpenWRT 编译固件口碑还不错，功能比较多。默认IP：192.168.1.1；默认密码：password

注：如果用这个固件做旁路由的话不要忘了加自定义防火墙规则（网络->防火墙->自定义规则）：

iptables -t nat -I POSTROUTING -o eth0 -j MASQUERADE
也可以尝试（有桥接存在的情况下）

iptables -t nat -I POSTROUTING -o  br-lan  -j MASQUERADE 
原贴：地址；

固件备用下载地址
（解压密码 1024，若看不到下载链接，请关闭广告屏蔽插件刷新重试）

（2020-09-18）

（2020-06-13）

点击查看更多旧版▼展开

flippy - OpenWRT Docker 版
地址：unifreq/openwrt-aarch64

docker pull unifreq/openwrt-aarch64:r20.05.20  ##2020.06.13更新
docker pull unifreq/openwrt-aarch64:r20.04.08
docker pull unifreq/openwrt-aarch64:r9.12.03
docker pull unifreq/openwrt-aarch64:r9.10.24
或者可以下载镜像文件，离线导入。

2019.11.05更新：unifreq-openwrt-aarch64-r9.10.24

2019.12.06更新：unifreq-openwrt-aarch64-r9.12.03

2020.04.14更新：unifreq-openwrt-aarch64-r20.04.08

2020.06.13更新：unifreq/openwrt-aarch64:r20.05.20

Docker 镜像解压，得到 unifreq-openwrt-aarch64-r9.10.24.tar 这样的文件，上传到 N1 目录，比如 /tmp，然后 docker load 导入即可。

cd /tmp
docker load < unifreq-openwrt-aarch64-r9.10.24.tar
附：Docker 镜像导出方法

查看本地镜像

docker images 
导出本地镜像

docker save -o  unifreq-openwrt-aarch64-r9.10.24.tar unifreq/openwrt-aarch64:r9.10.24
gd772 - OpenWRT 支持写入 EMMC
帖子：https://www.right.com.cn/forum/thread-3160780-1-1.html

固件基于 lean大雕的 源码 编译。感谢 大雕、Lienol。同时也要感谢 flippy 大神提供的 自助打包脚本 及 Armbia 镜像。

OpenWrt 默认后台管理地址：192.168.123.2 默认用户名：root 密码：password

文件浏览器默认用户名及密码：admin；qBittorrent Web 用户界面默认用户名：admin 密码：adminadmin

如想摆脱U盘，将 Openwrt 写入N1盒子里的 EMMC 请按以下操作！

登陆 OpenWrt 管理后台，依次来到 系统---TTYD终端 看到 OpenWrt login: 输入 root 敲回车 Password: 输入 password 敲回车

看到 root@OpenWrt:~# 输入执行写入EMMC脚本命令：./inst-to-emmc.sh 敲回车 脚本运行后会有个 y/n 确认写入EMMC的提示，输入 y 后 敲回车

待脚本跑完 出现 "All done, please reboot!" 字样提示 即可 关机，拔电，拔出U盘，再接上电源即可从EMMC启动 Openwrt

升级至新版且写入到EMMC，方法：下载新版本固件，把新版固件写入U盘里，从U盘启动，登录管理后台，系统--TTYD终端 执行 ./update-to-emmc.sh 即可在「保留原有的设置情况下」完成版本升级！

gd772 - OpenWRT 固件备用下载
（解压密码 1024，若看不到下载链接，请关闭广告屏蔽插件刷新重试）

（2020-09-20）

（2020-06-17）

（2020-06-17）

（2020-05-13）

（2020-05-13）

bobotoy-OpenWRT-Docker 版本
项目地址：Github、Docker

目前最新版本：r20.04.08

docker pull unifreq/openwrt-aarch64:r20.04.08
可以直接 pull 或者离线下载导入使用。

备用离线下载：docker-img-openwrt-aarch64-0419（解压密码 1024）

食用方法：

①.将 docker-img-openwrt-aarch64-0317.gz 文件上传至 N1 /root 目录

②.导入软路由 docker 包：

gzip -dc docker-img-openwrt-aarch64-0317.gz | docker load
或者

docker pull bobotoy/openwrt-aarch64:latest
（推荐跳过②①直接拉取使用）

③运行容器：

docker run -d --device=/dev/snd:/dev/snd --restart always --network macnet --ip 192.168.2.1 --privileged bobotoy/openwrt-aarch64:latest /sbin/init
斐讯盒子 N1_YYFROM 讯飞语音实用版
线刷，最新版本为 20190421，官方说此固件专为有T1原厂遥控器用户而定制，移植讯飞语音功能。

帖子：地址 · 固件备用下载地址（解压密码1024）

相关教程：YYF 语音版部署 optware 和 samba - N1 化身电视盒子与 NAS 服务器

Lilith 官改固件
特点：官改，大而全。

帖子：地址 · 固件备用下载地址-分卷1 · 固件备用下载地址-分卷2（解压密码1024）

斐讯 N1 盒子 Volumio 数播系统
Volumio OS本质上是一个高度定制的Linux系统，它支持树莓派、任何X86电脑以及比较流行的其它几款ARM迷你电脑。它没有图形界面，播放和系统控制是通过WEB界面实现的，Andorid和iOS上也有相应的APP客户端可用，并且易于安装和设置，支持简体中文语言和显示。

帖子：地址

固件：备用下载地址（解压密码 1024）

CoreELEC
20191015 更新，N1 适配的 CoreELEC-9.2 最终版本。

帖子：地址 · 固件备用下载地址（解压密码1024）

FastNas Home Media Center OS + OpenMediaVault 一键安装包
FastNas Home Media Center OS 基于 Armbian Debian 5.77+OMV，OMV（OpenMediaVault）本身也是一个集合了多媒体功能的NAS系统。

帖子：地址

EmuELEC/Sx05RE 游戏整合镜像
EmuELEC 原(Sx05RE)，一个游戏模拟系统，古老的回忆，80/90后可能都有深刻印象，当然可能95后已经不喜欢这些古董了！

最新版应该是：[N1盒子] [2020-01-21]斐讯N1用EmuELEC最强整合包-2020春节整合版 ，不只能刷N1，其他 S905 芯片也大部分都能刷。（文件太大了，在度娘网盘，下载速度太慢，没有搬下来备份）

EmuELEC_3.2_PHICOMM_N1

相关资料：

2GU盘人中日月EmuELEC3.4系统，roms管理直拷极简版

精简版本：[N1盒子] 【2020-02-22】N1_EmuELEC3.4 (骨头)2.9GB WIN下游戏直拷

下载地址：N1-EMUELEC3.4(骨头).part1 · N1-EMUELEC3.4(骨头).part2 · N1-EMUELEC3.4(骨头).part3 · N1-EMUELEC3.4(骨头).part4 · N1-EMUELEC3.4(骨头).part5（解压密码 1024）

EmuELEC 原(Sx05RE)N1_2.5.3 繁体中文版：帖子 · 备用下载地址（解压密码 1024）

橙子_MAX OpenWRT 当旁路由
作者博客：https://www.maxlicheng.com/category/openwrt/phicommn1

帖子：L大源码自编译 N1 OpenWRT 支持2.4G和5G无线，顺便给盒子安装个外置天线、eMMC刷入OP系统-N1降级及U盘启动OpenWRT当旁路由设置视频教程

备用下载地址（解压密码 1024）

RUSH 极限精简斐讯 T1/N1 极客开发者 ROM
骨灰精简固件，去除后台：斐讯账号，百度语音/语音后台，斐讯出厂测试，斐讯管家/加速，斐讯手机遥控器；去除全家桶：谷歌服务，谷歌视频；系统开机速度，约15秒；桌面环境：蛮荒桌面永不升级版（6.23），自制精简桌面没别的功能了，谁用谁知道，支持鼠标（6.23，6.24，6.25）冷桌面（6.25）；自带应用：原生设置，斐讯设置，ES管理器，文件管理器……

帖子：地址 · 备用下载地址（解压密码 1024）

斐讯 T1/N1 盒子 轻巧简装版固件
基于YYFROM无语音实用版改进，地址。

固件下载：斐讯N1-Lite-Root-V2.10B（盒子）、斐讯N1-Lite-Root-V2.10（盒子）、斐讯盒子T1_Lite_Root-V3.12C（解压密码 1024）

斐讯 N1 盒子遥控器收集
斐讯原装T1遥控器
蓝牙+语音，几乎完美匹配任何按键，几乎所有系统都能用，配对简单。唯一缺点就是贵。

小米蓝牙遥控器
蓝牙+语音，也比较完美匹配几乎所有按键，几乎所有系统都能用，配对也比较简单，正品做工、体验跟斐讯原装的相比应该只好不差。正品也不便宜。

天猫魔盒/精灵蓝牙遥控器
据说更贵，一般要110+。

2.4G 万能遥控器（空中飞鼠）
还支持 Windows7、8、8.1和10，能遥控大部分电脑播放器，能当鼠标用。缺点是要占用一个USB口插接收器，只支持关机，不支持开机。不贵。

中国移动魔盒蓝牙+语音遥控器
据说咸鱼上最便宜的6元不包邮。配对稍麻烦，需要在遥控器上同时按住【菜单键+返回键】，直接狂闪，再在盒子菜单里找到网络-蓝牙，搜索并连接。

斐讯遥控器 App
手机与盒子在同一个局域网网段内，如果提示未连接，请手动输入IP，功能也比较多，可以截图、当遥控，投屏，尤其是截图功能，很实用，秒杀悟空遥控。免费。

Android：官方地址貌似无法下载了。

iOS：AppStore

鼠标
实用，使用不方便。

参考资料
N1盒子的ROM集合及遥控器讨论

斐讯 N1 折腾记录

斐讯 N1 折腾记录（二）

斐讯N1折腾记录（三）

后记-更新
不得不说 N1 玩法真心多，折腾资料也很多，单臂主路由+无线 AP 也不错。上面提到的帖子网页基本上备份了一份，有需要可以下载看看。（解压密码1024）


from ：https://cyhour.com/1311/
