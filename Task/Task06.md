# 作业

## 1、9*9乘法表

```java
class Task1 {
	public static void main(String[] args) {
		for (int i = 1; i <= 9 ; i++) {
			for (int j = 1 ; j <= i ; j++) {
				System.out.print(j + "*" + i + "=" + j * i + "\t");
			}
			System.out.println();
		}
	}
}
```

## 2、将一个正整数进行分解质因数操作

```java
import java.util.Scanner;

class Task2 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请输入一个正整数：");
		int num = scanner.nextInt();
		
		if (num <= 0) {
			System.out.println("输入了错误的数据~");
			System.exit(0);
		}
		
		System.out.print(num + "=1");
		
		for (int index = 2; index <= num ; index++) {
			while (num % index == 0) {
				num /= index;
				System.out.print("*" + index);
				
			}
		}
	}
}
```

## 3、使用循环完成30位以内的斐波那契数列

```java
class Task3 {
	public static void main(String[] args) {
		int num1 = 0;
		int num2 = 1;
		int result = 0;
		
		System.out.print(1);
		
		for (int num = 2; num <= 30 ; num++) {
			result = num1 + num2;
			num1 = num2;
			num2 = result;
			System.out.print("\t" + result);
		}
	}
}
```

## 4、15的阶乘

```java
class Task4 {
	public static void main(String[] args) {
		long result = 1L;
		
		for (int i = 1 ; i <= 15 ; i++) {
			result *= i;
		}
		
		System.out.println(result);
	}
}
```

## 5、逢七过，1 ~ 100以内的所有数值展示

```java
class Task5 {
	public static void main(String[] args) {
		for (int i = 1 ; i <= 100; i++) {
			
			if (i % 7 == 0 || i / 10 == 7 || i % 10 == 7){
				System.out.println("过");
				continue;
			}
			
			System.out.println(i);
		}
	}
}
```

