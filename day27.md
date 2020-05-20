## 1. File 类

文件和目录路径名的抽象表示形式

### 1.1 构造方法

```java
File(String pathName);
	根据指定的文件路径，或者文件夹路径，创建对应的File类对象。路径可以是相对路径，可以是绝对路径
File(String parent, String childName);
	根据指定的父目录文件夹路径，和子文件或者子文件夹的名字，创建对应的File类对象
File(File parent, String childName);
	根据指定的父目录File类对象，和子文件或者子文件夹的名字，创建对应的File类对象
```

【注意】如果是文件必须要有后缀名，否则就是文件夹

```java
public class Test {
	public static void main(String[] args) {
		File file1 = new File("D:/aaa");
		File file2 = new File("D:/aaa", "1.txt");
		File file3 = new File(file1, "1.txt");
		
		System.out.println(file1);	// D:\aaa
		System.out.println(file2);	// D:\aaa\1.txt
		System.out.println(file3);	// D:\aaa\1.txt
	}
}
```

### 1.2 创建方法

```java
boolean createNewFile();
	通过File类对象调用，创建File类对象中对应地址的普通文件，创建成功返回true，创建失败返回false;
	失败原因:
		1. 路径不合法，路径不存在，路径错误。
		2. 对应文件夹没有写入权限。
			D:/aaa/bb/cc/1.txt
				cc里面 cc是文件夹，没有写入权限，创建失败。
				.lock
		3. 对应文件已存在。
		4. 磁盘坏道，电脑蓝屏。
       
boolean mkdir();
	通过File类对象创建，创建File类对象中对应的文件夹，创建成功返回true，失败返回false
	失败原因:
		1. 路径不合法，路径不存在，路径错误。
		2. 对应文件夹没有写入权限。
		3. 对应文件夹已存在。
		4. 磁盘坏道，电脑蓝屏。

boolean mkdirs();
	操作很变态。
	创建文件夹过程中可以完成中间路径

boolean renameTo(File dest);
	通过File类对象调用，转为目标dest指定File类对象，可以操作普通文件，可以操作文件夹。移动，重命名
```

```java
public class Test {
	public static void main(String[] args) throws IOException {
		File file1 = new File("C:/Users/CJF/Desktop/啥啥啥.txt");

		boolean createNewFile = file1.createNewFile();
		System.out.println(createNewFile);

		File file2 = new File("C:/Users/CJF/Desktop/啥啥啥");
		boolean mkdir = file2.mkdir();
		System.out.println(mkdir);

		File file3 = new File("C:/Users/CJF/Desktop/啥啥啥/afaf/aggr/htedfgb/er");
		boolean mkdirs = file3.mkdirs();
		System.out.println(mkdirs);

		File file4 = new File("C:/Users/CJF/Desktop/什么鬼.txt");

		boolean renameTo = file1.renameTo(file4);
		System.out.println(renameTo);
	}
}
```

### 1.3 删除方法

```java
boolean delete();
	通过File类对象调用，删除File类对象对应的文件或者文件夹。
	注意事项:
		1. 从磁盘中直接抹掉数据，慎用
		2. 删除操作只针对于空文件夹操作，不能删除非空文件夹
	
void deleteOnExit();
	程序退出之后，删除调用该方法File类对象，对应的普通文件或者文件夹。
	用于缓冲文件，缓存问题，日志文件
```

```java
public class Test {
	public static void main(String[] args) throws IOException {
		File file = new File("C:/Users/CJF/Desktop/Test.txt");
		
		System.out.println(file.createNewFile());	// true
		
		System.out.println(file.delete());	// true
		
		file.deleteOnExit();
	}
}
```

### 1.4 获取方法

```java
方法和文件或者文件夹是否存在无关。
String getPath();
	获取File类对象中保存的路径
String getName();
	获取File类对象操作对应的文件名或者文件夹名

String getParent();
	获取File类对象操作文件或者文件夹的上级目录

String getAbsolutePath();
	获取当前File类对象对应路径的绝对路径

long length();
	获取当前【文件】的占用磁盘空间字节数
	根据不同的系统环境，文件夹调用length方法 0L 或者 4096L
long lastModified();
	获取当前文件夹上一次修改时间的【时间戳】
	是从计算机元年1970-01-01 00:00:00 到修改时间的秒数
```

```java
public class Test {
	public static void main(String[] args) {
		File file = new File("D:/aaa/bbb/ccc/1.txt");
		
		System.out.println(file.getPath());	// D:\aaa\bbb\ccc\1.txt
		System.out.println(file.getParent());	// D:\aaa\bbb\ccc
		System.out.println(file.getName());	// 1.txt

		System.out.println(file.length());	// 0
		
		System.out.println(file.lastModified());// 0
		
		System.out.println(new File(".").getAbsolutePath());	// D:\Qfeng\day27\.
	}
}
```

### 1.5 判断方法

```java
boolean isFile();
	判断当前File类对象对应的是不是普通文件。
boolean isDirectory();
	判断当前File类对象对应的是不是文件夹。
boolean exists();
	判断当前File类对象对应的内容是否存在。
boolean isAbsolute();
	判断当前File类对象保存的路径是不是绝对路径。
boolean isHidden();
	判断当前File类对象对应的文件是不是一个隐藏文件。
```

```java
public class TestFileDecide {
	public static void main(String[] args) {
		File file = new File("D:/Adobe");
		
		System.out.println(file.exists());	// true
		System.out.println(file.isFile());	// false
		System.out.println(file.isDirectory());	// true
		System.out.println(file.isAbsolute());	// true
		System.out.println(file.isHidden());	// false
	}
}
```

### 1.6 列表方法

```java
static File[] listRoots();	
	获取Windows操作系统下的所有盘符
	Linux中没有什么作用。

String[] list();
	获取File类对象对应文件夹中所有子文件或者子文件夹名字，String类型数组
	
File[]	listFiles();
	获取File类对象对应文件夹中所有子文件或者子文件夹的File类对象数组
```

```java
public class Test {
	public static void main(String[] args) {
		File file = new File("C:/Users/CJF/Desktop");

		String[] list = file.list();
		for (String fileName : list) {
			System.out.println(fileName);
		}

		File[] listFiles = file.listFiles();
		for (File file2 : listFiles) {
			System.out.println(file2);
		}

		File[] listRoots = File.listRoots();
		for (File file2 : listRoots) {
			System.out.print(file2 + "\t"); // C:\ D:\ E:\
		}
	}
}
```

### 1.7 FilenameFilter 文件名过滤器接口

实现此接口的类实例可用于过滤器文件名。

```java
boolean accept(File dir, String name);
	dir是当前操作获取文件列表的文件夹File类对象
	name是当前文件夹下的文件名或者文件夹名
```

```java
public class Test {
	public static void main(String[] args) {
		File file = new File("D:\\Qfeng\\day05\\code");

		String[] fileNameArray = file.list(new FilenameFilter() {

			@Override
			public boolean accept(File dir, String name) {
				return new File(dir, name).isFile() && name.endsWith(".java");
			}
		});

		for (String fileName : fileNameArray) {
			System.out.println(fileName);
		}
	}
}
```
