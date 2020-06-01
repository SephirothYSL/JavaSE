## 1. List

### 1.1 概述

有序的 collection ，可以根据索引操作元素，数据可重复

>ArrayList
>
>​	可变长数组
>
>LinkedList
>
>​	双向链表
>
>Vector
>
>​	线程安全的可变长数组

### 1.2 增加方法

```java
boolean add(E e);	
	List接口继承Collection接口 add方法，使用操作和Collection一致，并且这里采用的添加方式是【尾插法】
	
boolean add(int index, E e);
	List接口【特有方法】，在指定位置，添加指定元素。
	
boolean addAll(Collection<? extends E> c);
	List接口继承Collection接口 addAll方法，使用操作和Collection一致，并且这里采用的添加方式是【尾插法】
	
boolean addAll(int index, Collection<? extends E> c);
	List接口【特有方法】，在指定下标位置，添加另一个集合中所有内容
```

```java
public class Test {
	public static void main(String[] args) {
		List<String> arrayList = new ArrayList<String>();

		arrayList.add("Hello");
		arrayList.add("World");
		arrayList.add("Android");

		arrayList.add(0, "Java");
		System.out.println(arrayList);

		List<String> al = new ArrayList<String>();

		al.add("ArrayList是线程不安全的可变长数组");
		al.add("LinkedList是双向链表：增删快，查询慢");

		al.addAll(arrayList);

		System.out.println(al);

		arrayList.addAll(0, al);

		System.out.println(arrayList);
	}
}
```

### 1.3 删除方法

```java
E remove(int index);
	List接口【特有方法】，获取指定下标位置的元素并删除。

boolean remove(Object obj);
	List接口继承Collection接口方法。删除集合中的指定元素
	
boolean removeAll(Collection<?> c);
	List接口继承Collection接口方法。删除当前集合中和参数集合重复元素
	
boolean retainAll(Collection<?> c);
	List接口继承Collection接口方法。保留当前集合中和参数集合重复元素
	
clear();
	List接口继承Collection接口方法。清空整个集合中的所有元素
```

```java
public class TestRemove {
	public static void main(String[] args) {
		List<Integer> al = new ArrayList<Integer>();

		al.add(1);
		al.add(2);
		al.add(3);
		al.add(4);

		System.out.println("删除指定下标位置为0的元素： " + al.remove(0));

		System.out.println("al : " + al);

		List<Integer> al1 = new ArrayList<Integer>();

		al1.add(4);
		al1.add(5);
		al1.add(6);

		System.out.println("al.removeAll(al1) : " + al.removeAll(al1));
		System.out.println("al : " + al);

		List<Integer> al2 = new ArrayList<Integer>();

		al2.add(5);
		al2.add(7);
		al2.add(6);

		System.out.println("al1.reatinAll(al2) : " + al1.retainAll(al2));

		System.out.println("al1 ： " + al1);

		al2.clear();

		System.out.println("al2.clear() ： " + al2);
	}
}
```

### 1.4 修改方法

```java
E set(int index, E e);
		List接口【特有方法】，使用指定元素替代指定下标的元素，返回值是被替换的元素
```

```java
public class TestModify {
	public static void main(String[] args) {
		List<Character> al = new ArrayList<Character>();

		al.add('A');
		al.add('B');
		al.add('C');

		al.set(0, 'M');

		System.out.println(al); // [M, B, C]
	}
}
```

### 1.5 查询方法

```java
int size();
	List接口继承Collection接口方法。获取集合中有效元素个数

boolean isEmpty();
	List接口继承Collection接口方法。判断当前集合是否为空

boolean contains(Object obj);
	List接口继承Collection接口方法。判断指定元素是否包含在当前集合中

boolean containsAll(Collection<?> c);
	List接口继承Collection接口方法。判断参数集合是不是当前集合在子集合
	
Object[] toArray();
	List接口继承Collection接口方法。获取当前集合中所有元素Object数组

E get(int index);
	List接口【特有方法】。获取指定下标对应的元素

List<E> subList(int fromIndex, int toIndex);
	List接口【特有方法】。获取当前集合指定子集合，从fromIndex开始，到toIndex结束。fromIndex <= 范围 < toIndex

int indexOf(Object obj);
	List接口【特有方法】。获取指定元素在集合中第一次出现位置

int lastIndexOf(Object obj);
	List接口【特有方法】。获取指定元素在集合中最后一次出现的位置
```

```java
public class TestGet {
	public static void main(String[] args) {
		List<String> al = new ArrayList<String>();
		al.add("Hello");
		al.add("World");
		al.add("Java");
		al.add("Android");
		al.add("Hello");

		List<String> al2 = new ArrayList<>();
		al2.add("Java");
		al2.add("Hello");

		System.out.println(al.size()); // 4
		System.out.println(al.isEmpty()); // false
		System.out.println(al.contains("Java")); // true
		System.out.println(al.containsAll(al2)); // true

		Object[] array = al.toArray();
		for (Object str : array) {
			System.out.println(str);
		}

		System.out.println(al.indexOf("World")); // 1
		System.out.println(al.lastIndexOf("Hello")); // 4

		System.out.println(al.get(0)); // Hello

		System.out.println(al.subList(1, 3)); // [World, Java]
	}
}
```

## 2. ArrayList

### 2.1 概述

```java
List 接口的大小可变数组的实现。实现了所有可选列表操作，并允许包括 null 在内的所有元素。除了实现 List 接口外，此类还提供一些方法来操作内部用来存储列表的数组的大小。（此类大致上等同于 Vector 类，除了此类是不同步的。）
```

### 2.2 特有方法

```java
void ensureCapacity(int minCapacity);
	如有必要，增加此 ArrayList 实例的容量，以确保它至少能够容纳最小容量参数所指定的元素数。
trimToSize();
	将此 ArrayList 实例的容量调整为列表的当前大小。节省空间
```

### 2.3 效率

```
增删慢
	增加慢
		1、数组当前容量无法满足添加操作，需要进行grow扩容方法执行，在扩容方
		法中，存在数组创建，数组数据拷贝。非常浪费时间，而且浪费内存。
		2、数组在添加数据的过程中，存在在指定位置添加元素，从指定位置开始，
		之后的元素整体向后移动。
		
	删除慢
		1、删除数据之后，从删除位置开始，之后的元素整体向前移动，移动过程非
		常浪费时间
		2、删除操作会导致数据空间的浪费，内存的浪费
	
查询快
	ArrayList 底层是一个数组结构，在查询操作的过程中，是按照数组+下标的方式
	来操作对应的元素，数组+下标方式可以直接获取对应的空间首地址，CPU访问效率
	极高。
```

