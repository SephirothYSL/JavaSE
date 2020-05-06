## 1. static关键字

### 1.1 概述

static 关键字方便在**没有创建对象的情况下来进行调用方法和变量**(优先级高于对象)，可以用来修饰类的成员方法、类的成员变量，另外可以编写static代码块来优化程序性能

### 1.2 static变量

static变量也称作静态变量，静态变量和非静态变量的区别是：静态变量被所有的对象所共享，在内存中只有一个副本，它当且仅当在类初次加载时会被初始化。

```java
class Person {
	static String name;
}

public class TestPerson {
	public static void main(String[] args) {
		System.out.println(new Person().name);	// The static field Person.name should be accessed in a static way
		System.out.println(new Person().name);	// The static field Person.name should be accessed in a static way

		Person.name = "Buffer";

		System.out.println(new Person().name);	// The static field Person.name should be accessed in a static way
		System.out.println(Person.name);
	}
}
```

结果

```shell
null
null
Buffer
Buffer
```

#### 总结

```shell
1、通过类名调用静态变量，因为静态变量与对象无关
2、静态变量被所有对象共享，一处更改处处更改
```

### 1.3 static方法

static方法一般称作静态方法，由于静态方法不依赖于任何对象就可以进行访问，因此对于静态方法来说，是没有this的，因为它不依附于任何对象，既然都没有对象，就谈不上this了。并且由于这个特性，在静态方法中不能访问类的非静态成员变量和非静态成员方法，因为非静态成员方法/变量都是必须依赖具体的对象才能够被调用。

```java
class Student{
	static String name;
	int age;
	
	public void testMember() {
		
	}
	
	public static void testStatic() {}
	
	public static void test() {
		age = 10;	// 报错：Cannot make a static reference to the non-static field age
		this.age = 10;	// 报错：Cannot use this in a static context
		testMember();	// 报错：Cannot make a static reference to the non-static method test() from the type Student
		this.testMember();	// 报错：Cannot use this in a static context
		
		name = "Buffer";	// 编译通过
		testStatic();	// 编译通过
	}
}
```

#### 总结

```shell
1、static修饰的方法不能访问本类中的非静态变量和方法，不能使用this
2、通过类名来调用静态方法，工具类的应用很广泛
```

## 2. Arrays工具类

### 2.1 toString(数组名)

返回任意类型数组的内容的字符串表示形式

### 2.2 sort(数组名)

使用快速排序算法，将任意类型数组排序为上升的数值顺序

### 2.3 binarySearch(数组名, 指定元素) 

使用二分法在指定升序数组中搜索指定元素。 返回指定元素所在的一个下标，如果没有指定值就返回负数

### 2.4 copyOf(原数组, 新长度) 

通过原数组(从下标0开始)复制一个新数组，容量为自定义，返回一个数组

```java
public class Test {
	public static void main(String[] args) {
		int[] array = { 1, 3, 2, 6, 4 };
		
		// toString 方法，打印数组中的元素
		System.out.println(Arrays.toString(array));
		
		// sort 方法，快速排序(升序)
		Arrays.sort(array);
		System.out.println(Arrays.toString(array));

		// binarySearcg 方法，二分查找指定元素
		System.out.println(Arrays.binarySearch(array, 3));

		// copyOf 方法，复制数组
		int[] newArray = Arrays.copyOf(array, 5);
		System.out.println(Arrays.toString(newArray));
	}
}
```

结果

```shell
[1, 3, 2, 6, 4]
[1, 2, 3, 4, 6]
2
[1, 2, 3, 4, 6]
```

## 3. 代码块

在 Java 中，使用{}括起来的代码被称为代码块，根据其位置和声明的不同，可以分为局部代码块，构造代码块，静态代码块，同步代码块(多线程)

### 3.1 构造代码块

```shell
格式：
	{
	
	}
```

#### 注意

```shell
1、用于给对象初始化，多个构造方法中相同的代码存放到一起，每次调用构造都执行，并且在构造方法前执行
2、只有创建对象时调用，类不能调用
3、构造代码块只能有一个
```

```java
class Person {
	{
		System.out.println("Person构造代码块执行");
	}

	public Person() {
		System.out.println("Person构造方法执行");
	}
}

public class TestPerson {
	public static void main(String[] args) {
		System.out.println("main方法");
		new Person();
		new Person();
	}
}
```

### 3.2 静态代码块

```java
格式：
    static {
    
	}
```

#### 注意

```shell
1、用于给类进行初始化，在加载的时候就执行，并且只执行一次
2、优先级高于主函数
3、静态代码块可以有多个，顺序执行
```

```java
class Person {
	static {
		System.out.println("Person静态代码块执行");
	}

	public Person() {
		System.out.println("Person构造方法执行");
	}
}

public class TestPerson {
	static {
		System.out.println("静态代码块1执行");
	}

	public static void main(String[] args) {
		System.out.println("main方法");
		new Person();
		new Person();
	}

	static {
		System.out.println("静态代码块2执行");
	}
}
```

结果

```shell
静态代码块1执行
静态代码块2执行
main方法
Person静态代码块执行
Person构造方法执行
Person构造方法执行
```

### 3.3 面试题

执行顺序

```java
public class Test {
	static Test test1 = new Test();
	static Test test2 = new Test();

	static {
		System.out.println("静态代码块");
	}

	{
		System.out.println("构造代码块");
	}

	public Test() {
		System.out.println("构造方法");
	}

	public static void main(String[] args) {
        System.out.println("main方法");
		new Test();
	}
}
```

结果

```shell
构造代码块
构造方法
构造代码块
构造方法
静态代码块
main方法
构造代码块
构造方法
```

根据结果可以发现，虽然main方法是程序执行的入口，但是程序执行前的加载过程，要对static修饰的变量、方法、代码块进行加载，按照顺序执行，刚开始我不理解为什么静态代码块没有在最开始就执行，但其实把静态对象当成普通的变量就好理解了，就是按照static出现的顺序往下执行
