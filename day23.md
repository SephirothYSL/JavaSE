## 1. 包装类

**包装类的 parseXXX(String str) 方法用来将字符串解析成对应的基本数据类型**

【注意】Charator 类没有 parseCharacter() 方法

```java
public class Test {
	public static void main(String[] args) {
		String str1 = "123";
		String str2 = "34.5F";
		String str3 = "false";

		int parseInt = Integer.parseInt(str1);
		System.out.println("parseInt：" + parseInt);	// parseInt：123

		System.out.println("----------------");

		byte parseByte = Byte.parseByte(str1);
		System.out.println("parseByte：" + parseByte);	// parseByte：123

		System.out.println("----------------");

		short parseShort = Short.parseShort(str1);
		System.out.println("parseShort：" + parseShort);	// parseShort：123

		System.out.println("----------------");

		Long parseLong = Long.parseLong(str1);
		System.out.println("parseLong：" + parseLong);	// parseLong：123

		System.out.println("----------------");

		float parseFloat = Float.parseFloat(str2);
		System.out.println("parseFloat：" + parseFloat);	// parseFloat：34.5

		System.out.println("----------------");

		double parseDouble = Double.parseDouble(str2);
		System.out.println("parseDouble：" + parseDouble);	// parseDouble：34.5

		System.out.println("----------------");

		boolean parseBoolean = Boolean.parseBoolean(str3);
		System.out.println("parseBoolean：" + parseBoolean);	// parseBoolean：false
		
		System.out.println("----------------");
		
		char charAt = str3.charAt(0);
		System.out.println("charAt：" + charAt);	// charAt：f
	}
}
```

## 2. 集合

### 2.1 集合框架

```java
interface Collection<E> Java中所有集合的总接口
--| interface List<E> List接口，数据存储可重复，有序。
----| class ArrayList<E> 
	重点 可变长数组
----| class LinkedList<E> 
	重点 双向链表模式
----| class Vector<E> 
	线程安全的可变长数组
--| interface Set<E> Set接口，数据存储不可以重复，无序
----| HashSet<E> 
	底层存储数据的结构是一个哈希表，存储效率，查询效率极高！！！
----| TreeSet<E> 
	底层存储数据的结构是一个平衡二叉树结构，要求数据必须有比较方式！！！
```

### 2.2 collection 接口

#### 2.2.1 增

```java
boolean add(E e)
	添加当前集合约束的指定数据类型到当前集合中
	
boolean addAll(Collection<? extends E> c);
	添加另一个集合到当前集合中，要求添加集合中保存的元素必须是当前集合中保存
	元素本身或者其子类对象 【泛型的上限】
	class Dog extends Animal
	class Cat extends Animal
	class Tiger extends Animal
```

```java
public class Test {
	public static void main(String[] args) {
		Collection<String> collection1 = new ArrayList<String>();
		Collection<String> collection2 = new ArrayList<String>();
		
		collection1.add("Buffer");
		collection1.add("Hello");
		
		collection2.add("Buffer");
		collection2.add("Hello");
		collection2.add("World");
		
		System.out.println(collection1);	// [Buffer, Hello]
		
		collection1.addAll(collection2);		
		System.out.println(collection1);	// [Buffer, Hello, Buffer, Hello, World]
	}
}
```

#### 2.2.2 删

```java
boolean remove(Object obj);
	删除集合中的指定元素，删除成功返回true,未找到指定元素，无法删除返回
	false，并且在多个元素的情况下，删除找到的第一个元素。
	
boolean removeAll(Collection<?> c);
	在当前集合中删除两个集合的交集
	
boolean retainAll(Collection<?> c);
	在当前集合中保留两个集合的交集
	
void clear();
	清空整个集合中的所有元素
```

```java
public class TestRemove {
	public static void main(String[] args) {
		Collection<String> collection1 = new ArrayList<String>();
		Collection<String> collection2 = new ArrayList<String>();
		
		collection1.add("Buffer");
		collection1.add("Hello");
		
		collection2.add("Buffer");
		collection2.add("Hello");
		collection2.add("World");
		
		collection1.remove("Hello");
		System.out.println(collection1);	// [Buffer]
		
		collection2.removeAll(collection1);
		System.out.println(collection2);	// [Hello, World]
		
		collection1.add("Hello");
		
		collection1.containsAll(collection2);
		System.out.println(collection1);	// [Buffer, Hello]
	}
}
```

#### 2.2.3 查

