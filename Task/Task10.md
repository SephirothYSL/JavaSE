# 作业

## 1. 找出数组中最大值的下标位置

```java
class Task1 {
	public static void main(String[] args) {
		int[] array = {31, 2, 54, 135, 963, 14, 735};
		
		System.out.println("最大值的下标位置为：" + seekIndexOfNum(array));
	}
	
	/**
	* 找出数组中最大值的下标位置
	*
	* @param array 传入一个数组
	* @return 返回最大值所在的下标
	*/
	public static int seekIndexOfNum(int[] array) {
		int max = 0;
		
		for (int i = 1; i < array.length; i++) {
			if (array[i] > array[max]) {
				max = i;
			}
		}
		
		return max;
	}
}
```

## 2. 找出数组中最小值的下标位置

```java
class Task2 {
	public static void main(String[] args) {
		int[] array = {31, 2, 54, 135, 963, 14, 735};
		
		System.out.println("最小值的下标位置为：" + seekIndexOfNum(array));
	}
	
	/**
	* 找出数组中最小值的下标位置
	*
	* @param array 传入一个数组
	* @return 返回最小值所在的下标
	*/
	public static int seekIndexOfNum(int[] array) {
		int min = 0;
		
		for (int i = 1; i < array.length; i++) {
			if (array[i] < array[min]) {
				min = i;
			}
		}
		
		return min;
	}
}
```

## 3. 在指定位置插入指定元素

```shell
存在一个数组，数组中的元素为
	int[] array = {1, 3, 5, 7, 9, 11, 13, 15, 17, 0};
	要求
		1. 0是无效元素，仅占位使用
		2. 当前数组中【有效元素】个数为9
```

```java
class Task3 {
	public static void main(String[] args) {
		int[] array = {1, 3, 5, 7, 9, 11, 13, 15, 17, 0};
		
		iterateOver(array);
		
		insert(array, 5, 100);
		
		iterateOver(array);
	}
	
	/**
	* 在指定位置插入指定元素
	*
	* @param array 插入一个数组
	* @param index 需要插入位置的int类型的下标
	* @param num   需要插入的数据
	*/
	public static void insert(int[] array, int index, int num) {
		if (index >= array.length || index < 0) {
			System.out.println("index out of bounds！");
		}
		
		System.out.println("执行 insert 方法----------------------");
		
		for (int i = array.length - 1; i > index; i--) {			
			array[i] = array[i - 1];
		}
		
		array[index] = num;
	}
	
	/**
	* 遍历数组
	*
	* @param array 插入一个数组
	*/
	public static void iterateOver(int[] array) {
		System.out.print("当前数组的元素为：[");
		
		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i] + " ");
		}
		
		System.out.println("]");
	}
}
```

### 改进：

```java
class Task3 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		int[] array = new int[5];		
		
		add(array, scanner);
		
		iterateOver(array);	
		
		iterateOver(insert(addLength(array), scanner));
	}

	
	/**
	* 给数组添加元素
	*
	* @param array 传入一个数组
	* @param scanner 传入一个扫描器，用以接收数据添加到数组中
	*/
	public static void add(int[] array, Scanner scanner) {
		for (int i = 0; i < array.length; i++) {
			System.out.println("请输入一个数：");
			array[i] = scanner.nextInt();
		}	
	}
	
	/**
	* 在指定位置插入指定元素
	*
	* @param array 插入一个数组
	* @param 传入一个扫描器，用以获取插入位置的下标和数据
	* @return 返回插入过数据的数组
	*/
	public static int[] insert(int[] array, Scanner scanner) {		
		System.out.println("请输入需要插入的下标：");
		int index = scanner.nextInt();
		
		System.out.println("请输入需要插入的数据：");
		int num = scanner.nextInt();
		
		for (int i = array.length - 1; i > index; i--) {					
			array[i] = array[i - 1];
		}

        array[index] = num;
		return array;
	}
	
	/**
	* 给数组增加一个长度 java.util.Arrays.copyOf(原数组, 新容量);
	*
	* @param array 传入一个数组
	* @return 返回容量+1的新数组
	*/
	public static int[] addLength(int[] array) {
		int[] newArray = java.util.Arrays.copyOf(array, array.length + 1);
		
		return newArray;
	}
	
	/**
	* 遍历数组
	*
	* @param array 插入一个数组
	*/
	public static void iterateOver(int[] array) {
		System.out.println("数组的元素为：");
		
		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i] + " ");
		}
		
		System.out.println();
	}
}
```

## 4. 删除数组中的指定下标的元素

```shell
存在一个数组，数组中的元素为
	int[] array = {1, 3, 5, 7, 9, 11, 13, 15, 17, 19};
		要求:
			1. 0是无效元素，仅占位使用
		需求:
			在当前数组中删除指定下标的元素
		例如:
			删除下标5的元素
			结果 {1, 3, 5, 7, 9, 13, 15, 17, 19, 0} 
			0占位！！！
```

