## 1. IO 流

### 1.1 概述

```shell
1、IO流用来处理设备之间的数据传输
	上传文件和下载文件
2、Java对数据的操作是通过流的方式
3、Java用于操作流的对象都在IO包中
```

### 1.2 分类

```java
按照数据流向
	输入流	读入数据
	输出流	写出数据
按照数据类型
	字节流
	字符流

class InputStream 字节输入流基类
--| class FileInputStream 文件操作字节输入流

class OutputStream 字节输出流基类
--| class FileOutputStream 文件操作字节输出流

class Reader 字符输入流基类
--| class FileReader 文件操作字符输入流

class Writer 字符输出流基类
--| class FileWriter 文件操作字符输出流
    
缓冲流:
	BufferedInputStream	
		字节输入缓冲流
	BufferedOutputStream
    	字节输出缓冲流	
	BufferedReader	
		字符输入缓冲流
	BufferedWriter	
		字符输出缓冲流
```

### 1.3 FileInputStream 文件操作字节输入流

```java
Constructor构造方法
	FileInputStream(String filePath);
		根据用户指定的文件路径创建对应的FileInputStream，文件操作输入字节流，
		如果文件不存在，抛出异常FileNotFoundException
	FileInputStream(File file);
		根据用户指定对应文件的File类对象，创建对应的FileInputStream，如果文件
		不存在，抛出异常FileNotFoundException

Method成员方法
	int read();
		从文件中读取一个字节数据返回。如果读取到底末尾，返回-1 EOF End Of File
	int read(byte[] buf); 【重点，效率高】
		从文件中读取数据到缓冲数组buf中，返回值类型是从文件中读取到的字节个数，如
		果读取到文件末尾，返回-1， EOF End Of File
	读取数据的方法，在运行过程中出现了问题，抛出异常IOException

操作流程:
	1. 明确对应文件的路径，可以选择直接给予对应的String类型路径，或者创建对应的File类对象，作为参数
	2. 创建FileInputStream文件操作字节输入流，打开文件操作管道
	3. 从FileInputStream对象中使用方法，读取数据
	4. 关闭资源！！！FileInputStream类对象 ==> 水龙头！！！
```

```java
public class Test1 {
	public static void main(String[] args) throws IOException {
		FileInputStream fileInputStream = new FileInputStream(new File("C:/Users/CJF/Desktop/Test.txt"));

		int content = fileInputStream.read();

		System.out.println((char) content);

//		byte[] buf = new byte[1024 * 16];

		while (-1 != (content = fileInputStream.read())) {
			System.out.print((char)content);
		}

		fileInputStream.close();
	}
}
```

```java
public class Test2 {
	public static void main(String[] args) throws IOException {
		FileInputStream fis = new FileInputStream(new File("C:/Users/CJF/Desktop/Test.txt"));

		byte[] buf = new byte[1024 * 16];

		int count = -1;
		
		while (-1 != (count = fis.read(buf))) {
			System.out.println(new String(buf, 0, count));
		}
		
		fis.close();
	}
}
```

【注意】一般都会使用缓冲数组，因为单个字节读取效率太低了

### 1.4 FileOutputStream 文件操作字节输出流

```java
Constructor构造方法
	FileOutputStream(String filePath);
		根据用户指定的路径，创建对应的FileOutputStream文件操作输出流对象。如果
		路径不合法，抛出异常FileNotFoundException。
		采用写入数据到文件的方式，是【删除写】！！！文件内容清空，在写入数据
	
	FileOutputStream(File file);
		根据用户指定的File类对象，创建对应FileOutputStream文件操作输出流对
		象，如果路径不合法，抛出异常FileNotFoundException。
		采用写入数据到文件的方式，是【删除写】！！！文件内容清空，在写入数据
	
	FileOutputStream(String filePath, boolean append);
		根据用户指定的路径，创建对应的FileOutputStream文件操作输出流对象。如果
		路径不合法，抛出异常FileNotFoundException。
		append参数是boolean类型，如果传入参数为true，表示【追加写】，在文件末
		尾写入数据	
	
	FileOutputStream(File file, boolean append);
		根据用户指定的File类对象，创建对应FileOutputStream文件操作输出流对
		象，如果路径不合法，抛出异常FileNotFoundException。
		append参数是boolean类型，如果传入参数为true，表示【追加写】，在文件末
		尾写入数据	
		
Method成员方法
	void write(int b);
		写入一个字节数据写入到文件中
	void write(byte[] buf);
		写入一个字节数组到文件中
	void write(byte[] buf, int off, int count);	
		写入一个字节数组到文件中，要求从off偏移位置开始，计数count

操作流程:
	1. 明确对应文件的路径，可以选择直接给予对应的String类型路径，或者创建对应的File类对象，作为参数
	2. 创建FileOutputStream文件操作输出字节流，打开文件操作管道
	3. 使用FileOutputStream对象写入数据到文件中
	4. 关闭资源！！！

【注意】
	1. FileOutputStream拥有创建文件的能力，在路径合法，且对应目录有写入权限下可以创建文件
	2. 区分删除写和追加写
```

