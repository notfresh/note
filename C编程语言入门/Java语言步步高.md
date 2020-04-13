# 目录

- 可变参数

- 泛型方法

- 错误示范
  - 泛型数组
  - 在创建类型的时候继续传入泛型形参

***

# 可变参数

代码示例

```java
	public static void main(String[] args) {
		print("1", "2", "3"); // 换行打印出1，2，3
	}
	
	public static void print(String... strs) { //三个点，表示不确定的个数
		for(String a:strs) {
			System.out.println(a);
		}
	}

```



# 泛型方法

```java
class B2{
	public String toString() {
		return "我是B类型";
	}
}

class A2{
	public String toString() {
		return "我是A类型";
	}
}
public class Test {
	public static void main(String[] args) {	
		print(new A2()); // 我是A类型
		print(new B2()); //我是B类型
	}
	
	public static <T> void print(T t) {
		System.out.println(t.toString());
	}
		
}
```



## 错误示范

## 错误示范1之泛型数组

```java

class G<T>{
	private T[] arr;
	
	public G(int n) {
		arr = new T[n]; // cannot create an array of generic T,报错
        // 我们思考一下原因，为什么不能这样呢？ 因为 new 关键字是要分配内存的，而 T 的类型不确定，是无法分分配内存的，因为分配内存是要根据类的属性等等为依据。
    		// 但是我们再思考一下为什么 List<Integer> arr = new ArrayList<>()可以呢。
    		// 我们必须注意到其不同。 
    		// new ArrayList<>() 创建了一个 ArrayList 对象，它里面可以维护一个数组，这个数组单纯的存放元素的地址，或者叫指针，指针的大小是确定的，比如我的64位系统，内存寻址是64位，那么一个地址，也就是 8 Byte，这是可以确定大小的。
    		// 我们都知道数组是连续存放的，所以泛型数组是不可行的。
    		// ArrayList 和数组 本质的不同之一就在于，ArrayList 存放的是高级对象的引用，而非实际地址，这也说明了为什么 List 接口接受的泛型实参都必须是类而不是基础类型。     
	}	
}
```



## 错误示范2之实现泛型接口

先看个正确的例子作为对比

```java
interface G<T>{ // 接口声明一个 T 
	
	public T next();
}

class G2 implements G{
	@Override
	public Object next() {
		return "abc";
	}	
}
```



错误的方法

```java
interface G<T>{
	
	public T next();
}

class G2 implements G<T>{

	@Override
	public Object next() { //编译器会提示你， Object类型不对，应该是T，等你把Object类型改为T，又发现G2类没有声明 T, 所以正确的做法参见下面的代码
		return "abc";
	}	
}
```



改正之后的代码

```java
interface G<T>{
	
	public T next();
}

class G2<T> implements G<T>{ //传入形参，也就是一个符号T，而非具体的类型的时候，必须给类也同样声明

	@Override
	public T next() {
		// return new T(); // 泛型不能使用 new,否则编译不通过,正如泛型不能创建数组一样
		return null;
	}	
}
```

<>表示泛型

再补充一段代码, 如果实现的时候指定泛型参数为具体的类型

```java
interface G<T>{
	
	public T next();
}

class G2 implements G<String>{  // 注意,如果把T改为实参,也就是具体的类型的时候,这么写合法

	@Override
	public String next() {
		return "abcde";
	}	
}
```



再看这样一段例子：

```java
interface G<T>{
	
	public T next();
}

class G2 implements G<Number>{  

	public Integer next() { // Integer 是 Number 的子类,这样写是合法的.
		return 123;
	}	
}
```





如果该有的泛型参数不写的话，那么就默认泛型参数为 Object

```java

class G2<T>{  

	public T next() {
		return null;
	}	
}

public class Sort {

	public static void main(String[] args) {
		G2 g2 = new G2(); // 相当于 G2<Object> g2 = new G2<Object>();
		Object a = g2.next();	
		print(a);
	}
	
	public static <T> void print(T t) {
		if(t == null) {
			System.out.println("t is null");
			return;
		}
		System.out.println(t.toString());
	}
```



## 在创建类型的时候继续传入泛型形参

```java
List<T> a = new ArrayList<T>(); // 这样写是不对的， 因为 T 必须是具体的类型，继续传递泛型只能在定义泛型类的时候使用，而创建实例对象的时候，泛型则无法应用
```



## 泛型的特点

编译时检查语法错误，运行时就被取消了。





# 参考

- java 泛型详解-绝对是对泛型方法讲解最详细的，没有之一

  https://www.cnblogs.com/coprince/p/8603492.html