```java
class Task4 {
	public static void main(String[] args) {
		int[] array = {1, 3, 5, 7, 9, 11, 13, 15, 17, 19};
		
		iterateOver(array);
		
		delete(array, 0);
		
		iterateOver(array);
	}
	
	/**
	* 删除数组中的指定下标的元素
	*
	* @param array 插入一个数组
	* @param index 指定删除的下标位置 int类型
	*/
	public static void delete(int[] array, int index) {
		System.out.println("delete方法执行-------------------");
		
		for (int i = index; i < array.length - 1; i++) {
				int temp = array[i];
				array[i] = array[i + 1];
				array[i + 1] = temp;
		}
		
		array[array.length - 1] = 0;
	}
	
	/**
	* 遍历数组
	*
	* @param array 插入一个数组
	*/
	public static void iterateOver(int[] array) {
		System.out.print("当前数组的元素为：[");
		
		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i] + " ");
		}
		
		System.out.println("]");
	}
}
```

## 5. 找出指定元素在指定数组中所有下标位置

### 5.1 不使用 int[] 数组作为返回值

```shell
需求：
		1、不允许在方法内打印展示
		2、考虑多个数据情况
		3、需要在方法外获取到下标数据信息
		4、不允许使用数组作为返回值
```

```java
class Task5 {
	public static void main(String[] args) {
		int[] array = {3, 3, 5, 3, 9, 11, 3, 15, 3, 3};
		
		iterateOver(array);
		
		int index = 0;
		
		System.out.println("指定元素的下标为：");
		
		while (index < array.length) {
			int result = showIndexOfNum(array, 3, index);
		
			if (-1 == result) {
				System.out.print("当前元素不存在");
				break;
			}
		
			if (index == result) {
				System.out.print(result + " ");
			}
						
			index++;
		}				
	}
	
	/** 
	* 找出指定元素在指定数组中所有下标位置
	*
	* @param array 插入一个数组
	* @param num 指定的元素 int类型
	* @param index 插入下标 从下标位置开始检索
	* @return int类型的下标 如果指定元素不存在就返回-1
	*/
	public static int showIndexOfNum(int[] array, int num, int index) {		
		for (int i = index; i < array.length; i++) {
			if (num == array[i]) {				
				index = i;	
				return index;
			}
		}
		
		return -1;
	}
	
	/**
	* 遍历数组
	*
	* @param array 插入一个数组
	*/
	public static void iterateOver(int[] array) {
		System.out.print("当前数组的元素为：[");
		
		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i] + " ");
		}
		
		System.out.println("]");
	}
}
```

### 5.2 使用 int[] 数组作为返回值

```java
import java.util.Scanner;

class Task5 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		int[] array = new int[5];
		
		addNumber(scanner, array);
		
		printArrayNumber(array);
		
		seekIndex(array, scanner);
	}
	
	/**
	* 找出指定元素在指定数组中所有下标位置，将下标依次存入 newArray 中，然后跳转到printArrayIndex方法
	*
	* @param array 传入一个数组
	* @param scanner 键盘录入需要查找的元素
	*/
	public static void seekIndex(int[] array, Scanner scanner) {
		int[] newArray = new int[array.length];
		int capacity = newArray.length;
		
		System.out.println("请输入需要查询的元素：");
		int num = scanner.nextInt();
		
		for (int i = 0; i < array.length; i++) {			
			if (num == array[i]) {
				newArray[newArray.length - capacity] = i;
				capacity--;
			}			
		}	
		
		// 此方法的功能为打印 newArray 中的元素，即 array 数组中指定元素的所有下标
		printArrayIndex(newArray, num);			
	}
	
	/**
	* 给数组添加元素
	*
	* @param array 传入一个空数组
	* @param scanner 扫描器
	* @return array 返回一个有元素的int数组
	*/
	public static int[] addNumber(Scanner scanner, int[] array) {
		for (int i = 0; i < array.length; i++) {
			System.out.println("请输入一个数：");
			int num = scanner.nextInt();
			
			array[i] = num;
		}
		
		return array;
	}
	
	/**
	* 打印数组下标
	*
	* @param array 传入一个数组
	* @param num 查找的元素
	*/
	public static void printArrayIndex(int[] array, int num) {
		System.out.println("元素 " + num + " 在数组中的下标位置为：");
		
		System.out.print(array[0] + " ");
		
		for (int i = 1; i < array.length; i++) {
			
			if (array[i] == 0) {
				break;
			}
			System.out.print(array[i] + " ");
		}
				
		System.out.println();
	}
	
	/**
	* 打印数组元素
	*
	* @param array 传入一个int数组
	*/
	public static void printArrayNumber(int[] array) {
		System.out.println("该数组的元素为：");
		
		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i] + " ");
		}
		
		System.out.println();
	}
}
```

## 6. 找出数组中最大值元素，放到下标为0的位置

