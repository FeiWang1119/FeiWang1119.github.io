---
title: “linux command”
collection: notes
type: "command"
permalink: /notes/2022-command-1
venue: "Uniontech. Company"
date: 2022-11-10
location: "WuHan, China"
---

Commands commonly used at work

# 构建依赖
1. sudo apt install devscripts
2. cd 到项目的根目录
3. sudo mk-build-deps --install --tool='apt -o Debug::pkgProblemResolver=yes --no-install-recommends --yes' debian/control

# 构建deb包
dpkg-buildpackage -us -uc -nc

# 安装包依赖
sudo apt build-dep dde-daemon

# Qt  

| 命令                                                        | 说明                                |   
|----------------------------------------------------------- |------------------------------------ |    
|-nograb -platformpluginpath qtbuilddir/plugins              | 指定平台插件                          | 
|LD_LIBRARY_PATH                                             | 设置程序运行时链接库的路径              |
|QT_QPA_PLATFORM_PLUGIN_PATH=qtbuilddir/plugins/platforms    | 平台相关插件                          |
|QT_PLUGIN_PATH=qtbuilddir/plugins                           | Qt插件                               |
|PKG_CONFIG_PATH=qtbuilddir/lib/pkgconfig                    | 查找该目录下的.PC文件,实现头文件和库的引入  |
|libqt5gui5-dbgsym libqt5widgets5-dbgsym libqt5core5a-dbgsym | Qt的调试库包                          |
|LANG=bo_CN LANGUAGE=bo_CN dde-file-manager                  | 藏语                                 |
|qtbase5-examples qt5-doc-html                               | Qt例子和帮助文档包                     |
|qtbase5-dev qt5-default                                     | qt5源码包和默认配置包（qmake找不到qt5）  |
|libqt5waylandclient5-dev qtwayland5-private-dev             | qtwayland的开发包                     |

# 仓库

gerrit http://aptly.uniontech.com/pkg/uos-exprimental/commit/
索引 http://aptly.uniontech.com/pkg/uos-exprimental/commit/dists/unstable/main/binary-amd64/

#  gsetting

|命令                                |说明                                             |
|-----------------------------------|---------------------------------------         |
|glib-compile-schemas               | /usr/share/glib-2.0/schemas                    |
|gsettings list-schemas             | 显示系统已安装的不可重定位的schema  
|gsettings list-relocatable-schemas | 显示已安装的可重定位的schema  
|gsettings list-children SCHEMA     | 显示指定schema的children，SCHEMA指xml  文件中schema的id属性值 |
|gsettings list-keys SCHEMA         | 显示指定schema的所有项(key)                       |
|gsettings range SCHEMA KEY         | 查询指定schema的指定项KEY的有效取值范围             |
|gsettings get SCHEMA KEY           | 显示指定schema的指定项KEY的值                      |
|gsettings set SCHEMA KEY VALUE     | 设置指定schema的指定项KEY的值为VALUE                |
|gsettings reset SCHEMA KEY         | 恢复指定schema的指定项KEY的值为默认值                | 
|gsettings reset-recursively SCHEMA | 恢复指定schema的所有key的值为默认值                  |
|gsettings list-recursively [SCHEMA]| 有SCHEMA参数，则递归显示指定schema的所有项(key)和值(value)，否则递归显示所有schema的|

#  dde-daemon

定位 dde-daemon：sudo pkill -ef /usr/lib/deepin-daemon/dde-system-daemon; sudo DDE_DEBUG_LEVEL=debug DDE_DEBUG_MATCH=account /usr/lib/deepin-daemon/dde-system-daemon 

#  翻译

|命令                  |说明                          |
|---------------------|------------------------------|
|tx pull -s -b m20    | 拉取翻译（-a -f 全部拉取）      |
|tx push -s -b master | 推送翻译                       |

# coredump

