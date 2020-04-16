# 流程控制语句

流程控制语句分为

```java
1、顺序结构：自顶向下，从左往右，依次执行
2、选择分支结构：根据不同的选择，执行不同的代码
3、循环结构：重复执行代码
```

## 1. 选择分支结构

### 1.1 if 结构

#### 1.1.1 if 分支结构

```java
格式：
    if (判断条件) {
        代码块
    }
执行流程：
    首先进行条件判断，如果为真就大括号内的代码，如果为假则跳过大括号内的代码继续执行后面的代码
```

```java
class TestIf {
	public static void main(String[] args) {
		int num = 100;
		
		if (num > 0) {
			num++;
		}
		
		System.out.println(num);	// 101
	}
}
```

#### 1.1.2 if else 分支结构

```java
格式：
    if (判断条件) {
        代码块1
    } else {
        代码块2
    }
执行流程：
    首先进行条件判断，如果为真就执行代码块1，如果为假则执行代码块2
```

```java
/*
	需求：
		A:获取两个数据中较大的值
		B:判断一个数据是奇数还是偶数,并输出是奇数还是偶数
*/

class TestIfElse {
	public static void main(String[] args) {
		int num1 = 5;
		int num2 = 10;
		int maxNum = 0;		
		
		if(num1 > num2){
			maxNum = num1;
		} else {
			maxNum = num2;
		}
        
		System.out.println("最大值为：" + maxNum);
	}
}
```

#### 1.1.3 if else if 分支结构

```java
格式：
    if (判断条件1) {
        代码块1
    } else if (判断条件2) {
        代码块2
    } else {
        代码块3
    }
执行流程：
    首先进行条件判断，如果为真就执行代码块1，如果为假则继续判断第二个条件，如果为真则执行代码块2，否则执行代码块3
```

```java
/*
	需求：键盘录入x的值，计算出y的并输出。					
		x>=3	y = 2x + 1;
		-1<=x<3	y = 2x;
		x<=-1	y = 2x – 1;
*/	

import java.util.Scanner;

class TestIfElseIf {
	public static void main(String[] args) {	
		Scanner scanner = new Scanner(System.in);
		System.out.println("请输入一个整数：");
		
		int num = scanner.nextInt();
		int result = 0;
		
		if (num>=3) {
			result = 2 * num + 1;
		} else if (-1 <= num) {
			result = 2 * num;
		} else {
			result = 2 * num -1;
		}
		
		System.out.println("result = " + result);
	}
}
```

#### 1.1.4 总结

```java
1、if 语句中的各个代码块相互排斥，只要有一个条件为真，就不会进行其他代码的判断，也不会执行其他代码
2、if 语句常用于区间判断
3、判断条件必须为布尔表达式，无论长短
4、if 语句不建议省略大括号
5、一般来说，有左大括号存在就没有分号，有分号就没有左大括号
6、else 后面没有 if 的话不会出现判断条件
7、else if 的个数不受限制，可以用于多个条件的判断
8、三元运算符和 if 语句的关系：
    所有的三元运算符能够实现的，if语句都能实现。反之不成立。
		比如：如果if语句的代码块是输出语句，就不可以。因为三元运算符是一个运算符，必须要有一个结果返回，不能是一个输出语句。
```

### 1.2 switch 分支结构

## 2. 控制台录入

### 2.1 Scanner

```java
Scanner 使用流程：
    1、导包
    	import java.util.Scanner;
		位置：class上面，package下面
    2、创建对象
        Scanner scanner = new Scanner(System.in);
    3、获取数据
        int num = scanner.nextInt();
		float num = scanner.nextFloat();
		Double num = scanner.nextDouble();
		char ch = scanner.nextLine().charAt(0);
		String str = scanner.next();       
```

【注意】

1、用户友好性提示

```java
代码运行需要站着用户的角度来思考问题。用户进行操作时，需要给予用户足够的提示和引导，告知用户当前操作如何完成，考虑代码的友好性！！！
	用户粘性问题！！！用户提示！！！用户友好性！！！
```

2、对录入数据进行合法性判断

```java
就算在提示中告知用户需要输入的数据范围是多少，但是用户在实际使用的过程中，依然存在输入错误的情况。需要对于用户输入的数据进行合法性判断，如果用户输入的内容符合我们的判断逻辑需求，进入数据处理过程。如果不符合要求，直接终止程序！！！
```

【补充】

```java
// 程序退出
System.exit(0);
```

## 3. 作业

### 3.1 判断奇偶

```java
import java.util.Scanner;

class TestIfJob {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请输入一个整数：");
		
		int num = scanner.nextInt();
		
		if(num % 2 == 0){
			System.out.println("这是一个偶数");
		} else {
			System.out.println("这是一个奇数");
		}
	}
}
```

### 3.2 判断浮点型数据类型

```java
import java.util.Scanner;

class TestIfJob2 {
	public static void main(String[] args){
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请输入一个浮点型的数据：");
		
		float num = scanner.nextFloat();
		
		if (num > 99.99) {
			System.out.println("您是VVIP");
		} else {
			System.out.println("您是VIP");
		}
	}
}
```

### 3.3 判断游戏段位

小于等于1000	青铜
1000 - 1200		白银
1200 - 1400		黄金
1400 - 1600		白金
1600 - 1800		钻石
1800 - 2000		大师
2000以上			王者

```java
import java.util.Scanner;

class TestIfJob3 {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请输入一个整数：");
		
		int num = scanner.nextInt();
		
		if (num < 0 || num > 5000) {
			System.out.println("输入了非法的数据~");
			System.exit(0);
		}
		
		if(num <= 1000){
			System.out.println("您的段位是青铜~");
		} else if (num <= 1200) {
			System.out.println("您的段位是白银~");
		} else if (num <= 1400) {
			System.out.println("您的段位是黄金~");
		} else if (num <= 1600) {
			System.out.println("您的段位是白金~");
		} else if (num <= 1800) {
			System.out.println("您的段位是钻石~");
		} else if (num <= 2000) {
			System.out.println("您的段位是大师~");
		} else {
			System.out.println("您的段位是王者~");
		}
	}
}
```

