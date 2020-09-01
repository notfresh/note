# tar
tar --exclude="git_faq/.git" -zcvf git_faq.tgz git_faq 压缩

# shell快捷键
Q:
有时候调用历史命令，都是很长的那种，然后发现并不是自己想要的，需要重新输入，如何快速删除已有/已输入的命令/内容？
或者说，
比如我输入了 # ps -aux | grep yum，这个命令还没执行，现在我不想用这个命令了，如果快速删除已输入的内容，也就是# ps -aux | grep yum？

A:
直接按Ctrl + c

附上一些其他较长使用的快捷键：

ctrl + w 往回删除一个单词，光标放在最末尾
ctrl + u 删除光标以前的字符
ctrl + k 删除光标以后的字符
ctrl + a 移动光标至的字符头
ctrl + e 移动光标至的字符尾
ctrl + l 清屏


### iterm
Killing a fly with a cannon:

Go to Preferences... > Profiles > Keys (not Preferences... > Keys)
Press Presets...
Select Natural Text Editing
Then, you can move a word backwards using Option ⌥ + ← and a word forwards using Option ⌥ + →, move to the start of the line using fn + ← and to the end of the line with fn + →. Also you can delete a word backwards using Option ⌥ + ⌫, delete the whole line using Command ⌘ + ⌫.

If the preset doesn't appear, reinstall iTerm2. If you installed it using Homebrew+Cask:

brew cask reinstall iterm2


# 为什么不学 shell 编程了？

因为python 可以代替而且功能更强大，关键是好写。

 

# Linux 常用命令

## File CRUD

- mkdir  
  创建多级目录
  mkdir -p Project/a/src

- 链接  
  硬链接只能对单个文件  
  链接的目录必须是绝对路径，不能是相对路径  
  软链接, ln -s FROM TO ; 相当于 Windows 里面的快捷方式.  

  > 进入一个软链接文件夹不会把 pwd 切换到源目录里去。 还是把软链接当做一个链接
  > 但是软链接不可以移动, 否则就会失效. 这一点不像 windows 里的快捷方式.   

# COMMAND 

- 创建别名, 同义词  
  短名 alias a='xxxx xxx xxx'

 

- find  
  找文件, 根据名字找, 是最常用的, 找配置啥的.  
  格式: find DIRECTORY_RELATIVE_OR_ABSULUTE/ -name \*.cnf  [-d 3:深度为 3 层]  
  
  find 命令最奇怪的是它直接输入对象是目录，而不是要查找的对象的名字，这一点比较反常识。



- chmod命令  
  chmod u+x file  
  http://www.cnblogs.com/peida/archive/2012/11/29/2794010.html  



- zip  
  解压: unzip [-v:只看不解压]  X.zip -d OUT_PUT_DIR  
  压缩: zip OUT_PUT_ZIP_NAME.zip -r INPUT_ZIP_DIR  

- ps 命令详解  
  ps -ef 的各个字段解释如下, 依照出现顺序:  
  UID, user_id  
  PID  
  PPID  
  ...  
  CMD, 启动这个进程用到的命令, 最后一个字段特别重要, 它还指明了这程序启动时用到的参数, 有的时候找不到出错的原因就是因为没有注意到程序后面跟的配置.  

   > 参考: https://www.cnblogs.com/freinds/p/8074651.html

- grep  
  答: grep 子串  文件或者管道输出  -A后多少行 -B前多少行 

- 重启  
  For shutdown:
  sudo poweroff
  For restart:
  sudo reboot 

# 前台后台操作

https://segmentfault.com/a/1190000000349722
ctrl+z 暂停到后台, ctrl+c 杀掉,  
带上&, 直接放到后台
使用jobs 可以查看后台任务
bg %i 放到后台, fg %i 放到前台.

# 快速入门的小抄用法

curl cheat.sh/COMMAND  

- su  
  su 的语法为： su [-] username
  加”-“后会连同用户的环境变量一起切换过来

