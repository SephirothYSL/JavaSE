## 1. 包装类

### 1.1 概述

为了让基本类型的数据进行更多的操作，Java就为每种基本类型提供了对应的包装类类型

### 1.2 对应类型

```java
byte 		Byte
short		Short
int			Integer
long		Long
float		Float
double		Double
char		Character
boolean		Boolean
```

### 1.3 自动拆装箱

```java
public class TestInteger {
	public static void main(String[] args) {
		int num1 = 10;
		// 自动装箱
		Integer num2 = num1;

		// 自动拆箱
		num2++;
		
		System.out.println(num2);	// 11
	}
}
```

## 2. 泛型

### 2.1 泛型概述

泛型是一种特殊的类型，它把指定类型的工作推迟到客户端代码声明并实例化类或方法的时候进行。也被称为参数化类型，可以把类型当作参数一样传递过来，在传递过来之前我不明确，但是在使用的时候我就用明确了。泛型也体现了封装的思想

### 2.2 泛型的优点

```shell
1、提高了程序的安全性(类型安全)
2、提高了程序的可扩展性、可重用性
2、将运行期遇到的问题转移到了编译期
3、省去了类型强转的麻烦(Object类对象)
```

### 2.3 泛型格式

```java
泛型标识符：<自定义无意义英文大写单字母占位符>
    常用格式：		
		<T> Type 
		<E> Element
		<K> Key
		<V> Value

泛型类：把泛型定义在类上
	格式:public class 类名<泛型类型1,…>
    	【注意】泛型类型必须是引用类型
        
泛型方法：把泛型定义在方法上
	格式:public <泛型类型> 返回类型 方法名(泛型类型 .)
        
泛型接口：把泛型定义在接口上
	格式:public  interface 接口名<泛型类型1…>
```

### 2.4 泛型方法

```java
public class TestGenericityMethod {
	public static void main(String[] args) {
		String type = getType("ABCD");
		System.out.println(type);	// ABCD
		
		Integer type2 = getType(1);
		System.out.println(type2);	// 1
		
		TestGenericityMethod test = new TestGenericityMethod();		
		TestGenericityMethod type3 = getType(test);
		
		System.out.println(type3);	// code.genericity.TestGenericityMethod@7852e922
	}
	
    /**
	 * 带有自定义泛型 T 对应的方法
	 * 
	 * @param <T> 自定义泛型无意义英文单个大写字母占位符
	 * @param t T类型
	 * @return T类型
	 */
	public static <T> T getType(T t) {
		return t;
	}
}
```

【注意】

```shell
1、要求形式参数列表中必须有一个参数是当前自定义泛型，因为需要通过参数来约束当前方法运行过程中泛型对应的具体数据类型是哪一个
		
2、返回值类型可以使用自定义泛型，而且是被形式参数列表中传入的泛型对应具体数类型控制
		
3、方法体内也可以使用自定义泛型，同时也是被参数当中泛型对应具体数据类型约束监控
```

### 2.5 泛型类

```java
class Test<T> {

	public void print(T t) {
		System.out.println(t);
	}

	public T getType(T t) {
		return t;
	}
}

public class TestGenericityClass {
	public static void main(String[] args) {
		Test<String> test1 = new Test<>();
		test1.print("Hello");	// Hello

		String type = test1.getType("World");
		System.out.println(type);	// World
	}
}
```

【注意】

```shell
1、类内的成员方法可以直接使用对应的类名声明泛型
2、类内成员方法使用的泛型具体数据类型是在创建当前类对象时约束
3、在创建当前类对象时没有约束泛型对应的具体数据类型，那么所有使用到泛型的位置都是Object类型，有悖于泛型使用原则
4、如果类声明过了泛型，那么类中所有使用此泛型的方法都同时被声明，即无法使用其他类型
5、成员变量不能使用泛型
6、泛型类中定义的静态方法不能直接使用类声明的泛型，因为泛型需要在创建对象时声明，而静态方法在类加载时就加载完成，此时泛型还没有声明。如果静态方法想要使用泛型，只能自己声明自己使用
```

### 2.6 泛型接口

```java
public interface Print<T> {
	public abstract T print(T t);
}
```

```java
/**
 * 接口实现类不指定泛型类型，在创建对象时约束泛型的具体数据类型
 *
 * @param <T>
 */
class GetObject<T> implements Print<T> {

	@Override
	public T print(T t) {
		System.out.println(t);
		return t;
	}

}

/**
 * 接口实现类指定泛型类型，创建对象后可以直接使用无需再定义
 */
class GetString implements Print<String> {

	@Override
	public String print(String t) {
		System.out.println(t);
		return t;
	}
}

public class TestGenericityinterface {
	public static void main(String[] args) {
		GetString getString = new GetString();

		getString.print("实现类声明时指定泛型类型");	// 实现类声明时指定泛型类型

		GetObject<String> getObject = new GetObject<>();

		getObject.print("实现类未声明泛型类型");	// 实现类未声明泛型类型
	}
}
```

【注意】

```shell
1、接口中的成员变量不能使用泛型，因为static、final
2、泛型接口的实现可以指定泛型的类型，也可以不指定
```

