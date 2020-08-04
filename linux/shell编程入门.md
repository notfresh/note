### 为什么要学Shell？

多一个本事多一条路。  

很多人会说 Shell 编程属于运维方面的知识了，应该是运维人员来做，我们做后端开发的没必要学。我觉得这种说法大错特错，相比于专门做Linux运维的人员来说，我们对 Shell 编程掌握程度的要求要比他们低，但是shell编程也是我们必须要掌握的！

校招明文写着会shell加分！  


### 什么是 Shell？

壳子，壳子，壳子。  

操作系统暴露给程序员用户的交互界面（和暴露给普通用户的图像化界面为互补关系）。  



### 怎么写一个helloWorld?  
```shell
echo "echo 'hello world'" >> hello.sh
chmod a+x hello.sh 
./hello.sh
```

# 语言要素
shell中 # 符号表示注释。shell 的第一行比较特殊，一般都会以#!开始来指定使用的 shell 类型，我强调一下***#!后面不跟空格***。在linux中，除了bash shell以外，还有很多版本的shell， 例如zsh、dash等等...不过bash shell还是我们使用最多的。但是我个人喜欢zsh。



# Linux 权限管理概念？

TODO 



# shell字符串拼接

不用+！，注意了。  

${}表示一个占位符， 放在单引号里无效。  



## expr命令

运算符左右必须有空格  



## Length

${#VARIBLE_NAME}  



## 需要转移的运算符

对于某些运算符，还需要我们使用符号`\`进行转义，否则就会提示语法错误。比如乘号。 



**截取子字符串:**

```
str="SnailClimb is a great man"
echo ${str:0:10} #输出:SnailClimb
```



# 数组

bash支持一维数组（不支持多维数组），并且没有限定数组的大小。

定义数组使用 （元素1 元素2）即可，中间用***空格而非逗号***隔开。

获取数组的长度：

```
length=${#array[@]}
```

```
echo ${array[2]} #输出：3
```

```
unset array[1]# 删除下标为1的元素也就是删除第二个元素
```



# 关系运算符有哪些？(仅支持数字)

-eq, -lt -gt -ge -le, -ne



# 字符串运算符？

=  !=  -z 



# 如何定义和使用函数

使用函数不能带（），第一个参数叫做 $1



# 表达式运算符 

$(())



# 循环式

for((i=1;i<10;i++))

for in 语句

```
for i in ${array[@]};do echo $i ;done # 遍历数组，输出： 1 3 4 5 
```



# 接受键盘输入

read FILM  
read -p "提示语" a



# case

```shell
#!/bin/bash

if [ 1 -gt 2 ]
	then echo 1
else echo 4
fi

echo "*****************************"
b="1234567890"
echo $b
echo ${b:1:3}
echo "b的长度是${#b}"
echo "*****************************"

echo "***************数组**************"
arr=(1 2 3 4 5)
echo "数组的长度是${#arr[@]}"
echo "数组的第二个元素是${arr[1]}"
echo "*****************************"

for i in ${arr[@]};
do
	echo $i;
done
echo "*****************************"

for i in ${arr[*]};
do
	echo $i;
done


c=`expr 1 + 2`
echo $c
```



```shell
#!/bin/bash
a=1
b=1
if [ $a -eq $b ]
then echo "a==b"
else echo "a!=b"
fi

echo "124"

if [ $a -eq $b -o $a -lt $b ]
then echo "1"
else echo "2"
fi

if [ !false ] 
then echo "b"
fi

c=""
if [ ${#c}==0 ]
then echo "length is 0"
fi

 
```

