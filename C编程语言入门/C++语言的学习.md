# 第八章关键词

8.1 

内联 inline

8.2

引用变量

8.3 

默认参数

8.



# 书签

- cout 数字格式 p367

  科学计数法

- 

# C++明确知道的问题：

1. 默认声明了private，接着声明publi成员变量，会编译报错，如果一旦使用public声明，那么必须显式声明private范围
2. string 是小写的， 在std空间里面，可以直接使用。
3. main里面可以没有 void，直接写 int main(){}

4. 函数定义结尾的大括号后面不跟`;` ，但是类定义和结构体定义后面必须跟 `;`。
5. 



## 类和对象

1. C++的构造函数虽然可以重载，但是不可以相互调用。一旦调用构造函数，就会立刻新建一个新的对象。

   如果要解决构造函数之间相同代码初始化的问题，那么可以使用一个初始化函数来做。

2. 成员变量如果不初始化，那么值就会随意被赋予一个值。



## 关于构造函数的demo，详细的说明了一些问题

```c++
#include <iostream>
using namespace std;

class A{
public:
	void hello(){
		cout << a << endl;
	}
	A(int a2){
		a = a2;
		cout << this << endl;
	}
	A(A& obj){
		cout << "调用拷贝构造函数" << endl;
		a = obj.a;
	}
	int a;
	int b=3;
};


int main(){
	A a2(10);
	a2.hello();
	a2.b = 13;
	A a3(a2);
	A a4(11);

	cout << "a3 a value" << a3.a << endl;
	cout << "a4 address  xx " << &a4 << endl;
	a4 = a2; // 这里使用的是构造函数, 而不是引用传递,注意,这里和Java不一样!!,想专门使用引用,请使用 & 声明一个变量, 这里使用a2
	// 所有的值去覆盖a4的值
	// 纠正,这里不是用的构造函数,而是用的赋值机制
	cout << "a4 a value" << a4.a << endl;
	cout << "a2 address" << &a2 << endl;
	cout << "a4 address" << &a4 << endl;
	cout << "a4 b value " << a4.b << endl;
	A a5 = a2; // 这里使用的是拷贝构造函数,我们看的出来,只修改了a的值,并没有修改b的值.
	cout << "a5 b value" << a5.b << endl;
}
```









# C++语言疑问

1. 这个是一个数组还是一个单独的整数？

```
int* a = new int(10);  //这个呢？
// int* arr = new int[10]; 这是数组
```

2. delete p， 接下来的步骤是什么？

3. 什么是**左值**？？

4. 如何打印指针的位置？

5. 直接声明的类存放的内存位置是栈里面吗？知不是只有new指针才能放到堆里面去？

   ```c++
   class A{};
   
   
   int main(){
   	int b = 10;
   	int *a = &b;
   	*a = 10;
   	A *aa;
   	A *aa2 = new A;
   	cout << a << endl;
   	cout << aa << endl;
   	cout << aa2 << endl;
   	// 就目前的结果来看,看来他们的内存位置并不连续!!!
   	//	0x7ffee709b4cc
   	//	0x100000000
   	//	0x7f86be402690
   
   }
   ```

6. 

## 类和对象

1. 如何调用一个构造函数的重载函数？
2. 



