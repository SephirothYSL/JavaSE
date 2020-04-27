## 1. 数组

打印数组中指定元素的所有下标

```shell
分析：
    固定格式		
    	public static		
    返回值类型		
    	void、boolean、int
    	如果是int类型，需要返回有效元素的个数，如果没有有效元素就返回0
    方法名
    	seekAllIndex
    形参列表
    	1、需要查询的目标数组
    	2、需要查询的元素 int类型
    	3、用来存放下标的新数组 int类型
    	
方法声明：
	public static int seekAllIndex(int[] array, int num, int[] indexes)
	
问题：
	找到的下标如何保存，并且可以让方法外可以得到
思路：
	既然不能返回int类型的数组，那么就新建一个数组当做参数传递给方法，在方法内把下标保存在新数组中，因为引用传递的缘故，方法外的也能得到下标

新问题：
	如何判断indexes数组的第一个元素是否是有效元素
思路：
	用一个累加器来判断来统计找到的有效元素个数，当做返回值返回给方法外
```

```java
import java.util.Arrays;

public class Task1ExtendFinal {
	public static void main(String[] args) {
		// 指定的数组
		int[] array = { 1, 2, 3, 1, 2, 3, 1, 2, 3 };

		// 用来接收有效下标的数组，初始化容量等于指定数组容量
		int[] indexes = new int[array.length];

		// 接收有效元素的个数
		int count = seekAllIndex(array, indexes, 1);

		if (0 == count) {
			System.out.println("查询的元素不存在.....");
		} else {
			// 创建一个数组剔除无效元素
			int[] result = Arrays.copyOf(indexes, count);
			System.out.println(Arrays.toString(result));
		}

	}

	/**
	 * 打印指定数组中的所有下标
	 * 
	 * @param array   传入指定的数组
	 * @param indexes 传入用来接收下标的空数组
	 * @param num     指定被查找的元素
	 * @return count 返回有效下标元素的个数 
	 */
	public static int seekAllIndex(int[] array, int[] indexes, int num) {
		// 合法性判断
        if (indexes.length < array.length) {
			System.out.println("Input Parameter is Invalid！！！");
			return 0;
		}

        // 累加器，存放有效元素的个数
		int count = 0;

        /*
         * 遍历数组中所有元素，当发现指定元素时将对应的下标存储在indexes数组中
         * 累加器 +1
         */
		for (int i = 0; i < array.length; i++) {
			if (num == array[i]) {
				indexes[count] = i;
				count++;
			}
		}

		return count;
	}
}
```

## 2. 面向对象

### 2.1 面向对象思想

```shell
1、面向对象是基于面向过程的编程思想

2、万物皆对象

3、对象具有唯一性

4、任何对象都具有一定的特征和行为；特征是事物的基本描述，行为是事物的功能

5、类是一组相关的属性和方法的集合，是一个抽象的概念

6、对象是类的具体存在

7、在一组相同或相似的对象中，抽取出共性的特征和行为，保留所关注的部分就是类的抽取

8、类是模板、图纸，通过类创造的对象就是实体
```

### 2.2 类的定义

```shell
格式：
	class 类名 {
		成员变量;
		成员方法;
	}

类名：
	大驼峰命名，首字母大写，见名知意
	
成员变量：
	定义在类中，方法外的变量，用来描述类的特征
	
成员方法：
	定义在类中，用来描述类的功能
```

```java
class Person {
	String name;
	int age;
	char sex;

	public void eat() {
		System.out.println("吃");
	}

	public void sleep() {
		System.out.println("睡");
	}

	public void play() {
		System.out.println("玩");
	}
}
```

### 2.3 对象的创建

```java
格式：
    类名 对象名 = new 类名(参数);
```

```java
Person person = new Person();
```

### 2.4 对象的使用

```java
格式：
	使用成员变量：
		对象名.成员变量
    
	使用成员方法：
    	对象名.成员方法()
```

```java
person.name = "Buffer";
person.age = 23;
person.sex = '男';

person.eat();
person.sleep();
person.play(); 
```
