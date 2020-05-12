## 1. 异常

### 1.1 异常处理

#### 1.1.1 捕获

```java
格式：
    try{
        // 有可能出现问题的代码，存在一定隐患的代码
    } catch (异常类型) {
        // 对应当前异常类型的处理方式
    }
```

```java
public class Test {
	public static void main(String[] args) {
		int num1 = 0;
		int num2 = 20;

		int ret = 0;

        /*
         * 除数不能为0
         */
		try {
			ret = num2 / num1;
		} catch (ArithmeticException e) {
			e.printStackTrace();
		}

		System.out.println(ret);
	}
}
```

结果

```java
java.lang.ArithmeticException: / by zero
	at code.exception.Test.main(Test.java:11)
0
```

【注意】

```shell
1、代码中出现异常，JVM会终止代码运行，如果使用try catch捕获处理异常，JVM会认为当前代码中不存在异常，可以继续运行。
    
2、try、catch代码块中都是局部变量，需要提前定义
    
3、try - catch捕获处理异常，可以处理多种异常情况

4、代码中存在多种隐患，存在多个异常情况，try - catch捕获有且只能处理第一个出现异常的代码，因为JVM从异常代码开始直接进入异常捕获阶段

5、Exception作为Java中所有异常的超类，在捕获异常处理时如果直接使用Exception进行捕获处理，无法具体到对某一个异常来处理

6、Exception可以作为try - catch 最后一个，用于处理其他异常捕获之后没有对症方式遗留问题
```

#### 1.1.2 抛出

```shell
关键字:
	throw
		在方法内特定条件下抛出指定异常
	throws
		在【方法声明】位置，告知调用者，当前方法有哪些异常抛出

	用于处理非当前方法操作问题，导致出现的异常，一般情况下是用于处理方法运行过程中因为参数传入，参数处理，运算结果导致的问题，抛出异常。
	throw是一个高级的参数合法性判断
```

```java
public class TestThrows {
	public static void main(String[] args) {

		try {
			test(1, 0);
		} catch (ArithmeticException e) {
			e.printStackTrace();
		}
	}

	/**
	 * 测试方法，打印两个数的差
	 * 
	 * @param num1 第一个参数，被除数
	 * @param num2 第二个参数，除数
	 * @throws ArithmeticException 如果除数为0，抛出异常
	 */
	public static void test(int num1, int num2) throws ArithmeticException {

		if (0 == num2) {
			throw new ArithmeticException("除数不能为0");
		}

		System.out.println(num1 / num2);
	}
}
```

结果

```java
java.lang.ArithmeticException: 除数不能为0
	at code.exception.TestThrows.test(TestThrows.java:23)
	at code.exception.TestThrows.main(TestThrows.java:7)
```

【注意】

```shell
1、throw 和 throws 必须同时出现，并且体现在注释上

2、代码如果运行到throw抛出异常，之后的代码不再运行，之后的代码是成为无参触及代码

3、代码中存在多种隐患，按照隐含的情况，分门别类处理，不能在同一个条件内抛出两个异常。并且在方法的声明位置，throws之后，不同的异常，使用逗号隔开

4、当调用带有异常抛出的方法时，对于方法抛出的异常，有两种处理方式，可以捕获处理，也可以抛出处理。
```

### 1.2 异常分类

#### 1.2.1 运行时异常

```java
RuntimeException：代码运行过程中出现的异常，没有强制处理的必要性，因为JVM会处理RuntimeException异常，即报错
```

#### 1.2.2 其他异常

```java
强制要求处理，不管是捕获处理还是抛出处理，都需要进行操作，如果未处理就会报错
```

### 1.3 自定义异常

继承自 Exception 或者 RuntimeException，只需要提供无参构造和一个带参构造即可

自定义异常类

```java
public class MyException extends Exception {
	public MyException() {}
	
	public MyException(String message) {
		super(message);
	}
}
```

测试

