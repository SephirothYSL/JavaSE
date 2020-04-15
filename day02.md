## 1. 第一行代码

```java
class FirstJava {
	public static void main(String[] args){
		System.out.println("第一个Java程序");
	}
}
```

### 1.1 编译执行代码

```shell
编译格式：javac 类名.java
	经过编译，把.java文件转换成.class文件|字节码文件
	
执行格式：java 类名
	通过不同系统的jvm解释使用
```

### 1.2 常见问题

```shell
1、类名需要和文件名完全一致，并且一定要保存为.java文件
2、注意拼写错误
3、注意标点符号错误（半圆角），成对的标点符号一次性写完 "" '' <> {} []
4、记得保存
5、保存之后重新编译，并检查是否生成了.class文件
```

## 2. 计算机中的存储

### 2.1 计算机中的存储单元

```
计算机中的最小存储单元是【字节】 byte

比特流：01010101

8bit	 == 1byte
1024byte == 1KB
1024KB	 == 1MB
1024MB   == 1GB
1024GB   == 1TB
1024TB   == 1PB
1024PB   == 1EB
```

### 2.2 进制关系

```
二进制
八进制（0开头）	每三位二进制数表示一位八进制数
十进制
十六进制（0x或者0X开头）	每四位二进制数表示一位八进制数
```

|   进制   | 基数范围 | 进制关系 |
| :------: | :------: | :------: |
|  二进制  |   0,1    | 逢二进一 |
|  八进制  |   0~7    | 逢八进一 |
|  十进制  |   0~9    | 逢十进一 |
| 十六进制 | 0~9，A~F | 逢G进一  |

#### 2.2.1 进制转换

```
8421法： 516	  256 	128	  64	32	 16	   8	4	 2	   1
		2^9	   2^8	 2^7  2^6	 2^5  2^4  2^3	2^2	  2^1	2^0
		

二进制转十进制：0110 0011(2)
			1+2+32+64=99(10)
十进制转二进制：113
			0111 0001 
```

### 2.3 原码反码补码

```
目的：原码、反码、补码是为了解决计算机运行逻辑的复杂度（计算机只会做加法）

正数：原码反码补码都是一致地，都是其二进制数
	十进制		99
	二进制	 0110 0011
	原码	0110 0011
	反码	0110 0011
	补码	0110 0011
	
负数：
	十进制		-99
	二进制		1110 0011
	原码	1110 0011	正数的二进制，首位变成1，代表符号位
	反码	1001 1100	符号位不变，其他位取反
	补码	1001 1101	反码加1

```

## 3. 常量

### 3.1 概念

常量就是不会发生改变的量，在计算机程序中不会因为操作而改变常量的值，常量可以是任意基本数据类型和字符串类型

### 3.2 代码

```java
class TestConstant {
	public static void main(String[] args){
		/*
			整型
		*/
		System.out.println(100);
		System.out.println(-100);
		/*
			浮点型
		*/
		System.out.println(3.1415926);
		System.out.println(0.618);
		/*
			布尔型
		*/
		System.out.println(true);
		System.out.println(false);
		/*
			字符型
		*/
		System.out.println('A');
		System.out.println('a');
		/*
			字符串型
		*/
		System.out.println("Hello, World");
		System.out.println("Hello, Java");
	}
}
```

### 3.3 字符常量相关

#### 3.3.1 编码集

```
ASCII:
	1、美国信息交换标准代码，一共定义了128个字符
	2、65~90 为A~Z(大写)
	3、97~122 为a~z(小写)，大小写中间不连续
	4、其他字符为控制字符、标点符号、运算符号
	5、写代码时不能使用字符所对应的编号【重点】
		char ch1 = 'A';		true
		char ch2 = 65;		false
		
GB2312:
	1、简体汉字字符集，通用于中国大陆，收录了一部分其他地区非简体汉字字符
	
GBK:
	1、GB2312的扩展，加入了更多的汉字，GB2312编码的汉字可以通过GBK来解码

Unicode编码集:
	1、万国码，收录了每种语言的每个字符
	2、三种编码方式：UTF-8 UTF-16 UTF-32
	【重点】UTF-8常用，后续javaWEB 数据库 HTML前端都需要使用UTF-8编码
		
Big5:
	1、大五码，收录了繁体中文字符，一般用于中国香港、澳门、台湾等地
```

