## 作业

### 第一题

员工类：

```java
public class Employee {
	String name;

	public Employee() {
		super();
	}

	public Employee(String name) {
		super();
		this.name = name;
	}

	/**
	 * 回家方法
	 * @param vehicle 传入一个交通工具，如果为空就走路回家，否则搭载对应的
	 * 交通工具回家
	 */
	public void goHome(Vehicle vehicle) {

		if (null == vehicle) {
			System.out.println("没钱还是走路回家吧~~~");
			return;
		}

		System.out.println(name + "正在乘坐" + vehicle.type + "回家");
		vehicle.run();
	}

	/**
	 * 买交通工具方法
	 * @param money 传入金额
	 * @return 返回一种交通工具，如果钱不够返回空值
	 */
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
}
```

交通工具类

```java
public class Vehicle {
	String type;
	double price;
	int speed;

	public void run() {
		System.out.println("Vehicle run！！！");
	}
}

/*
 * 小汽车类
 */
class Car extends Vehicle {
	String brand;

	@Override
	public void run() {
		System.out.println("Car run！！！");
	}
}

/*
 * 公交车类
 */
class Bus extends Vehicle {
	int seatNum;

	@Override
	public void run() {
		System.out.println("Bus run！！！");
	}
}

/*
 * 自行车类
 */
class Bike extends Vehicle {
	String color;

	@Override
	public void run() {
		System.out.println("Bike run！！！");
	}
}
```

测试类

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

		Employee employee2 = new Employee("Banlance");
		Vehicle veh = employee2.buyVehicle(100);
		employee2.goHome(veh);	

		// 拆箱
		if (veh instanceof Bike) {
			Bike bike1 = (Bike) veh;
			System.out.println("自行车的颜色：" + bike1.color);
		} else if (veh instanceof Bus) {
			Bus bus1 = (Bus) veh;
			System.out.println("公交车的座位数：" + bus1.seatNum);	
		} else if (veh instanceof Car) {
			Car car1 = (Car) veh;
			System.out.println("小汽车的品牌：" + car1.brand);
		}
	}
}
```

结果

```java
Buffer正在乘坐小汽车回家
Car run！！！
Buffer正在乘坐公交车回家 
Bus run！！！
Banlance正在乘坐公交车回家
Bus run！！！
公交车的座位数：16
```

### 第二题

```java
public class Test {

	public static void main(String[] args) {
		Super sup = new Sub();

		sup.method1(); 
		sup.method2(); 

		Sub sub = (Sub) sup;

		sub.method1(); 
		sub.method2(); 
	}
}

class Super {
	public static void method1() {
		System.out.println("Super method1");
	}

	public void method2() {
		System.out.println("Super method2");
	}
}

class Sub extends Super {
	public static void method1() {
		System.out.println("Sub method1");
	}

	@Override
	public void method2() {
		System.out.println("Sub method2");
	}
}
```

结果

```java
Super method1
Sub method2
Sub method1
Sub method2
```

### 第三题

```java
public class Task2 {
	public static void main(String[] args) {
		Myclass mc1 = new Myclass();
		System.out.println(mc1.i);

		Myclass mc2 = new Myclass(10);
		System.out.println(mc2.i);
	}
}

class Myclass {
	static int i = 10;

	static {
		i = 20;
		System.out.println("In static");
	}

	public Myclass() {
		System.out.println("Myclass()");
	}

	public Myclass(int i) {
		System.out.println("Myclass(int)");
		this.i = i;
	}
}
```

结果

```java
In static
Myclass()
20
Myclass(int)
10
```