```java
class Task6 {
	public static void main(String[] args) {
		int[] array = {31, 2, 54, 135, 963, 1224, 735};
		
		iterateOver(array);
		
		replaceOfMax(array);
		
		iterateOver(array);
	}
	
	/**
	* 找出数组中最大值元素，放到下标为0的位置
	*
	* @param array 插入一个数组
	*/
	public static void replaceOfMax(int[] array) {
		System.out.println("找出最大值后：");
		
		for (int i = 1; i < array.length; i++) {
			if (array[0] < array[i]) {
				int temp = array[0];
				array[0] = array[i];
				array[i] = temp;
			}
		}	
	}
	
	/**
	* 遍历数组
	*
	* @param array 插入一个数组
	*/
	public static void iterateOver(int[] array) {
		System.out.print("当前数组的元素为：[");
		
		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i] + " ");
		}
		
		System.out.println("]");
	}
}
```

## 7. 找出数组中最大值元素，放到下标为0的位置，第二大的值放在下标1的位置

```java
class Task7 {
	public static void main(String[] args) {
		int[] array = {31, 2, 54, 135, 963, 1224, 735};
		
		iterateOver(array);
		
		replaceOfMax(array);
		
		iterateOver(array);
	}
	
	/**
	* 找出数组中最大值元素，放到下标为0的位置，第二大的值放在下标1的位置
	*
	* @param array 插入一个数组
	*/
	public static void replaceOfMax(int[] array) {
		System.out.println("找出最大值的前两个值后：");
		
		for (int j = 0; j < 2; j++) {
			for (int i = j + 1; i < array.length; i++) {					
				if (array[j] < array[i]) {
					int temp = array[j];
					array[j] = array[i];
					array[i] = temp;
				}
			}			
		}	
	}
	
	/**
	* 遍历数组
	*
	* @param array 插入一个数组
	*/
	public static void iterateOver(int[] array) {
		System.out.print("当前数组的元素为：[");
		
		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i] + " ");
		}
		
		System.out.println("]");
	}
}
```

## 8. 找出数组中最大值元素，放到下标为0的位置，第二大的值放在下标1的位置，第三大的值放在下标为2的位置

```java
class Task8 {
	public static void main(String[] args) {
		int[] array = {31, 2, 54, 135, 963, 1224, 735};
		
		iterateOver(array);
		
		replaceOfMax(array);
		
		iterateOver(array);
	}
	
	/**
	* 找出数组中最大值元素，放到下标为0的位置，第二大的值放在下标1的位置
	* 第三大的值放在下标为2的位置
	*
	* @param array 插入一个数组
	*/
	public static void replaceOfMax(int[] array) {
		System.out.println("找出最大值的前两个值后：");
		
		for (int j = 0; j < 3; j++) {
			for (int i = j + 1; i < array.length; i++) {						
				if (array[j] < array[i]) {
					int temp = array[j];
					array[j] = array[i];
					array[i] = temp;
				}
			}			
		}	
	}
	
	/**
	* 遍历数组
	*
	* @param array 插入一个数组
	*/
	public static void iterateOver(int[] array) {
		System.out.print("当前数组的元素为：[");
		
		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i] + " ");
		}
		
		System.out.println("]");
	}
}
```

## 9. 选择排序算法

```java
class Task9 {
	public static void main(String[] args) {
		int[] array = {31, 52, 4, 135, 963, 1224, 735};
		
		iterateOver(array);
		
		sort(array);
		
		iterateOver(array);
	}
	
	/**
	* 选择排序
	*
	* @param array 插入一个数组
	*/
	public static void sort(int[] array) {
		System.out.println("选择排序(从大到小)：");
		
		for (int j = 0; j < array.length - 1; j++) {
			for (int i = j + 1; i < array.length; i++) {						
				if (array[j] < array[i]) {
					int temp = array[j];
					array[j] = array[i];
					array[i] = temp;
				}
			}			
		}	
	}
	
	/**
	* 遍历数组
	*
	* @param array 插入一个数组
	*/
	public static void iterateOver(int[] array) {
		System.out.print("当前数组的元素为：[");
		
		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i] + " ");
		}
		
		System.out.println("]");
	}
}
```

## 10. 冒泡排序算法

```java
class Task10 {
	public static void main(String[] args) {
		int[] array = {31, 52, 4, 135, 963, 1224, 735};
		
		iterateOver(array);
		
		sort(array);
		
		iterateOver(array);
	}
	
	/**
	* 冒泡排序
	*
	* @param array 插入一个数组
	*/
	public static void sort(int[] array) {
		System.out.println("冒泡排序(从大到小)：");
		
		for (int i = 1; i < array.length; i++) {
			for (int j = 0; j < array.length - i; j++) {
				if (array[j] < array[j + 1]) {
					int temp = array[j];
					array[j] = array[j + 1];
					array[j + 1] = temp;
				}
			}
		}
	}
	
	/**
	* 遍历数组
	*
	* @param array 插入一个数组
	*/
	public static void iterateOver(int[] array) {
		System.out.print("当前数组的元素为：[");
		
		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i] + " ");
		}
		
		System.out.println("]");
	}
}
```

