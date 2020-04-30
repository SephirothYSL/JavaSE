## 1. 继承

子类构造方法执行前默认先执行父类的无参构造方法

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

```shell
Father's Constrator be performed
Son's Constrator be performed
```

【注意】Son 的构造方法中编译器默认生成 super(); 用来调用父类的构造方法，目的是为了初始化父类字段，因为子类可能会用到

## 2. 方法重写【Override】

子类中方法声明与父类完全一致

### 2.1 要求

```shell
1、返回值类型，方法名，形参列表与父类一致
2、使用@Override注解来标识
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

### 2.2 优点

既沿袭了父类的方法名，又实现了子类的扩展

## 3. 抽象类

不能实例化的类就是抽象类，用 abstract 修饰

### 3.1 构成

```java
abstract class 类名 {
    成员变量
    构造方法
    成员方法
        非抽象方法
        抽象方法
}
```

### 3.2 要求

```shell
1、抽象类和抽象方法必须用关键字abstract修饰
2、抽象类中不一定有抽象方法,但是有抽象方法的类一定是抽象类
3、抽象类不能实例化，因为 abstract 类中有 abstract 方法
4、抽象类的子类
	也是一个抽象类。
	是一个具体类。这个类必须重写抽象类中的所有抽象方法。(可以实例化)
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

## 4. 方法重载【Overload】

一个类或者接口中定义多个相同名称的方法

### 4.1 要求

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

### 4.2 优点

屏蔽使用差异，灵活、方便

## 5. this关键字

### 5.1 this关键字可以在构造方法中调用其它构造方法

```java
class Son {
	String name;
	int age;
	float salary;

	public Son() {
	}

	public Son(String name) {
        // 调用Son()
		this();
		this.name = name;
	}

	public Son(String name, int age, float salary) {
        // 调用Son(String name)
		this(name);
		this.age = age;
		this.salary = salary;
	}
}
```

【注意】

```shell
1、this()只能在构造方法中使用
2、this()只能在第一行
3、构造方法中不能同时出现两个this()，因为2
4、不能自己调用自己，不能相互调用
```

### 5.2 规范化this()

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

## 6. super关键字

### 6.1 调用父类的属性和方法

```java
package code.superSon;

/*
 * 测试super关键字
 */
public class TestSon {
	public static void main(String[] args) {
		Son son = new Son();
		son.test();
		son.show();
	}
}

class Father {
	public int num = 10;

	public void play() {
		System.out.println("下象棋");
	}
}

class Son extends Father {
	public int num = 20;

	public void play() {
		System.out.println("玩电脑");
	}

	public void test() {
		play();	// 玩电脑
		super.play();	// 下象棋
	}
	
	public void show() {
		int num = 30;
		System.out.println(num); // 30
		System.out.println(this.num); // 20
		System.out.println(super.num); // 10
	}
}
```

### 6.2 调用父类的构造方法

默认调用父类的无参构造，且必须在代码的第一行

```java
class Father {
	private String name;

	public Father() {
		System.out.println("Father's Constrator be performed");
	}
    
    public Father(String name) {
        System.out.println("Father's Constrator be performed with name");
    }
}

class Son extends Father {
	private int age;

	public Son() {
        super();
		System.out.println("Son's Constrator be performed");
	}
    
    public Son(String name, int age) {
        super(name);
        this.age = age;
		System.out.println("Son's Constrator be performed with name and age");
	}
}

public class TestSon {
	public static void main(String[] args) {
		Son son = new Son();
	}
}
```

【注意】super() 和this() 代码不能共存(都必须在首行)，但是实际效果其实是可以的，如果不写 super() 也会自动调用

## 7. final关键字

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

