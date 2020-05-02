## 作业

```
尝试完成以下功能
	实体类:
		学生类:
			id, 姓名，年龄，性别，成绩
	需要使用数组保存学生信息
		Student[] allStu
	需要完成的方法
		1. 根据学生的ID，找到对应的学生对象
		2. 完成方法，添加新学生
		3. 完成方法，删除指定ID的学生
		4. 完成方法，展示数组中所有的学生信息
		5. 根据学生成绩，完成降序排序
```

### 学生类

```java
public class Student {
	private int id;
	private String name;
	private int age;
	private char sex;
	private float grade;

	public Student() {
		super();
	}

	public Student(int id) {
		super();
		this.id = id;
	}

	public Student(String name, int age, char sex, float grade) {
		super();
		
		this.name = name;
		this.age = age;
		this.sex = sex;
		this.grade = grade;
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

	public float getGrade() {
		return grade;
	}

	public void setGrade(float grade) {
		this.grade = grade;
	}
}
```

### 管理类

```java
public class Control {
	Student[] student = new Student[100];

	int index = 0;

	/**
	 * 查询方法，通过学生的id查询，如果id存在返回学生对象，如果id不存在， 返回id为0的学生对象
	 * 
	 * @param id 被查询的学生id
	 * @return id所持有的学生对象，如果没有id则返回一个id为0的学生对象
	 */
	public Student seek(int id) {
		System.out.println("开始查询id为" + id + "的学生信息~~~");
		for (int i = 0; i < student.length; i++) {
			if (student[i] != null && id == student[i].getId()) {
				return student[i];
			}
		}
		return new Student(0);
	}

	/**
	 * 添加方法
	 * 
	 * @param student
	 */
	public void add(Student student) {
		System.out.println("添加新同学：" + student.getName());
		if (0 == index) {
			student.setId(1);
			this.student[0] = student;
			index++;
			System.out.println("添加成功，新同学的id为：" + 1);
			return;
		}

		for (int i = 0; i < index; i++) {

			if (this.student[i].getName() == student.getName()) {
				System.out.println("此id或姓名已存在，添加失败~~");
				return;
			}

			if (null == this.student[i + 1]) {
				student.setId(i + 1 + 1);
				this.student[i + 1] = student;
			}
		}
		index++;
		System.out.println("添加成功，新同学的id为：" + student.getId());
	}

	/**
	 * 删除学生方法，将被删除学生的id置为0
	 * @param id 学生id
	 * @param name 学生姓名
	 */
	public void delete(int id, String name) {
		System.out.println("删除操作执行[" + id + " " + name + "]~~~");
		for (int i = 0; i < index; i++) {
			if(id == student[i].getId() && name.equals( student[i].getName())) {
				student[i].setId(0);
				System.out.println("删除操作成功~~~");
				return;
			}
		}
		System.out.println("输入的id或姓名有误，删除失败");
	}

	/**
	 * 展示学生信息 依次展示每个学生的id、姓名、年龄、性别、成绩
	 * 如果student内有空元素则立刻return
	 * 如果学生id为0说明该学生的信息被删除，跳过当前循环
	 */
	public void show() {
		System.out.println("展示所有学生的信息：");
		System.out.println("学生id\t" + "学生姓名\t" + "学生年龄\t" + "学生性别\t" + "学生成绩\t");
		for (int i = 0; i <= index; i++) {
			
			if (null == student[i]) {
				return;
			}			

			if(student[i].getId() == 0) {
				continue;
			}

			System.out.print(student[i].getId() + "\t");
			System.out.print(student[i].getName() + "\t");
			System.out.print(student[i].getAge() + "\t");
			System.out.print(student[i].getSex() + "\t");
			System.out.print(student[i].getGrade() + "\t");
			System.out.println();
		}
	}
	
	/**
	 * 重载展示学生信息
	 * 依次展示每个学生的id、姓名、年龄、性别、成绩
	 * @param student 传入一个学生对象
	 */
	public void show(Student student) {		
		if (0 == student.getId()) {
			System.out.println("找不到当前学生~");
			return;
		}

		System.out.println("查询成功，学生信息如下：");
		System.out.println("学生id\t" + "学生姓名\t" + "学生年龄\t" + "学生性别\t" + "学生成绩\t");
			
		System.out.print(student.getId() + "\t");
		System.out.print(student.getName() + "\t");
		System.out.print(student.getAge() + "\t");
		System.out.print(student.getSex() + "\t");
		System.out.print(student.getGrade() + "\t");
		System.out.println();
	}

	/**
	 * 根据学生的成绩降序排序
	 * 使用选择排序算法
	 * 先创建一个float数组 studentGrade，容量为index
	 * 遍历student数组中的每个学生的成绩，并录入 studentGrade
	 * 对 studentGrade 进行排序
	 */
	public void sortOfGrade() {
		System.out.println("排序~~~");

		/*
		 *	Student[] student = java.util.Arrays.copyOf(this.student, index);
		 *	for (int i = 0; i < index; i++) {
		 *		for (int j = i + 1; j < index; j++) {
		 *			if (student[i].getGrade() < student[j].getGrade()) {
		 *				float temp = student[i].getGrade();
		 *				student[i].setGrade(student[j].getGrade());
		 *				student[j].setGrade(temp);
		 *			}
		 *		}
		 *	}
		 * 
		 */
		
		float[] studentGrade = new float[index];

		for (int i = 0; i < index; i++) {
			studentGrade[i] = student[i].getGrade();
		}

		for (int i = 0; i < index; i++) {
			for (int j = i + 1; j < index; j++) {
				if (studentGrade[i] < studentGrade[j]) {
					float temp = studentGrade[i];
					studentGrade[i] = studentGrade[j];
					studentGrade[j] = temp;
				}
			}
		}

		// 调用打印学生成绩方法
		printOfGrade(studentGrade);
	}

	/**
	 * 打印学生成绩，通过调用student类的getGrade方法实现
	 */
	public void printOfGrade() {
		System.out.println("打印学生成绩~~~");
		for (int i = 0; i < index; i++) {
			System.out.print(student[i].getGrade() + "\t ");
		}
		System.out.println();
	}

	/**
	 * 打印学生成绩，通过遍历成绩数组来实现
	 * 
	 * @param studentGrade 传入float类型的数组
	 */
	public void printOfGrade(float[] studentGrade) {
		System.out.println("打印学生成绩~~~");
		for (int i = 0; i < index; i++) {
			System.out.print(studentGrade[i] + "\t ");
		}
		System.out.println();
	}
}
```

