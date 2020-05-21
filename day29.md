## 1. 缓冲流

### 1.1 概述

```java
BufferedInputStream
	字节缓冲输入流
BufferedOutputStream
	字节缓冲输出流
BufferedReader
	字符缓冲输入流
BufferedWriter
	字符缓冲输出流

1、缓冲流是Java中提供的系统缓冲，底层都是一个缓冲数组，根据处理的数据方式不同，提供的数据有字节缓冲数组和字符缓冲数组。
2、字节缓冲流，默认的字节数组缓冲区是8KB 
	byte[] buffer = new byte[1024 * 8];
3、字符缓冲流，默认的字符数组缓冲区是16KB
	char[] buffer = new char[1024 * 8];
4、【重点】
	任何一个缓冲流都没有任何操作文件的能力！！！读取文件数据，写入文件数据，都是依赖于对应的字符流或者字节流提供的！！！
5、缓冲流使用的方法，也是read write 而且是对应创建当前缓冲流使用的字符流或者字节流的！！！
6、缓冲流减少了CPU通过内存访问磁盘或者说文件的次数。极大的提高了开发效率。IO流操作文件内容都是在缓冲流内部的缓冲数组中，也就是内存中。
```

### 1.2 BufferedInputStream 字节缓冲输入流

```java
构造方法 Constructor
	BufferedInputStream(InputStream in);
		这里需要的参数是字节输入流对象

成员方法 Method 
	int read();
	int read(byte[] buf);
	其实就是InputStream中使用的方法
```

```java
public class Test {
	public static void main(String[] args) throws IOException {
		BufferedInputStream bis = new BufferedInputStream(
				new FileInputStream(new File("C:/Users/CJF/Desktop/Test.txt")));

		byte[] buf = new byte[1024 * 8];

		int count = -1;

		while (-1 != (count = bis.read(buf))) {
			System.out.println(new String(buf, 0, count));
		}

		bis.close();
	}
}
```

### 1.3 BufferedOutputStream 字节缓冲输出流

```java
构造方法 Constructor
	BufferedOutputStream(OutputStream out);
		这里需要一个字节输出流作为方法的参数

常用方法 Method	
	void write(int b);
	void write(byte[] buf);
	void write(byte[] buf, int off, int len);
    以上方法都是OutputStream提供的方法。

	所有的数据都是首先都是写入保存到BufferedOutputStream 底层操作的数组中，当数组填满以后，或者执行指定的方法，才会将数据之间写入到内存中。
```

```java
public class Test {
	public static void main(String[] args) throws IOException {
		BufferedOutputStream bos = new BufferedOutputStream(
				new FileOutputStream(new File("C:/Users/CJF/Desktop/Test.txt"), true));

		bos.write("\n今天是个好天气".getBytes());

		bos.close();
	}
}
```

### 1.4 效率总结

```shell
1、使用缓冲时间效率是远远高于未使用缓冲情况，这里是一个非常经典的空间换时间概念
	缓冲占用内存 16KB 非缓冲 4byte 时间效率大于250倍 空间占用4000倍
2、利用代码可以发现，非缓冲IO操作时使用数组作为缓冲区和使用缓冲流操作，时间效率相似。这里还是推荐使用系统提供的缓冲流，更加安全，并且提供了一些其他方法，可以作为一定参考和使用。
```

### 1.5 BufferedReader 字符输入缓冲流

```java
构造方法 Constructor：
	BufferedReader(Reader in);

常用方法 Method:
	int read();
	int read(byte[] buf);
	String readLine(); 【新方法】
		从文件中读取一行数据，返回值类型是字符串，如果读取到文件默认，返回null
		一行数据??? 结尾标记 \r\n
```

```java
public class Test {
	public static void main(String[] args) throws IOException {
		BufferedReader br = new BufferedReader(new FileReader(new File("C:/Users/CJF/Desktop/Test.txt")));

		char[] buf = new char[1024 * 8];

		int count = -1;
		while (-1 != (count = br.read(buf))) {
			System.out.println(new String(buf, 0, count));
		}

		String content = null;
		while (null != (content = br.readLine())) {
			System.out.println(content);	// 这里不会再输出，因为上面已经读到文件末尾，即 null == content
		}

		br.close();
	}
}
```

### 1.6 BufferedWriter 字符输出缓冲流

```java
构造方法 Constructor:
	BufferedWriter(Writer in);

常用方法:
	void write(int ch);
	void write(char[] buf);	
	void write(char[] buf, int off, int len);	
	void write(String str);	
	void write(String str, int off, int len);	
	void newLine(); 
		换行操作
```

```java
public class Test {
	public static void main(String[] args) throws IOException {
		BufferedWriter bw = new BufferedWriter(new FileWriter(new File("C:/Users/CJF/Desktop/Test.txt"), true));

		bw.write("\n今天又是个好天气");

		bw.newLine();

		bw.close();
	}
}
```

