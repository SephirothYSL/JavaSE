## 1. 类与类之间的调用

屏幕类：三个私有的成员变量，一个三参构造

```java
public class Screen {
	private String brand;
	private String name;
	private float size;

	public Screen() {
	}

	public Screen(String brand, String name, float size) {
		super();
		this.brand = brand;
		this.name = name;
		this.size = size;
	}

	public String getBrand() {
		return brand;
	}

	public void setBrand(String brand) {
		this.brand = brand;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public float getSize() {
		return size;
	}

	public void setSize(float size) {
		this.size = size;
	}
}
```

键盘类：两个成员变量，一个两参构造

```java
public class Keyboard {
	private String brand;
	private int keyCount;

	public Keyboard() {
		super();
	}

	public Keyboard(String brand, int keyCount) {
		super();
		this.brand = brand;
		this.keyCount = keyCount;
	}

	public String getBrand() {
		return brand;
	}

	public void setBrand(String brand) {
		this.brand = brand;
	}

	public int getKeyCount() {
		return keyCount;
	}

	public void setKeyCount(int keyCount) {
		this.keyCount = keyCount;
	}
}
```

电脑类：两个成员变量screen和keyboard，一个两参构造，一个show方法

```java
public class PC {
	private Screen screen;
	private Keyboard keyboard;

	public PC() {
		super();
	}

	public PC(Screen screen, Keyboard keyboard) {
		super();
		this.screen = screen;
		this.keyboard = keyboard;
	}

    // 展示屏幕和键盘的成员变量
	public void show() {
		System.out.println("屏幕品牌：" + screen.getBrand() + " 屏幕名字：" + screen.getName() + " 屏幕尺寸：" + screen.getSize());

		System.out.println("键盘品牌：" + keyboard.getBrand() + " 键帽个数：" + keyboard.getKeyCount());
	}

	public Screen getScreen() {
		return screen;
	}

	public void setScreen(Screen screen) {
		this.screen = screen;
	}

	public Keyboard getKeyboard() {
		return keyboard;
	}

	public void setKeyboard(Keyboard keyboard) {
		this.keyboard = keyboard;
	}
}
```

测试类

```java
public class TestPC {
	public static void main(String[] args) {
        
		PC pc = new PC(new Screen("三星","好屏幕",15.6F), new Keyboard("ikbc",87));
		
		pc.show();
		
		System.out.println("-------------------------------------");
		
		pc.setScreen(new Screen("苹果","更好的屏幕",16));
		
		pc.show();
		
		System.out.println("-------------------------------------");

		pc.setKeyboard(new Keyboard("阿米洛", 104));
		
		pc.show();
	}
}
```

## 2. 匿名对象

### 2.1 概述

没有名字的对象，是对象的一种简化表示形式

### 2.2 使用情景

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

### 2.3 优点

提高开发效率，简化代码结构

## 3. 继承

#### 3.1 概念

把多个类中相同的成员给提取出来定义到一个独立的类中。然后让这多个类和该独立的类产生一个关系，这多个类就具备了这些内容。这个关系叫继承。

```java
格式:
	class A extends B {
    
	}
```

#### 3.2 特点

```shell
1、Java为单继承，一个类只能有一个直接父类，但可以多级继承，属性和方法逐级叠加
2、构造方法只可服务于本类，不可继承。但是可以通过super()去访问
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

#### 3.3 优点

```shell
1、提高了代码的复用性
2、提高了代码的维护性
3、让类与类之间产生了一个关系，是多态的前提
```

#### 3.4 缺点

```shell
1、让类的耦合性增强。这样某个类的改变，就会影响打其他和该类相关的类
2、打破了封装性
```

