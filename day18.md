## 学生管理系统项目

```shell
尝试完成以下功能
	实体类:
		学生类:
			id, 姓名，年龄，性别，成绩
	需要使用数组保存学生信息
		Student[] allStu
	需要完成的方法
		1. 根据学生的ID，找到对应的学生对象【完成】
		2. 完成方法，添加新学生
		3. 完成方法，删除指定ID的学生
		4. 完成方法，展示数组中所有的学生信息
		5. 根据学生成绩，完成降序排序
```

### 1. 包结构划分

```
1、实体类：student.system.entity
2、管理类：student.system.controller
3、主方法类：student.system.mainproject
4、测试类：student.system.testsystem
```

【注意】报名规范：所有单词全部小写，单词之间用 . 隔开

### 2. 学生实体类

包含了学生信息，属性全部私有化，提供两个构造方法，id系统分配，不允许自定义id，提供getter & setter 方法对外使用，重写 toString 方法对外展示所有属性

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

	public Student(String name, int age, char sex, float score) {
		super();
		this.name = name;
		this.age = age;
		this.sex = sex;
		this.score = score;
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

	public char getSex() {
		return sex;
	}

	public void setSex(char sex) {
		this.sex = sex;
	}

	public float getScore() {
		return score;
	}

	public void setScore(float score) {
		this.score = score;
	}

	@Override
	public String toString() {
		return "Student [id=" + id + ", name=" + name + ", age=" + age + ", sex=" + sex + ", score=" + score + "]";
	}	
}
```

### 3. 学生管理类

定义了对学生进行操作的类，包含了增、删、查的主要方法，附带包含了学生数组的扩容、展示数组中所有学生信息，通过id查找所在的下标方法。

```java
import project.student.system.entity.Student;

public class Controller {
	/**
	 * 私有化学生数组，只能类内使用 Controller类的所有方法都直接或间接作用于这个学生数组
	 */
	private Student[] allStudents = null;

	/**
	 * 定义数组的默认容量为10
	 */
	private static final int DEFAULT_CAPACITY = 10;

	/**
	 * 定义数组的最大容量
	 */
	private static final int MAX_ARRAY_CAPACITY = Integer.MAX_VALUE - 8;

	/**
	 * 定义当前数组的有效元素个数
	 */
	private int size = 0;

	/**
	 * 无参构造方法，使用默认容量初始化
	 */
	public Controller() {
		this.allStudents = new Student[DEFAULT_CAPACITY];
	}

	/**
	 * 带参构造，参数为数组的容量，进行合法性判断，如果超过范围就抛出一个异常
	 * 
	 * @param initCapacity 传入数组的容量
	 */
	public Controller(int initCapacity) {

		if (initCapacity < 0 || initCapacity >= MAX_ARRAY_CAPACITY) {
			System.out.println("Input parameter is Invalid!!!");

			/*
			 * 抛出一个异常
			 */
			System.exit(0);
		}

		this.allStudents = new Student[initCapacity];
	}

	/**
	 * 添加方法，传入一个学生对象，成功返回true，失败返回false 
	 * 添加之前先判断是否需要扩容
	 * 学生的id从creatId()获取，从1开始
	 * 
	 * @param student 传入一个学生对象
	 * @return 添加成功返回true，否则返回false
	 */
	public boolean add(Student student) {

		/*
		 * 通过有效元素的个数和数组的容量来判断数组是否已满，
		 * 如果相等就执行扩容数组操作，传入的最小容量为当前数组容量+1
		 */
		if (size == allStudents.length) {
			grow(size + 1);
		}

		/*
		 * 通过调用creatId()方法为学生对象设置id。默认从1开始
		 */
		student.setId(creatId());
		
		// 添加学生对象到数组中，默认从0开始
		allStudents[size] = student;
		
		// 有效元素个数加1
		size++;
		
		return true;
	}

	/**
	 * 扩容方法，对数组的容量进行扩容，大约扩容50%的容量
	 * 当数组容量不够时执行此方法
	 * 
	 * @param minCapacity 传入最小扩容
	 */
	private void grow(int minCapacity) {

		// 获取原数组的容量
		int oldCapacity = allStudents.length;

		// 定义新数组容量
		int newCapacity = oldCapacity + oldCapacity / 2;

		// 新容量与最小容量比较，如果小于最小容量，就把最小容量的值传给新容量
		if (minCapacity > newCapacity) {
			newCapacity = minCapacity;
		}

		// 新容量与最大容量比较，如果超过最大容量，抛出异常
		if (newCapacity > MAX_ARRAY_CAPACITY) {
			System.exit(0);
		}

		// 根据新容量创建新数组
		Student[] temp = new Student[newCapacity];

		// 将旧数组中的元素复制到新数组
		for (int i = 0; i < oldCapacity; i++) {
			temp[i] = allStudents[i];
		}

		// 新数组地址指向旧数组
		allStudents = temp;

		// 扩容完成友好性提示
		System.out.println("grow be called~~~新容量为：" + newCapacity);
	}

	/**
	 * 删除方法，通过传入的id删除对应的学生对象
	 * 
	 * @param id 传入需要被删除学生的id
	 * @return 删除成功返回true，否则返回false
	 */
	public boolean remove(int id) {
		// 通过findIndexById()方法得到id所在的下标
		int index = findIndexById(id);

		/*
		 * 如果下标为-1，说明没有找到id所在的学生对象，提供友好性提示并返回false
		 */
		if (-1 == index) {
			System.out.println("Not Found!");
			return false;
		}

		/*
		 * 后续学生对象前移覆盖前一个对象
		 */
		for (int i = index; i < size; i++) {
			allStudents[i] = allStudents[i + 1];
		}

		// 删除最后一个学生对象
		allStudents[size - 1] = null;

		// 有效元素减1
		size--;

		return true;
	}

	/**
	 * 查询方法，通过传入的id查询学生信息
	 * 
	 * @param id 传入一个id
	 * @return 返回当前id的学生对象，如果id不存在返回null
	 */
	public Student get(int id) {
		// 通过findIndexById()方法得到id所在的下标
		int index = findIndexById(id);

		return 0 <= index ? allStudents[index] : null;
	}

	/**
	 * 通过id返回下标
	 * 
	 * @param id 传入一个id
	 * @return 返回一个下标，如果id不存在返回-1
	 */
	private int findIndexById(int id) {
		int index = -1;

		/*
		 * 遍历数组，将学生对象所在下标赋值给index，用来返回
		 */
		for (int i = 0; i < size; i++) {
			if (id == allStudents[i].getId()) {
				index = i;
				break;
			}
		}

		return index;
	}

	/**
	 * 生成一个学生的id，用于给数组添加学生元素前的学生id赋值
	 * 如果数组中没有元素，则返回1，如果有元素，则返回最后一个有效元素的 id + 1
	 * 
	 * @return 返回学生id
	 */
	public int creatId() {
		int id = 1;

		if (0 != this.size) {
			id = allStudents[this.size - 1].getId() + 1;
		}

		return id;
	}

	/**
	 * 展示所有元素
	 */
	public void show() {
		for (int i = 0; i < size; i++) {
			System.out.println(allStudents[i]);
		}
	}
}
```