```java
public class Test {
	public static void main(String[] args) {
		try {
			buy(false);
		} catch (MyException e) {
			e.printStackTrace();
		}
	}

	/**
	 * 买方法，当没有女朋友的时候，抛出异常
	 * @param hasGirlFriend boolean类型，是否有女朋友
	 * @throws MyException 自定义单身狗异常
	 */
	public static void buy(boolean hasGirlFriend) throws MyException {
		if (false == hasGirlFriend) {
			throw new MyException("你还没有女朋友");
		}
		
		System.out.println("买一送一");
	}
}
```

结果

```java
code.myexception.MyException: 你还没有女朋友
	at code.myexception.Test.buy(Test.java:19)
	at code.myexception.Test.main(Test.java:6)
```

### 1.4 注意

```shell
1、父的方法有异常抛出,子的重写方法在抛出异常的时候必须要小于等于父的异常 

2、父的方法没有异常抛出,子的重写方法不能有异常抛出

3、父的方法抛出多个异常,子的重写方法必须比父少或者小
```

## 2. String 类

### 2.1 概述

String字符串类型是Java中引用数据类型，并且String类型是使用final修饰，没有自己的子类。并且 String 类重写了 Object 类的 equals 方法，以用来比较字符串的值

```java
public class TestString {
	public static void main(String[] args) {
		String s1 = "Buffer";
		String s2 = "Buffer";
		String s3 = new String("Buffer");
		String s4 = new String(s1);
		
		System.out.println(s1 == s2);
		System.out.println(s2 == s3);
		System.out.println(s3 == s4);
		System.out.println(s4 == s1);
		
		System.out.println("------------------");
		
		System.out.println(s1.equals(s2));
		System.out.println(s2.equals(s2));
		System.out.println(s3.equals(s4));
		System.out.println(s4.equals(s1));
	}
}
```

结果

```shell
true
false
false
false
------------------
true
true
true
true
```

【注意】

```shell
1、字符串直接赋值的方式是先到字符串常量池里面去找，如果有就直接返回，没有，就创建并返回

2、字符串是常量,它的值在创建之后值不能更改
```

### 2.2 获取方法

```java
int length();
	获取字符串的长度
	
char charAt(int index);
	从字符串中获取对应下标位置的字符，(存在下标越界问题)

int indexOf(char ch);
	找出指定字符在当前字符串中的下标位置
	"ABCDEFGABCDEFG"
	查询 'E' ==> result 4
	
int indexOf(String str);
	找出指定字符串在当前字符串中的下标位置
	"ABCDEFGABCDEFG"
	查询 "DE" ==> result 3
	
int lastIndexOf(char ch); 
	找出指定字符最后一次出现的下标位置
    "ABCDABCD";
	查询 'B' ==> result 5
        
int lastIndexOf(String str); 
	找出指定字符串最后一次出现的下标位置
    "ABCDABCD";
	查询 "CD" ==> result 6
```

```java
public class TestStringGetMethod {
	public static void main(String[] args) {
		String str = "ABCDEFGABCDEFG";
		
		/*
		 * int length();  
		 * 获取字符串的长度
		 */
		System.out.println(str.length());	// 14
		
		/*
		 * char charAt(int index); 
		 * 从字符串中获取对应下标位置的字符，(存在下标越界问题)
		 */
		System.out.println(str.charAt(0));	// A
		
		/*
		 * int indexOf(char ch); 
		 * 找出指定字符在当前字符串中的下标位置
		 */
		System.out.println(str.indexOf('B'));	// 1
		
		/*
		 * int indexOf(String str); 
		 * 找出指定字符串在当前字符串中的下标位置
		 */
		System.out.println(str.indexOf("AB"));	// 0
		
		/*
		 * int lastIndexOf(String str); 
		 * 找出指定字符串最后一次出现的下标位置
		 */
		System.out.println(str.lastIndexOf('A'));	// 7
		
		/*
		 * int lastIndexOf(char ch); 
		 * 找出指定字符最后一次出现的下标位置
		 */
		System.out.println(str.lastIndexOf("AB"));	// 7
	}
}
```

