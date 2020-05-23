## 1. Map

Map 接口允许以键集、值集或键-值映射关系集的形式查看某个映射的内容。映射顺序 定义为迭代器在映射的 collection  视图上返回其元素的顺序。某些映射实现可明确保证其顺序，如 TreeMap 类；另一些映射实现则不保证顺序，如 HashMap  类。

【重点】将键映射到值的对象。一个映射不能包含重复的键；每个键最多只能映射到一个值。

```java
public interface Map<K,V>
```

### 1.1 HashMap

基于哈希表的 Map 接口的实现。此实现提供所有可选的映射操作，并允许使用 null 值和 null  键。（除了非同步和允许使用 null 之外，HashMap 类与 Hashtable 大致相同。）此类不保证映射的顺序

```java
public class HashMap<K,V>
```

```java
增
	put(K key, V value);
		添加符合Map要求的键值对存入到双边队列中
	putAll(Map<? extends K, ? extends V> map)
		添加另一个Map到当前Map中，要求K是当前Map本身对应的K，或者其子类
		V是当前Map本身对应的V，或者其子类
删
	remove(Object key); 
		删除对应Key键值对
改
	put(K key, V value);
		使用value修改已存在的key对应的值
查
	int size();
		Map双边队列个数
	boolean isEmpty();
		判断当前Map双边队列中是否为空
	boolean containsKey(Object key);
		判断指定Key是否存在
	boolean containsValue(Object value);
		判断指定Value是否存在
	Set<K> keySet();
		返回Map双边队列中所有Key对应的Set集合
	Collection<V> values();
		返回Map双边队列中所有value对应Collection集合
```

```java
public class TestHashMap {
	public static void main(String[] args) {
		Map<String, Integer> map = new HashMap<String, Integer>();

		map.put("Buffer", 23);
		map.put("Balance", 23);
		map.put("Amy", 32);

		System.out.println(map);

		HashMap<String, Integer> hashMap = new HashMap<>();
		hashMap.put("Candy", 33);
		hashMap.put("David", 29);

		hashMap.putAll(map);
		System.out.println(hashMap);

		hashMap.remove("Balance");
		System.out.println(hashMap);

		hashMap.put("Buffer", 16);
		System.out.println(hashMap);

		System.out.println("map.size() :" + map.size());

		System.out.println("map.isEmpty() : " + map.isEmpty());

		System.out.println("have Buffer : " + map.containsKey("Buffer"));

		System.out.println("have Buffer's age : " + hashMap.containsValue(16));

		Set<String> keySet = map.keySet();
		System.out.println(keySet);

		Collection<Integer> values = map.values();
		System.out.println(values);
	}
}
```

【注意】HashMap 添加自定义数据类型元素时需要重写其 equals 和 hashCode 方法

学生类

```java
public class Student {
	private String name;
	private int age;
	private char sex;
	
	// Constructor setter getter toString equals hashCode
}
```

测试类

```java
public class TestMap2 {
	public static void main(String[] args) {
		Map<Student, Integer> hashMap = new HashMap<Student, Integer>();

		hashMap.put(new Student("Buffer", 23, '男'), 1);
		hashMap.put(new Student("Balance", 23, '男'), 2);
		hashMap.put(new Student("Buffer", 22, '男'), 3);
		hashMap.put(new Student("Buffer", 23, '女'), 4);
		hashMap.put(new Student("Buffer", 23, '男'), 5);

		Set<Entry<Student, Integer>> entrySet = hashMap.entrySet();

		for (Entry<Student, Integer> entry : entrySet) {
			System.out.println(entry);
		}
	}
}
```

结果

```java
Student [name=Balance, age=23, sex=男]=2
Student [name=Buffer, age=23, sex=女]=4
Student [name=Buffer, age=22, sex=男]=3
Student [name=Buffer, age=23, sex=男]=5
```

### 1.2 TreeMap

基于红黑树（Red-Black tree）的 NavigableMap  实现。该映射根据其键的自然顺序进行排序，或者根据创建映射时提供的 Comparator  进行排序，具体取决于使用的构造方法。 

学生类

```java
public class Student {
	private String name;
	private int age;
	private char sex;
    
    // Constructor and setter、getter
}
```

Comparator 接口实现类

```java
public class MyCompare implements Comparator<Student> {

    /**
     * 返回两个学生的年龄差
     */
	@Override
	public int compare(Student o1, Student o2) {
		return o1.getAge() - o2.getAge();
	}

}
```

测试类

