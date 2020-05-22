## 第一题

通过修改配置文件来实现不同的方法（反射）

### 实体类

```java
public class Student {
	public void play() {
		System.out.println("学生喜欢玩游戏");
	}
}

public class Teacher {
	public void play() {
		System.out.println("老师喜欢玩斗地主");
	}
}
```

### 配置文件

```shell
className=task.Teacher
classMethod=play
```

### 测试类

```java
public class Task {
	public static void main(String[] args)
			throws IOException, ClassNotFoundException, InstantiationException, IllegalAccessException,
			IllegalArgumentException, InvocationTargetException, NoSuchMethodException, SecurityException {
		
		// 加载键值对数据
		Properties prop = new Properties();
		BufferedReader fr = new BufferedReader(new FileReader(new File("./src/task/class.txt")));
		prop.load(fr);
		fr.close();

		// 获取数据
		String className = prop.getProperty("className");
		String classMethod = prop.getProperty("classMethod");

		// 反射
		Class<?> cls = Class.forName(className);
		Object obj = cls.getConstructor().newInstance();

		// 调用方法
		Method method = cls.getMethod(classMethod);
		method.invoke(obj);
	}
}
```

### 结果

```java
老师喜欢玩斗地主
```

## 第二题

给 ArrayList<Integer> 集合添加 String 类型的元素

```java
public class Task2 {
	public static void main(String[] args)
			throws ClassNotFoundException, InstantiationException, IllegalAccessException, IllegalArgumentException,
			InvocationTargetException, NoSuchMethodException, SecurityException {
		ArrayList<Integer> al = new ArrayList<Integer>();

		Class<?> className = Class.forName("java.util.ArrayList");

		Method method = className.getMethod("add", Object.class);

		method.invoke(al, "Hello");

		System.out.println(al);	// [Hello]
	}
}
```