### 2.3 判断方法

```java
boolean endsWith(String str);
	判断当前字符串是不是指定字符串结尾，如果是返回true，不是返回false
        
boolean startsWith(String str);
	判断当前字符串是不是指定字符串开始，如果是返回true，不是返回false
        
boolean isEmpty();
	判断当前字符串是否为空，空字符串是指 "" 双引号什么都没有
        
boolean contains(String str) 是否包含指定序列 应用：搜索
    判断该指定字符串是否是当前字符串的子字符串
    当前字符串:
		"ABCDEFG";
    参数字符串:
		"CDE"; ==> result true;
	参数字符串:
		"CE"; ==> result false
    原码是调用String类的indexOf方法，找出指定字符串的下标位置，indexOf方法下标为大于等于0，返回 true，否则返回 false
            
boolean equals(Object anObject);
	重写 Override Object类内方法，判断两个字符串是否一致
        
boolean equalsIgnoreCase(String anotherString);
	忽略大小写是否相等，不考虑英文大小写方式比较两个字符串是否一致
```

```java
public class TestStringIsMethod {
	public static void main(String[] args) {
		String str = "ABCDEFGABCDEFG";
		
		/*
		 * boolean endsWith(String str);
	     * 判断当前字符串是不是指定字符串结尾，如果是返回true，不是返回false
		 */
		System.out.println(str.endsWith("EFG"));	// true
		
		/*
		 * boolean startsWith(String str);
	     * 判断当前字符串是不是指定字符串开始，如果是返回true，不是返回false
		 */
		System.out.println(str.startsWith("EFG"));	// false
		
		/*
		 * boolean isEmpty();
		 * 判断当前字符串是否为空，空字符串是指 "" 双引号什么都没有
		 */
		System.out.println(str.isEmpty());	// false
		
		/*
		 * boolean contains(String str)
		 * 判断该指定字符串是否是当前字符串的子字符串
		 */
		System.out.println(str.contains("ABC"));	// true
		
		/*
		 * boolean equals(Object anObject);
		 * 重写 Override Object类内方法，判断两个字符串是否一致
		 */
		System.out.println(str.equals("ABCDEFGABCDEFG"));	// true
		
		/*
		 * boolean equalsIgnoreCase(String anotherString);
		 * 忽略大小写是否相等，不考虑英文大小写方式比较两个字符串是否一致
		 */
		System.out.println(str.equalsIgnoreCase("abcdefgAbCdEfG"));	// true
	}
}
```

### 2.4 转换方法

```java
String(char[] value);
	将字符数组转换为字符串
        
String(char[] value, int offset, int count);
	将字符数组转换为字符串，从指定offset位置开始，计数count
        offset是开始位置
        count是截取个数
    例如:
		char[] arr = {'A', 'B', 'C', 'D', 'E'};
	调用方法参数:
		new String(arr, 2, 3); ==> result "CDE"
            
static String valueOf(char[] data);
	同理String(char[] value);
	tips: 底层代码是 return new String(data);
        
static String valueOf(char[] data, int offset, int count);
	同理String(char[] value, int offset, int count);
	tips: 底层代码是 return new String(data, offset, count);

char[] toCharArray();
	将字符串转换为字符数组
    例如:
		"ABCDE";
	返回值:
		{'A', 'B', 'C', 'D', 'E'};
```

```java
public class TestStringTransferMethod {
	public static void main(String[] args) {
		String str = "ABCDEFGABCDEFG";
		char[] arr = { 'H', 'e', 'l', 'l', 'o' };

		/*
		 * String(char[] value); 
		 * 将字符数组转换为字符串
		 */
		System.out.println(new String(arr)); // Hello

		/*
		 * String(char[] value, int offset, int count);
		 * 将字符数组转换为字符串，从指定offset位置开始，计数count
		 */
		System.out.println(new String(arr, 3, 2)); // lo

		/*
		 * static String valueOf(char[] data); 
		 * 同理String(char[] value);
		 */
		System.out.println(String.valueOf(arr)); // Hello

		/*
		 * static String valueOf(char[] data, int offset, int count); 同理String(char[]
		 * value, int offset, int count);
		 */
		System.out.println(String.valueOf(arr, 3, 2)); // lo

		/*
		 * char[] toCharArray(); 
		 * 将字符串转换为字符数组
		 */
		char[] charArray = str.toCharArray();

		for (int i = 0; i < charArray.length; i++) {
			System.out.print(charArray[i]); // ABCDEFGABCDEFG
		}
	}
}
```

