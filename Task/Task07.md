# 作业

## 1. 将一个正整数进行分解质因数

```java
import java.util.Scanner;

class Task1 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请输入一个数：");		
		resolveNumber(scanner.nextInt());
	}
	
    /**
	* 分解质因数
	*
	* @param num 需要执行分解质因数的值 int类型
	*/
	public static void resolveNumber(int num) {
		System.out.print(num + "=1");
		
		for (int i = 2; i <= num; i++) {
			while(num % i == 0) {
				System.out.print("*" + i);
				num /= i;
			}
		}
	}
}
```

## 2. 15的阶乘

```java
class Task2 {
	public static void main(String[] args) {
		System.out.println(getFactorial(15));
	}
	
    /**
	* 求阶乘
	*
	* @param num 阶乘的最后一位 long类型
	*
	* @return total long类型的阶乘值
	*/
	public static long getFactorial(long num) {
		long total = 1;
		
		for (int i = 2; i <= num; i++) {
			total *= i;
		}
		
		return total;
	}
}
```

*****

## 3. 打印矩形

```java
class Task3 {
	public static void main(String[] args) {
		printGraphs(5);
	}
	
    /**
	* 打印矩形
	*
	* @param line 行号 ine类型
	*/
	public static void printGraphs(int line){
		for (int i = 1; i <= line; i++) {
			for (int j = 1; j <= line; j++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}
}
```

## 4. 打印直角三角形

```java
import java.util.Scanner;

class Task4 {
	public static void main(String[] args) {
		printGraphs(5);
	}
	
    /**
	* 打印直角三角形
	*
	* @param line 行号 ine类型
	*/
	public static void printGraphs(int line) {
		for (int i = 1; i <= line; i++) {
			for (int j = 1; j <= i; j++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}
}
```

## 5. 打印等腰三角形

```java
class Task5 {
	public static void main(String[] args) {
		printGraphs(5);
	}
	
    /**
	* 打印等腰三角形
	*
	* @param line 行号 ine类型
	*/
	public static void printGraphs(int line) {
		for (int i = 1; i <= line; i++) {
			for(int j = line - 1; j >= i; j--) {
				System.out.print(" ");
			}
			
			for (int k = 1; k <= 2 * i - 1; k++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}
}
```

## 6. 打印菱形

```java
class Task6 {
	public static void main(String[] args) {
		printGraphs(9);
	}
	
    /**
	* 打印菱形 
	*
	* @param line 行号 ine类型
	*/
	public static void printGraphs(int line) {
		for (int i = 1; i <= line / 2 + 1; i++) {
			for (int j = line / 2; j >= i; j--) {
				System.out.print(" ");
			}
			for (int k = 1; k <= 2 * i - 1; k++) {
				System.out.print("*");
			}
			System.out.println();
		}
		
		for (int i = line / 2; i >= 1; i--) {
			for (int j = line / 2; j >= i; j--) {
				System.out.print(" ");
			}
			
			for (int k = 1; k <= 2 * i - 1; k++) {
				System.out.print("*");
			}
			System.out.println();
		}
	}
}
```

## 7. 打印字符型等腰三角形

```java
class Task7 {
	public static void main(String[] args) {
		printGraphs(6);
	}
	
    /**
	* 打印字符型等腰三角形 
	*
	* @param line 行号 ine类型
	*/
	public static void printGraphs(int line) {
		char ch = 'A';
		
		for (int i = 1; i <= line; i++) {
			for (int j = line - 1; j >= i; j--) {
				System.out.print(" ");
			}
			
			for (int k = 1; k <= 2 * i - 1; k++) {
				System.out.print(ch);
			}
			ch++;
			System.out.println();
		}
	}
}
```

## 8. 打印字符型菱形

```java
class Task8 {
	public static void main(String[] args) {
		printGraphs(9);
	}
	
	/**
	* 打印字符型菱形
	*
	* @param line 行号 ine类型
	*/
	public static void printGraphs(int line) {
		char ch = 'A';
		
		for (int i = 1; i <= line / 2 + 1; i++) {
			for (int j = line / 2; j >= i; j--) {
				System.out.print(' ');
			}
			
			for (int k = 1; k <= 2 * i - 1; k++) {
				System.out.print(ch);
			}
			
			ch++;
			System.out.println();
		}
		
		ch--;
		for (int i = line / 2; i >= 1; i-- ) {
			for (int j = line / 2; j >= i; j--) {
				System.out.print(' ');
			}
			
			ch--;
			for (int k = 1; k <= 2 * i - 1; k++) {
				System.out.print(ch);
			}
						
			System.out.println();
		}
	}
}
```

