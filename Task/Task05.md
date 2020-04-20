# 作业

### 1、编写程序，计算用户输入数据的立方

```java
import java.util.Scanner;

class TestTask1 {
	public static void main (String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请输入一个数：");
		int num = scanner.nextInt();
		
		System.out.println("您输入的数的立方为：" + num * num * num);
	}
}
```

【注意】需要考虑可能会超出范围的问题，最好用double类型来接收

### 2、输入4个数，若第一个数第二个数相等，第三个数和第四个数的和与第一个数和第二个数的和相等，输出1，否则输出0

```java
import java.util.Scanner;

class TestTask2 {
	public static void main (String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请输入第1个数：");
		int num1 = scanner.nextInt();
		
		System.out.println("请输入第2个数：");
		int num2 = scanner.nextInt();
		
		System.out.println("请输入第3个数：");
		int num3 = scanner.nextInt();
		
		System.out.println("请输入第4个数：");
		int num4 = scanner.nextInt();
		
		if (num1 == num2 && num1 + num2 == num3 + num4) {
			System.out.println(1);
		} else {
			System.out.println(0);
		}
	}
}
```

### 3、定义两个整型变量x,y，从键盘初始化变量值，判断两个变量的大小，将较大的值赋给变量max,将max输出,注意输入使用Scanner输入

```java
import java.util.Scanner;

class TestTask3 {
	public static void main (String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请输入一个数：");
		int x = scanner.nextInt();
		System.out.println("请再输入一个数：");
		int y = scanner.nextInt();
		
		int max = x > y ? x : y;
		System.out.println("max：" + max);
	}
}
```

### 4、定义三个整型变量x,y,z，从键盘初始化变量值，判断三个变量的大小，将较大的值赋给变量max，将max输出,注意输入使用Scanner输入 

```java
import java.util.Scanner;

class TestTask4 {
	public static void main (String[] args) {
		Scanner scanner = new Scanner(System.in);
		int max = 0;
		
		System.out.println("请输入第一个数：");
		int x = scanner.nextInt();
		
		System.out.println("请输入第二个数：");
		int y = scanner.nextInt();
		
		System.out.println("请输入第三个数：");
		int z = scanner.nextInt();
		
		if (x >= y) {
			max = x;			
		} else {
			max = y;
		}
		
		if (max >= z) {
			
		} else {
			max = z;
		}
		
		System.out.println("max：" + max);
	}
}
```

改进：

```java
import java.util.Scanner;

class TestTask4 {
	public static void main (String[] args) {
		Scanner scanner = new Scanner(System.in);
		int max = 0;
		
		System.out.println("请输入第一个数：");
		int x = scanner.nextInt();
		
		System.out.println("请输入第二个数：");
		int y = scanner.nextInt();
		
		System.out.println("请输入第三个数：");
		int z = scanner.nextInt();
		
        max = x;
        
		if (y >= max) {
			max = x;			
		}
		
		if (z >= max) {
			max = z;
		}
		
		System.out.println("max：" + max);
	}
}
```

### 5、输入一个月数，然后输出对应月份有多少天（不考虑闰年），将天数输出

```java
import java.util.Scanner;

class TestTask5 {
	public static void main (String[] args) {
		Scanner scanner = new Scanner(System.in);
		System.out.println("请输入一个月数：");
		
		int month = scanner.nextInt();
		
		switch (month) {
			case 1:
			case 3:
			case 5:
			case 7:
			case 8:
			case 10:
			case 12:
				System.out.println(31);
				break;
			case 2:
				System.out.println(28);
				break;
			case 4:
			case 6:
			case 9:
			case 11:
				System.out.println(30);
				break;
			default:
				System.out.println("输入； 错误的数据");
				break;
		}
	}
}
```

【注意】1 == month，常量在前，避免少写一个等号导致的错误

### 6、9*9乘法表

```java
class TestTask6 {
	public static void main (String[] args) {		
		int i = 1 ;
		
		while (i <= 9) {
			int j = 1;
			
			while (j <= i) {
				System.out.print(j + "*" + i + "=" + j * i + "\t");
				j++;
			}
			
			System.out.println();			
			i++;
		}
	}
}
```

