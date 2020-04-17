





## 1. 运算符

### 1.1 算术运算符(二元运算符)

```
+
	加
-
	减
*
	乘
/
	除
%
	取余
=
	赋值
+=
	加赋值
-=
	减赋值
*= 
	乘赋值
/=
	除赋值
%=
	取余赋值
```

```java
class TestOperator{
	public static void main(String[] args){
		int num1 = 20;
		int num2 = 10;
	
		int result1 = num1 + num2;
		System.out.println(result1);	// 30

		int result2 = num1 - num2;
		System.out.println(result2);	// 10
	
		int result3 = num1 * num2;
		System.out.println(result3);	// 200
	
		int result4 = num1 / num2;
		System.out.println(result4);	// 2
	
		int result5 = num1 % num2;
		System.out.println(result5);	// 0
		
		System.out.println("----------------");
			
		num1 += num2;
		System.out.println(num1);	// 30
				
		num1 -= num2;
		System.out.println(num1);	// 20
			
		num1 *= num2;
		System.out.println(num1);	// 200
			
		num1 /= num2;
		System.out.println(num1);	// 20
				
		num1 %= num2;
		System.out.println(num1);	// 0
	}
}
```

【注意】

​	1、代码自顶向下，从左到右运行

​	2、变量需要先赋值(初始化)后才能进行操作

​	2、优先级问题：小括号的优先级最高，赋值的优先级可以说是最低。乘除的优先级大于加减

​	3、小括号里面的内容对于小括号外部而言是一个整体，是一个【常量】 

​	4、取余只能对整数进行操作，小数不能取余

### 1.2 一元运算符

```shell
++ 
	自增
--
	自减
```

```java
class TestOperator2 {
	public static void main(String[] args){
		int num1 = 10;
		int num2 = 20;
		
		System.out.println(num1++);	// 10
		System.out.println(num1);	// 11
		
		System.out.println(++num2);	// 21
		System.out.println(num2);	// 21
	}
}
```

【注意】

​	1、自增自减运算符【有且只能操作变量】，不可以操作常量

​	2、开发中应尽量减少或者规范化使用自增自减运算符，规范化使用指自成一行

```
++ 自增运算符 操作的变量自增1 等价于 += 1
-- 自减运算符 操作的变量自减1 等价于 -= 1
++a; or a++; 自成一行，没有歧义
```

​	3、变量在前，操作的是未进行加1操作的变量，即先运算再赋值加1；变量在后，操作的是进行加1操作后的变量，即先赋值加1再运算

```java
++a :先运算再赋值
a++ :先赋值再运算
```

### 1.3 关系运算符

```
>
	大于
<
	小于
>=
	大于等于
<=
	小于等于
==
	等于
!=
	不等于
```

```java
class TestOperator3{
	public static void main(String[] args){
		boolean result = false;
		
		result = 5 > 3;
		System.out.println(result);	// true
		
		result = 5 < 3;
		System.out.println(result);	// fale
		
		result = 5 >= 3;
		System.out.println(result);	// true
		
		result = 5 <= 3;
		System.out.println(result);	// false
		
		result = 5 == 3;
		System.out.println(result);	// false
		
		result = 5 != 3;
		System.out.println(result);	//true
	}
}
```

【注意】

​	1、关系运算符判断的结果为一个Boolean类型的值，只能是 true 或 false

​	2、一般用于逻辑判断，条件过滤

### 1.4 逻辑运算符

```
&&	与	同真即为真，有假即为假
||	或	同假即为假，有真即为真
!	非	取反
```

```java
class TestOperator4{
	public static void main(String[] args){
		boolean result = false;
		
		result = 5 > 3 && 5 > 4;
		System.out.println(result);	// true
		
		result = 5 > 3 && 5 > 6 ;
		System.out.println(result);	// false
		
		result = 5 > 6 && 5 > 3;
		System.out.println(result);	// false
		
		System.out.println("----------------");
		
		result = 5 > 6 || 5 > 7;
		System.out.println(result);	// false
		
		result = 5 > 3 || 5 > 6 ;
		System.out.println(result);	// true
		
		result = 5 > 6 || 5 > 3;
		System.out.println(result);	// true
		
		System.out.println("----------------");
		
		result = !(5 > 3);
		System.out.println(result);	// false
		
		result = !(5 > 6);
		System.out.println(result);	// true
	}
}
```

【注意】

​	1、关系运算符判断的结果为一个Boolean类型的值，只能是 true 或 false

​	2、一般用于逻辑判断，条件过滤

