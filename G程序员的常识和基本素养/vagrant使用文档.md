# 搭建环境的过程

vagrant是一款虚拟机管理工具，使用它可以快速搭建可复用、可移植的开发环境。
使用一个命令，vagrant就可以完成以下所有事情:

- 在电脑上快速创建一台虚拟机
- 改变虚拟机的物理配置
- 建立网络连接，使得你可以访问在你电脑上运行的虚拟机或局域网下的其他虚拟机
- 共享目录，你在电脑上对文件的修改可以同步到虚拟机
- 启动虚拟机
- 设置虚拟机主机名使得该虚拟机下的软件能够正确的设置
- 使用shell script或配置管理工具(例如：chef、puppet)来配置软件安装
- 调整主机和客户机的工作方式来解决可能出现的问题，例如：VirtualBox的默认网络配置在Ubuntu 12.04 LTS下是无效的，因此vagrant调整了Ubuntu的配置使得VirtualBox网络能够正常使用，vagrant解决了很多类似这种主机和客户机组合常见的问题。

使用vagrant搭建好一个配置好的开发环境在大约在一分钟内就能完成，耗时多少取决于你要安装的软件数量。
一旦vagrant完成了虚拟机的创建，你将拥有一个配置好的开发环境，因为已经默认创建好了共享目录和网络连接，当你测试你的web应用的时候，代码实际是运行在虚拟机里。
vagrant提供了完善的管理虚拟机的命令，除了创建开发环境，vagrant还可以实现以下所有事情：

- 使用ssh连接到虚拟机
- 关闭虚拟机
- 彻底删除虚拟机
- 暂停或恢复虚拟机
- 打包虚拟机镜像

vagrant搭建开发环境就像瑞士军刀一样犀利，它帮你解决了创建和管理开发环境的所有工作，并且开发环境更接近于生产环境。



# 关闭实例

关闭实例可以使用三种方式vagrant suspending, vagrant halt, vagrant destroy。

- suspending，暂停虚拟机，保存虚拟机当前的状态（内存和磁盘均不释放），可以使用vagrant up命令恢复运行；
- halt，关机，虚拟机停止运行，但是虚拟机实例保留，不销毁，可以理解为是正常的关机；
- destroy，销毁虚拟机，虚拟机的实例被销毁;

# vagrant ssh
如果是官方的box，那么用户名和密码默认都是vagrant

# vagrant命令详解

命令	作用
vagrant box add　　	　　添加box的操作　　
vagrant init 	　　初始化box的操作，会生成vagrant的配置文件Vagrantfile　　
vagrant up	启动本地环境
vagrant ssh	通过 ssh 登录本地环境所在虚拟机
vagrant halt	关闭本地环境
vagrant suspend	暂停本地环境
vagrant resume	恢复本地环境
vagrant reload	修改了 Vagrantfile 后，使之生效（相当于先 halt，再 up）
vagrant destroy	彻底移除本地环境
vagrant box list	显示当前已经添加的box列表
vagrant box remove	删除相应的box
vagrant package	打包命令，可以把当前的运行的虚拟机环境进行打包
vagrant plugin	用于安装卸载插件
vagrant status	获取当前虚拟机的状态
vagrant global-status	显示当前用户Vagrant的所有环境状态



# 关闭实例

关闭实例可以使用三种方式vagrant suspending, vagrant halt, vagrant destroy。

- suspending，暂停虚拟机，保存虚拟机当前的状态（内存和磁盘均不释放），可以使用vagrant up命令恢复运行；

- halt，关机，虚拟机停止运行，但是虚拟机实例保留，不销毁，可以理解为是正常的关机；

- destroy，销毁虚拟机，虚拟机的实例被销毁;

# 增加box
vagrant box add nachosEnv  ~/Documents/上课有关/操作系统/xenial-server-cloudimg-i386-vagrant.box

# 导出box
vagrant package --output NAME.box



# 参考资料
https://www.cnblogs.com/mr-amazing/p/9606222.html
https://www.cnblogs.com/wangkongming/p/4070782.html
https://blog.csdn.net/zc474235918/article/details/51039150
https://homes.cs.washington.edu/~tom/nachos/
http://www.vagrantbox.es/

- Vagrant入门
https://www.cnblogs.com/alexyang8/p/3380936.html
- vagrant初识（一）
https://www.cnblogs.com/slang/p/9919400.html

- vagrant 14.04 32位下载地址
https://c4ys.com/archives/1230
https://mirrors.tuna.tsinghua.edu.cn/ubuntu-cloud-images/vagrant/trusty/current/
https://blog.csdn.net/weixin_30367169/article/details/94909666

- 如何获取box

  https://blog.csdn.net/weixin_33814685/article/details/91938829

- 国内下载地址

  https://segmentfault.com/q/1010000011063709

  



# 管理多个机器

```ruby
# -*- mode: ruby -*-
# vi: set ft=ruby :

BOX_IMAGE = "./hadoop_master.box"
NODE_COUNT = 2

Vagrant.configure("2") do |config|

  config.vm.define "hadoop-master" do |subconfig|

    subconfig.vm.box = BOX_IMAGE # use the same IMAGE with the slaves
    subconfig.vm.network "private_network", ip: "192.168.33.10"
    subconfig.vm.hostname = "hadoop-master"
  end

  (1..NODE_COUNT).each do |i|

    config.vm.define "hadoop-slave#{i}" do |subconfig|
      subconfig.vm.box = BOX_IMAGE
      subconfig.vm.network "private_network", ip: "192.168.33.#{i+10}"
      subconfig.vm.hostname = "hadoop-slave#{i}"
    end
  end
end
```