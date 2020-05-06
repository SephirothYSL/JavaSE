## 面试题一

```java
public class Test extends Base {
	static {
		System.out.println("test static");
	}

	public Test() {
		System.out.println("test constructor");
	}

	public static void main(String[] args) {
		new Test();
	}
}

class Base {

	static {
		System.out.println("base static");
	}

	public Base() {
		System.out.println("base constructor");
	}
}
```

结果

```java
base static
test static
base constructor
test constructor
```

在程序执行的开始，先要寻找到main方法，因为main方法是程序的入口，但是在执行main方法之前，必须先加载Test类，而在加载Test类的时候发现Test类继承自Base类，因此会转去先加载Base类，在加载Base类的时候，发现有static块，便执行了static块。在Base类加载完成之后，便继续加载Test类，然后发现Test类中也有static块，便执行static块。在加载完所需的类之后，便开始执行main方法。在main方法中执行new Test()的时候会先调用父类的构造器，然后再调用自身的构造器。因此，便出现了上面的输出结果。

## 面试题二

```java
public class Test2 {
	Person person = new Person("Test");
	
	static {
		System.out.println("test static");
	}

	public Test2() {
		System.out.println("test constructor");
	}

	public static void main(String[] args) {
		new MyClass();
	}
}

class Person {
	
	static {
		System.out.println("person static");
	}

	public Person(String str) {
		System.out.println("person " + str);
	}
}

class MyClass extends Test2 {
	Person person = new Person("MyClass");
	
	static {
		System.out.println("myclass static");
	}

	public MyClass() {
		System.out.println("myclass constructor");
	}
}
```

结果

```java
test static
myclass static
person static
person Test
test constructor
person MyClass
myclass constructor
```

首先加载Test类，因此会执行Test类中的static块。接着执行new  MyClass()，而MyClass类还没有被加载，因此需要加载MyClass类。在加载MyClass类的时候，发现MyClass类继承自Test类，但是由于Test类已经被加载了，所以只需要加载MyClass类，那么就会执行MyClass类的中的static块。在加载完之后，就通过构造器来生成对象。而在生成对象的时候，必须先初始化父类的成员变量，因此会执行Test中的Person person = new  Person()，而Person类还没有被加载过，因此会先加载Person类并执行Person类中的static块，接着执行父类的构造器，完成了父类的初始化，然后就来初始化自身了，因此会接着执行MyClass中的Person person = new Person()，最后执行MyClass的构造器。

## 面试题三

```java
public class Test3 {

	static {
		System.out.println("test static 1");
	}

	public static void main(String[] args) {
		System.out.println("test static 2");
	}

	static {
		System.out.println("test static 3");
	}
}
```

结果

```java
test static 1
test static 3
test static 2
```

首先我们要明确：1、static块可以出现类中的任何地方（只要不是方法内部，记住，任何方法内部都不行），并且执行是按照static块的顺序执行的。2、static代码块的优先级高于main方法。这样执行的结果就显而易见了

## 面试题四

```java
public class Test {
	static Test test1 = new Test();
	static Test test2 = new Test();

	static {
		System.out.println("静态代码块");
	}

	{
		System.out.println("构造代码块");
	}

	public Test() {
		System.out.println("构造方法");
	}

	public static void main(String[] args) {
        System.out.println("main方法");
		new Test();
	}
}
```

结果

```shell
构造代码块
构造方法
构造代码块
构造方法
静态代码块
main方法
构造代码块
构造方法
```

根据结果可以发现，虽然main方法是程序执行的入口，但是程序执行前的加载过程，要对static修饰的变量、方法、代码块进行加载，按照顺序执行，刚开始我不理解为什么静态代码块没有在最开始就执行，但其实把静态对象当成普通的变量就好理解了，就是按照static出现的顺序往下执行
