## 1. 循环

### 1.1 for

```shell
格式：
	for (循环条件初始化条件;循环条件判断;循环条件变更) {
		代码块
	}
	
执行流程
	1、首先进行循环条件初始化
	2、循环条件判断，为真就执行代码块，为假则退出循环
	3、循环条件变更
	4、回到2
```

```java
class TestFor {
	public static void main(String[] args) {
		for (char ch = 'A' ; ch <= 'Z' ; ch++) {
			System.out.print(ch);
		}
	}
}
```

### 1.2 控制流程关键字

#### 1.2.1 break

用于switch分支结构和循环结构，跳出当前循环(就近原则)

```java
class TestBreak {
	public static void main(String[] args) {
		for (int i = 1 ; i <= 100 ; i++) {
			
			if (50 == i) {
				System.out.println("执行了break");
				break;
			}
			
			System.out.println(i);
		}
	}
}
```

#### 1.2.2 continue

在循环结构中使用，用于跳过当次循环，直接执行下次循环

```java
class TestContinue2 {
	public static void main(String[] args) {
		for (int i = 1 ; i <= 10 ; i++) {
			
			if (i == 5) {
				System.out.print("continue±»Ö´ĞĞ");
				continue;
			}
			
			System.out.print(i + " ");
		}
	}
}
```

【注意】continue 在 while 循环、do while循环中使用时，循环条件变更需要在 continue 前执行，否则可能会造成死循环

#### 1.2.3 return

它的作用不是结束循环的，而是结束方法的。

```java
class ReturnDemo {
	public static void main(String[] args) {
		for(int x=0; x<10; x++) {
			if(x == 2) {
				System.out.println("退出");
				return;
			}
			
			System.out.println(x);
		}
		
		System.out.println("over");
	}
}
```

### 1.3 嵌套循环

在一个完整的循环中嵌套另一个循环，外层控制循环次数，内层控制单次循环操作

```java
class Test {
	public static void main(String[] args) {		
		for (int i = 1; i <= 9; i++) {
			for (int j = 1; j <= i; j++) {
				System.out.print(j + "*" + i + "=" + j * i + "\t");
			}
			
			System.out.println();
		}
	}
}
```

### 1.4 注意

```shell
1、注意修改控制条件，否则容易出现死循环

2、for死循环
	for (;;) {
	
	}
	
3、while死循环
	while (true) {
	
	}
```

## 2. 注释

### 2.1 单行注释

```shell
//
```

### 2.2 多行注释

```shell
/*
*
*/
```

### 2.3 文档注释

```
/**
* 方法的功能解释
*
* @author 	标识一个类的作者
* @exception 	标志一个类抛出的异常
* @param 	说明一个方法的参数
* @return 	说明返回值类型
* @version 	指定类的版本
*/
```

【注意】

```
1、单行注释和多行注释都不会被 Java虚拟机解释执行
2、文档注释可通过 javadoc 工具生成对应 HTML 格式的信息、
3、建议先写注释再写代码
```

## 3. 方法

### 3.1 概念

实现特定功能的一段代码，可以被反复使用

### 3.2 方法的构成

```
固定格式：
    public static
返回值类型：
    如果没有返回值类型就用 void ，如果有就使用对应的返回值类型
方法名：
    小驼峰命名，见名知意，动宾结构
形参：
    用来接收用户传入的数据，可以是基本数据类型或者引用数据类型，需要声明局部变量。
    如果不需要形参就写 ()
实参：
    方法调用时用于传入的数据，用来给形参赋值，数据类型要求一致
```

【注意】

```shell
1、main方法是程序的入口，所有的代码和方法都需要在main方法中被完成和调用
2、方法名的后面一定要跟 ()
3、方法和其他方法的关系是并列关系
4、方法具有单一职能原则，一个方法只做一件事
```

### 3.3 方法声明格式

```
public static returnType methodName(dataType FormerParameter) {
    method body;
}
```

### 3.4 声明位置

定义在类中，与主函数并列

### 3.5 形参实参

```
形参：用来接收调用该方法时传递的参数。只有在被调用的时候才分配内存空间，一旦调用结束，就释放内存空间。因此仅仅在方法内有效。
实参：传递给被调用方法的值，预先创建并赋予确定值
```

【注意】

```shell
1、如果方法声明时带有形式参数，那么方法调用时就必须携带实际参数
2、如果方法声明时没有形式参数，方法调用时就不能有实参
3、声明时有几个形式参数，调用时就传入几个实际参数，形参实参个数不一样编译会报错
4、实参与形参的数据类型不一样，编译器会报错
```

### 3.6 返回值

方法中的返回值有两种情况，即有返回值和无返回值，如果定义方法时有返回值类型，就需要返回相对应的数据类型

#### 3.6.1 返回值类型

```
无返回值类型 void

基本数据类型

引用数据类型
```

#### 3.6.2 return 关键字

##### 3.6.2.1 作用

结束当前函数，返回至调用函数处，如果定义了返回值类型就返回对应类型的数据，未定义返回值类型不需要返回值或者返回 null

【注意】数据类型一致化

##### 3.6.2.2 格式

```
return 需要返回的数据;
```

【注意】

```shell
1、break 是退出当前循环结构，return 是退出当前函数

2、如果返回值类型是 void ，可以返回 null 或者不返回

3、一个函数可以有多个 return，但只能有一个返回值

4、返回值可以接收也可以不接收

5、分支结构里的每一个分支都需要有正确的返回值

6、对返回值的处理方式因情况而定，可以打印、参与运算或者当做其他方法的实参
```

### 3.7 方法调用

哪里需要哪里吼

```
mothodName(actualParameter);
```

#### 3.7.1 无参无返回值调用