# 需要理解机制

- bash加载顺序  
  mac 下的bash的配置文件的加载顺序,以及zsh的配置  
  https://www.jianshu.com/p/020f3d02f538  


- Linux的环境变量  
  一、Linux的变量种类
     按变量的生存周期来划分，Linux变量可分为两类：
     1、永久的：需要修改配置文件，变量永久生效。
     2、临时的：使用export命令声明即可，变量在关闭shell时失效。
  二、设置变量的三种方法
     1、在/etc/profile文件中添加变量【对所有用户生效（永久的）】
     2、在用户目录下的.bash_profile文件中增加变量【对单一用户生效（永久的）】
     3、直接运行export命令定义变量【只对当前shell（BASH）有效（临时的）】
  三、PATH声明，其格式为：
     PATH=`$PATH:<PATH 1>:<PATH 2>:<PATH 3>:------:<PATH N>`

- locale  
  export LC_ALL=en_US.UTF-8  
  http://www.cnblogs.com/dolphi/p/3622570.html

- fhs  
  file system hierachy standard
  /usr/local 第三方文件夹.
  https://blog.csdn.net/dongfei2033/article/details/76302190

- linux中的正则表达式  
  https://www.cnblogs.com/andysd/p/3434067.html

# shell  

- 查看当前 shell 
  echo $SHELL

- 查看当前可用 shell  
  cat /etc/shells  

- 改变当前用户的 shell  
  ch -s $(which zsh/bash)


# 使用频率很低, 没卵用的命令  

- diff  
  < 表示左边有, >表示右边独有, 右边的为参考, 左边的是主动比较文件.
  d表示删除,c表示改变.
  更完整的推荐答案参考这里: https://www.computerhope.com/unix/udiff.htm
  从这篇帖子我们可以看出, a, c, d, 不同模式, 参数含义是不一样的. 参数含义由模式决定.
  目前我只要会用 diff -c file1 file2, 或者 diff -u file1 file2就可以了

- scp  
  次重要 scp命令 server copy secure cop
  scp [-r, 表示文件夹] 系统用户@IP:文件路径   本地路径 

- 网络端口占用查询
  sudo netstat -tulpn
  例如:
  (venv) root@zx_vultr:/srv/www/jobplus# netstat -tulpn| grep 5000
  tcp        0      0 0.0.0.0:5000            0.0.0.0:*               LISTEN      10913/python3
  (venv) root@zx_vultr:/srv/www/jobplus# kill -9 10913


- 不重要 # tar命令
  http://man.linuxde.net/tar 
  解压到指定命令 tar -C
  http://www.cnblogs.com/peida/archive/2012/11/30/2795656.html
  tar -z(压缩格式){x(解压)|c(压缩)}f(文件) 文件名 

- 7. awk 完整形式是什么? (2)怎么用?  
     答: 三个作者的名字第一个字母.(2) awk接受输入, 然后 以'{}'开始指定命令, NR表示

- 编译安装
  configure, make ,make install是什么意思?手动编译,安装软件
  https://blog.csdn.net/linzhiji/article/details/6774410

- Shell 脚本   

9. 有不错的shell帖子吗?
   https://blog.csdn.net/M_SIGNALs/article/details/53490074
   https://blog.csdn.net/hyszyl/article/details/60970307 关于shell的面试题.

- 改密码  
  passwd [username]  

- 查看一个文件夹的大小  
  du -sh [dictory1] [directory2]  



# 软件安装

## 修改Ubuntu源为阿里云

https://blog.csdn.net/hang916/article/details/79465458  



add-apt-repository

- 安装软件 查看已经安装的软件  dpkg –l |grep vim

- 更改软件源

https://blog.csdn.net/dearsq/article/details/51492847

- 删除ppa源 https://blog.csdn.net/li_hai/article/details/8189290

<br>

linux安装搜狗输入法

http://blog.csdn.net/ljheee/article/details/52966456

