# 数组

## 1. 数组作为参数传递

### 1.1 数组的遍历

```java
class TestArray1 {
	public static void main(String[] args) {
		int[] array = {1, 2, 3, 4, 5, 6, 7, 8, 9};
		
		iterateOver(array);
	}
	
	/**
	* 遍历数组并打印元素
	*
	* @param array 传入需要遍历的数组
	*/
	public static void iterateOver(int[] array) {
		System.out.println("当前数组的元素为：");
		
		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i] + " ");
		}
		
		System.out.println();
	}
}
```

### 1.2 获取最值

```java
class TestArray2 {
	public static void main(String[] args) {
		int[] array = {34,98,10,25,67};
		
		int max = getMax(array);
		System.out.println("max:"+max);
			
		int min = getMin(array);
		System.out.println("min:"+min);
	}
	
	/**
	* 获取数组中的最大值
	*
	* @param array 传入一个int类型的数组	
	*/
	public static int getMax(int[] array) {
		int max = array[0];
        
		for(int x=1; x<array.length; x++) {
			if(array[x] > max) {
				max = array[x];
			}
		}

		return max;
	}
	
    /**
	* 获取数组中的最小值
	*
	* @param array 传入一个int类型的数组	
	*/
	public static int getMin(int[] array) {
		int min = array[0];

		for(int x=1; x<array.length; x++) {
			if(array[x] < min) {
				min = array[x];
			}
		}

		return min;
	}
}
```

### 1.3 替换数组中指定数据

```java
class TestArray3 {
	public static void main(String[] args) {
		int[] array = {1, 2, 3, 4, 5, 4, 3, 5, 3, 1};
		
		iterateOver(array);
		
		replace(array, 5, 100);
		
		iterateOver(array);
	}
	
	/**
	* 替换方法，将指定元素替换
	*
	* @param array 传入一个数组
	* @param oldNum 传入需要被替换的数据
	* @param newNum 传入替换的数据
	*/
	public static void replace(int[] array, int oldNum, int newNum) {
		for (int i = 0; i < array.length; i++) {
			if (oldNum == array[i]) {
				array[i] = newNum;
			}
		}
	}
	
	/**
	* 遍历数组并打印元素
	*
	* @param array 传入需要遍历的数组
	*/
	public static void iterateOver(int[] array) {
		System.out.println("当前数组的元素为：");
		
		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i] + " ");
		}
		
		System.out.println();
	}
}
```

### 1.4 数组的逆序

```java
class TestArray4 {
	public static void main(String[] args) {
		int[] array = {1, 2, 3, 4, 5, 6, 7, 8, 9, 10};
		
		iterateOver(array);
		
		reverse(array);
		
		iterateOver(array);
	}
	
	/**
	* 逆序数组
	*
	* @param array 传入需要逆序的数组
	*/
	public static void reverse(int[] array) {
		System.out.println("执行逆序操作~");
		
		for (int i = 0; i < array.length / 2; i++) {
			int temp = array[i];
			array[i] = array[array.length - 1 - i];
			array[array.length - 1 - i] = temp;
		}
	}
	
	/**
	* 遍历数组并打印元素
	*
	* @param array 传入需要遍历的数组
	*/
	public static void iterateOver(int[] array) {
		System.out.println("当前数组的元素为：");
		
		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i] + " ");
		}
		
		System.out.println();
	}
}
```

### 1.5 总结

```java
1、数组作为形参：
    (数组类型[] 数组名)

2、数组作为实参
    (数组名)
    
3、数组作为参数，是将数组的地址复制一份传递给形参，形参对数组名的操作不会影响实参本身(值传递)。对数组内的元素做操作才会影响到实参本身(引用传递)
```

```java
class Test {
	public static void main(String[] args) {
		int[] array1 = new int[3];
		int[] array2 = new int[5];
		
		method(array1, array2);
				
		System.out.println(array1.length);	// 3
		System.out.println(array2.length);	// 5
	}
	
	/**
	* 传入两个数组，互换其首地址
	* 
	* @param array1 传入的第一个数组
	* @param array2 传入的第二个数组
	*/
	public static void method(int[] array1, int[] array2) {
		array1 = array2;
		
		System.out.println(array1.length);	// 5
		System.out.println(array2.length);	// 5
		System.out.println("--------------");
	}
}
```

## 2. 地址转移分析

```java
int[] array1 = new int[3];
int[] array2 = new int[3];
		
array1[0] = 10;
array2[0] = 20;
		
array1[2] = 30;
		
array2 = array1;
		
array1[0] = 40;
array2[0] = 50;
				
System.out.println(array1[0]);
System.out.println(array2[0]);
```

![](https://p.pstatp.com/origin/feb90000df52e4cedd6e)

## 3. 数组作为参数传递分析

```java
int[] array ={1, 2, 3};
		
int num = seek(array, 1);
	
public static int seek(int[] array, int index) {
		return array[index];
}
```

![](https://pic.images.ac.cn/image/5ea2f0c0d83f8.html)

