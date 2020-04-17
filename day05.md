# 流程控制

## 1. 循环结构

### 1.1 循环的组成

```shell
1、初始部分	循环用以判断的变量
2、循环条件	决定是否继续循环的依据
3、循环操作	一次循环所要执行的逻辑代码
4、迭代部分	使循环条件改变的增量
```

### 1.2 while 循环结构

```shell
格式：
	while (判断条件) {
		代码块
		控制条件语句
	}
	
执行流程：
	当程序运行到 while 循环结构时，首先判断 while 后面的条件是否为 true ，如果为 true 就执行大括号内的代码，执行完毕后再次对 while 后面的条件进行判断，直到判断的结果为 false 才终止
```

```java
/*
	打印1~100的和
*/

class TestWhile3 {
	public static void main (String[] args) {
		int num = 1;
		int sum = 0;
		
		while (num <= 100) {
			sum += num;
			num++;
		}
		
		System.out.println("sum：" + sum);	// 5050
	}
}
```

【注意】

```shell
1、while 语句首次执行具有入口条件，先判断再执行，如果第一次为 false 就不执行

2、while 语句适用于循环次数明确的场景
```

### 1.3 do while 循环结构

```shell
格式：
	do {
		代码块
		控制条件语句
	} while (判断条件);
	
执行流程：
	当程序执行到 do - while 语句时，先执行一遍大括号内的代码，再对 while 后面的条件进行判断，如果为 true 就循环执行，如果为 false 就终止
```

```java
/*
	打印1 ~ 100 所有的偶数
*/

class TestDoWhile {
	public static void main (String[] args) {
		int num = 2;
		
		do {
			System.out.println(num);
			num += 2;
		} while (num <= 100);
	}
}
```

```java
/*
	打印大写字母A ~ Z
*/

class TestDoWhile3 {
	public static void main (String [] args) {
		char ch = 'A';
		
		do {
			System.out.println(ch);
			ch++;	// 	编译通过
			// ch += 1; 编译通过
			// ch = ch + 1;	编译失败
			// char类型与int类型相加结果应为int类型，用char类型接收可能会丢失精度
		} while (ch <= 'Z');
	}
}
```

【注意】

```
1、do - while 语句首次执行没有入口条件，先执行后判断

2、do - while 语句适用于循环次数不明确的场景

3、while 后面的小括号后面需要加上 ; 表示一行语句的结束
```

### 1.4 for 循环

### 1.5 控制跳转关键字

break

continue

return

### 1.6 循环嵌套

```java
/*
	周一上语文课
	周二上数学课
	周三上英语课
	周四上美术课
	周五上音乐课
	周六上体育课
	周日不上课
*/

import java.util.Scanner;

class TestNest {
	public static void main (String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请输入今天是周几(1~7)：");
		
		int date = 0;
		
		do {
			date = scanner.nextInt();
		
			switch (date) {
				case 1:
					System.out.println("今天是周一，要上语文课~");
					break;
				case 2:
					System.out.println("今天是周二，要上数学课~");
					break;
				case 3:
					System.out.println("今天是周三，要上英语课~");
					break;
				case 4:
					System.out.println("今天是周四，要上美术课~");
					break;
				case 5:
					System.out.println("今天是周五，要上音乐课~");
					break;
				case 6:
					System.out.println("今天是周六，要上体育课~");
					break;
				case 7:
					System.out.println("今天是周日不需要上课了~");
					break;
				default:
					System.out.println("输入了非法的数据！！！");
					break;
			}
		} while (date != 7);		
	}
}
```

### 1.7 总结

```shell
1、循环过程中最核心的内容就是循环变量，需要对于循环变量的执行的过程中数值变量完全掌握！！！如果无法明确循环的次数，循环变量的值，循环的过程，可以将循环代码中变量的变更过程记录。

2、循环过程中需要注意无限循环问题，控制无限循环问题的出现。一定要保证循环条件有效性或者代码中存在一个跳出循环的机制。

3、do while 循环中，第一次循环体的执行是没有经过任何的条件判断的，需要注意！

4、while 、 do while 、 for 之间可以相互转换，一般使用 while 和 for 多一点
```



## 2. 作业

```shell
1. 表达式（立方）	
		编写程序，计算用户输入数据的立方
    2. 表达式（取值操作）	
        输入4个数，若第一个数第二个数相等，第三个数和第四个数的
        和与第一个数和第二个数的和相等，输出1，否则输出0
    3. 流程控制（数值比较1）	
    	定义两个整型变量x,y，从键盘初始化变量值，判断两个变量的大小，将较大的值赋
    	给变量max,将max输出,注意输入使用Scanner输入 
    4. 流程控制（数值比较2）	
    	定义三个整型变量x,y,z，从键盘初始化变量值，判断三个变量的大小，将较大的值
    	赋给变量max，将max输出,注意输入使用Scanner输入 
    5. 流程控制（月份天数判断）	
    	输入一个月数，然后输出对应月份有多少天（不考虑闰年），将天数输出,注意输入
    	使用Scanner输入 
    	比如：
       		输入 6  输出为30
        	输入 2  输出为28
    6. 完成一个9*9乘法表
	7. 将一个正整数进行分解质因数操作 例如: 输入90 结果 2*3*3*5
	8. 使用循环完成30位以内的斐波那契数列
		1 1 2 3 5 8 11 19...
	9. 利用循环完成15的阶乘
	10. 判断一个三位数是否是水仙花数,如果是,输出YES,如果不是,输出NO
	说明: 水仙花就是一个数的每个数字的立方和等于它本身的数, 例如 153就是一个水仙
	花数 1*1*1+5*5*5+3*3*3=153
	11. 逢七过，1 ~ 100以内的所有数值展示，如果带有7或者和7有关，打印过
	12. 逆序数值
		用户输入123456 展示654321
		用户输入987654 展示456789
```

