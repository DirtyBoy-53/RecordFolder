1、 首先创建一个打包程序的文件夹，`mkdir dpkg_deb` ，进入该文件夹`cd dpkg_deb`

2、创建一个存储程序包的文件夹`mkdir myscript`，再创建一个自动打包的脚本`touch MakeScript.sh`，并赋予可执行权限`sudo chmod 777 MakeScript.sh`，将下面的程序粘贴至MakeScript.sh中。

```sh
#!/bin/bash
clear
function cecho {
	echo -e "\033[$1m$2\033[0m"
	#fonts color: 31-red;32-green;36-deepgreen;34-blue;
}
[ -d ~/myscript ] || sudo mkdir ~/myscript
###########################选择菜单##################################
function menu {
	read -p "请输⼊即将要制作的包名：" softname
	read -p "请输⼊即将要制作的包的版本：" version
cat <<EOF
*************************************************************
1) mips64el platform
2) amd64 platform
3) i386 platform
4) arm64 platform
5) exit
*************************************************************
EOF
read -p "请选择你要制作什么平台的安装包：" platform
case $platform in
1)
platform=mips64el;;
2)
platform=amd64;;
3)
platform=i386;;
4)
platform=arm64;;
5)
cecho 32 Byebye
exit;;
*)
cecho 31 "选择有误，程序将退出，请重新选择！"
exit;;
esac
cat <<EOF
***********************************************************
1) 安装在/opt/nvidia/LaserFusion/下
2）安装在/home/nvidia/LaserFusion/下
3）⾃定义
4）exit
EOF
read -p "你希望此安装包安装在哪⾥：" choice
case $choice in
1)
sudo mkdir -p $softname/opt/nvidia/LaserFusion
softpath=$softname/opt/nvidia/LaserFusion/;;
2)
sudo mkdir -p $softname/home/nvidia/LaserFusion
softpath=$softname/home/nvidia/LaserFusion/;;
3)
read -p "请⼿动输入你想要安装的目录" wheredir
softpath=$softname/$wheredir;;
4)
cecho 32 Byebye
exit;;
*)
cecho 31 "选择有误，程序将退出，请重新选择！"
exit;;
esac
}
###################################编写control⽂件#####################################
function make-control {
sudo mkdir -p $softname/DEBIAN
sudo touch $softname/DEBIAN/{control,postinst,preinst,postrm,prerm}
sudo chmod -R 0775 $softname/DEBIAN/{postinst,preinst,postrm,prerm}
sudo cat >$softname/DEBIAN/control<<EOF
Package: $softname
Source: Unknown
Version: $version
Architecture: $platform
Maintainer: Unknown
Installed-Size: Unknown
Depends: Unknown
Recommends: Unknown
Suggests: Unknown
Conflicts: Unknown
Breaks: Unknown
Replaces: Unknown
Provides: Unknown
Section: Unknown
#Priority: Unknown
#Multi-Arch: Unknown
Homepage: Unknown
Description: -_-=

EOF
}
####################################主程序编包#########################################
function make-soft {
	sudo mkdir -p $softpath
	sudo cp -rf myscript/* $softpath
	sudo [ -d build ] || sudo mkdir build
	sudo dpkg -b $softname build
	cecho 32 正在制作$softname"_"$version"_"$platform.deb...... && sleep 3
	[ $? -eq 0 ] && cecho 32 安装包制作完成，已放在当前build⽬录下，请查看！|| cecho 31 "安装包制作失败，请从新运⾏程序！"
	rm -rf $softname
}
cecho
menu
make-control
make-soft

```

3、把需要打包的文件放到myscript中

[![xm3Ibt.png](https://s1.ax1x.com/2022/09/28/xm3Ibt.png)](https://imgse.com/i/xm3Ibt)

4、执行脚本`sudo ./MakeScript.sh`

[![xm35DI.png](https://s1.ax1x.com/2022/09/28/xm35DI.png)](https://imgse.com/i/xm35DI)

5、根据提示录入信息

注意：

- 填写程序名称时，不要出现main字符

- 填写版本号时，一定要使用数字开头，建议按照图中的格式填写
- 制作的平台根据需求自行判断，选择对应的序号即可
- 选择安装路径建议选择第2项

[![xmGnyj.png](https://s1.ax1x.com/2022/09/28/xmGnyj.png)](https://imgse.com/i/xmGnyj)

6、软件打包完成后，会在MakeScript.sh相同目录下创建一个build文件夹存放打包好的文件。
[![xm34KA.png](https://s1.ax1x.com/2022/09/28/xm34KA.png)](https://imgse.com/i/xm34KA)