TODO http://www.cnblogs.com/hupeng1234/p/6956645.html  安装完记得注销，否则找不到搜狗输入法

<br>

linux安装deb包

1. 下载deb包

2. dpkg –i 包名

3. <strong>apt-get –f install : 修复依赖关系</strong> 非常重要!!

<br>

安装软件解锁

sudo rm /var/lib/apt/lists/lock

sudo rm /var/cache/apt/archives/lock

sudo rm /var/lib/dpkg/lock

<br>

安装sublime

1、安装Sublime Text 3

首先添加sublime text 3的仓库：

sudo add-apt-repository ppa:webupd8team/sublime-text-3

根据提示按ENTER 继续，建立信任数据库

更新软件库

sudo apt update

安装Sublime Text 3

sudo apt install sublime-text-installer

https://www.linuxidc.com/Linux/2017-02/140918.htm

<br>

安装mysql

sudo apt update

sudo apt search mysql-server-version(说不定可以加通配符)

<br>

安装报错

dpkg: 另外一个进程已经为状态数据库加了锁  

http://blog.csdn.net/qq_33160271/article/details/73800477

稍作等等，后台正在更新，想要解决这个问题， 在系统设置里把自动更新关掉！！！

<br>

ubuntu安装python3

# 使用apt安装

https://blog.csdn.net/lzzyok/article/details/77413968

sudo add-apt-repository ppa:jonathonf/python-3.6

sudo apt-get update

sudo apt-get install python3.6

sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.5 1

sudo update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.6 2

sudo update-alternatives --config python3

python3 –V

which python3: /usr/local/bin/python3

 

# 安装anaconda

https://blog.csdn.net/yimingt/article/details/72518562 地址

https://blog.csdn.net/gjq246/article/details/70848831 安装方法



2.1 .bash

3.1 如何安装linux

https://segmentfault.com/a/1190000002954932



3.2 linux创建别名，节省时间。

alias py=”python3”（shell里不能有空格，不是编辑器！！）

http://man.linuxde.net/alias



3.3查看linux 32位还是64位？

uname -a

https://linux.cn/article-3048-1.html



 



3.4

开启SSH

http://www.cnblogs.com/nodot/archive/2011/06/10/2077595.html

对上文的补充:

在配置的最上面打开监听0.0.0.0 , 否则无法远程连接.

 

快捷键

显示桌面 ctrl+alt+d

网址https://zhidao.baidu.com/question/237679542.html



 



linux Shell执行循环报错：

linux shell 报错 Syntax error: Bad for loop variable

因为Ubuntu为了加快开机速度，用dash代替了传统的bash，所以我们这样执行就没问题．

bash test.sh

http://www.cnblogs.com/wangkongming/p/4876693.html



 



6.shell脚本

https://github.com/qinjx/30min_guides/blob/master/shell.md#os

linux命令

cat命令

sudo命令



7. sudo cd报错 执行sudo su,或者 sudo -sH

原因:http://blog.csdn.net/gatieme/article/details/49106865





筛选命令 | grep keyword

创建文件夹并且进入命令

mkdir rent_proj && cd rent_proj



linux环境变量

打印环境变量echo $PATH


如何修改环境变量

http://www.powerxing.com/linux-environment-variable/

# 翻墙

https://www.sundabao.com/ubuntu%E4%BD%BF%E7%94%A8shadowsocks/ 

# 安装包下载和安装过程

http://teliute.org/linux/Ubsetup/lesson24/lesson24.html

# 外部跳转到chrome浏览器无法打开网页

https://blog.csdn.net/Artprog/article/details/71076111

平台：Ubuntu 16.04 Desktop

出现这个问题跟 google-chrome.desktop 有关，它缺少一个参数 %U。 
打开文件：$HOME/.local/share/applications/google-chrome.desktop 
找到下面这行: 
Exec=/opt/google/chrome/chrome 
在末尾添加一个空格和%U: 
Exec=/opt/google/chrome/chrome %U 
然后保存文件即可。

 # service错误查看