### 测试类

```java
public class TestStudent {
	public static void main(String[] args) {
		Control control = new Control();
		
		control.add(new Student("Buffer",23,'男',100.0F));
		control.add(new Student("Smoot",21,'男',97.0F));
		control.add(new Student("Balance",21,'男',99.0F));
		control.add(new Student("Wizard",21,'男',99.6F));
		control.add(new Student("Waner",30,'女',99.9F));
		control.add(new Student("Candy",32,'女',96.0F));
		control.add(new Student("Yancy",20,'女',94.0F));
		control.add(new Student("Steven",21,'男',91.0F));
		control.add(new Student("Arthur",29,'男',98.0F));
		control.add(new Student("Xavier",21,'男',99.3F));
		System.out.println("--------------------------------");
		
		control.show();
		System.out.println("--------------------------------");
		
		control.printOfGrade();
		System.out.println("--------------------------------");
		
		control.sortOfGrade();
		System.out.println("--------------------------------");
		
		control.show(control.seek(2));
		System.out.println("--------------------------------");
		
		control.delete(2, "Smoot");
		System.out.println("--------------------------------");
		
		control.show();
		System.out.println("--------------------------------");
	}
}
```

### 结果

```java
添加新同学：Buffer
添加成功，新同学的id为：1
添加新同学：Smoot
添加成功，新同学的id为：2
添加新同学：Balance
添加成功，新同学的id为：3
添加新同学：Wizard
添加成功，新同学的id为：4
添加新同学：Waner
添加成功，新同学的id为：5
添加新同学：Candy
添加成功，新同学的id为：6
添加新同学：Yancy
添加成功，新同学的id为：7
添加新同学：Steven
添加成功，新同学的id为：8
添加新同学：Arthur
添加成功，新同学的id为：9
添加新同学：Xavier
添加成功，新同学的id为：10
--------------------------------
展示所有学生的信息：
学生id	学生姓名	学生年龄	学生性别	学生成绩	
1	Buffer	23	男	100.0	
2	Smoot	21	男	97.0	
3	Balance	21	男	99.0	
4	Wizard	21	男	99.6	
5	Waner	30	女	99.9	
6	Candy	32	女	96.0	
7	Yancy	20	女	94.0	
8	Steven	21	男	91.0	
9	Arthur	29	男	98.0	
10	Xavier	21	男	99.3	
--------------------------------
打印学生成绩~~~
100.0	 97.0	 99.0	 99.6	 99.9	 96.0	 94.0	 91.0	 98.0	 99.3	 
--------------------------------
排序~~~
打印学生成绩~~~
100.0	 99.9	 99.6	 99.3	 99.0	 98.0	 97.0	 96.0	 94.0	 91.0	 
--------------------------------
开始查询id为2的学生信息~~~
查询成功，学生信息如下：
学生id	学生姓名	学生年龄	学生性别	学生成绩	
2	Smoot	21	男	97.0	
--------------------------------
删除操作执行[2 Smoot]~~~
删除操作成功~~~
--------------------------------
展示所有学生的信息：
学生id	学生姓名	学生年龄	学生性别	学生成绩	
1	Buffer	23	男	100.0	
3	Balance	21	男	99.0	
4	Wizard	21	男	99.6	
5	Waner	30	女	99.9	
6	Candy	32	女	96.0	
7	Yancy	20	女	94.0	
8	Steven	21	男	91.0	
9	Arthur	29	男	98.0	
10	Xavier	21	男	99.3	
--------------------------------
```

