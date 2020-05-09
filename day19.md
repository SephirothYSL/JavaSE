## 1. 学生管理系统项目

### 1.1 学生管理类

#### 1.1.1 修改学生信息

```java
/**
 * 修改方法，通过id修改对应的学生信息
 * id不可修改
 * 
 * @param id 用户指定的id
 * @return 修改成功返回true，否则返回false
 */
public boolean modify(int id) {
	// 用户友好性提示
	System.out.println("执行修改方法~~~");
    
	// 通过id获取对应的对象
	Student student = get(id);
    
	// 定义一个扫描器
	Scanner scanner = new Scanner(System.in);
    
	// 定义一个变量接收控制台的录入
	int choose = 0;
    
	// 如果对象为null，返回false
	if (student == null) {
		System.out.println("Not Found！！！");
		return false;
	}
    
	/*
     *当控制台录入不等于5，循环执行，choose为5时退出循环
     */
	while (choose != 5) {
		// 展示学生信息
		System.out.println(student);
        
		// 友好性提示
		System.out.println("1. 修改学生姓名");
		System.out.println("2. 修改学生年龄");
		System.out.println("3. 修改学生性别");
		System.out.println("4. 修改学生成绩");
		System.out.println("5. 退出");
        
		// 接收控制台录入
		choose = scanner.nextInt();
        
		// 控制台换行
		scanner.nextLine();
        
		// 根据 choose 来执行不同的修改项
		switch (choose) {
		case 1:
			System.out.println("请输入学生姓名：");
			student.setName(scanner.next());
			scanner.nextLine();
			break;
		case 2:
			System.out.println("请输入学生年龄：");
			student.setAge(scanner.nextInt());
			scanner.nextLine();
			break;
		case 3:
			System.out.println("请输入学生性别：");
			student.setSex(scanner.nextLine().charAt(0));
			scanner.nextLine();
			break;
		case 4:
			System.out.println("请输入学生成绩：");
			student.setScore(scanner.nextFloat());
			scanner.nextLine();
			break;
		case 5:
			System.out.println("退出");
			break;
		default:
			System.out.println("Input parameter is valied!!!");
			break;
		}
	}
    
	System.out.println("修改成功");
	return true;
}
```

#### 1.1.2 根据学生的成绩降序排序

```java
/**
 * 根据学生成绩降序排序
 */
public void sortDescOfScore() {
	// 根据有效元素个数为容量创建新数组
	Student[] sortScoreArray = new Student[size];
    
	// 复制学生元素到新数组中
	for (int i = 0; i < sortScoreArray.length; i++) {
		sortScoreArray[i] = allStudents[i];
	}
	// 降序排序(选择排序算法)
	for (int i = 0; i < sortScoreArray.length - 1; i++) {
		for (int j = i + 1; j < sortScoreArray.length; j++) {
			if (sortScoreArray[i].getScore() < sortScoreArray[j].getScore()) {
				Student temp = sortScoreArray[i];
				sortScoreArray[i] = sortScoreArray[j];
				sortScoreArray[j] = temp;
			}
		}
	}
    
	// 调用展示数组内容方法
	show(sortScoreArray);
}
```

#### 1.1.3 通过传入指定数组展示其内容

```java
/**
 * 传入一个数组，展示数组内所有元素
 * 重载 show() 方法
 * 
 * @param student 传入一个学生数组
 */
public void show(Student[] student) {
	for (int i = 0; i < student.length; i++) {
		System.out.println(student[i]);
	}
}
```

### 1.2 主方法类

```java
package project.student.system.mainproject;

import project.student.system.controller.Controller;
import project.student.system.entity.Student;

public class MainProject {

	public static void main(String[] args) {
		// 创建一个控制器
		Controller controller = new Controller();

        // 添加5个学生对象到控制器中
		for (int i = 1; i <= 5; i++) {
			Student student = new Student();
			student.setName("Buffer" + i);
			student.setAge((int) (Math.random() * 50));
			student.setSex(Math.random() <= 0.5 ? '男' : '女');
			student.setScore((int) (Math.random() * 100));

			controller.add(student);
		}

        // 展示学生信息
		controller.show();

		System.out.println("-----------------------------------");

        // 添加学生
		controller.add(new Student("Smoot", 22, '男', 96));

        // 展示学生信息
		controller.show();

		System.out.println("-----------------------------------");

        // 删除id为1的学生
		controller.remove(1);

        // 展示学生信息
		controller.show();

		System.out.println("-----------------------------------");

        // 修改id为3的学生信息
		controller.modify(3);

        // 展示学生信息
		controller.show();

		System.out.println("-----------------------------------");

        // 展示id为2的学生信息
		System.out.println(controller.get(2));

		System.out.println("-----------------------------------");

        // 根据学生成绩降序排序
		controller.sortDescOfScore();
		
	}
}
```

## 2. 接口的多态

### 2.1 会跑接口

实现了这个接口的类都拥有 run() 方法

```java
public interface Runnable {
	void run();
}
```

### 2.2 动物类

动物类是个抽象类，不能创建对象，实现了 Runnable 接口，但是未重写 run() 方法，所以子类必须重写 run() 方法

```java
public abstract class Animal implements Runnable{
	String breed;
	int age;
	
	public abstract void run();
	
	public void eat() {
	}
	
	public void sleep() {		
	}
}

// Dog 类继承自 Aminal 类，重写了 run() 方法
class Dog extends Animal{

	@Override
	public void run() {
		System.out.println("狗在跑~~~");
	}
	
}

// Cat 类继承自 Aminal 类，重写了 run() 方法
class Cat extends Animal{
	
	@Override
	public void run() {
		System.out.println("猫在跑~~~");
	}
}
```

### 2.3 交通工具类

交通工具类是个抽象类，不能创建对象，实现了 Runnable 接口，但是未重写 run() 方法，所以子类必须重写 run() 方法

```java
public abstract class Vehicle implements Runnable{
	String brand;
	float price;
	
	public abstract void run();
}

// Bike 类继承自 Vehicle 类，重写了 run() 方法
class Bike extends Vehicle{

	@Override
	public void run() {
		System.out.println("自行车在跑~~~");
	}
	
}

// Bus 类继承自 Vehicle 类，重写了 run() 方法
class Bus extends Vehicle{

	@Override
	public void run() {
		System.out.println("公交车在跑~~~");
	}
	
}
```

### 2.4 测试类

通过传入不同的 Runnable 实现类来测试 Observer 类的 testRun() 方法，体现了接口的多态

```java
public class Test {
	public static void main(String[] args) {
		Observer observer = new Observer();
		
        // 只要是 Runnable 接口的实现类都可以作为参数传递
		observer.testRun(new Cat());
		observer.testRun(new Dog());
		observer.testRun(new Bus());
		observer.testRun(new Bike());
	}
}

/**
 * Observer 类有一个 testRun() 方法，用来查看谁具有 run() 功能
 *
 * @param runnable 传入一个接口或其实现类
 */
class Observer{
	public void testRun(Runnable runnable) {
		System.out.print("看看谁会跑：");
		runnable.run();
	}
}
```

### 2.5 结果

```java
看看谁会跑：猫在跑~~~
看看谁会跑：狗在跑~~~
看看谁会跑：公交车在跑~~~
看看谁会跑：自行车在跑~~~
```

