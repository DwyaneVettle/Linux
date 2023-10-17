# 第一章 Linux系统-Ubuntu的下载和安装

## 1.下载Ubuntu

​	进入https://cn.ubuntu.com/download中文官网下载iso映像文件：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657376.png" alt="image-20220422121923253" style="zoom: 33%;" />



## 2.安装Ubuntu

1.打开虚拟机，点击创建新的虚拟机：

<img src="C:/Users/HP/Desktop/202302171657377.png" alt="image-20220422122549349" style="zoom:50%;" />

2.选择“典型”，然后点击“下一步”：

<img src="C:/Users/HP/Desktop/202302171657378.png" alt="image-20220422122639669" style="zoom: 50%;" />

3.选择“稍后安装操作系统”，然后点击“下一步”：

<img src="C:/Users/HP/Desktop/202302171657379.png" alt="image-20220422122733098" style="zoom:50%;" />

4.选择操作系统位Linux，版本位Ubuntu 64,然后点击下一步：

<img src="C:/Users/HP/Desktop/202302171657380.png" alt="image-20220422122820256" style="zoom:50%;" />

5.自定义虚拟机名称，选择安装虚拟机的路径，点击下一步：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657381.png" alt="image-20220422122927190" style="zoom:50%;" />

6.选择“将虚拟机存储为单个文件”，点击下一步：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657382.png" alt="image-20220422123008796" style="zoom:50%;" />

7.点击完成：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657383.png" alt="image-20220422123035094" style="zoom:50%;" />

8.在“设备”栏。选择“DVD/CD”，将iso文件加载进去：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657384.png" alt="image-20220422123204484" style="zoom:50%;" />

9.点击“开启此虚拟机“，系统将会进行一段时间的自检：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657385.png" alt="image-20220422123427388" style="zoom:50%;" />

10.选择安装语言为中文，点击”安装Ubuntu“：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657386.png" style="zoom:50%;" />

11.语言环境选择好后按Enter或确认，按以下方式默认安装，再按Enter键确认：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657387.png" style="zoom:50%;" />

12.按默认项，点击”现在安装“：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657388.png" style="zoom:50%;" />

13.点击你所在的地区设置时区，然后点击”继续“：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657389.png" style="zoom:50%;" />

14.创建用户后，点击”继续“：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657390.png" style="zoom:50%;" />

15.下载安装需要一点时间，安装完成后需要重启，点击”现在重启“：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657391.png" style="zoom:50%;" />

16.重启登录后跳过导航，进入系统。



## 3.配置软件源

将Ubuntu的软件下载源更改为中国的服务器，提高下载速度。

1.点击左下角菜单栏，点击”软件“： 

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657392.png" style="zoom:50%;" />

2.按下图所示修改：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657393.png" style="zoom:50%;" />

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657394.png" style="zoom:50%;" />

3.点击关闭后，再重新载入：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657395.png" style="zoom:50%;" />



4.进入终端界面：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657396.png" alt="image-20220923222630469" style="zoom:50%;" />

更新软件源：

```shell
sudo apt-get update       			# 系统更新
sudo apt-get upgrade				# 系统软件升级
```





## 4.拓展

以下命令可以实现Windows系统和Ubuntu系统之间跨系统复制粘贴,**通过安装VMtools实现了Windows与Ubuntu跨系统复制粘贴，也实现了Ubuntu窗口自适应**：

```shell
sudo apt-get autoremove open-vm-tools  # 检测删除
sudo apt-get install open-vm-tools     # 安装
sudo apt-get install open-vm-tools-desktop  # 安装桌面版
```





## 5.远程连接

1.在系统中我们可以使用超级管理员来登录系统，因为他具有Linux系统中的最高权限，具体操作需要先设置root的密码：

```shell
sudo passwd root							# 为root设置密码
# 连续输入两次roo的密码
su root										# 切换root登录
```

2.安装ssh服务，只有安装了这个服务才能进行远程连接