## 3. 学生管理项目

### 3.1 异常处理

#### 3.1.1 自定义异常类

```java
/*
 * 用于创建StudentManager对象时用户传入的初始化容量不合法操作
 */
class IllegalCapacityException extends Exception{
	public IllegalCapacityException() {
	}
	
	public IllegalCapacityException(String message) {
		super(message);
	}
}

/*
 * 数组元素下标越界异常，用于扩容方法
 */
class OverflowMaxArraySizeException extends Exception {
	public OverflowMaxArraySizeException() {
	}

	public OverflowMaxArraySizeException(String message) {
		super(message);
	}
}
```

#### 3.1.2 核心代码调用

```java
// 构造方法
public Controller(int initCapacity) throws IllegalCapacityException {
	if (initCapacity < 0 || initCapacity >= MAX_ARRAY_CAPACITY) {
		/*
		 * 抛出一个异常
		 */
		throw new IllegalCapacityException("Input parameter is valid!");
	}
	this.allStudents = new Student[initCapacity];
}

// 扩容方法
private void grow(int minCapacity) throws OverflowMaxArraySizeException {
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
		throw new OverflowMaxArraySizeException("Overflow MAX_VALUE_SIZE！！");
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
```

### 3.2 排序算法优化(接口回调)

#### 3.2.1 自定义接口

```java
/*
 * 工具接口，想使用工具必须实现这个类
 */
public interface Tools {
	/**
	 * 排序方法，用于比较两个学生的信息大小
	 */
	public abstract boolean sort(Student stu1, Student stu2);

}
```

#### 3.2.2 接口实现类

```java
/*
 * 学生成绩降序排序类，实现了工具类中的排序方法，
 */
public class SortDescOfScord implements Tools{

    /**
	 * 返回第一个学生的成绩小于第二个学生的成绩
	 */
	@Override
	public boolean sort(Student stu1, Student stu2) {
		return stu1.getScore() < stu2.getScore();
	}

}
```

```java
/*
 * 学生成绩升序排序类，实现了工具类中的排序方法
 */
public class SortAsceOfScore implements Tools{

	/**
	 * 返回第一个学生的成绩大于第二个学生的成绩
	 */
	@Override
	public boolean sort(Student stu1, Student stu2) {
		return stu1.getScore() > stu2.getScore();
	}

}
```

#### 3.2.3 核心代码调用

```java
/**
 * 根据学生的信息排序
 * @param tool 这里传入一个接口类型的变量，调用方法时可以根据不同的实现类
 * 来实现不同的功能，比如比较学生的年龄、成绩、升序、降序等
 */
public void sortOfTooks(Tools tool) {
	// 根据有效元素个数为容量创建新数组
	Student[] sortScoreArray = new Student[size];
	// 复制学生元素到新数组中
	for (int i = 0; i < sortScoreArray.length; i++) {
		sortScoreArray[i] = allStudents[i];
	}
	// 降序排序算法(选择排序)
	for (int i = 0; i < sortScoreArray.length - 1; i++) {
		for (int j = i + 1; j < sortScoreArray.length; j++) {
			/*
			 * 这里传入一个接口调用的排序方法，返回值为true或false
			 */
			if (tool.sort(sortScoreArray[i], sortScoreArray[j])) {
				Student temp = sortScoreArray[i];
				sortScoreArray[i] = sortScoreArray[j];
				sortScoreArray[j] = temp;
			}
		}
	}
	// 展示元素
	show(sortScoreArray);
}
```

```java
/**
 * 主方法
 */
public class MainProject {
	public static void main(String[] args) {

		Controller controller = new Controller();

		for (int i = 1; i <= 5; i++) {
			Student student = new Student();
			student.setName("Buffer" + i);
			student.setAge((int) (Math.random() * 50));
			student.setSex(Math.random() <= 0.5 ? '男' : '女');
			student.setScore((int) (Math.random() * 100));

			try {
				controller.add(student);
			} catch (OverflowMaxArraySizeException e) {
				System.out.println("当前人数已达上限，麻烦转学吧~");
			}
		}

		controller.sortOfTooks(new SortAsceOfScore());
		
		System.out.println("-----------------------------------");

		controller.sortOfTooks(new SortDescOfScord());
		
	}
}
```

#### 3.2.4 结果

```java
Student [id=2, name=Buffer3, age=46, sex=女, score=5.0]
Student [id=4, name=Buffer5, age=13, sex=男, score=40.0]
Student [id=1, name=Buffer2, age=37, sex=女, score=44.0]
Student [id=3, name=Buffer4, age=14, sex=男, score=70.0]
Student [id=5, name=Smoot, age=22, sex=男, score=96.0]
-----------------------------------
Student [id=5, name=Smoot, age=22, sex=男, score=96.0]
Student [id=3, name=Buffer4, age=14, sex=男, score=70.0]
Student [id=1, name=Buffer2, age=37, sex=女, score=44.0]
Student [id=4, name=Buffer5, age=13, sex=男, score=40.0]
Student [id=2, name=Buffer3, age=46, sex=女, score=5.0]
```

