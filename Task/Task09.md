# 作业

## 1. 找出数组中元素 == 5 所在下标位置

```java
import java.util.Scanner;

class Task1 {
	public static void main(String[] args) {
		int[] array = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
		
		Scanner scanner = new Scanner(System.in);
		System.out.println("请输入需要查询的元素：");
		int num = scanner.nextInt();
		
		System.out.println("该元素的下标为："+ seek(array, num));
	}
	
	/**
	* 查找数组中的元素所在的下标位置
	*
	* @param array 传入一个数组
	* @param num 传入一个元素，在数组中遍历寻找是否有和元素相同的值
	* @return 返回查询元素所对应的下标，如果没有该元素则返回-1
	*/
	public static int seek(int[] array, int num) {
		for (int i = 0; i < array.length; i++) {
			if (array[i] == num) {
				return i;
			}
		}
		
		return -1;
	}
}
```

## 2. 找出数组中下标为5的元素

```java
class Task2 {
	public static void main(String[] args) {
		int[] array = {1, 3, 5, 7, 9, 2, 4, 6, 8, 10};
		
		seekIndex(array);
	}
	
	/**
	* 找出下标为5的元素
	*
	* @param array 传入一个数组
	*/
	public static void seekIndex(int[] array) {
		for (int i = 0; i < array.length; i++) {
			if (5 == i) {
				System.out.println(array[i]);
				return;
			}
		}
		
		System.out.println("下标为5的元素不存在~");
		return;
	}
}
```

## 3. 找出数组中最大元素所在下标位置

```java
class Task3 {
	public static void main(String[] args) {
		int[] array = {1, 3, 5, 17, 9, 2, 4, 6, 8, 10};
		System.out.println("最大元素所在下标位置为：" + seekIndex(array));
	}
	
	/**
	* 找出数组中最大元素所在下标位置
	*
	* @param array 传入一个数组
	* @return int类型的下标
	*/
	public static int seekIndex(int[] array) {
		int max = 0;
		int index = 0;
		
		for (int i = 0; i < array.length; i++) {
			if (array[i] > max) {
				max = array[i];
				index = i;
			}
		}
		
		return index;
	}
}
```

## 4. 找出数组中最小元素所在下标位置

```java
class Task4 {
	public static void main(String[] args) {
		int[] array = {11, 3, 5, 17, 9, 2, 4, 6, 8, 10};
		System.out.println("最大元素所在下标位置为：" + seekIndex(array));
	}
	
	/**
	* 找出数组中最小元素所在下标位置
	*
	* @param array 传入一个数组
	* @return int类型的下标
	*/
	public static int seekIndex(int[] array) {
		int min = array[0];
		int index = 0;
		
		for (int i = 0; i < array.length; i++) {
			if (array[i] < min) {
				min = array[i];
				index = i;
			}
		}
		
		return index;
	}
}
```

