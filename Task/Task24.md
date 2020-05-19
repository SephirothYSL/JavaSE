## 嵌套集合遍历自定义学生对象

学生类

```java
public class Student {
	private String name;
	private int age;

	// Constructor setter&&getter toString
}
```

测试类

```java
public class Task {
	public static void main(String[] args) {
		ArrayList<ArrayList<Student>> arrayList = new ArrayList<ArrayList<Student>>();

		ArrayList<Student> FirstArrayList = new ArrayList<Student>();

		FirstArrayList.add(new Student("Buffer", 23));
		FirstArrayList.add(new Student("Smoot", 22));
		FirstArrayList.add(new Student("Balance", 21));
		FirstArrayList.add(new Student("Wizard", 23));

		ArrayList<Student> SecondArrayList = new ArrayList<Student>();

		SecondArrayList.add(new Student("Benny", 34));
		SecondArrayList.add(new Student("Amy", 32));
		SecondArrayList.add(new Student("Tina", 25));
		SecondArrayList.add(new Student("Candy", 35));
		SecondArrayList.add(new Student("Una", 31));

		ArrayList<Student> ThirdArrayList = new ArrayList<Student>();

		ThirdArrayList.add(new Student("Kun", 26));
		ThirdArrayList.add(new Student("Zhan", 25));
		ThirdArrayList.add(new Student("Bo", 27));

		arrayList.add(FirstArrayList);
		arrayList.add(SecondArrayList);
		arrayList.add(ThirdArrayList);

		for (ArrayList<Student> bigArray : arrayList) {
			for (Student student : bigArray) {
				System.out.println(student);
			}
			System.out.println("--------------------");
		}
	}
}
```

结果

```java
Student [name=Buffer, age=23]
Student [name=Smoot, age=22]
Student [name=Balance, age=21]
Student [name=Wizard, age=23]
--------------------
Student [name=Benny, age=34]
Student [name=Amy, age=32]
Student [name=Tina, age=25]
Student [name=Candy, age=35]
Student [name=Una, age=31]
--------------------
Student [name=Kun, age=26]
Student [name=Zhan, age=25]
Student [name=Bo, age=27]
--------------------
```

