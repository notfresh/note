# 介绍一下pycharm中的常用技巧.  



# 编辑器的快速操作  
command + d:向下复制本行.  
command + y:删除本行. 
MORE...

# 快速运行和调试
这些是我自己的补充.    
- 如果运行单独的文件: preference->keymap->other->run context configuration 设置为 command + shift + r  
- 调试运行单独的文件: preference->keymap->other->debug context configuration 设置为 command + shift + d  

# 隐藏和显示各种工具窗口的快捷键
默认绑定`command+1`快速隐藏和打开`项目`工具栏, 可以在 preference>keymap>tool_windows 修改绑定的快捷键组合.  
另外 termimal窗口, 因为其接受输入, 所以不要绑定 command+2这样, 应该绑定comand+shift+2. 为什么不绑定command+ctr+2, 因为ctrl和command在同一行, 按着不方便.  
另外, 还可以按command+shift+左右调整工具窗口的大小.  
tip: 如果想让terminal窗口最大化, 又可以使用快捷键快速`显示/隐藏`, 那么不要把编辑区完全挤没了, 留一点空间, 这样下次就能记住terminal窗口的大小了, 否则会把terminal窗口尺寸强行设置为屏幕的一半大小.  



# Pycharm 显示提示

按住 command 键或者 ctrl+q， 鼠标放到一个函数上面就有了。





# 如何在pycharm中搜索? - ykozxy的回答 - 知乎 

源地址:  
https://www.zhihu.com/question/279803333/answer/409405858  

# 在Mac中的实践  

- 搜索本项目内的类名: command + n:成功: 我建议改名为 command + option + c  

  > 注意: 按ctrl+n是新建选项.  

- 打开最近的文档:  command + e: 建议改为 command + option + r   

- 搜索文件, 根据文件名字搜索: command + shift + n: ok:我建议改键为 command + shift + f

- 搜索类名, 变量名, 函数名, 类方法名使用 command + shift + option + n:建议改为 command + shift + m .  

  > 注意: 常量名, 字符串, 是无法搜索到的. 不要使用这个命令搜索字符串.  

- 搜索pycharm命令: command + shift + a: pycharm的各种菜单和命令都可以找到了.  

- 设置搜索范围: 右上角的漏斗图标, 选择特定后缀的文件.  

- 实用价值最高的快捷键:  双击shift, 集成以上各种搜索.  

- 唯一的文本搜索: edit->"find->find in path", 快捷键是 ctrl+shift+f, 非常的强大.  


# 最后

如果在Windows系统上的Pycharm, 估计就是把command换成ctrl就可以了. 基本没啥问题. 



# 在windows中

需要配置默认terminal为 gitbash.  

