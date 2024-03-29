# Linux简介

​	总所周知，计算机系统包含硬件和软件两部分。硬件部分被称为裸机，主要包括中央处理器（CPU）、内存、外存和各种外部设备。软件部分主要包括系统软件和应用软件两部分。系统软件包括操作系统、汇编语言、编译程序、数据库管理系统等软件。应用软件是为多种应用而编制的程序，例如办公自动化软件、财务管理软件、杀毒软件、即时通讯软件等。计算机系统必须先配置好系统软件，才能安装应用软件，应用软件也只有在系统软件的支持下才能为用户提供服务。计算机系统结构如图：

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308041652688.png" alt="计算机系统" style="zoom:50%;" />

​	在所有的系统软件中，操作系统是配置在计算机硬件上的第一层软件，是用户或应用程序与计算机硬件之间的接口。在日常的计算机使用中，操作系统有：Windows、Linux、Android等。



## 1.什么是Linux

​	Linux的发展和UNIX系统、Minix系统、Internet、GNU计划密不可分。它们对Linux产生和发展都有着深远的影响，为Linux成长奠定了坚实的基础。

### 1.1.UNIX系统

​	**Linux是一个类UNIX系统。**它们的涉及有很多相似之处。早在20世纪70年代UNIX系统就已产生，1971年，UNIX操作系统诞生于AT&T公司的贝尔实验室UNIX是一个多用户、多任务的分时操作系统，它的出现源于贝尔实验室的两位软件工程师肯.汤普森和丹尼斯.里奇。UNIX的产生与美国国防计划署的MULTICS项目密切相关。

<img src="https://gitee.com/zou_tangrui/note-pic/raw/master/img/202308041706808.jpeg" alt="c349bdf7836343aeddcc8c87711a0d9b" style="zoom: 50%;" />

​		1964年，由贝尔实验室、麻省理工学院和美国通用电气公司共同开发MULTICS系统，这是一套安装在大型主机上的多用户、多任务的分时操作系统。但是MULTICS项目的工作进度过于缓慢，通用电气公司首先退出计划。1969年，贝尔实验室也推出了。当时，肯.汤普森为MULTICS项目撰写了一个称为《星际旅行》(Star Travel)的游戏程序。贝尔实验室退出MULTICS项目后，肯.汤普森开始利用闲置的PDP-7计算机开发了一种多用户、多任务操作系统，目的是为了能够运行《星际旅行》(Star Travel)游戏，很快，丹尼斯.里奇也加入了这个项目，在他们共同努力下诞生了最早的UNIX操作系统。早期的UNIX是用汇编语言编写的，1972年，丹尼斯.里奇设计了C语言并重构了UNIX操作系统。通过此次重新编写，UNIX得以移植到更为强大的DEC PDP-11/45与PDP-11/70计算机上运行。UNIX内核短小精悍，只有两万行代码，但性能优异，且源码公开。在20世纪70年代UNIX系统是免费的，因此，它的应用范围迅速向实验室外扩展，遍布各科研院所和高校。为了表彰丹尼斯.里奇和肯.汤普森的功绩，1983年他们一同被授予计算机界的最高奖项---图灵奖。



### 1.2.Minix

​	随着UNIX系统的广泛应用，它逐渐由一个免费软件变成一个商用软件，因此需要花费高昂的源码许可证费用才能获得UNIX的源代码，并且UNIX对硬件性能的要求也较高，这些都限制了UNIX系统在教学科研领域的应用。1987年荷兰人Andrew S. Tanenbaum教授利用业余时间开发设计了一个微型的UNIX操作系统---Minix。Minix系统的名称取自英语Mini UNIX，全部程序共12000行代码，约300MB，十分精巧，且它对硬件要求不高，可以运行在廉价的PC上。Linux系统就是在Minix系统的基础上开发的。



### 1.3.Internet

​	20世纪80年代中期，Internet形成，通过Internet，全球的计算机通过网络连接在一起，所有用户都可以通过Internet相互交流和获取信息。Linux是网络时代的产物，无数的程序员通过Internet参与了Linux的技术改进和测试工作，这样Linux在来自世界各地的人们的共同协作下，通过Internet发展起来，可以说，没有Internet就没有今天生命力如此强大、不断发展的Linux操作系统。



### 1.4.GUN计划

​	20世纪80年代，自由软件运动兴起。自由软件（Free Software）是一种可以不受限制的自由使用、赋值、研究、修改和分发的软件。