## 2. 常用类

### 2.1 StringBuffer & StringBuilder

线程安全的可变字符序列

#### 2.1.1 构造方法

```java
StringBuffer();	
	创建一个StringBuffer类对象，在底层char类型数组中，初始化容量为16，并且
	未存储任何的数据
StringBuffer(String str); [最常见]
	根据用户传入参数String类型字符串，创建对应的StringBuffer对象，底层
	char类型数组保存对应的字符串信息。
StringBuffer(int capacity);
	根据用户传入初始化底层char类型数组容量确定StringBuffer对象
```

#### 2.1.2添加方法

```java
append(EveryThing);
	在StringBuffer末尾追加内容，可以是任意数据类型
insert(int index, EveryThing);
	在StringBuffer指定下标位置添加内容，可以是任意数据类型
```

```java
public class Test {
	public static void main(String[] args) {
		StringBuffer stringBuffer = new StringBuffer("Buffer is mine.");
	
		String str = null;
		
		stringBuffer.append(" Hello ");

		stringBuffer.insert(7, "forever ");
		
		stringBuffer.append(str);
		
		System.out.println(stringBuffer); // Buffer forever is mine. Hello null
	}
}
```

【注意】StringBuffer 类 的 append(Object obj) 调用 String 类的 valueOf(Object obj)，如果传入的参数为null，转为字符串 "null"

#### 2.1.3 查看方法

```java
String toString();
	将StringBuffer底层保存数据的char类型字符数组内容，转换为String类型返回

int indexOf(String str);
	指定字符串在StringBuffer出现的第一次下标位置
int lastIndexOf(String str);
	指定字符串在StringBuffer中最后一次出现的下标位置
	
String substring(int begin);
	从指定位置开始，到字符串末尾截取获得对应的字符串
String substring(int begin, int end);
	从指定位置begin开始，到end结束，获取对应的字符串，要头不要尾
```

```java
public class TestGet {
	public static void main(String[] args) {
		StringBuffer stringBuffer = new StringBuffer("1234512345");

		System.out.println(stringBuffer.toString()); // 1234512345
		System.out.println(stringBuffer.indexOf("23")); // 1
		System.out.println(stringBuffer.lastIndexOf("23")); // 6
		System.out.println(stringBuffer.substring(3)); // 4512345
		System.out.println(stringBuffer.substring(3, 4)); // 4
	}
}
```

#### 2.1.4 修改方法

```java
replace(int start, int end, String str)  
	使用给定 String 中的字符替换此序列的子字符串中的字符。该子字符串从指定的 start 处开始，一直到索引 end - 1 处的字符
setCharAt(int index, char ch)  
	指定索引位置替换一个字符
```

```java
public class TestReplace {
	public static void main(String[] args) {
		StringBuffer stringBuffer = new StringBuffer("1234512345");

		System.out.println(stringBuffer.replace(3, 4, "Buffer")); // 123Buffer512345

		stringBuffer.setCharAt(1, '0');

		System.out.println(stringBuffer);// 103Buffer512345
	}
}
```

#### 2.1.5 删除和反序方法

```java
delete(int start, int end);
	删除从start开始，到end结束区间的所有内容，要头不要尾

deleteCharAt(int index);
	删除指定下标的字符
	
reverse();
	StringBuffer内容反序
```

```java
public class TestRemove {
	public static void main(String[] args) {
		StringBuffer stringBuffer = new StringBuffer("123456");

		System.out.println(stringBuffer.delete(3, 5)); // 1236

		System.out.println(stringBuffer.deleteCharAt(0)); // 236

		System.out.println(stringBuffer.reverse()); // 632
	}
}
```

#### 2.1.6 StringBuilder

```shell
ArrayList<E> 线程不安全，效率高
Vector<E> 线程安全，效率低

StringBuffer 线程安全，效率低
StringBuilder 线程不安全，效率高
	StringBuffer和StringBuilder操作使用的方法，是一致的，只不过StringBuffer的方法带有大量的同步问题。效率比较低。
```

### 3. System

System 类包含一些有用的类字段和方法。它不能被实例化。

```java
static Properties getProperties();【重点】
		获取系统属性
static long currentTimeMillis();
		获取当前时间的毫秒数
static void exit(int status);
		JVM退出程序，0表示正常退出
            
Properties类是一个重点
	属性类，里面保存的数据都是键值对形式。
```

```java
public class TestSystem {
	public static void main(String[] args) {
		long start = System.currentTimeMillis();

		Properties properties = System.getProperties();

		System.out.println(properties);

		long end = System.currentTimeMillis();

		System.out.println("\n" + (end - start));
		
		System.exit(0);
	}
}
```