```java
public class Test {
	public static void main(String[] args) throws IOException {
		FileOutputStream fos = new FileOutputStream(new File("C:/Users/CJF/Desktop/Test.txt"));

		fos.write(97);
		System.out.println();

		FileOutputStream fos2 = new FileOutputStream(new File("C:/Users/CJF/Desktop/Test.txt"), true);

		fos2.write("\n今天是个好天气".getBytes());
        
        fos2.close();
		fos.close();
	}
}
```

### 1.5 FileReader 文件操作字符输入流

```java
Constructor构造方法
	FileReader(String filePath);	
		根据指定路径的文件创建对应的文件字符输入流对象，如果文件不存在，抛出异常
		FileNotFoundException
	FileReader(File file);
		根据指定路径的File类对象创建文件字符输入流对象，如果文件不存在，抛出异常
		FileNotFoundException
		
Method成员方法
	int read();
		从文件中读取一个字符数据，返回值为int类型，int类型数据中有且只有低十六位
		是有效数据，如果读取到文件末尾返回-1 EOF End Of File
	int read(char[] buf);
		从文件中读取数据到char类型缓冲数组buf，返回值是读取到字符个数。如果读取
		到文件末尾返回-1 EOF End Of File

操作流程:
	1. 明确需要读取数据的文件
	2. 创建FileReader对象，打开文件操作管道
	3. 使用FileReader类对象方法，读取文件数据
	4. 关闭资源
```

```java
public class Test {
	public static void main(String[] args) throws IOException {
		FileReader fr = new FileReader(new File("C:/Users/CJF/Desktop/Test.txt"));

		char[] buf = new char[1024 * 16];

		int content = -1;

		while (-1 != (content = fr.read(buf))) {
			System.out.println(new String(buf, 0, content));
		}
        
        fr.close();
	}
}
```

### 1.6 FileWriter文件操作字符输出流

```java
Constructor构造方法
	FileWriter( String filePath);
		根据用户指定的路径，创建对应的FileWriter文件操作字符输出流对象。如果
		路径不合法，抛出异常FileNotFoundException。
		采用写入数据到文件的方式，是【删除写】！！！文件内容清空，在写入数据
	
	FileWriter(File file);
		根据用户指定的File类对象，创建对应FileWriter文件操作字符输出流对
		象，如果路径不合法，抛出异常FileNotFoundException。
		采用写入数据到文件的方式，是【删除写】！！！文件内容清空，在写入数据
	
	FileWriter(String filePath, boolean append);
		根据用户指定的路径，创建对应的FileWriter文件操作字符输出流对象。如果
		路径不合法，抛出异常FileNotFoundException。
		append参数是boolean类型，如果传入参数为true，表示【追加写】，在文件末
		尾写入数据	
	
	FileWriter(File file, boolean append);
		根据用户指定的File类对象，创建对应FileWriter文件操作字符输出流对
		象，如果路径不合法，抛出异常FileNotFoundException。
		append参数是boolean类型，如果传入参数为true，表示【追加写】，在文件末
		尾写入数据	
		
Method成员方法
	void write(int ch);
		写入一个字符数据写入到文件中
	void write(char[] buf);
		写入一个字符数组到文件中
	void write(char[] buf, int off, int count);	
		写入一个字符数组到文件中，要求从off偏移位置开始，计数count
	void write(String str);
    	写入一个字符串到文件中
	void write(String str, int offset, int count);
		写入一个字符串到文件中，要求从offset偏移位置开始，计数count
	

【注意】
	1. FileWriter拥有创建文件的能力，在路径合法，且对应目录有写入权限下可以创建文件
	2. 区分删除写和追加写
```

```java
public class Test {
	public static void main(String[] args) throws IOException {
		FileWriter fw = new FileWriter(new File("C:/Users/CJF/Desktop/Test.txt"), true);

		fw.write("\n今天是520情人节");

		fw.close();
	}
}
```

### 1.7 复制文件

```java
public class TestCopyFile {
	public static void main(String[] args) throws IOException {
		FileInputStream fis = new FileInputStream(new File("C:/Users/CJF/Desktop/Test.txt"));

		FileOutputStream fos = new FileOutputStream(new File("C:/Users/CJF/Desktop/测试.txt"));

		byte[] buf = new byte[1024 * 16];

		int content = -1;

		while (-1 != (content = fis.read(buf))) {
			fos.write(buf, 0, content);
		}
        
		fos.close();
		fis.close();
	}
}
```

### 1.8 总结

```java
1、流程是一样的
	明确文件
	打开管道
	操作文件
	关闭资源
2、核心方法
	read 读取，输入
	write 写入，输出
3、输出流有创建文件的能力。
4、 输出流需要注意是删除写还是追加写。
5、输入流有缓冲比没有缓冲效率高很多
6、一定要注意关闭资源！！！resource
7、一般还是用字节流，避免文件损坏
```

