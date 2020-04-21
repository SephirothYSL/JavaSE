## 1. 嵌套循环

### 1.1 概念

在一个循环中套入另一个循环

```java
/*
	    A
	   ABA
	  ABCBA
	 ABCDCBA
	ABCDEDCBA
	 ABCDCBA
	  ABCBA
	   ABA
	    A
*/
class TestNestedLoop5 {
	public static void main(String[] args) {
		int line = 5;
		
		for (int i = 1; i <= line; i++) {
			for(int j = line - 1; j >= i; j--) {
				System.out.print(" ");
			}
			
			char ch = 'A';
			for(int k = 1; k <= i; k++) {
				System.out.print(ch);
				ch++;
			}
			
			ch--;
			for (int l = 1; l < i; l++) {
				ch--;
				System.out.print(ch);			
			}
			
			System.out.println();
		}
		
		for (int i = 1; i <= line - 1; i++) {
			for (int j = 1; j <= i; j++) {
				System.out.print(" ");
			}
			
			char ch = 'A';
			for (int k = line - 1; k >= i;k--) {
				System.out.print(ch);
				ch++;
			}
			
			ch--;
			for (int l = line - 1; l > i; l--) {
				ch--;
				System.out.print(ch);
			}
			
			System.out.println();
		}
	}
}
```

【注意】外层循环决定行数，内存循环决定单行的循环操作

## 2. 注释

### 2.1 单行注释

```java
//
```

### 2.2 多行注释

```java
/*
*
*/
```

### 2.3 文档注释

```java
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

```shell
1、单行注释和多行注释都不会被 Java虚拟机解释执行
2、文档注释可通过 javadoc 工具生成对应 HTML 格式的信息、
3、建议先写注释再写代码
```

## 3. 方法

### 3.1 概念

实现特定功能的一段代码，可以被反复使用

### 3.2 方法的构成

```shell
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

### 3.3 方法声明格式

```java
public static returnType methodName(dataType FormerParameter) {
    method body;
}
```

### 3.4 声明位置

定义在类中，与主函数并列

### 3.4 方法调用

```java
mothodName(actualParameter);
```

#### 3.4.1 无参无返回值调用

```java
class TestMethod1 {
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

【注意】

```shell
1、main方法是程序的入口，所有的代码和方法都需要在main方法中被完成和调用
2、方法名的后面一定要跟 ()
3、方法和其他方法的关系是并列关系
```

#### 3.4.2 有参无返回值调用

```java
import java.util.Scanner;

class TestMethod3 {
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

【注意】

```shell
1、如果方法声明时带有形式参数，那么方法调用时就必须携带实际参数
2、如果方法声明时没有形式参数，方法调用时就不能有实参
3、声明时有几个形式参数，调用时就传入几个实际参数，形参实参个数不一样编译会报错
4、实参与形参的数据类型不一样，编译器会报错
```



### 3.5 形参实参

```shell
形参：用来接收调用该方法时传递的参数。只有在被调用的时候才分配内存空间，一旦调用结束，就释放内存空间。因此仅仅在方法内有效。
实参：传递给被调用方法的值，预先创建并赋予确定值
```