```java
public class TestTreeMap {
	public static void main(String[] args) {
		TreeMap<Student, Integer> treeMap = new TreeMap<Student, Integer>(new MyCompare());
		
		treeMap.put(new Student("Buffer",23,'男'), 1);
		treeMap.put(new Student("Buffer",22,'男'), 1);
		treeMap.put(new Student("Buffer",21,'男'), 1);
		
		System.out.println(treeMap);
		System.out.println(treeMap.size());		
	}
}
```

### 1.3 Map 中的 Entry

Map双边队列中把Key和Value进行一个封装操作，完全按照一个数据类型来处理。是 Map 中的一个成员接口

```java
interface Map.Entry<K,V>
```

```java
Set<Map.Entry<K, V>> entrySet();
	返回值类型是Entry键值对形式数据的Set集合
        
Set<Map.Entry<K, V>>
	Map.Entry<K, V> Map接口的内部接口Entry，使用的泛型 K,V对应Map创建过程中约束的K,V
	因为返回值是Set集合，集合带有泛型 Set<Map接口中的内部接口Entry>
			
Entry 对应的方法
	K getKey();
		返回与此项对应的键
	V getValue();
		返回与此项对应的值。
	V setValue(V value);
		用指定的值替换与此项对应的值，返回与此项对应的旧值 
```

```java
public class TestEntry {
	public static void main(String[] args) {
		Map<String, Integer> map = new HashMap<String, Integer>();

		map.put("Buffer", 23);
		map.put("Balance", 23);
		map.put("Amy", 32);

		Set<Entry<String, Integer>> entrySet = map.entrySet();

		for (Entry<String, Integer> entry : entrySet) {
			System.out.println(entry.getKey() + " setVaule: " + entry.setValue(16));
			System.out.println(entry.getKey() + " : " + entry.getValue());
		}
	}
}
```

## 2. 项目

Tools 工具类

```java
public class Tools {
	
	/**
	 * 通过指定的规则对用户传入的数组进行排序
	 * @param <T> 自定义泛型
	 * @param arr 用户指定类型的数组
	 * @param c Comparator接口的实现类
	 */
	public static <T> void selectSort(T[] arr, Comparator<T> c) {
		for (int i = 0; i < arr.length - 1; i++) {
			for (int j = i + 1; j < arr.length; j++) {
				if (c.compare(arr[i], arr[j]) > 0) {
					T temp = arr[i];
					arr[i] = arr[j];
					arr[j] = temp;
				}
			}
		}
	}
}
```

Comparator 接口实现类

```java
/**
 * 通过学生成绩升序排序
 */
public class MyCompareByStudentScore implements Comparator<Student> {

	@Override
	public int compare(Student o1, Student o2) {
		return (int) (o1.getScore() - o2.getScore());
	}

}
```

Controller 

```java
public class Controller {
	/**
	 * 排序	 
	 */
	public void sortOfTooks() {
		// 根据有效元素个数为容量创建新数组
		Student[] sortScoreArray = new Student[size];

		// 复制学生元素到新数组中
		for (int i = 0; i < sortScoreArray.length; i++) {
			sortScoreArray[i] = allStudents[i];
		}

        // 调用 Tools 工具类的 selectSort 方法，传入指定的数组和 Comparator 实现类
		Tools.selectSort(sortScoreArray, new MyCompareByStudentScore());

		// 展示元素
		show(sortScoreArray);
	}
}
```

测试

```java
@Test
public void TestSotr() throws OverflowMaxArraySizeException {
	Controller controller = new Controller();
	controller.add(new Student("Buffer",23,'男',41));
	controller.add(new Student("Banlance",21,'男',99));
	controller.add(new Student("Smoot",22,'男',37));
	controller.add(new Student("Amy",30,'女',79));
	controller.add(new Student("Catherine",27,'女',93));
	
	controller.sortOfTooks();
}
```

## 3. 匿名内部类

### 3.1 概述

把类定义在其他类的内部，这个类就被称为内部类，匿名内部类是内部类的简化写法，简化了类名。

### 3.2 前提

存在一个类或者接口，这里的类可以是具体类也可以是抽象类

### 3.3 格式

```java
new 类名或者接口名() {重写方法}
```

### 3.4 本质

是一个继承了类或者实现了接口的子类匿名对象

```java
interface Test {
	public abstract void test();
}

public class TestAnony {
	public static void main(String[] args) {
		new Test() {

			@Override
			public void test() {
				System.out.println("匿名内部类");
			}
		}.test();	// 匿名内部类
	}
}
```

