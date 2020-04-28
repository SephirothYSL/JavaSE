# 面向对象

## 1. 构造方法

### 1.1 作用

类中的特殊方法，用于创建对象

```java
格式：
    public Person(){}
```

### 1.2 对象的创建过程

```shell
1、内存中开辟对象空间
2、为各个属性赋予初始值
3、执行构造方法中的代码
4、将对象的地址赋值给变量
```

### 1.3 构造方法的重载

```java
public Person(String name){
    this.name = name;
}

public Person(String name, int age){
    this.name = name;
    this.age = age;
}
```

### 1.4 总结

```shell
1、构造方法的方法名与类名完全相同
2、构造方法没有返回值类型
3、创建对象时，触发构造方法的调用，不可手动调用
4、如果没有声明构造方法，编译器默认生成无参构造方法
5、如果定义了有参构造，编译器就不会创建无参构造
```

## 2. this关键字

### 2.1 概述

this代表所在类的对象引用，即当前对象

### 2.2 作用

1、调用本类中的属性和方法

2、调用本类中的其他构造方法：this()

```java
public Rabbit(String color) {
    // 调用本来中的属性
		this.color = color;
	}

	public Rabbit(String color, int age, double weight) {
        // 调用本类中的其他构造方法
		this(color);
		
		this.age = age;
		this.weight = weight;
	}
```

【注意】this()不能使用在普通方法中，只能写在构造方法中，且必须是构造方法中的第一条语句

## 3. 反编译

```java
javap -c -l -private 类名.class
```

## 4. 访问(权限)修饰符

### 4.1 private(私有)

```java
1、可以修饰成员变量和成员方法

2、被private修饰的变量和方法仅本类中可用

3、被private修饰的变量需要提供get、set方法供类外调用使用    

4、boolean类型的 get 方法比较特殊：
    
    public boolean isName(String name){
        return name;
	}
```

### 4.2 public(公共)

公开内容，只要存在对应的类对象，都可以通过类对象调用类内的public修饰的成员变量和成员方法

### 4.3 default

### 4.4 protected

## 5. 面向对象三大特征

### 5.1 封装

#### 5.1.1 概述

是指隐藏对象的属性和实现细节，仅对外提供公共访问方式。

#### 5.1.2 JavaBean 规范化封装

```shell
1. 要求Java中的所有实体类成员变量全部私有化，最少提供一个无参数构造方法，对应成员变量实现setter和getter方法
2. JavaBean规范，是为了后期开发汇总更好的代码适配度，提高代码运行的统一性，能够满足框架的使用
3. JavaBean规范只是一个规范，而且是作为一个基础规范，操作都是可以使用快捷键来完成的！！！
```

### 5.2 继承

### 5.3 多态

## 6. 类与类之间的调用

汽车类：

```java
public class Car {
    // 成员变量：品牌 速度 价格
	private String brand;
	private int speed;
	private double price;

    // 无参构造方法
	public Car() {
		super();
	}

    // 有参构造方法
	public Car(String brand, int speed, double price) {
		super();
		this.brand = brand;
		this.speed = speed;
		this.price = price;
	}

    // 跑方法，当速度低于60说明发生故障，需要到修车厂维修
	public void run() throws InterruptedException {
		if (speed < 60) {
			System.out.println("车好像坏了，跑得太慢---");
		} else {
			System.out.println("价值" + price + "元的" + brand + "牌的车正在以每小时" + speed + "迈的速度前进...");
			Thread.sleep(500);
		}

	}

	public String getBrand() {
		return brand;
	}

	public void setBrand(String brand) {
		this.brand = brand;
	}

	public int getSpeed() {
		return speed;
	}

	public void setSpeed(int speed) {
		this.speed = speed;
	}

	public double getPrice() {
		return price;
	}

	public void setPrice(double price) {
		this.price = price;
	}

}
```

修车厂类：

```java
public class Garage {
    // 成员变量
	private String name;
	private String address;
	private String teleNumber;

    // 无参构造方法
	public Garage() {
		super();
	}

    // 有参构造方法
	public Garage(String name, String address, String teleNumber) {
		super();
		this.name = name;
		this.address = address;
		this.teleNumber = teleNumber;
	}

    // 修车类，传入一个Car类型的变量，当speed<60时就修车，调用setSpeed方法设置为80
	public void repair(Car car) throws InterruptedException {
		if (car.getSpeed() < 60) {
			System.out.println("修车ing---");
			
			Thread.sleep(1000);
			
			car.setSpeed(80);
			System.out.println("车修好了，收费1000");
		} else {
			System.out.println("车没毛病，你有毛病///");
		}
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public String getAddress() {
		return address;
	}

	public void setAddress(String address) {
		this.address = address;
	}

	public String getTeleNumber() {
		return teleNumber;
	}

	public void setTeleNumber(String teleNumber) {
		this.teleNumber = teleNumber;
	}

}
```

Test类：

```java
public class TestCar {
	public static void main(String[] args) throws InterruptedException {
        // 创建汽车类
		Car car = new Car("奔驰", 100, 640000.0);

		for (int i = 0; i < 10; i++) {
			car.run();
		}

		Thread.sleep(1000);
		System.out.println("车胎炸了，boom！！！");
		car.setSpeed(50);

		car.run();
		Thread.sleep(1000);

        // 创建修车厂类
		Garage garage = new Garage("王子修车厂", "北京市东城区王府井大街138号", "1383838438");

        // 调用修车方法
		garage.repair(car);

		for (int i = 0; i < 10; i++) {
			car.run();
		}
	}
}
```

