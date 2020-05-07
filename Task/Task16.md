## 作业

### 1.

```java
public class Task1 {
	static int num1 = 10;
	static int num2 = 20;

	{
		System.out.println("构造代码块");
	}

	static {
		num1 = 20;
		num2 = 100;
	}

	public Task1() {
		System.out.println("构造方法");
	}

	public static void main(String[] args) {
		new Task1();
		System.out.println(num1);
		System.out.println(num2);
	}
}
```

结果

```java
构造代码块
构造方法
20
100
```

### 2.

```java
class Task2 {
	Task2 demo1 = new Task2();
	Task2 demo2 = new Task2();
    
    {
    	System.out.println("构造代码块");   
    }
    
    static {
        System.out.println("静态代码块");  
    }
    
    public Task2() {
        System.out.println("构造方法");  
    }
    
    public static void main(String[] args) {
    	new Task2();
    }
}
```

结果

```java
静态代码块
Exception in thread "main" java.lang.StackOverflowError
```

递归创建对象，死循环
