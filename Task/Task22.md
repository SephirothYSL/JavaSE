## 作业

### 需求

```shell
使用接口完成数据展示过滤功能：
	1、只要学生成绩50分以上
	2、只要学生年龄30岁以下
```

### 实体类

```java
public class Student {
	private int id;
	private String name;
	private int age;
	private char sex;
	private float score;

	public Student() {
		super();
	}

	public Student(int id, String name, int age, char sex, float score) {
		super();
		this.id = id;
		this.name = name;
		this.age = age;
		this.sex = sex;
		this.score = score;
	}

	/* 此处的 setter/ getter 方法省略 */

	@Override
	public String toString() {
		return "Student [id=" + id + ", name=" + name + ", age=" + age + ", sex=" + sex + ", score=" + score + "]";
	}	
}
```

### 接口

```java
/*
 * Tools工具接口，想要使用 accept 方法必须实现此接口
 */
public interface Tools {
	/**
	 * 这个方法可以根据特定需求过滤学生的信息
	 * @param stu 传入一个学生对象
	 * @return 返回true或false
	 */
	public abstract boolean accept(Student stu);
}
```

### 接口实现类

```java
/*
 * Tools 接口的实现类
 */
public class AcceptOverAge implements Tools {

	/**
	 * 判断成绩是否大于50
	 */	
	@Override
	public boolean accept(Student stu) {
		return stu.getAge() < 30;
	}
}
```

```java
/*
 * Tools 接口的实现类
 */
public class AcceptOverScore implements Tools {

	/**
	 * 判断成绩是否大于50
	 */	
	@Override
	public boolean accept(Student stu) {
		return stu.getScore() > 50;
	}
}
```

### 管理类

```java
public class Controller {
	private Student[] array = new Student[] {
				new Student(1,"Buffer",23,'男',10),
				new Student(2,"Banlance",32,'男',99),
				new Student(3,"Smoot",22,'男',97),
				new Student(4,"Amy",30,'女',29),
				new Student(5,"Catherine",27,'女',93)};
	
	public Controller() {
	}
	
	/**
	 * 过滤方法，通过传入不同的 Tools 接口的实现类实现不同的效果
	 * @param tool 接口实现类
	 */
	public void accept(Tools tool) {
        // 定义一个容量，用来接收过滤后的学生个数
		int capacity = 0;
        // 定义过滤后的数组有效元素个数
		int index = 0;
		
        // 遍历 this 数组获取过滤后的学生个数
		for (int i = 0; i < this.array.length; i++) {
			if (tool.accept(array[i])) {
				capacity++;
			}
		}
		
        // 通过过滤后的学生个数创建临时数组
		Student[] temp = new Student[capacity];
		
        // 遍历 this 数组获取过滤后的学生添加到临时数组中
		for (int i = 0; i < this.array.length; i++) {
			if(tool.accept(array[i])) {
				temp[index] = array[i];
				index++;
			}
		}
		
        // 遍历过滤后的学生信息
		for (int i = 0; i < capacity; i++) {
			System.out.println(temp[i]);
		}
	}
}
```

### 测试类

```java
public class Main {
	public static void main(String[] args) {
		Controller controller = new Controller();
		
        // 过滤成绩50分以下的学生
		controller.accept(new AcceptOverScore());
		
		System.out.println("--------------------");

        // 过滤年龄30岁以上的学生
		controller.accept(new AcceptOverAge());
	}
}
```

### 结果

```java
Student [id=2, name=Banlance, age=32, sex=男, score=99.0]
Student [id=3, name=Smoot, age=22, sex=男, score=97.0]
Student [id=5, name=Catherine, age=27, sex=女, score=93.0]
--------------------
Student [id=1, name=Buffer, age=23, sex=男, score=10.0]
Student [id=3, name=Smoot, age=22, sex=男, score=97.0]
Student [id=5, name=Catherine, age=27, sex=女, score=93.0]
```