systemctl status mysql.service

# 多个版本的gcc

首先查看有几个版本
ls /usr/bin/gcc*
如果有多个, 想设置一个默认的. 那么就选择
安装好后输入以下指令：

sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.4 50
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.8 40
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-4.9 30

接着输入：
sudo update-alternatives --config gcc
版本就被改过来了.


# zsh

history -10



# 打印当前执行目录并且保存到某个文件

echo `pwd` >> FILENAME



# 14.04源更新

deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-security main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-updates main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-backports main restricted universe multiverse
deb http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-proposed main restricted universe multiverse
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty main restricted universe multiverse
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-security main restricted universe multiverse
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-updates main restricted universe multiverse
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-backports main restricted universe multiverse
deb-src http://mirrors.tuna.tsinghua.edu.cn/ubuntu/ trusty-proposed main restricted universe multiverse
————————————————
版权声明：本文为CSDN博主「yue492008824」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/yue492008824/article/details/44947135

# 如何安装java

sudo apt-get install default-jre/openjdk-7-jre
sudo apt-get install default-jdk/openjdk-7-jdk

# 压缩命令

tar -zcvf test.tar.gz aaa.txt bbb.txt ccc.txt或：tar -zcvf test.tar.gz /test/



# 什么是Make

源码的安装一般由3个步骤组成：配置(configure)、编译(make)、安装(make install)。

https://zhuanlan.zhihu.com/p/81060079





例解 Linux 下 Make 命令

https://www.cnblogs.com/hazir/p/linux_make_examples.html




# apt-get -y install中的-y是什么意思?

等于无脑单击下一步.

# curl

下载用的, 有很多选项.  
我也见过好几次这个命令, 今天(2019-06-18)查阅了一下, 大致明白, 就是个下载资源的命令.  
我好奇为什么叫curl(TODO)?  
参考网址: https://www.cnblogs.com/gbyukg/p/3326825.html  

# wget命令  

http://www.cnblogs.com/peida/archive/2013/03/18/2965369.html 
-O 重命名
--no-check-certificate的含义
https://op.ci/104.html



# 鸟哥的私房菜

## 网址  

http://linux.vbird.org/  

# Bash 讲解  

位置:  Linux基础文件->10.认识与学习BASH

- 查看可用的 shell  
  cat /etc/shells

- 查看每个用户对应的 shell  





# Less的使用

## 参考地址:

https://www.cnblogs.com/xd502djj/p/10460555.html  

## 几个基本的技巧 

列举一两个实用的less使用方法

## 在Mac下

less -N FILE: 可以查看文件以及行号.

### 行跳转

和Vim相同. 

### 搜索

和Vim相同

### 在编辑器总打开, 按v, 默认的编辑器是v

## 写在最后

Mac下和Linux下是不一样的, 所以我也不知道Linux的less啥样子的.  
Mac下的less命令是不会把文本内容打印到终端里的, 但是Linux的bash好像会? 我记得一个服务器的bash里是这样子的.





# 例解 Linux 下 Make 命令

https://mp.weixin.qq.com/s/W385xVtSOYRU66T3AznTEg





# lsof命令--列出当前系统打开文件

https://www.geek-share.com/detail/2646305868.html





# Vim

## Vim的哲学

Vim不同于其他文本编辑器的特点是, 把文档当做一个对象, 使用命令对这个对象进行操作.  
Vim诞生于早期没有GUI界面的年代, 基于命令行的文本编辑器, 或者说基于黑窗口, 面向的群体是程序员, 所以一切必须基于命令.   
所以, 必须理解的是Vim的流程是不同于其他GUI界面的文本编辑器的. 没有那么多可视化按钮, 可以方便的点点点, 很多命令都是必须要记下来的.  
如何很好的记住这些命令, 这是学好Vim的关键.  
大道至简, Vim被设计成很简单的操作.  常用的操作用一个手都能数清.  
学会Vim就是要学会这5个以内的命令, 可以解决90%的使用场景.  
在我看来, Vim就是平时不方便用GUI的时候, 用一下, 不用知道的太多, 学的太多也是个浪费.  
生命的时间很短, 没有必要学一些太偏的骚操作.  
<br> 


