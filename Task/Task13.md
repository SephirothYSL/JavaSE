## 1. 类之间的调用

员工类

```java
class Employee {
	//员工编号
	private String employeeId;
	//姓名
	private String name;
	//年龄
	private int age;
	
	//构造方法
	public Employee() {}
	
	public Employee(String employeeId, String name, int age) {
		super();
		this.employeeId = employeeId;
		this.name = name;
		this.age = age;
	}

	//getXxx()/setXxx()
	public String getEmployeeId() {
		return employeeId;
	}
	
	public void setEmployeeId(String employeeId) {
		this.employeeId = employeeId;
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
	
	//显示所有成员信息的方法
	public void show() {
		System.out.println("员工编号是："+employeeId+"的这个人是："+name+"的年龄是："+age);
	}
}
```

公司类

```java
public class Company {
	private String name;
	private String address;
	private String teleNumber;

	public Company() {
		super();
	}

	public Company(String name, String address, String teleNumber) {
		super();
		this.name = name;
		this.address = address;
		this.teleNumber = teleNumber;
	}

	public void joinUs(Employee employee) {
		if (employee.getAge() > 18) {
			System.out.println("欢迎加入我们" + this.name + "公司，我们的地址是：" + this.address + "，我们的联系方式为：" + this.teleNumber);
		} else {
			System.out.println("年龄太小了弟弟，好好学习吧");
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

测试类

```java
public class TestEmployee {

	public static void main(String[] args) {
		Employee employee = new Employee("001","Buffer",20);
		
		employee.show();
		
		System.out.println("找一份工作");
		
		Company company = new Company("红星拖拉机厂","南宁罗志祥","1383838438");

		company.joinUs(employee);
		
	}

}
```

## 2. 十二生肖规范版

```java
public class TestChineseZodiac {
	public static void main(String[] args) {
		Mouse mouse = new Mouse(12.0,20.0,2);

		System.out.println("鼠的年龄：" + mouse.getAge() + " 鼠的长度：" + mouse.getLength() + " 鼠的重量：" + mouse.getWeight());

		mouse.eat();
		mouse.sleep();
		mouse.burrow();
		
		System.out.println();

		Cattle cattle = new Cattle(4,300.0,"花花牛");

		System.out.println("牛的年龄：" + cattle.getAge() + " 牛的品种：" + cattle.getBreed() + " 牛的重量：" + cattle.getWeight());
				
		cattle.eat();
		cattle.sleep();
		cattle.work();

		System.out.println();
		
		Tiger tiger = new Tiger("华南虎",6,"虎皮色");

		System.out.println("虎的年龄：" + tiger.getAge() + " 虎的品种：" + tiger.getBreed() + " 虎的颜色" + tiger.getColor());

		tiger.eat();
		tiger.sleep();
		tiger.catchAndHunt();

		System.out.println();
		
		Rabbit rabbit = new Rabbit("白色",3,20.0);

		System.out.println("兔的年龄：" + rabbit.getAge() + " 兔的颜色：" + rabbit.getColor() + " 兔的重量：" + rabbit.getWeight());
	
		rabbit.eat();
		rabbit.sleep();
		rabbit.run();
		
		System.out.println();
		
		Dragon dragon = new Dragon();

		dragon.setAge(1000);
		dragon.setColor("黑色");
		dragon.setLength(40);

		System.out.println("龙的年龄：" + dragon.getAge() + " 龙的颜色：" + dragon.getColor() + " 龙的长度：" + dragon.getLength());

		dragon.eat();
		dragon.fly();
		dragon.sleep();

		System.out.println();
		
		Snake snake = new Snake();

		snake.setAge(10);
		snake.setColor("青色");
		snake.setWeight(20.0);

		System.out.println("蛇的年龄：" + snake.getAge() + " 蛇的颜色：" + snake.getColor() + " 蛇的重量：" + snake.getWeight());
	
		snake.eat();
		snake.sleep();
		snake.climb();

		System.out.println();
		
		Horse horse = new Horse();

		horse.setAge(10);
		horse.setColor("黄色");
		horse.setWeight(200.0);

		System.out.println("马的年龄：" + horse.getAge() + " 马的颜色：" + horse.getColor() + " 马的重量：" + horse.getWeight());
	
		horse.run();
		horse.eat();
		horse.sleep();

		System.out.println();
		
		Sheep sheep = new Sheep();

		sheep.setAge(5);
		sheep.setColor("白色");
		sheep.setWeight(200.0);

		System.out.println("羊的年龄：" + sheep.getAge() + " 羊的颜色：" + sheep.getColor() + " 羊的重量：" + sheep.getWeight());
	
		sheep.eat();
		sheep.sleep();
		sheep.run();

		System.out.println();
		
		Monkey monkey = new Monkey();

		monkey.setAge(3);
		monkey.setBreed("猴哥");
		monkey.setColor("黄色");

		System.out.println("猴的年龄：" + monkey.getAge() + " 猴的颜色：" + monkey.getColor() + " 猴的种类：" + monkey.getBreed());
	
		monkey.eat();
		monkey.sleep();
		monkey.climb();

		System.out.println();
		
		Chook chook = new Chook();

		chook.setBreed("打鸣鸡");
		chook.setSex('公');
		chook.setWeight(15);

		System.out.println("鸡的性别：" + chook.getSex() + " 鸡的品种：" + chook.getBreed() + " 鸡的重量：" + chook.getWeight());
	
		chook.eat();
		chook.sleep();
		chook.jump();

		System.out.println();
		
		Dog dog = new Dog();

		dog.setAge(5);
		dog.setBreed("中华田园犬");
		dog.setColor("黄色");

		System.out.println("狗的年龄：" + dog.getAge() + " 狗的颜色：" + dog.getColor() + " 狗的品种：" + dog.getBreed());
	
		dog.eat();
		dog.sleep();
		dog.run();

		System.out.println();
		
		Pig pig = new Pig("家猪",2,500.0);

		System.out.println("猪：" + pig.getAge() + " " + pig.getBreed() + " " + pig.getWeight());

		pig.eat();
		pig.sleep();
		pig.arch();
		
		System.out.println();		
	}
}