```java
class Test {
	public static void main(String[] args) {
		printHelloWorld();
	}
	
	/**
	* 打印Hello World
	*/
	public static void printHelloWorld() {
		System.out.println("Hello World");
	}
}
```

#### 3.7.2 有参无返回值调用

```java
import java.util.Scanner;

class Test {
	public static void main(String[] args) {
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请输入一个数：");
		int num = scanner.nextInt();
		
		printIntNum(num);
	}
	
	/**
	* 展示用户传入的int类型数据
	*
	* @param num 这里需要传入一个int类型的数据
	*/
	public static void printIntNum(int num) {
		System.out.println("您输入的数为：" + num);
	}
}
```

#### 3.7.3 无参有返回值调用

```java
class Test {
	public static void main(String[] args) {
		System.out.println(giveMeFive());
	}
	
	/**
	* 返回一个整数 5
	*
	* @return 5 int类型
	*/
	public static int giveMeFive() {
		return 5;
	}
}
```

#### 3.7.4 有参有返回值调用

```java
class TestMethod4 {
	public static void main(String[] args) {
		System.out.println(getCompare(3,2));
	}
	
	/**
	* 比较大小，返回较大的那个数
	*
	* @param num1 int类型
	* @param num2 int类型
	* @return int类型的结果
	*/
	public static int getCompare(int num1, int num2) {
		return num1 > num2 ? num1 : num2;
	}
}
```

【注意】调用带有多参数的方法，要求传入的参数数据类型，个数和顺序必须和方法声明一致

## 4. 局部变量

#### 4.1 概念

在函数内部定义的变量（包括主函数）

#### 4.2 作用域

从定义局部变量的那一行到所在的代码块结束

```java
for (int i = 1; i <= 10; i++) {
    
}

for (int i = 1; i <= 10; i++) {
    
}
```

【注意】两个for循环中，i 循环变量分别属于不同的大括号以内，不同的作用域空间，并不冲突

#### 4.3 生存期

从函数被调用的时刻算起到函数返回调用处的时刻结束

```java
for (int i = 1; i <= 10; i++) {
    
}

System.out.println(i); // 报错，找不到符号
```

【注意】for 循环结束时局部变量 i 的生存期结束，在 for 循环外无法使用 i

#### 4.4 单一性，不能重名

```java
// 报错！
for (int i = 1; i <= 10; i++) {
    for (int i = 1; i <= 10; i++) {
        
    }
}
```

【注意】在一个方法内局部变量不能多次定义

#### 4.5 值传递

```java
class Test {
	public static void main(String[] args) {
        int num = 5;
        test(num);
        
        System.out.println(num);	// 5
    }
    
    public static void test(int num) {
        num = 10;
    }
}
```

【注意】基本数据类型作为参数传递给局部变量时，传递的是值，局部变量的更改不影响实参本身

#### 4.6 引用传递

```java
class Test {
	public static void main(String[] args) {		
		int[] array = {0, 1, 2};
		
		method(array);
		
		System.out.println(array[0]); // 1
	}
	
	public static void method(int[] array) {
		array[0] = 1;
	}
}
```

【注意】引用数据类型传递时传递的是地址，局部变量对对象的操作直接作用于实参本身

#### 4.7 总结

```
1、局部变量声明在函数中，从定义的那一行开始到函数结束时被销毁
2、局部变量必须先赋值再使用
3、局部变量不能重复定义
4、值传递：基本数据类型的传递不改变实参
5、引用传递：引用数据类型的传递会改变实参
6、Java 中只有值传递
```

## 5. 数组

### 5.1 概念

一组连续的存储空间，用以存储一组相同数据类型的值

【注意】

```
1、类型相同
2、长度固定
3、空间连续
```

### 5.2 概述

```
1、数组中的每个存储空间称为数组的“元素”
2、对元素的访问有”赋值“和”取值“
3、访问元素需要通过下标(索引)，下标从0开始依次加1，到数组的长度-1结束
4、数组的长度：数组名.length
5、如果超过了数组的长度，会报错：ArrayIndexOutOfBoundsException
```

### 5.3 创建

```java
int[] array1 = new int[5];

int[] array2 = new int[]{1, 2, 3};

int[] array3 = {1, 2, 3};
```

### 5.4 使用

```java
array[0] = 1;
array[1] = 2;
array[2] = 3;

System.out.println(array[0]); // 1
System.out.println(array[1]); // 2
System.out.println(array[2]); // 3
```

### 5.5 数组作为方法的实参传递

```java
class Test {
	public static void main(String[] args) {		
		int[] array = {0, 1, 2};
		
		method(array);
		
		System.out.println(array[0]); // 1
	}
	
	public static void method(int[] array) {
		array[0] = 1;
	}
}
```

【注意】数组作为实参传递给形参时，是把自己的地址复制一份传递给形参，形参对数组中元素的操作会影响到实参本身

### 5.6 遍历

```java
/**
* 打印数组元素
*
* @param array 传入一个int数组
*/
public static void printArray(int[] array) {
	for (int i = 0; i < array.length; i++) {
		System.out.println(array[i]);
	}
}
```

### 5.7 默认值

```shell
整型
	0
浮点型
	0.0
字符型
	\u0000
布尔型
	false
引用数据类型
	null
```

### 5.8 数组的操作

```java
遍历
    java.util.Arrays.toString(数组名)
   
复制
    java.util.Arrays.copyOf(原数组, 新容量)
    返回带有原值的数组
    
    System.arraycopy(原数组. 原数组初始位置, 新数组, 新数组初始位置, 容量)
    
排序
    java.util.Arrays.sort(数组名)
    默认升序
```

## 6. 引用数据类型

1、栈中存放引用数据类型的变量名，通过地址指向堆中的变量

2、除了8种基本数据类型，其他都是引用数据类型