## Vim的简单操作

Vim的第一个模式就是命令模式, 而且是进入Vim后的默认模式. 在这个命令模式下, 不能直接输入字符到文档中.  
前面说过Vim把一个文档当做一个对象.  所以要使用命令对这个对象进行操作.  
字符是最基本的操作单位, 光标所在的位置就是当前的被操作的字符. 对字符的操作有最简单的是删除, 按x键.  
其次的操作单位是行.   



## 最常用的命令

### set 命令  

在命令行模式下, set 是一个非常高频的命令.

- set nu/nonu: 显示/隐藏行号, 默认是隐藏的  
- set hlsearch: 设置搜索高亮, 这个和下面的搜索有关, 找到搜索结果后, 高亮显示.  

### 搜索  

- /ABC: 搜索, 配合搜索 n:查找下一个, N:查找上一个.  
  需要注意的是:  `/`是大小写敏感的搜索.  
  输入完带搜索单词, 要先按一下 Enter 键, 才能开始搜索.  
- set hlsearch: 设置搜索高亮, 找到搜索结果后, 自动高亮显示.

> 保存常用 vim 配置  
> 在~目录下, 新建文件 .vimrc , 每行输入一个命令行. 新打开的 vim 窗口就会自动先加载这些命令.  


## <font color=red>一条命令执行多次相同操作</font>  

**这是**最重要的一条技巧, 这是 vim 的灵魂.  
如果你要重复执行 N 次操作, 比如删除当前光标所在字符. 按 Nx.  

### 光标级操作  

删除当前光标所在的字符: x.

### 行操作  

- 行跳转: G    
  跳转到第 10 行, 按 10G; 跳转到最后一行, 按 G.  

- 行拷贝: yy  
  粘贴用 p.

- 行剪切(等于行删除): dd

### 撤销和回退操作

u: undo, 撤销  
ctrl + r: redo, 重做. 

### 查找和替换

在命令行下, 输入 :LNE1,LINE2<font color=red>s</font>/REPLACE/TO_REPLACE/g 刚好可以. 这个`s`不能丢.  


## 不常用的命令

可视化模式, 按v进入. 大片的选择.  

## 阅读翻页命令

ctrl + u/d 向上/下翻半页  
ctrl + f/b 想下/上翻一页.  
为什么f/b翻的页数多呢? f, forward, b, back, 这两牛逼就完了.  



## Vimium的使用

b 搜索书签窗口

o 搜索历史记录



## 缺陷

- 如果进入一个页面，这个页面有自动让某个输入框获取焦点的设定，那么vimium 就会暂时失效。

- Vimium 在空白页和特殊页会失效 。

- Vimium 会在页面载入的时候，因为chrome 全力加载JS而 屏蔽其相应。



# 列举

首先我们使用ls命令，列出当前文件夹下的所有文件和文件夹，然后我们使用cd命令打开我们需要查看文件夹大小的文件夹，

然后我们使用

du -s命令，此时我们可能会看到一长串的数字，这就是我们先要的文件夹的大小，只不过显示的是文件夹的字节数。

du -sh

du -sh /输入你想要查询的文件夹路径



# zip命令
 zip git_faq.zip -r git_faq -x "git_faq/.git/*" 
 当涉及正则的时候，最好引起来。



# 参考

[1]查看 Linux 发行版名称和版本号的 8 种方法 | Linux 中国

https://mp.weixin.qq.com/s/7cGemMmDQPLpS1tViHERVA

[2] find 命令

http://c.biancheng.net/view/779.html



