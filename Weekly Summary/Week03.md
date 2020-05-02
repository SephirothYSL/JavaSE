# 1. 数组

## 1.1 选择排序算法

```java
public static void selectionSort(int[] array) {		
	for (int i = 0; i < array.length - 1; i++) {
		for (int j = i + 1; j < array.length; j++) {
			if (array[i] < array[j]) {
				int temp = array[i];
				array[i] = array[j];
				array[j] = temp;
			}
		}
	}
}
```

## 1.2 冒泡排序算法

```java
public static void bubbleSort(int[] array) {
		for (int i = 0; i < array.length - 1; i++) {
			for (int j = i + 1; j < array.length; j++) {
				if (array[j - 1] < array[j]) {
					int temp = array[j - 1];
					array[j - 1] = array[j];
					array[j] = temp;
				}
			}
		}
	}
```

## 1.3 打印数组中指定元素的所有下标

```java
public class TestBinarySearch {
	public static void main(String[] args) {
		int[] array = { 10, 7, 3, 9, 3, 2, 8, 1, 3, 5 };
		int index = 0;

		while (index <= array.length) {
			int result = binarySearch(array, 3, index);

			if (-1 == result) {
				break;
			}

			System.out.println(result);
            // index赋值为有效元素的下标加1，确保下次循环不出现重复的下标
			index = result + 1;
		}
	}

	/**
	 * 查找指定元素的所有下标
	 * @param array 传入一个数组
	 * @param num 指定的元素
	 * @param index 循环的初始条件
	 * @return 返回每个指定元素的下标，当找不到指定元素的下标时返回-1
	 */
	public static int binarySearch(int[] array, int num, int index) {
		for (int i = index; i < array.length; i++) {
			if (num == array[i]) {
				return i;
			}
		}
		return -1;
	}
}
```



# 2. Eclipse快捷键

```shell
alt + ? 或 alt + /：自动补全代码
ctrl + 1：弹出错误修复 / Quick fix
ctrl + shift + r：打开资源列表
ctrl + shift + f：代码格式化
ctrl + shift + o：自动导包删包
ctrl + M：全屏代码区
Alt + 上下：移动选中行
ctrl + Alt + 上下：复制选中行
ctrl + /：注释选中行（//形式）
ctrl + shift + /：注释选中行（/**/形式，使用ctrl+shift+\取消）
ctrl + H 查找文件
ctrl + shift + L：快捷键提示
ctrl + d：删除选中行
```

# 3. 面向对象

## 3.1面向对象思想

```shell
1、面向对象是基于面向过程的编程思想

2、万物皆对象

3、对象具有唯一性

4、任何对象都具有一定的特征和行为；特征是事物的基本描述，行为是事物的功能

5、类是一组相关的属性和方法的集合，是一个抽象的概念

6、对象是类的具体存在

7、在一组相同或相似的对象中，抽取出共性的特征和行为，保留所关注的部分就是类的抽取

8、类是模板、图纸，通过类创造的对象就是实体
```

### 3.1.1 类

```java
格式：
	class 类名 {
		成员变量;
		成员方法;
	}

类名：
	大驼峰命名，首字母大写，见名知意
	
成员变量：
	定义在类中，方法外的变量，用来描述类的特征
	
成员方法：
	定义在类中，用来描述类的功能    
```

```java
class Person {
	String name;
	int age;
	char sex;

	public void eat() {
		System.out.println("吃");
	}

	public void sleep() {
		System.out.println("睡");
	}

	public void play() {
		System.out.println("玩");
	}
}
```

### 3.1.2 对象

```java
创建格式：
    类名 对象名 = new 类名(参数);

使用格式：
	使用成员变量：
		对象名.成员变量
    
	使用成员方法：
    	对象名.成员方法()
```

```java
Person person = new Person();

person.name = "Buffer";
person.age = 23;
person.sex = '男';

person.eat();
person.sleep();
person.play(); 
```

## 3.2 三大特性

### 3.2.1 封装

#### 3.2.1.1 概述

是指隐藏对象的属性和实现细节，仅对外提供公共访问方式

#### 3.2.1.2 JavaBean 规范化封装

```
1. 要求Java中的所有实体类成员变量全部私有化，最少提供一个无参数构造方法，对应成员变量实现setter和getter方法
2. JavaBean规范，是为了后期开发汇总更好的代码适配度，提高代码运行的统一性，能够满足框架的使用
3. JavaBean规范只是一个规范，而且是作为一个基础规范，操作都是可以使用快捷键来完成的！！！
```

### 3.2.2 继承

#### 3.2.2.1 概念

把多个类中相同的成员给提取出来定义到一个独立的类中。然后让这多个类和该独立的类产生一个关系，这多个类就具备了这些内容。这个关系就叫继承

```java
格式:
	class A extends B {
    
	}
```

#### 3.2.2.2 特点

```shell
1、Java为单继承，一个类只能有一个直接父类，但可以多级继承，属性和方法逐级叠加
2、构造方法只可服务于本类，不可继承。但是可以通过super()去访问父类的构造方法
3、private 修饰的属性和方法不能被继承
```