### 7、将一个正整数进行分解质因数操作 

```java
import java.util.Scanner;

class TestTask7 {
	public static void main (String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请输入一个正整数：");
		int num = scanner.nextInt();
		
		if (num <= 0) {
			System.out.println("输入了非法的数据~");
			System.exit(0);
		}
		
		System.out.print(num + "=1");

		for (int index = 2 ; index <= num ; index++) {
		
			while (num % index == 0) {
				num = num / index;
				System.out.print("*" + index);
			}
		}
	}
}
```

改进：

```java
import java.util.Scanner;

class TestTask7 {
	public static void main (String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请输入一个正整数：");
		int num = scanner.nextInt();
		int index = 2;
		
		if (num <= 0) {
			System.out.println("输入了非法的数据~");
			System.exit(0);
		}
		
		 System.out.print(num + "=1");

		while (index <= num) {	
            
			if (num % index == 0) {
				num = num / index;
				System.out.print("*" + index);
				index--;
			}
			
			index++;
		}
	}
}
```

### 8、30位以内的斐波那契数列

```java
class TestTask8 {
	public static void main (String[] args) {
		for (int i = 1 ; i <= 30 ;i++) {
			System.out.print(mothed(i)+"\t");
		}		
	}
	
	public static int mothed (int num) {
		
		if (num == 2 || num == 1) {
			return 1;
		}
		
		return mothed(num-1) + mothed(num-2);
	}
}
```

非递归写法：

```java
class TestTask8 {
	public static void main (String[] args) {			
		int count = 0;
		int num1 = 0;
		int num2 = 1;
		int index = 2;
		
		System.out.print(1 + "\t");
	
		while (index <= 30) {
			count = num1 + num2;		
			num1 = num2;
			num2 = count;
			System.out.print(count + "\t");
			index++;
		}
	}
}
```

### 9、15的阶乘

```java
class TestTask9 {
	public static void main (String[] args) {
		
		long total = 1;
		
		for (int num = 15 ; num > 0 ; num--) {
			total *= num;
		}
		
		System.out.println(total);	
	}
}
```

### 10、判断一个三位数是否是水仙花数,如果是,输出YES,如果不是,输出NO

```java
import java.util.Scanner;

class TestTask10 {
	public static void main (String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请输入一个三位数：");
		int num = scanner.nextInt();
		
		if (num < 100 || num > 999) {
			System.out.println("输入了非法的数据~");
			System.exit(0);
		}
		
		int hundreds = num / 100;
		int decade = num % 100 / 10;
		int unit = num % 10;
		
		if (hundreds * hundreds * hundreds + decade * decade * decade + unit * unit * unit == num) {
			System.out.println("yes");
		} else {
			System.out.println("no");
		}	
	}
}
```

### 11、逢七过，1 ~ 100以内的所有数值展示，如果带有7或者和7有关，打印过

```java
import java.util.Scanner;

class TestTask11 {
	public static void main (String[] args) {		
				
		for (int num = 1 ; num <= 100 ; num++) {
			
			int decade = num / 10;
			int unit = num % 10;
		
			if (num % 7 == 0 || decade == 7 || unit == 7) {
				continue;
			}
			
			System.out.println(num);
		}
	}
}
```

### 12、逆序数值

```java
import java.util.Scanner;

class TestTask12 {
	public static void main (String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请输入一个数：");
		int num = scanner.nextInt(); 
		
		int index = 0;
		int result = 0;
		
		while (num != 0) {
			index = num % 10;
			result += index;
			num /= 10;	
			if (num % 10 != 0){
				result *= 10;
			}				
		}
		
		System.out.println(result);
	}
}
```

```java
import java.util.Scanner;

class TestTask12 {
	public static void main (String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请输入一个数：");
		int num = scanner.nextInt(); 

		while (num > 0) {
			System.out.print(num %= 10);
            num /= 10; 
		}
	}
}
```

