## 1. static关键字的应用

static关键字和构造代码块结合，用来做对象创建个数的计数器

Vip类：

```java
public class Vip {
	private int id;
	private String name;
	private int age;
	private String address;

    // 定义私有静态计数器
	private static int count = 1;

    // 构造代码块，每当创建对象的时候调用，给id赋值并自增
	{
		id = count;
		count++;
	}

	public Vip() {
		super();
	}

	public Vip(String name) {
		super();
		this.name = name;
	}

	public Vip(String name, int age) {
		super();
		this.name = name;
		this.age = age;
	}

	public Vip(String name, int age, String address) {
		super();
		this.name = name;
		this.age = age;
		this.address = address;
	}

	public int getId() {
		return id;
	}

	public void setId(int id) {
		this.id = id;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public String getAddress() {
		return address;
	}

	public void setAddress(String address) {
		this.address = address;
	}

	@Override
	public String toString() {
		return "Vip [id=" + id + ", name=" + name + ", age=" + age + ", address=" + address + "]";
	}
}
```

测试类

```java
public class TestVip {
	public static void main(String[] args) {
		Vip vip1 = new Vip();
		Vip vip2 = new Vip("Buffer");
		Vip vip3 = new Vip("Balance", 21);
		Vip vip4 = new Vip("Smoot", 22, "商丘");

		System.out.println(vip1);
		System.out.println(vip2);
		System.out.println(vip3);
		System.out.println(vip4);
	}
}
```

结果

```java
Vip [id=1, name=null, age=0, address=null]
Vip [id=2, name=Buffer, age=0, address=null]
Vip [id=3, name=Balance, age=21, address=null]
Vip [id=4, name=Smoot, age=22, address=商丘]
```

实现了每个对象的id都不同，并且呈自增的效果

## 2. 接口

接口是一系列方法的声明，是一些方法特征的集合，**一个接口只有方法的特征没有方法的实现，因此这些方法可以在不同的地方被不同的类实现，而这些实现可以具有不同的行为（功能）**。

```java
声明格式：
    interface 接口名 {
    	常量;
    	抽象方法;
	}

调用格式：
    class 类名 implements 接口名 {
        
    }
```

### 2.1 特点

```java
1、接口中的成员变量只能是常量，定义时必须初始化。默认修饰符：public static final
2、接口中没有构造方法，因为接口不能实例化对象
3、接口中的成员方法只能是抽象方法，没有方法体。默认修饰福：public abstract
4、接口的实现类必须重写接口中方法，或者是一个抽象类(可以重写也可以不重写接口中的方法)
```

### 2.2 接口的声明和实现

```java
interface play{
	// 常量，缺省修饰符：public static final
	int time = 10;
		
	// 抽象方法，缺省修饰符：public abstract
	void geme();
}

public class TestInterface3 implements play{

    // 重写接口中的方法
	@Override
	public void geme() {
		System.out.println("玩游戏");
	}

}
```

【注意】接口的实现类必须重写接口中的方法

### 2.3 抽象类实现接口

```java
interface servlet {
	void init();

	void service();
}

abstract class BaseServlet implements servlet {
    // 重写init()方法
	@Override
	public void init() {
		System.out.println("初始化");
	}
}

class MyServlet extends BaseServlet {

	@Override
	public void service() {
		System.out.println("服务方法");
	}
}

public class Test {
	public static void main(String[] args) {
		new MyServlet().init();
		new MyServlet().service();
	}
}
```

【注意】抽象类实现接口，可以选择性重写也可以不重写接口中的方法

### 2.4 类的接口多实现

```java
interface Play {
	void geme();
}

interface Eat {
	void noodles();
}

public class TestInterface3 implements Play, Eat {

    // 重写Play类中的方法
	@Override
	public void geme() {
		System.out.println("玩游戏");
	}

    // 重写Eat类中的方法
	@Override
	public void noodles() {
		System.out.println("吃面条");
	}

}
```

【注意】接口的实现类必须重写所有接口中的方法

### 2.5 接口的继承

```java
interface Eat {
	void noodles();
}

interface Play {
	void happy();
}

// 单继承
interface Person extends Play {

}

// 多继承
interface Animal extends Play, Eat {

}

// 实体类实现Animal接口，重写所有方法
class Biology implements Animal {

	@Override
	public void happy() {
		System.out.println("玩得开心");
	}

	@Override
	public void noodles() {
		System.out.println("面条好吃");
	}
	
}

public class Test {
	public static void main(String[] args) {
		Biology biology = new Biology();
		biology.happy();	// 玩得开心
		biology.noodles();	// 面条好吃
	}
}
```

【注意】接口之间可以单继承，也可以多继承

### 2.6 jdk1.8新特性：default接口

```java
interface Function {
	void test();

	default void testDefault() {
		System.out.println("default修饰的接口可以有方法体");
	}
}

// default 修饰的接口可以不被重写
class Base implements Function {

	@Override
	public void test() {
		System.out.println("Base类重写Function接口中的方法");
	}
}

// default 修饰的接口也可以重写
class Boost implements Function {

	@Override
	public void test() {
		System.out.println("Boost类重写Function接口中的方法");
	}

	@Override
	public void testDefault() {
		System.out.println("Boost类重写Function接口中的default方法");
	}
}

public class TestInterface2 {
	public static void main(String[] args) {
		Base base = new Base();
		Boost boost = new Boost();

		base.test();		// Base类重写Function接口中的方法
		base.testDefault();	// default修饰的接口可以有方法体
		boost.test();		// Boost类重写Function接口中的方法
		boost.testDefault();// Boost类重写Function接口中的default方法
	}
}
```

