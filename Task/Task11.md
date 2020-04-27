# 作业

需求：找出指定元素在数组中的所有下标

## 解法一

在方法中直接打印

```java
public class Task1 {
	public static void main(String[] args) {
		int[] array = { 1, 2, 3, 1, 2, 3, 1, 2, 3 };

		System.out.println("指定元素的所有下标位置为：");

		seekAllIndex(array, 1);
	}

	/**
	 * 打印指定元素在数组中的所有下标
	 * @param array 传入一个数组
	 * @param num 指定的元素
	 */
	public static void seekAllIndex(int[] array, int num) {
		for (int i = 0; i < array.length; i++) {
			if (num == array[i]) {
				System.out.print(i + " ");
			}
		}
	}
}
```

## 解法二

方法返回首次出现的有效下标，通过循环方法获得所有的有效下标

```java
public class Task2 {
	public static void main(String[] args) {
		int[] array = { 1, -2, 3, 1, -2, 3, 1, -2, 3 };

		int index = 0;

		System.out.println("指定元素的所有下标位置为：");
		/*
		 * 从index等于0开始循环，result用来接收seekAllIndex方法返回的下标 
		 * 如果发现下标为-1说明已经没有有效下标，就跳出循环，只要没有发现下标为-1就打印有效下标 
		 * 每次循环都把index赋值为有效下标加1， 这样下一轮循环就过上一个有效下标，避免重复
		 * 当index的值等于数组长度时结束while循环
		 */
		while (index < array.length) {
			int result = seekAllIndex(array, 1, index);

			if (-1 == result) {
				break;
			}
			System.out.print(result + " ");
			index = result + 1;
		}

	}

	/**
	 * 打印指定元素在数组中的所有下标
	 * 
	 * @param array 传入一个数组
	 * @param num   指定的元素
	 * @param index 传入一个下标
	 * @return 返回数组中第一个指定元素的下标，如果没有指定元素就返回-1
	 */
	public static int seekAllIndex(int[] array, int num, int index) {
		for (int i = index; i < array.length; i++) {
			if (num == array[i]) {
				index = i;
				return index;
			}
		}

		return -1;
	}
}
```

## 解法三

方法返回一个包含有效元素的数组

```java
import java.util.Arrays;

public class Task3 {
	public static void main(String[] args) {
		int[] array = { 1, -2, 3, 1, -2, 3, 1, -2, 3 };

		int[] newArray = seekAllIndex(array, 1);

		System.out.println("指定元素的所有下标位置为：" + Arrays.toString(newArray));
	}

	/**
	 * 打印指定元素在数组中的所有下标
	 * 
	 * @param array 传入一个数组
	 * @param num   指定的元素
	 * @return 返回一个只带有需求下标的int数组，如果没有指定元素，就返回空数组
	 */
	public static int[] seekAllIndex(int[] array, int num) {
		int index = 0;

		int[] tempArray = new int[array.length];

		int[] finalArray;

		for (int i = 0; i < array.length; i++) {
			if (num == array[i]) {
				tempArray[index] = i;
				index++;
			}
		}

		finalArray = Arrays.copyOf(tempArray, index);

		return finalArray;
	}
}
```

## 解法四

方法返回一个拼接了有效下标的字符串

```java
import java.util.Arrays;

public class Task4 {

	public static void main(String[] args) {
		int[] array = { 1, 2, 3, 1, 2, 3, 1, 2, 3 };

		System.out.println(Arrays.toString(array));

		String result = seekIndexOfNum(array, 1);

		System.out.println("指定元素的所有下标位置为：" + result);

	}

	/**
	 * 打印指定元素在数组中的所有下标
	 * 
	 * @param array 传入一个数组
	 * @param num   指定的元素
	 * @return 返回以字符串形式的结果，如果没有指定元素，返回空字符串
	 */
	public static String seekIndexOfNum(int[] array, int num) {
		String result = "";

		for (int i = 0; i < array.length; i++) {
			if (num == array[i]) {
				result = result + i + " ";
			}
		}

		return result;
	}
}
```

## 解法五

返回有效元素的个数

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
		if (indexes.length < array.length) {
			System.out.println("Input Parameter is Invalid！！！");
			return 0;
		}

		int count = 0;

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