​	1983年，自由软件运动的领导者理查德.斯托曼提供GNU计划。GNU是GNU is Not UNIX的递归缩写，是自由软件基金会的一个项目，该项目的目标是开发一个自由的类UNIX操作系统，包括内核、软件开发工具和各种应用程序。为了保证GNU计划的软件能够被广泛共享，斯托曼又为GNU计划设计了通用软件许可证GPL（General Public License）。此类软件的开发不是为了经济目的，二十为了不断开发并传播新的软件，并让每个人都能获得和拥有。GPL允许团建作者拥有软件版权，但授予其他任何人以合法复制、发行和修改软件的权力。GPL也是一个针对免费发布软件的具体的发布条款。对于遵照GPL发布的软件，用户可以免费得到软件的源代码和永久使用权，可以任意修改和复制，同时也有义务公开修改后的代码。

​	到1991年Linux内核发布时，GNU几乎完成了除了系统内核之外得各种必备软件的开发，其中大部分是按GPL发布的。虽然Linux内核并不是GNU计划的一部分，但是它已经融入GNU计划，并服务于GNU计划，称为GNU/Linux的操作系统。



## 2.Linux的诞生

​	Linux起源于芬兰赫尔辛基大学计算机系学生Linus Torvalds的个人爱好，因为他所用的教材正是Minix创始人安德鲁.塔能巴鲁教授所编著的《操作系统---设计与实现》，为了方便学习，Linus购买了装有Minix操作系统的PC机，但是安德鲁.塔能巴鲁教授为了教学简明扼要，他不允许别人在Minix上添加其他模块。由于Linus对Minix的功能并不满意，在UNIX和Minix的启发下开始编写一个新的操作系统。Linus在1991年10月5日在赫尔辛基大学的FTP上发布了Linux系统的第一个版本，版本号为0.02，并给它起名Freax（Free免费+Freak怪诞+X的组合），后来在赫尔辛基大学FTP服务器管理员的建议下改为Linux，以为Linus的Minix。

### 2.1.Linux系统的组成

​	Linux操作系统由内核、Shell、文件系统、应用程序等组成：

- **内核：**不同发行版本的Linux系统使用的系统内核只有一个版本，即Linux内核。内核由Linus和它的内核团队负责维护和发布。Linux内核时Linux的核心，是运行程序和管理硬件设备（如磁盘、打印机等）的核心程序，他是提供硬件抽象层、磁盘及文件系统控制、多任务等功能的系统软件。
- **Shell：**它是Linux系统的用户界面，是用户与内核进行交互操作的一种接口，Shell负责接收、解释和执行用户的命令，一个Shell即是一个命令集合。
- **文件系统：**它是文件存放在磁盘等设备上的组织方法。Linux支持多种文件系统，如EXT2、EXT3、EXT4、FAT、ISO9660、NFS等。
- **应用程序：**一套Linux系统的应用程序集，包括办公工具、数据库、文本编辑器等，它可以根据用户的需求进行扩展。

### 2.2.Linux的版本

​	Linux具有发行版和内核版，内核版由Linus及其团队维护，发行版由Linux各个发行组织、公司或个人发行。



#### 2.2.1.Linux内核版本

​	截至到2023年8月13日，Linux的内核版本已更新到6.5.x，其内核版本可参考官方网站 https://kernel.org/

内核源代码可以通过github上查看：https://github.com/torvalds/linux 。

​	内核版本号由3部分组成，即“主版本号+次版本号+修订序列号”，主版本号不同的内核有很大的功能差异，次版本号为偶数表示稳定版本，奇数表示测试版本，有可能存在错误，修订序列号数字越大表示功能越强，且错误越少。



#### 2.2.2.Linux的发行版本

​	Linux的发行版是由一个组织、公司或个人发行，它基于Linux内核，搭配了各种人机界面、应用软件和服务软件。Linux发行版本主要包括以下几种：

- **Fedora Project：**Fedora Linux (第七版以前为Fedora Core)是众多Linux发行版之一，它是一套从 Red Hat Linux发展出来的免费Linux系统，可运行的体系结构包括 x86 (即 i386-i686), x86_64和PowerPC。 Fedora 由Fedora Project 社群开发，这个社区的成员以自己的不懈努力，提供并维护自由、开放源码的软件和开放的标准。Fedora 项目由 Fedora 基金会管理和控制，得到了Red Hat的大力支持。它是一个开放、创新和具有前瞻性的Linux操作系统和平台，允许任何人自由地使用、修改和重发布，无论现在还是将来。

  Fedora Project主页: http://fedoraproject.org/