【注意】default修饰的接口可以不被重写

### 2.7 总结

```shell
1、接口中只有全局常量和抽象方法，所有不能实例化
2、接口的实现类必须重写所有方法，或者是个抽象类
3、接口可以多实现
4、接口可以单继承，也可以多继承
```

## 3. 多态

**二者具有直接或间接的继承关系时，父类引用指向子类对象，从而产生多种形态；接口的引用指向实现接口的类对象也是多态**

### 3.1 特点

多态场景下，父类引用调用方法，如果被子类重写过，优先执行子类重写过后的方法

```java
public class TestCar {
	public static void main(String[] args) {
        // 父类引用指向子类对象
		Vehicle vehicle = new Car();
        
        // 优先执行子类重写过的方法
		vehicle.run();	// Car run！！！
	}
}

class Vehicle {
	public void run() {
		System.out.println("Vehicle run！！！");
	}
}

class Car extends Vehicle {
	@Override
	public void run() {
		System.out.println("Car run！！！");
	}
}
```

### 3.2 应用场景一

使用父类作为方法形参实现多态，使方法参数的类型更为宽泛

```java
public class TestCar {
	public static void main(String[] args) {        
        Vehicle vehicle = new Car();
		vehicle.type = "小汽车";
        
		Bike bike = new Bike();
		bike.type = "自行车";
		
		Bus bus = new Bus();
		bus.type = "公交车";
		
		Employee employee = new Employee("Buffer");
		employee.goHome(vehicle);
		employee.goHome(bus);
	}
}

class Vehicle {
	String type;

	public void run() {
		System.out.println("Vehicle run！！！");
	}
}

class Bus extends Vehicle {
	@Override
	public void run() {
		System.out.println("Bus run！！！");
	}
}

class Bike extends Vehicle {
	@Override
	public void run() {
		System.out.println("Bike run！！！");
	}
}
```

结果

```java
Buffer正在乘坐小汽车回家
Car run！！！
Buffer正在乘坐公交车回家
Bus run！！！
```

### 3.3 应用场景二

使用父类作为方法返回值实现多态，使方法可以返回不同子类对象

```java
public Vehicle buyVehicle(int money) {
		Vehicle vehicle = null;

		if (money >= 100) {
			Bus bus = new Bus();
			bus.speed = 60;
			bus.price = 1230000.0;
			bus.seatNum = 16;
			bus.type = "公交车";
			vehicle = bus;

		} else if (money >= 30) {
			Car car = new Car();
			car.price = 310000.0;
			car.speed = 90;
			car.type = "小汽车";
			car.brand = "BMW";
			vehicle = car;

		} else if (money >= 1) {
			Bike bike = new Bike();
			bike.type = "捷安特自行车";
			bike.speed = 40;
			bike.price = 2000.0;
			bike.color = "红色";
			vehicle = bike;
		}

		return vehicle;
	}
```

### 3.4 向上装箱与向下拆箱

```java
class Animal{}

class Cat extends Animal{}

class Dog extends Animal{}

class Fish extends Animal {}

public class Test {
	public static void main(String[] args) {
		showAnimal(new Animal());	// code.polymorphic.animal.Animal@7852e922
		// 向上转型
		showAnimal(new Cat());	// code.polymorphic.animal.Cat@4e25154f
		// 向上转型
		showAnimal(new Dog());	// code.polymorphic.animal.Dog@70dea4e
		// 向上转型
		showAnimal(new Fish());	// code.polymorphic.animal.Fish@5c647e05
		
		System.out.println("----------------------");
		
		Animal animal = getAnimal();
		// 向下转型
		Cat cat = (Cat) getCat();
		// 向下转型
		Dog dog = (Dog) getDog();
		// 向下转型
		Fish fish = (Fish) getFish();
		
		System.out.println(animal);	// code.polymorphic.animal.Animal@33909752
		System.out.println(cat);	// code.polymorphic.animal.Cat@55f96302
		System.out.println(dog);	// code.polymorphic.animal.Dog@3d4eac69
		System.out.println(fish);	// code.polymorphic.animal.Fish@42a57993
	}
	
	/**
	 * 展示动物
	 * @param animal
	 */
	public static void showAnimal(Animal animal) {
		System.out.println(animal);
	}
	
	/**
	 * 得到动物
	 * @return 返回一个Animal对象
	 */
	public static Animal getAnimal() {
		return new Animal();
	}
	
	/**
	 * 得到猫
	 * @return 返回一个Cat对象
	 */
	public static Animal getCat() {
		return new Cat();
	}
	
	/**
	 * 得到狗
	 * @return 返回一个Dog对象
	 */
	public static Animal getDog() {
		return new Dog();
	}
	
	/**
	 * 得到鱼
	 * @return 返回一个Fish对象
	 */
	public static Animal getFish() {
		return new Fish();
	}
}
```