#### 3.4 转义字符

用于表示一些不能正常显示的字符或者带有特殊含义的字符

```
\t	制表符

\n	换行符

\\	\

\‘	'

\"	"
```

#### 3.5 总结

```
1、常量在代码中是无法修改的，主要功能是提供给程序运行使用的数据，存在基本数据类型常量和字符串常量
2、【重点】不能给字符型变量赋值其对应的编码，只能使用字符本身
```

## 4. 变量

### 4.1 概念

​	计算机内存中的一块用于存储数据的基本单元

### 4.2 变量的组成

​	数据类型 + 变量名 = 值

#### 4.2.1 数据类型

基本数据类型

| 整型  | 占用内存大小 |   取值范围   |
| :---: | :----------: | :----------: |
| byte  |  1字节(8位)  |   -128~127   |
| short | 2字节(16位)  | -32768~32767 |
|  int  | 4字节(32位)  | -2^31~2^31-1 |
| long  | 8字节(64位)  | -2^63~2^63-1 |

| 浮点型 | 占用内存大小 |      取值范围       |
| :----: | :----------: | :-----------------: |
| float  | 4字节(32位)  |     ±3.4*10^38      |
| double | 8字节(64位)  | -1.7E+308～1.7E+308 |

| 字符型 | 占用内存大小 |        取值范围         |
| :----: | :----------: | :---------------------: |
|  char  | 2字节(16位)  | 0~65535（能够保存中文） |

| 布尔型  |  占用内存大小  |  取值范围   |
| :-----: | :------------: | :---------: |
| boolean | 1字节或4个字节 | true，false |

引用数据类型

```
数组
字符串
对象
```

### 4.3 变量名/标识符规范

```
规范：
	1、只能使用A~Z、a~z、数字、下划线
	2、数字不能开头，英文字母开头
	3、标识符没有严格的长度限制，但是会根据实际的情况来约束标识符长度
	4、Java是强类型语言，严格区分大小写
	5、标识符要见名知意，动宾结构
	6、驼峰命名
		大驼峰：TestJava StudentClass
			用于类名、接口名
		小驼峰：getName	setName
			用于变量、方法
	7、下划线命名
		一般用于常量
			MAX_VALUE
			DEFAULT_CAPACITY
	8、Java中被占用的关键字和保留字不能用
		编辑器中高亮提示的不能用
```

### 4.4 代码

```java
class TestVariable {
	public static void main(String[] args){
		// 整型变量	Java默认的整数类型为int，所以long型要加L
		byte byteNumber = 10;
		short shortNumber = 20;
		int intNumber = 30;
		long longNumber = 40L;
		
		System.out.println(byteNumber);
		System.out.println(shortNumber);
		System.out.println(intNumber);
		System.out.println(longNumber);
		
		System.out.println("------------------");
		
		// 浮点型变量	Java默认的浮点型为double，float型要加F
		float floatNumber = 3.14F;
		double doubleNumber = 0.618;
		
		System.out.println(floatNumber);
		System.out.println(doubleNumber);
		
		System.out.println("------------------");
		
		// 字符型变量
		char charNumber = 'A';
		char charNumber2 = '我';
		
		System.out.println(charNumber);
		System.out.println(charNumber2);
		
		System.out.println("------------------");
		
		// 布尔型变量
		boolean result1 = true;
		boolean result2 = false;
		
		System.out.println(result1);
		System.out.println(result2);
	}
}
```



### 4.5 总结

```java
1、变量一行只定义一个，定义时就赋值，赋的值要和数据类型一致

2、使用变量时，直接使用其变量名

3、double类型丢失精度问题：
	Java默认的浮点型为double型，在给float类型赋值的时候如果不声明F，有可能会导致丢失精度。同理，Java默认的整型为int型，byte和short都会默认转成int型，因为不存在溢出的问题，但是long型就需要声明L
	float floatNumber = 3.14F;
	long longNumber = 40L;

4、要求字符类型的常量有且只能用字符本身来赋值
    
5、变量名未声明得话不能使用
    
6、变量名未赋值得话不能使用
```