class Animals {
}

class Mouse {
	private double length;
	private double weight;
	private int age;

	public Mouse() {
		super();
	}

	public Mouse(double length, double weight, int age) {
		super();
		this.length = length;
		this.weight = weight;
		this.age = age;
	}

	public void eat() {
		System.out.println("老鼠吃");
	}

	public void sleep() {
		System.out.println("老鼠睡");
	}

	public void burrow() {
		System.out.println("老鼠打洞");
	}

	public double getLength() {
		return length;
	}

	public void setLength(double length) {
		this.length = length;
	}

	public double getWeight() {
		return weight;
	}

	public void setWeight(double weight) {
		this.weight = weight;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}
}

class Cattle {
	private int age;
	private double weight;
	private String breed;

	public Cattle() {
		super();
	}

	public Cattle(int age, double weight, String breed) {
		super();
		this.setAge(age);
		this.setWeight(weight);
		this.setBreed(breed);
	}

	public void eat() {
		System.out.println("牛吃");
	}

	public void sleep() {
		System.out.println("牛睡");
	}

	public void work() {
		System.out.println("牛干活");
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public double getWeight() {
		return weight;
	}

	public void setWeight(double weight) {
		this.weight = weight;
	}

	public String getBreed() {
		return breed;
	}

	public void setBreed(String breed) {
		this.breed = breed;
	}
}

class Tiger {
	private String breed;
	private int age;
	private String color;

	public Tiger() {
		super();
	}

	public Tiger(String breed) {
		super();
		this.setBreed(breed);
	}

	public Tiger(String breed, int age, String color) {
		this(breed);
		
		this.setAge(age);
		this.setColor(color);
	}

	public void eat() {
		System.out.println("老虎吃肉肉");
	}

	public void sleep() {
		System.out.println("不睡也成");
	}

	public void catchAndHunt() {
		System.out.println("逮虾户");
	}

	public String getBreed() {
		return breed;
	}

	public void setBreed(String breed) {
		this.breed = breed;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public String getColor() {
		return color;
	}

	public void setColor(String color) {
		this.color = color;
	}
}

class Rabbit extends Animals {
	private String color;
	private int age;
	private double weight;

	public Rabbit() {
		super();
	}

	public Rabbit(String color) {
		super();
		this.setColor(color);
	}

	public Rabbit(String color, int age, double weight) {
		this(color);
		
		this.setAge(age);
		this.setWeight(weight);
	}

	public void eat() {
		System.out.println("兔子吃胡萝卜");
	}

	public void sleep() {
		System.out.println("兔子不睡我不睡");
	}

	public void run() {
		System.out.println("跑得贼快");
	}

	public String getColor() {
		return color;
	}

	public void setColor(String color) {
		this.color = color;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public double getWeight() {
		return weight;
	}

	public void setWeight(double weight) {
		this.weight = weight;
	}
}

class Dragon {
	private int age;
	private String color;
	private double length;

	public Dragon() {
		super();
	}

	public Dragon(int age, String color, double length) {
		super();
		this.age = age;
		this.color = color;
		this.length = length;
	}

	public void fly() {
		System.out.println("龙飞");
	}

	public void eat() {
		System.out.println("恶龙咆哮");
	}

	public void sleep() {
		System.out.println("沉睡千年");
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public String getColor() {
		return color;
	}

	public void setColor(String color) {
		this.color = color;
	}

	public double getLength() {
		return length;
	}

	public void setLength(double length) {
		this.length = length;
	}
}

class Snake {
	private int age;
	private String color;
	private double weight;

	public Snake() {
		super();
	}