### 2.5 其他方法

```java
String replace(char oldChar, char newChar); 
	替换使用newChar字符类型，替换当前字符串内的所有指定字符oldChar
    例如:
		"ABCDEABCDE";
	调用方法:
		"ABCDEABCDE".replace('A', '你');
	返回值结果:
		"你BCDE你BCDE"; 【注】原字符串不变
            
String[] split(String regex); 【重点】
	【重点】切割，将当前字符串按照指定字符串切割成String类型数组
    例如:
		String str = "你好!他好!大家好!广州好迪";
	调用方法:
		str.split("!");
	返回值结果:
		String[] arr = {"你好", "他好", "大家好", "广州好迪"};
	调用方法:
		str.split("好");
	返回值结果:
		String[] arr = {"你", "!他", "!大家","!广州", "迪"};

String substring(int beginIndex); 【重点】
	从指定beginIndex开始，到字符串结尾截取字符串
    例如:	
		String str = "ABCDEFG";
	调用方法:
		str.substring(3);
	返回值结果:
		"DEFG"
String substring(int beginIndex, int endIndex); 【重点】
	从指定beginIndex开始，到endIndex结束，截取字符串
    要头不要尾 beginIndex <= 结果范围 < endIndex [3,5)
                                     
    例如:	
		String str = "ABCDEFG";
	调用方法:
		str.substring(3, 5);
	返回值结果:
		"DE"
                                         
String toUpperCase();
	字符串中所有的英文字母转大写，返回新字符串
String toLowerCase(); 
	字符串中所有的英文字母转小写，返回新字符串                               
String trim(); 
	去除字符串两边的空格
```

```java
public class TestStringOthersMethod {
	public static void main(String[] args) {
		String str = "ABCDEFGABCDEFG";

		/*
		 * String replace(char oldChar, char newChar);
		 * 替换使用newChar字符类型，替换当前字符串内的所有指定字符oldChar
		 */
		System.out.println(str); // ABCDEFGABCDEFG
		System.out.println(str.replace("A", "ZZ")); // ZZBCDEFGZZBCDEFG

		/*
		 * String[] split(String regex); 
		 * 切割，将当前字符串按照指定字符串切割成String类型数组
		 */
		String[] array = str.split("C");

		for (int i = 0; i < array.length; i++) {
			System.out.print(array[i] + " "); // AB DEFGAB DEFG
		}
		System.out.println();
		
		/*
		 * String substring(int beginIndex);
		 * 从指定beginIndex开始，到字符串结尾截取字符串
		 */
		System.out.println(str.substring(3));	// DEFGABCDEFG
		
		/*
		 * String substring(int beginIndex, int endIndex);
		 * 从指定beginIndex开始，到endIndex结束，截取字符串
		 */
		System.out.println(str.substring(3, 5));	// DE
		
		/*
		 * String toUpperCase();
		 * 字符串中所有的英文字母转大写，返回新字符串
		 */
		System.out.println(new String("AbCdEfG").toUpperCase());	// ABCDEFG
		
		/*
		 * String toLowerCase();
		 * 字符串中所有的英文字母转小写，返回新字符串
		 */
		System.out.println(new String("AbCdEfG").toLowerCase());	// abcdefg
		
		/*
		 * String trim();
		 * 去除字符串两边的空格
		 */
		System.out.println(new String("    ABC   DEF   ").trim());	// ABC   DEF
	}
}
```