1. sudo apt install systemd-coredump 安装
2. sudo apt install dde-control-center-dbgsym 安装控制中心符号调试信息
如果没有进行core dump 的相关设置，默认是不开启的。可以通过ulimit -c查看是否开启。如果输出为0，则没有开启，需要执行ulimit -c unlimited开启core dump功能
3. 配置/etc/profile 中加上 ulimit -c unlimited生成coredump文件
4. 使用coredumpctl list查看崩溃列表 获取崩溃的pid 
5. 复现问题后马上使用coredumpctl dump查看堆栈信息 或者 coredumpctl info + 崩溃pid
6. sudo apt install lz4; lz4 -d FILE 来解压coredump文件

# uos 激活

uos-activator-cmd -s --kms kms.uniontech.com:8900:Vlc1cGIyNTBaV05v

# ssh

ssh-keygen -o

/usr/sbin/sshd -T 查看出错原因

no hostkeys available— exiting：

1. root权限下，重新生成密钥：

ssh-keygen -t dsa -f /etc/ssh/ssh_host_dsa_key
ssh-keygen -t rsa -f /etc/ssh/ssh_host_rsa_key 

2. 修改密钥权限：

chmod 600 /etc/ssh/ssh_host_dsa_key
chmod 600 /etc/ssh/ssh_host_rsa_key

3. 重启ssh

systemctl restart ssh
service ssh restart

# wayland 下复制两次问题

killall dde-clipboardloader 

# CRP跳过单元测试方法：

项目-编辑-构建参数列表
{'i386': 'DEB_BUILD_OPTIONS=nocheck ', 'arm64': 'DEB_BUILD_OPTIONS=nocheck ','amd64': 'DEB_BUILD_OPTIONS=nocheck ', 'mips64el': 'DEB_BUILD_OPTIONS=nocheck ', 'sw_64': 'DEB_BUILD_OPTIONS=nocheck ', 'loongarch64': 'DEB_BUILD_OPTIONS=nocheck '}

crp上ut失败时跳过ut

# Git

|命令                                 |说明                                  |
|------------------------------------|--------------------------------------|
|git push origin <src>:<dst>         | 提交本地分支src到远程分支dst（如果没有dst会创建dst）|
|git push origin --delete develop    | 删除远程分支develop                    |
|git fetch origin develop/snipe:snipe| 从远程分支到本地分支                     |

# 进程

|命令                                                                                      |说明                 |
|-----------------------------------------------------------------------------------------|-------------------|
|tr '\0' '\n' < /proc/12345/environ 或者 ps eww -p 12345                                   | 查看进程环境变量     |  
|pldd 12345 或者 cat /proc/12345/maps \| awk '{print $6}' \| grep '\.so' \| sort \| uniq   | 查看程依赖的so      |
|strings *.so                                                                             | 查看so的字符        |

# dbus

|命令                                                           |说明                             |
|--------------------------------------------------------------|---------------------------------|
|qdbus --session                                               | 查看当前session所有的service信息   |
|qdbus --system                                                | 查看当前system所有的service信息    |
|could not find a Qt installation of ''                        | sudo apt install qtchooser      | 
|qdbus com.deepin.dde.Clipboard /com/deepin/dde/Clipboard      | tab补全                          |
|dbus-monitor --session interface=org.freedesktop.Notifications| 监听dbus服务接口                  |

# xprop 查看窗口属性

# crontab 系统定时工具


WAYLAND_DEBUG=1


1. no source files under CMake project
   Additional generator should be specified to build project tree. I removed it before configuring project.

# 环境变量

|命令                           |说明            |
|------------------------------|----------------|
|XDG_SESSION_TYPE              | x11/wayland    |
|XDG_CURRENT_DESKTOP           | deepin （窗管信息）|
|WAYLAND_DISPLAY               |                |
|KDE_FULL_SESSION              |                 |
|GNOME_DESKTOP_SESSION_ID      |                 |  
|DESKTOP_SESSION | deepin      |                 |
|QT_WAYLAND_SHELL_INTEGRATION  | kwayland-shell   |
