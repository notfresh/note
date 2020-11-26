Linux中查看磁盘剩余空间的方法
https://blog.csdn.net/vip_linux/article/details/8985510



df -hl
　
　　显示格式为：
　
　　文件系统 容量 已用 可用 已用% 挂载点
　
　　/dev/hda5 487M 120M 342M 27% /
　
　　/dev/hda1 981M 21M 911M 3% /boot
　
　　none 125M 0 125M 0% /dev/shm
　
　　/dev/hda2 29G 4.9G 23G 18% /home
　
　　/dev/hda3 20G 4.8G 14G 27% /usr
　
　　/dev/hda7 24G 510M 22G 3% /var
　
　　/dev/hdb2 75G 75G 0 100% /
　
　　/dev/hdb2 75G 75G 0 100% /， 以此为例，表示的意思为：
　
　　HD硬盘接口的第二个硬盘（b），第二个分区（2），容量是75G，用了75G，可用是0，因此利用率是100%， 被挂载到根分区目录上（/）