- **Debian：**Debian Project诞生于1993年8月13日，它的目标是提供一个稳定容错的Linux版本。支持Debian 的不是某家公司，而是许多在其改进过程中投入了大量时间的开发人员，这种改进吸取了早期Linux的经验。Debian 以其稳定性著称，虽然它的早期版木Slink有一些问题，但是它的现有版本Potato已经相当稳定了。

  Debian的安装完全是基于文本的，对于其本身来说这不是一件坏事，但对于初级用户来说却并非这样。因为它仅仅使用 fdisk 作为分区工具而没有自动分区功能，所以它的础盘分区过程令人十分讨厌。磁盘设置完毕后，软件工具包的选择通过一个名为 dselect 的工具实现，但它不向用户提供安装基本工具组 (如开发工具) 的简易设置步骤。最后需要使用 anXious 工具配置 X Windows, 这个过程与其他版本的 X Windows 配置过程类似。完成这些配置后，Debian就可以使用了。

  Debian主要通过基于 Web 的论坛和邮件列表来提供技术支持。作为[服务器](https://cloud.tencent.com/product/cvm?from_column=20065&from=20065)平台，Debian提供一个稳定的环境。为了保证它的稳定性，开发者不会在其中随意添加新技术，而是通过多次测试之后才选定合适的技术加入。

  Debian主页：http://www.debian.org

- **Ubuntu：**Ubuntu是一个以桌面应用为主的 Linux 操作系统，其名称来自非洲南部祖鲁语或豪萨语的“ubuntu” 一词 (多译为乌班图)，意思是“人性”“我的存在是因为大家的存在”，是非洲传统的一种价值观， 类似华人社会的“仁爱”思想。Ubuntu 基于Debian发行版和GNOME桌面环境，与Debian 的不同在于它每6个月会发布一个新版本。

  Ubuntu的目标在于为一般用户提供一个最新的、同时又相当稳定的，主要由自由软件构建而成的操作系统。Ubuntu 具有庞大的社区力量，用户可以方便地从社区获得帮助。随着云计算的流行，Ubuntu推出了一个云计算环境搭建的解决方案，可以在其官方网站找到相关信息。

  Ubuntu主页: http://www.ubuntu.org

-  **SuSE：**总部设在德国的SuSE一直致力于创建一个连接[数据库](https://cloud.tencent.com/solution/database?from_column=20065&from=20065)的最佳Linux版本。为了实现这一目的，SuSE与Oracle 和 IBM 合作，以使他们的产品能稳定地工作。SuSE 还开发了SuSE Linux eMail Server III ,一个非常稳定的电子邮件群组应用。

  基于2.4.10内核的 SuSE 7.3,在原有版本的基础上提高了易用性。安装过程通过GUI完成，磁盘分区过程也非常简单，但它没有为用户提供更多的控制和选择。

  在 SuSE 操作系统下，可以非常方便地访问 Windows 磁盘，这使得两种平台之间的切换，以及使用双系统启动变得更容易。SuSE 的硬件检测非常优秀，该版本在服务器和工作站上都用得很好。

  SuSE 拥有界面友好的安装过程，还有图形管理工具，可方便地访问 Windows 磁盘，对于终端用户和管理员来说使用它同样方便，这使它成为了一个强大的服务器平台。

  SuSE 主页: http://www.suse .com

- **CentOS：**CentOS (Community ENTerprise Operating System)是知名的Linux发行版之一，它是来自于 Red Hat Enterprise Linux依照开放源代码规定释出的源代码所编译而成。由于出自同样的源代码，因此有些要求高度稳定性的服务器以 CentOS 替代商业版的 Red Hat Enterprise Linux使用。

  两者的不同在于，CentOS 并不包含封闭源代码软件，CentOS 是一个基于Red Hat Linux提供的可自由使用源代码的企业级Linux发行版本。每个版本的 CentOS 都会获得10年的支持(通过安全更新方式)。新版本的 CentOS 大约每两年发行一次，而每个版本的 CentOS 会定期(大概每6个月)更新一次，以便支持新的硬件。这样可以建立一个安全、低维护、稳定、高预测性、高重复性的Linux环境。

  CentOS 在Red Hat Enterprise Linux 的基础上修正了不少已知的bug,相对于其他Linux发行版，其稳定性值得信赖。

  CentOS主页: http://www.centos.org

- **Red Hat Linux：**Red Hat起源于1994年，可能是全世界最著名的Linux版本了，Red Hat Linux已经创造了自己的品牌，许许多多重要的服务器都在运行Red Hat Linux。

  Red Hat有两大Linux产品系列，一种就是前面介绍的免费的Fedora Core系列，主要用于桌面版本，其中提供了较多新特性的支持。另外一个产品是收费的 Enterprise 系列。

  Red Hat Linux是公共环境中表现上佳的服务器版本。它拥有自己的公司，用户可以免费使用，但付费后能够享受一套完整的服务，这使得它特别适合在公共网络中使用。这个版本的 Linux 也使用最新的内核，还拥有大多数人都需要使用的主体软件包。

  Red Hat Linux 的安装过程也十分简单明了。它的图形安装过程提供简易设置服务器的全部信息。磁盘分区过程可以自动完成，还可以选择GUI工具完成，即使对于Linux新手来说这些都非常简单。选择软件包的过程也与其他版本类似，用户可以选择软件包种类或特殊的软件包。系统运行起来后，用户可以从Web站点和Red Hat那里得到充分的技术支持。

  Red Hat是一个符合大众需求的最优版本。在服务器和桌面系统中它都工作得很好。Red Hat 的唯一缺陷是带有一 些不标准的内核补丁，这使得它难以按用户的需求进行定制。

  Red Hat主页: http://ww.redhat.com

- **红旗Linux：**红旗 Linux 是由北京中科红旗软件技术有限公司开发的一系列 Linux 发行版，包括桌面版、工作站版、数据中心服务器版、HA集群版和红旗嵌入式Linux等产品。红旗 Linux 是中国较大、较成熟的 Linux 发行版之一，连续多年在国产操作系统中排名第一。

  红旗 Linux是中国操作系统的一面旗帜，在维护国家信息安全等方面做出了重要贡献。20世纪80年代末，个人电脑开始进入中国。当时包括政府部门的在内的所有个人电脑儿乎全部是安装的微软的操作系统。1992 年海湾战争和1999年北约入侵南斯拉夫联盟科索沃地区时，成功运用信息战瘫痪了对方几乎所有通信系统。这使得政府和社会逐渐意识到拥有自己独立的计算机操作系统及相应的软件的重要性。于是中国科学院软件研究所奉命研制基于自由软件 Linux 的自主操作系统，并于1999年8月发布了红旗Linux 1.0版，最初主要用于关系国家安全的重要政府部门。

  随着发展壮大，Linux 进入关键行业的计算环境，用户对系统的要求也越来越严格。为了满足这种不断增长的要求，红旗软件对服务器操作系统产品线进行了全新的优化，推出了红旗 Linux 服务器系列产品。该产品包含了众多的研发成果，进一步体现了红旗服务器操作系统在管理性、可用性、可靠性和扩展性上的优势。

  作为全球领先的 Linux 发布厂商，红旗软件与全球硬件厂商都建立起了长期的紧密的合作关系，例如与 Intel 的合作，确保了红旗软件与主流PC硬件设备的高度兼容性，对 Intel 下一代无线和芯片技术都实现了最佳匹配。

  红旗 Linux 也有自己的鲜明特点: 比如完善的中文支持; 农历的支持和查询; 与Windows相似的用户界面; Linux下网页嵌入式多媒体插件的支持，实现了Windows Media Player和 RealPlayer 的标准 JavaScript 接口; 支持 MMS/RTSP/HTTP/FTP 协议的多线程下载工具; 界面友好的内核级实时检测防火墙; 可缩放的系统托盘; KDE 登录窗口、注销窗口、主题支持等。用户可通过红旗 Linux 官方网站提供的光盘镜像免费下载体验。

  红旗Linux主页: http://www.redflag-Linux.com



## 	3.Ubuntu

​	Ubuntu是一个以桌面应用为主的Linux操作系统，其来自于非洲南部祖鲁语的ubuntu一词（意为“乌班图”），它是基于Debian发行版和GNOME桌面环境或Unity界面，它每6个月会发布一个新版本，其中从Ubuntu16开始的双数版本为LTS（Long Term Support）。

​	Ubuntu由马克.舍特尔沃斯在2004年10月发布，它有如下几个特点：

1. 操作简单、方便，安装过程人性化；
2. Ubuntu使用APT包管理工具，可以方便的安装软件和升级；
3. Ubuntu具有很高的安全性；
4. 系统的可用性好，安装完即可使用；
5. Ubuntu每半年就会有新版本发布，会给用户带来新的体验。



​	截至到2023年8月，Ubuntu的最新版本为22.04。