	public Snake(int age, String color, double weight) {
		super();
		this.setAge(age);
		this.setColor(color);
		this.setWeight(weight);
	}

	public void climb() {
		System.out.println("蛇只会爬");
	}

	public void eat() {
		System.out.println("蛇吃兔兔");
	}

	public void sleep() {
		System.out.println("蛇冬眠");
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public String getColor() {
		return color;
	}

	public void setColor(String color) {
		this.color = color;
	}

	public double getWeight() {
		return weight;
	}

	public void setWeight(double weight) {
		this.weight = weight;
	}
}

class Horse {
	private int age;
	private String color;
	private double weight;

	public Horse() {
		super();
	}

	public Horse(int age, String color, double weight) {
		super();
		this.setAge(age);
		this.setColor(color);
		this.setWeight(weight);
	}

	public void run() {
		System.out.println("马跑得挺快");
	}

	public void eat() {
		System.out.println("马吃野菜");
	}

	public void sleep() {
		System.out.println("马站着睡觉");
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public String getColor() {
		return color;
	}

	public void setColor(String color) {
		this.color = color;
	}

	public double getWeight() {
		return weight;
	}

	public void setWeight(double weight) {
		this.weight = weight;
	}
}

class Sheep {
	private int age;
	private String color;
	private double weight;

	public Sheep() {
		super();
	}

	public Sheep(int age, String color, double weight) {
		super();
		this.setAge(age);
		this.setColor(color);
		this.setWeight(weight);
	}

	public void eat() {
		System.out.println("羊吃草");
	}

	public void sleep() {
		System.out.println("sleep --> sheep");
	}

	public void run() {
		System.out.println("羊跑得不快，毛有点多");
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public String getColor() {
		return color;
	}

	public void setColor(String color) {
		this.color = color;
	}

	public double getWeight() {
		return weight;
	}

	public void setWeight(double weight) {
		this.weight = weight;
	}
}

class Monkey {
	private int age;
	private String breed;
	private String color;

	public Monkey() {
		super();
	}

	public Monkey(int age, String breed, String color) {
		super();
		this.setAge(age);
		this.setBreed(breed);
		this.setColor(color);
	}

	public void climb() {
		System.out.println("猴子爬树");
	}

	public void eat() {
		System.out.println("猴子偷桃");
	}

	public void sleep() {
		System.out.println("猴子挂树上睡");
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public String getBreed() {
		return breed;
	}

	public void setBreed(String breed) {
		this.breed = breed;
	}

	public String getColor() {
		return color;
	}

	public void setColor(String color) {
		this.color = color;
	}
}

class Chook {
	private String breed;
	private char sex;
	private double weight;

	public Chook() {
		super();
	}

	public Chook(String breed, char sex, double weight) {
		super();
		this.setBreed(breed);
		this.setSex(sex);
		this.setWeight(weight);
	}

	public void eat() {
		System.out.println("鸡肉吃着还行，做着挺麻烦");
	}

	public void sleep() {
		System.out.println("鸡起得早，打鸣");
	}

	public void jump() {
		System.out.println("鸡会跳");
	}

	public String getBreed() {
		return breed;
	}

	public void setBreed(String breed) {
		this.breed = breed;
	}

	public char getSex() {
		return sex;
	}

	public void setSex(char sex) {
		this.sex = sex;
	}

	public double getWeight() {
		return weight;
	}

	public void setWeight(double weight) {
		this.weight = weight;
	}
}

class Dog {
	private int age;
	private String breed;
	private String color;

	public Dog() {
		super();
	}

	public Dog(int age, String breed, String color) {
		super();
		this.setAge(age);
		this.setBreed(breed);
		this.setColor(color);
	}

	public void eat() {
		System.out.println("狗吃屎");
	}

	public void sleep() {
		System.out.println("狗作息很规律");
	}

	public void run() {
		System.out.println("狗跑得挺快");
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public String getBreed() {
		return breed;
	}

	public void setBreed(String breed) {
		this.breed = breed;
	}

	public String getColor() {
		return color;
	}

	public void setColor(String color) {
		this.color = color;
	}
}

class Pig {
	private String breed;
	private int age;
	private double weight;

	public Pig() {
		super();
	}

	public Pig(String breed, int age, double weight) {
		super();
		this.setBreed(breed);
		this.setAge(age);
		this.setWeight(weight);
	}

	public void eat() {
		System.out.println("猪吃吃吃");
	}

	public void sleep() {
		System.out.println("猪就知道睡");
	}

	public void arch() {
		System.out.println("猪还会拱");
	}

	public String getBreed() {
		return breed;
	}

	public void setBreed(String breed) {
		this.breed = breed;
	}

	public int getAge() {
		return age;
	}

	public void setAge(int age) {
		this.age = age;
	}

	public double getWeight() {
		return weight;
	}

	public void setWeight(double weight) {
		this.weight = weight;
	}
}
```