```java
public class TestSon {
	public static void main(String[] args) {		
		Son son = new Son();
		
        // Son继承自Father的age成员变量
		son.age = 20;
		// 报错，private修饰的成员变量无法被继承，只能在类中使用
		// son.weight = 80.0F;
		
        // Son继承自Father的age成员方法
		son.study();
		// 报错，private修饰的成员方法无法被继承，只能在类中使用
		// son.play();
	}
}

class Father{
	public int age;
	private float weight;

	private void play() {
		System.out.println("象棋，打牌---");
	}
	
	public void eat() {
		System.out.println("吃---");
	}
}

class Son extends Father{
	public int count;

	public void study() {
		System.out.println("学习---");
	}
}
```

#### 3.2.2.3 注意

子类构造方法执行前默认先执行父类的无参构造，用来初始化父类的属性 super()

```java
class Father {
	String name;

	public Father() {
		System.out.println("Father's Constrator be performed");
	}
}

class Son extends Father {
	int age;

	public Son() {
		System.out.println("Son's Constrator be performed");
	}
}

public class TestSon {
	public static void main(String[] args) {
		Son son = new Son();
	}
}
```

结果

```java
Father's Constrator be performed
Son's Constrator be performed
```

#### 3.2.2.4 优点

```
1、提高了代码的复用性
2、提高了代码的维护性
3、让类与类之间产生了一个关系，是多态的前提
```

#### 3.2.2.5 缺点

```
1、让类的耦合性增强。这样某个类的改变，就会影响打其他和该类相关的类
2、打破了封装性
```

### 3.2.3 多态

## 3.3 构造方法

### 3.3.1 概述

类中的特殊方法，用于创建对象

```java
格式：
    public PersonP() {}
```

### 3.3.2 构造方法的重载

```
public Person(String name){
    this.name = name;
}

public Person(String name, int age){
    this.name = name;
    this.age = age;
}
```

### 3.3.3 总结

```
1、构造方法的方法名与类名完全相同
2、构造方法没有返回值类型
3、创建对象时，触发构造方法的调用，不可手动调用
4、如果没有声明构造方法，编译器默认生成无参构造方法
5、如果定义了有参构造，编译器就不会创建无参构造
```

## 3.4 this关键字

this代表所在类的对象引用，即当前对象

### 3.4.1 作用

1、调用本类中的属性和方法

2、调用本类中的其他构造方法 this()

```java
class Rabbit {
    String color;
    int age;
    double weight;
    
    public Rabbit(String color) {
    	// 调用本类中的属性
		this.color = color;
        // 调用本类中的方法
        this.run();
	}

	public Rabbit(String color, int age, double weight) {
        // 调用本类中的其他构造方法
		this(color);	
		this.age = age;
		this.weight = weight;
	}
    
    public void run() {
        System.out.println("跑");
    }
}
```

【注意】

```shell
1、this() 只能用在构造方法中，只能出现一次，且必须在第一行
2、不能自己调用自己，不能相互调用
```

### 3.4.2 规范化 this()

```java
class Son {
	String name;
	int age;
	float salary;

	public Son() {
	}

	public Son(String name) {
        // 调用Son(String name, int age, float salary)
		this(name, 0, 0.0F);
	}

	public Son(String name, int age) {
        // 调用Son(String name, int age, float salary)
		this(name, age, 0.0F);
	}

	public Son(String name, int age, float salary) {
		this.name = name;
		this.age = age;
		this.salary = salary;
	}
}
```

## 3.5 super关键字

super代表所在类的父类的对象引用，即父类对象

### 3.5.1 作用

调用父类的属性和方法

调用父类的构造方法

```java
public class TestSon {
	public static void main(String[] args) {
		Son son = new Son(1); // Father's Construct：1
		son.test();
		son.show();
	}
}

class Father {
	public int num = 10;

    public Father() {}
    
    public Father(int num) {
        System.out.println("Father's Construct：" + num);
    }
    
	public void play() {
		System.out.println("下象棋");
	}
}

class Son extends Father {
	public int num = 20;

    // 调用父类的无参构造方法
    public Son() {
        super();
    }
    
    // 调用父类的有参构造方法
    public Son(int num) {
        super(num);
    }
    
	public void play() {
		System.out.println("玩电脑");
	}

	public void test() {
		play();	// 玩电脑
        
        // 调用父类的成员方法
		super.play();	// 下象棋
	}
	
	public void show() {
		int num = 30;
		System.out.println(num); // 30
		System.out.println(this.num); // 20
        
        // 调用父类的成员变量
		System.out.println(super.num); // 10
	}
}
```

【注意】子类构造方法默认调用父类的无参构造，且必须在代码的第一行

## 3.6 访问修饰符

### 3.6.1 private(私有)

```java
1、可以修饰成员变量和成员方法

2、被 private 修饰的变量和方法仅本类中可用，不能被继承

3、被 private 修饰的变量需要提供get、set方法供类外调用使用    

4、boolean类型的 get 方法比较特殊：
    
    public boolean isName(String name){
        return name;
	}
```

