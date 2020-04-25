## 方法/函数

### 1. 返回值

方法中的返回值有两种情况，即有返回值和无返回值，如果定义方法时有返回值类型，就需要返回相对应的数据类型

#### 1.1 返回值类型

```shell
无返回值类型 void

基本数据类型

引用数据类型
```

#### 1.2 return 关键字

##### 1.2.1 作用

结束当前函数，返回至调用函数处，如果定义了返回值类型就返回对应类型的数据

【注意】数据类型一致化

##### 1.2.2 格式

```java
return 需要返回的数据;
```

#### 1.3 无参有返回值的方法：give me five

```java
class TestMethod1 {
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

#### 1.4 有参有返回值的方法：返回两个整数里的较大那个数

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

#### 1.5 总结

```shell
1、break 是退出当前循环结构，return 是退出当前函数

2、如果返回值类型是 void ，可以返回 null 或者不返回

3、一个函数可以有多个 return，但只能有一个返回值

4、返回值可以接收也可以不接收

5、分支结构里的每一个分支都需要有正确的返回值

6、对返回值的处理方式因情况而定，可以打印、参与运算或者当做其他方法的实参

7、调用带有多参数的方法，要求传入的参数数据类型，个数和顺序必须和方法声明一致
```

【注意】函数具有单一职能原则，一个函数只做一件事

### 2. 局部变量

#### 2.1 概念

在函数内部定义的变量（包括主函数）

#### 2.2 作用域

从定义局部变量的那一行到所在的代码块结束

```java
for (int i = 1; i <= 10; i++) {
    
}

for (int i = 1; i <= 10; i++) {
    
}
```

【注意】两个for循环中，i 循环变量分别属于不同的大括号以内，不同的作用域空间，并不冲突

#### 2.3 生存期

从函数被调用的时刻算起到函数返回调用处的时刻结束

```java
for (int i = 1; i <= 10; i++) {
    
}

System.out.println(i); // 报错，找不到符号
```

【注意】for 循环结束时局部变量 i 的生存期结束，在 for 循环外无法使用 i

#### 2.4 单一性，不能重名

```java
// 报错！
for (int i = 1; i <= 10; i++) {
    for (int i = 1; i <= 10; i++) {
        
    }
}
```

【注意】在一个方法内局部变量不能多次定义

#### 2.5 值传递

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

#### 2.6 引用传递

【注意】引用数据类型传递时传递的是地址，局部变量直接作用于实参本身

#### 2.7 总结

```shell
1、局部变量声明在函数中，从定义的那一行开始到函数结束时被销毁
2、局部变量必须先赋值再使用
3、局部变量不能重复定义
4、值传递：基本数据类型的传递不改变实参
5、引用传递：引用数据类型的传递会改变实参
```