```shell
apt install openssh-server					# 安装ssh服务
service ssh start 							# 启动服务
```

3.在系统终端中输入命令查看IP地址：

```shell
ifconfig
# 如果没有该命令，输入以下命令下载
apt install net-tools
```

4.打开远程连接工具MobaXterm，点击Session-->SSH-->输入如下：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657397.png" alt="image-20220428153100158" style="zoom:50%;" />

5.点击OK，输入密码进行连接。



**如果连接被拒绝按以下步骤操作：**

1.下载net-tools：

```shell
sudo apt-get install net-tools
```

2.下载vim编辑器：

```shell
sudo apt-get install vim
```

3.编辑/etc/ssh/sshd_config

```shell
vim /etc/ssh/sshd_config
或
gedit /etc/ssh/sshd_config
在#PermitRootLogin prohibit-password下面新增PermitRootLogin yes
```

4.重启ssh：

```shell
service sshd restart
```

如以上操作还是显示连接超时，可以尝试以下方法：

1. 重启宿主机的VMnet8的网卡；
2. 使用命令`service ufw stop/disable`关闭/禁用防火墙；
3. 编辑`/etc/ssh/sshd_config`文件，将端口修改为60022，并再次使用Mobaxterm连接（端口也改为60022）；
4. 直接在虚拟机的编辑--虚拟网络编辑器中还原默认配置。
5. 看看虚拟机左上角的网络是否连接。
6. 如显示网络连接未托管，可参考https://blog.csdn.net/forever_008/article/details/114011292?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522169578481916800186537516%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=169578481916800186537516&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduend~default-2-114011292-null-null.142^v94^insert_down28v1&utm_term=ubuntu20.04%E7%BD%91%E7%BB%9C%E6%9C%89%E7%BA%BF%E6%9C%AA%E6%89%98%E7%AE%A1&spm=1018.2226.3001.4187

**设置永久IP地址的方法：**

1.备份网络配置文件：

```shell
cp /etc/netplan/01-network-manager-all.yaml /etc/netplan/01-network-manager-all.yaml.bak
```

2.编辑配置文件：

原配置如下:

```shell
# Let NetworkManager manage all devices on this system
network:
  version: 2
  renderer: NetworkManager
```

修改配置为：

```shell
network:
    version: 2
    ethernets:
        ens33:
            dhcp4: false
            addresses: [192.168.18.128/24]
            gateway4: 192.168.18.1
            nameservers:
                    addresses: [223.5.5.5,223.6.6.6]
```

3.按ESC->:wq保存文件后输入以下命令使文件生效：

```shell
sudo netplan apply
```

4.重启网络：

```shell
service NetworkManager restart
```





## 6.关于安装界面太小的问题

**注：ubuntu的安装页面太小，看不到下面的确认键，我们可以点击右上角的红×，然后在倒三角中点击设置，在显示器功能栏选择分辨率设置成1024x768，然后再点击左上角的红色按钮安装**

![](https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657398.png)



## 7.初始登录常用命令-解决远程登录被拒绝的问题

```shell
# 确定防火墙状态是否关闭
service status ufw
# 禁用防火墙
service stop ufw
service disable ufw

sudo ps -e |grep ssh        #查看是否安装了SSH服务(如果显示为空则没安装)

sudo apt-get update        #先更新下资源列表

sudo apt-get install openssh-server      #安装openssh-server

sudo ps -e |grep ssh                            #查看是否安装成功

sudo service sshd start                         #重新启动SSH服务  (或者用命令 sudo systemctl restart sshd)

```

```shell
sudo apt install vim           # 下载vim编辑器
sudo vi /etc/ssh/sshd_config
把PermitRootLogin prohibit-password 注释掉

增加一行 PermitRootLogin yes 
```



<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202302171657400.png" alt="image-20220923230426216" style="zoom:50%;" />

```shell
service sshd restart  # 重启  
```