### 3.6.2 default(默认)

### 3.6.3 protected(受保护)

### 3.6.4 public(公共)

公开内容，只要存在对应的类对象，都可以通过类对象调用类内的public修饰的成员变量和成员方法

## 3.7 方法重载【Overload】

一个类或者接口中定义多个相同名称的方法

### 3.7.1 要求

```shell
1、方法名必须一致
2、参数必须不一致(个数，顺序，类型)	
3、与访问修饰符、返回值类型无关
```

```java
class Son {
	String name;
	int age;

	public Son() {
		super();
	}

    // 构造方法的重载
	public Son(String name, int age) {
		super();
		this.name = name;
		this.age = age;
	}

	public void play() {
		System.out.println("玩游戏");
	}

    // 成员方法的重载
	public void play(String name) {
		System.out.println(name + "玩游戏");
	}
}
```

### 3.7.2 优点

屏蔽使用差异，灵活、方便

## 3.8 方法重写【Overrid】

子类中方法声明与父类完全一致

### 3.8.1 要求

```shell
1、返回值类型，方法名，形参列表与父类一致
2、使用 @Override 注解来标识
3、重写方法的访问修饰符权限不能低于父类
	private < 默认(什么都不写) < protected < public
```

```java
public class TestSon {
	public static void main(String[] args) {
		Son son = new Son();
		son.eat();	// 吃菜
		son.play(); // 玩电脑
	}
}

class Father {
	String name;
	int age;	
	
	protected void eat() {
		System.out.println("吃肉");
	}
	protected void play() {
		System.out.println("下象棋");
	}
}

class Son extends Father {
	@Override
	public void eat() {
		System.out.println("吃菜");
	}
	
	@Override
	public void play() {
		System.out.println("玩电脑");
	}
}
```

### 3.8.2 优点

既沿袭了父类的方法名，又实现了子类的扩展

## 3.9 抽象类

不能实例化的类就是抽象类，用 abstract 修饰

### 3.9.1 构成

```java
abstract class 类名 {
    成员变量
    构造方法
    成员方法
        非抽象方法
        抽象方法
}
```

### 3.9.2 要求

```shell
1、抽象类和抽象方法必须用关键字abstract修饰
2、抽象类中不一定有抽象方法,但是有抽象方法的类一定是抽象类
3、抽象类不能实例化，因为 abstract 类中有 abstract 方法
4、抽象类的子类
	1.也是一个抽象类。
	2.是一个具体类(可以实例化)。这个类必须重写抽象类中的所有抽象方法。
```

```java
public class TestSon {
	public static void main(String[] args) {
		Son son = new Son();
		son.play();
	}
}

// 抽象类
abstract class Father {
	String name;
	int age;

	public Father() {
	}

	public void eat() {
		System.out.println("吃饭");
	}

    // 抽象方法
	abstract public void play();
}

class Son extends Father {
    // 抽象方法的重写
	@Override
	public void play() {
		System.out.println("玩游戏");
	}
}
```

## 3.10 匿名对象

### 3.10.1 概述

没有名字的对象，是对象的一种简化表示形式

### 3.10.2 使用情景

1、对象调用方法仅使用一次

2、作为实际参数传递

```java
public class TestDog{
	public static void main(String[] args) {
        // 对象调用方法仅使用一次
		new Dog().sleep();
		
        // 作为实际参数传递
		useDog(new Dog());
	}
	
	public static void useDog(Dog dog) {
		dog.sleep();
	}
}

class Dog {
	String name;
	int age;
	
	public void sleep() {
		System.out.println("小狗睡觉.....");
	}
}
```

### 3.10.3 优点

提高开发效率，简化代码结构

## 3.11 final关键字

### 3.11.1 特点

```shell
1、final 修饰的基本类型变量是一个常量(只能被赋值一次)，引用类型变量不可修改地址，如对象
2、final 修饰的方法不能被重写
3、final 修饰的类不能被继承
```

```java
public class TestSon {
	public static void main(String[] args) {
		// final 修饰的局部变量只能被赋值一次
		final int num = 1;

		final Son son = new Son();
		
		Son son1 = new Son();
		
		/* final 修饰的对象，其地址不能改变(不能被其他对象的地址赋值)
		 * 但指向的堆内空间不受影响
		 * 
		 * son = son1;
		 */ 
	}
}

// final修饰的类不能被继承
final class GrangPa {

}

class Father {
	// final修饰的成员方法不能被重写
	public final void play() {
		System.out.println("下象棋");
	}
}

class Son extends Father {
	// final修饰的成员变量必须初始化
	final int num = 10;
}
```

## 3.12 对象的创建过程

```java
1、内存中开辟父类和子类的对象空间
2、为父类的各个属性赋予初始值
3、执行父类的构造代码块
3、执行父类的构造方法
4、为自身各个属性赋予初始值
5、执行自身构造代码块
6、执行自身构造方法
7、将对象的地址赋值给变量
```

【注意】创建子类对象不会创建父类对象，但是会初始化父类和调用父类的构造方法