​	3、逻辑运算符的短路原则：（可以节约计算机性能）

​		&&	如果第一个表达式为假，则不再判断和执行后面的表达式

​		||	如果第一个表达式为真，则不再判断和执行后面的表达式

```java
class TestOperator5 {
	public static void main(String[] args){
		int num = 5;
		boolean result = num < 0 && num++ > 0;
		
		System.out.println(result);	// false
		System.out.println(num);	// 5
		
		result = num++ > 0 || --num < 0;
		
		System.out.println(result);	// true
		System.out.println(num);	// 6
	}
}
```

### 1.5 三目运算符

```
? :
格式：布尔表达式 ? 结果1 : 结果2
```

```java
class TestOperator6 {
	public static void main(String[] args) {
		int num = 5;
		boolean result = false;
		num = result ? num++ : --num;
		
		System.out.println(num);	// 4
	}
}
```

【注意】先对布尔表达式进行判断，如果为真，输出结果1，如果为假，输出结果2

### 1.6 总结

```
1、优先级：小括号的优先级最高，赋值的优先级最低，先乘除后加减，先 && 后 ||
2、小括号里面的内容对于小括号外部而言是一个整体，是一个【常量】
3、只有变量才能执行自增自减操作，不能使用变量的值进行自增自减操作
4、a++ :先运算后赋值；++a :先赋值后运算
5、逻辑运算符的短路原则，如果第一个条件可以判断出结果，就不再往后执行，以达到节约性能的目的
6、Java 中优先级高的表达式会被视为一个整体（如小括号相较于其他运算符，或 && 相较于 || ），但是执行顺序还是从左到右。在此基础上才会执行短路原则
```

## 2.面试题

### 2.1 面试题1

```java
class TestOperatorQuestion1{
	public static void main(String[] args){
		int num = 5;
		int result = num++ * ++num;
		
		System.out.println(result); // 35
		System.out.println(num);	// 7
	}
}
```

【注意】

​	a++ 先参与运算再赋值，++a 先赋值再参与运算



### 2.2 面试题2

```java
class TestOperatorQuestion2{
	public static void main(String[] args){
		int num = 5;
		++(num++);

		System.out.println(num);	// 报错：意外的类型			
	}
}
```

【注意】

​	只有变量才能执行自增自减操作，变量的值是常量，无法执行自增自减操作

小括号内的值优先度最高，对外显示的一个值，即一个常量，而常量无法进行自增操作，

同理：++a++ 也是错误的



### 2.3 面试题3

```java
class TestOperatorQuestion3{
	public static void main(String[] args){
		int num = 5;
		boolean result = false;
		
		result = num++ < 4 && (--num > 4 || num++ > 4);
		
		System.out.println(result);	// false
		System.out.println(num);	// 6		
	}
}
```

【注意】

​	1、逻辑与 后面的表达式需要先判断，那么两个条件不管是 true 还是 false 都需要判断；前面的表达式先判断得话，如果为 false 就不做后面表达式的判断

​	2、小括号的优先级大于 && 大于 || 大于 =



### 2.4 面试题4：求闰年

```java
import java.util.Scanner;

class TestOperatorQuestion4{
	public static void main(String[] args){

		Scanner sc = new Scanner(System.in);
		System.out.println("请输入一个年份：");		
		int year = sc.nextInt();
		
		if((year % 4 == 0 && year % 100 != 0) || year % 400 == 0){
			System.out.println("这是闰年");
		}else{
			System.out.println("非闰年");
		}
	}
}
```

【注意】

​	四年一闰，百年不闰，四百年再闰。即 能被4整除且不能被100整除 或 能被400整除

## 3. 作业

### 1. 写出判断【数字字符】的条件

```java
	char ch = ' ';
	boolean result = ch >= '0' && ch <= '9';
```

### 2. 写出判断数值0 ~ 9的条件

```java
	int num = 0;
	boolean result = num >= 0 && num <= 9; 
```

### 3. 代码阅读 

```java
int num = 5;
int ret = num++ - num++;
ret ? num ?
		
	A:	
		ret = -1;
		num = 7;
```

### 4. 代码阅读 

```java
int num = 10;
int ret = ++num % num--;
ret ? num?
		
	A:
		ret = 0;
		num = 10;
```

### 5. 代码阅读 

```java
int num1 = 10;
int num2 = 20;
	
int ret = num1 % num2;
ret = ?
ret = num1 / num2;
ret = ?
		
	A:
		ret = 10;
		ret = 0;
```