```java
int size();
	有效元素个数

boolean isEmpty();
	判断当前集合是否为空，是否存在有效元素

boolean contains(Object obj);
	判断指定元素是否在当前集合中存在

boolean containsAll(Collection<?> c);
	判断传入的参数集合是不是当前集合的子集合

Object[] toArray();
	返回集合中所有保存元素的Object类型数组
```

```java
public class TestGet {
	public static void main(String[] args) {
		Collection<String> collection1 = new ArrayList<String>();
		Collection<String> collection2 = new ArrayList<String>();

		collection1.add("Buffer");
		collection1.add("Hello");

		collection2.add("Buffer");
		collection2.add("Hello");
		collection2.add("World");

		System.out.println(collection1.size());	// 2

		System.out.println(collection1.isEmpty());	// fasle

		System.out.println(collection1.contains("Buffer"));	//true

		System.out.println(collection2.containsAll(collection1));	// true

		Object[] array = collection1.toArray();
		for (int i = 0; i < array.length; i++) {
			System.out.println(array[i]);
		}
	}
}
```

### 2.3 迭代器

是集合获取元素的另一种方式，依赖于集合存在

#### 2.3.1 获取迭代器的方法

```java
Iterator<E> iterator();
	获取迭代器对象，泛型对应的具体数据类型和集合中约束的泛型具体数据类型一致。
```

#### 2.3.2 其他方法

```java
boolean hasNext();
	判断当前集合中是否可以继续得到元素，继续遍历
        
E next();
	1. 获取迭代器当前指向的元素
	2. 将迭代器指向下一个元素
        
void remove();
	删除通过next方法获取到元素
		【注意】
		1、remove方法只能删除next方法获取到元素
		2、remove方法只能在next方法之后执行，且不能跨过一个next执行
		3、没有next不能使用remove
```

结果

```java
Buffer
Hello
World
[]
```

#### 2.3.3 【注意】

```java
public class Test {
	public static void main(String[] args) {
		Collection<String> c = new ArrayList<String>();

		c.add("雪花纯生");
		c.add("修道院啤酒");
		c.add("1664");
		c.add("泰山精酿");
		c.add("时光精酿");
		
		/*
		 * 根据当前集合，获取对应的迭代器对象
		 * 
		 * 得到的迭代器对象会依据，当前集合中的所有元素进行一个规划操作。
		 * 迭代器对于整个集合中的元素都是存在预期。
		 */
		Iterator<String> iterator = c.iterator();
		
		/*
		 * 迭代器遍历，利用迭代器的特征进行遍历操作
		 */
		while (iterator.hasNext()) {
			// 获取每一个迭代器指向元素，并且展示
			String string = iterator.next();
			System.out.println(string);
			
			/*
			 * 通过集合对象本身删除1664，对于迭代器而言，一脸懵逼，原本的规划
			 * 没有了！！！并且集合没有告知迭代器数据发生了改变，迭代器继续按照
			 * 原本的规划路径操作，保存！！！
			 * 
			 * 对于集合在内存中占用的空间而言
			 * 	1. 集合对应的引用数据类型变量可以操作对应空间
			 * 	2. 迭代器可以操作对应的空间
			 * 
			 * 对于集合和迭代器而言，【集合在内存中占用的空间】共享资源，在操作
			 * 共享资源过程中，我们要多多考虑共享资源的冲突问题。
			 * 后面课程中会讲到【多线程】
			 */
			c.remove("1664");
		}
		
		/*
		 Exception in thread "main" java.util.ConcurrentModificationException
				at java.util.ArrayList$Itr.checkForComodification(ArrayList.java:909)
				at java.util.ArrayList$Itr.next(ArrayList.java:859)
				at com.qfedu.b_iterator.Demo3.main(Demo3.java:30)
		 */
	}
}
```

## 3. 泛型

### 泛型通配符

```java
<?>
	任意类型，如果没有明确，那么就是Object以及任意的Java类了
    
泛型上限：向下限定，E及其子类
	? extends E
    
泛型下限：向上限定，E及其父类
    ? super E
```

```java
class Animal {}

class Dog extends Animal{}

class Cat extends Animal{}

class Person{}

public class TestAnimal {
	public static void main(String[] args) {
		Collection<Animal> collection1 = new ArrayList<Animal>();
		Collection<Dog> collection2 = new ArrayList<Dog>();
		Collection<Cat> collection3 = new ArrayList<Cat>();
		Collection<Person> collection4 = new ArrayList<Person>();
		
		collection1.addAll(collection1);	// 编译通过
		collection1.addAll(collection2);	// 编译通过
		collection1.addAll(collection3);	// 编译通过
		// collection1.addAll(collection4);	// 报错
		
	}
}
```
