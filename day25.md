## 1. LinkedList

### 1.1 概述

底层数据结构是一个双向链表，查询慢，增删快

### 1.2 方法

```java
LinkedList使用的方法都是从List接口实现而来的方法，需要了解的是LinkedList特有方法：
boolean addFirst(E e);
	在当前链表开始位置加元素
boolean addLast(E e);
	在当前链表末尾添加元素
E getFirst();
	获取第一个Node节点元素数据
E getLast();
	获取末尾Node节点元素数据
E removeFirst();2
	删除头节点
E removeLast();
	删除末尾节点
```

```java
public class Test {
	public static void main(String[] args) {
		LinkedList<String> linkedList = new LinkedList<String>();

		linkedList.add("Buffer");
		linkedList.add("Balance");
		linkedList.add("Wizard");
		linkedList.add("Blanche");
		linkedList.add("Eve");

		linkedList.addFirst("Hello");
		linkedList.addLast("World");

		System.out.println(linkedList.getFirst());	// Buffer
		System.out.println(linkedList.getLast());	// Eve

		System.out.println(linkedList);	// [Hello, Buffer, Balance, Wizard, Blanche, Eve, World]

		System.out.println("移除头元素" + linkedList.removeFirst());	// 移除头元素Hello
		System.out.println("移除尾元素" + linkedList.removeLast());	// 移除尾元素World

		System.out.println(linkedList);	// [Buffer, Balance, Wizard, Blanche, Eve]
	}
}
```

## 2. Set 集合

### 2.1 概述

一个不包含重复元素的 collection。存储元素的顺序无序。

### 2.2 HashSet

#### 2.2.1 概述

底层数据结构是哈希表，依赖 equals 方法和 hashCode 方法实现不可重复

#### 2.2.2 学生类：需要重写 equals() 和 hashCode()

```java
public class Student {
	private String name;
	private int age;

	// Construator setter/getter toString

	@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + age;
		result = prime * result + ((name == null) ? 0 : name.hashCode());
		return result;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		Student other = (Student) obj;
		if (age != other.age)
			return false;
		if (name == null) {
			if (other.name != null)
				return false;
		} else if (!name.equals(other.name))
			return false;
		return true;
	}
}
```

#### 2.2.3 测试类

```java
public class Test {
	public static void main(String[] args) {
		Set<Student> hashSet = new HashSet<Student>();

		hashSet.add(new Student("Buffer", 23));
		hashSet.add(new Student("Smoot", 22));
		hashSet.add(new Student("Wizard", 23));
		hashSet.add(new Student("Buffer", 23));
		hashSet.add(new Student("Buffer", 20));
		hashSet.add(new Student("Balance", 21));

		for (Student student : hashSet) {
			System.out.println(student);
		}
	}
}
```

#### 2.2.4 结果

```java
Student [name=Smoot, age=22]
Student [name=Wizard, age=23]
Student [name=Balance, age=21]
Student [name=Buffer, age=23]
Student [name=Buffer, age=20]
```

### 2.3 TreeSet

#### 2.3.1 概述

基于 TreeMap 的 NavigableSet  实现，底层数据结构是平衡二叉树。使用元素的自然顺序对元素进行排序，或者根据创建 set 时提供的 Comparator  进行排序，具体取决于使用的构造方法。

#### 2.3.2 Person 类

```java
package code.treeset;

public class Person {
	private String name;
	private int age;

	// Constructor setter/getter toString
}
```

#### 2.3.3 Comparator 接口实现类

```java
public class MyCompare implements Comparator<Person> {

    // 通过年龄判断是否为同一个 Person
	@Override
	public int compare(Person o1, Person o2) {
		return o1.getAge() - o2.getAge();
	}

}
```

#### 2.3.4 测试类

```java
public class TestPerson {
	public static void main(String[] args) {
        // 创建 TreeSet 集合时传入一个 Comparator 接口的实现类
		TreeSet<Person> treeSet = new TreeSet<Person>(new MyCompare());

		treeSet.add(new Person("Smoot", 22));
		treeSet.add(new Person("Buffer", 23));
		treeSet.add(new Person("Wizard", 23));
		treeSet.add(new Person("Balance", 21));
		
		System.out.println(treeSet);	// [Person [name=Balance, age=21], Person [name=Smoot, age=22], Person [name=Buffer, age=23]]
	}
}
```

