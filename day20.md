## 1. instanceof 关键字

用于判断当前对象是否是某个类，或者其子类、实现类的实例。如果是返回true，否则返回false。

Play接口

```java
public interface Play {

}
```

Person 类

```java
class Person {

}

// Man 类继承 Person，同时实现 Play 接口
class Man extends Person implements Play{

}
```

测试类

```java
package code.testinstanceof;

public class TestPerson {
	public static void main(String[] args) {
		Person person = new Person();
		
		Man man = new Man();
		
        // person 对象是通过Person类创建的，打印：person 是 Person
		if(person instanceof Person) {
			System.out.println("person 是 Person");
		}
		
        // 父类对象指向子类引用，不成立，结果为 false
		if(person instanceof Man) {
			System.out.println("person 是 Man");
		}
		
        // 子类对象指向父类引用，成立，打印：man 是 Persom
		if(man instanceof Person) {
			System.out.println("man 是 Persom");
		}
		
        // man 是Play接口的实现类创建的对象，成立，打印：man 是 Play
		if(man instanceof Play) {
			System.out.println("man 是 Play");
		}
		
        // Person 未实现 Play 接口，不成立
		if(person instanceof Play) {
			System.out.println("person 是 Play");
		}		
	}
}
```

结果

```java
person 是 Person
man 是 Persom
man 是 Play
```

【注意】**使用 instanceof 关键字做判断时， instanceof 操作符的左操作数必须和右操作数存在继承或实现关系**

## 2. Object 类

Object类是类层次结构的根类，所有类都直接或者间接的继承自该类

### 2.1 toString

用来返回对象的字符串表示形式

```java
public String toString()
```

返回值为：包名.类名@当前对象在内存空间中的首地址

```java
getClass().getName() + '@' + Integer.toHexString(hashCode())
```

由于默认情况下的数据对我们来说没有意义，一般会重写该方法用以展示对象的字段信息

```java
public class Student {
	String name;
	int age;
    
    // 重写 toString 方法
    @Override
	public String toString() {
		return "Student [name=" + name + ", age=" + age + "]";
	}
}
```

测试

```java
public class TestStudent {
	public static void main(String[] args) {
		Student student = new Student("Buffer",23);		
		System.out.println(student);
	}
}
```

结果

```shell
Student [name=Buffer, age=23]
```

### 2.2 equals

用来比较两个对象的地址是否相同

```
public boolean equals(Object obj) {
        return (this == obj);
}
```

如果调用此方法的对象与 obj 的地址相同(即为同一个对象)，返回true，否则返回false

一般需要重写 equals() 方法用以判断两个对象的字段是否相同

```java
public class Student {
	String name;
	int age;
    
    // 重写 equals 方法
    @Override
	public boolean equals(Object obj) {

        // 判断是否是同一个对象(地址相同)，如果是返回 true
		if (this == obj) {
			return true;
		}

        // 判断数据类型是否一致，如果不一致返回 false
		if (!(obj instanceof Student)) {
			return false;
		}

        // 强制类型转换为当前类对象
		Student student = (Student) obj;

        // 所有字段全部满足时返回 true ，否则返回false
		return this.name.equals(student.name) && this.age == student.age;
	}
}
```

测试

```java
public class TestStudent {
	public static void main(String[] args) {
		Student student1 = new Student("Buffer",23);
		Student student2 = new Student("Banlance",22);
		Student student3 = new Student("Buffer",23);
		
		System.out.println(student1.equals(student2));
		System.out.println(student1.equals(student3));
	}
}
```

结果

```java
false
true
```

【注意】基本数据类型不能使用 equals() 方法

### 2.3 hashCode

返回对象的哈希码值，**具有唯一指向性**

```java
public int hashCode()
```

hashCode方法要求必须和 equals() 方法的结果是对应的，如果两个对象的 equals 的结果为 true ，那这两个对象的 hashCode 的值一定相同，所以**只要重写了 equals 方法，就必须重写 hashCode 方法**

```java
public class Student {
	String name;
	int age;
    
    // 重写 equals 方法
    @Override
	public boolean equals(Object obj) {
		if (this == obj) {
			return true;
		}

		if (!(obj instanceof Student)) {
			return false;
		}

		Student student = (Student) obj;

		return this.name.equals(student.name) && this.age == student.age;
	}
    
    // 重写 hashCode 方法
    @Override
	public int hashCode() {
        // 调用 Objects 工具类的 hash 方法，根据传入的参数生成一个指定的 hashCode 值
		return Objects.hash(name, age);
	}
}
```

测试

```java
public class TestStudent {
	public static void main(String[] args) {
		Student student1 = new Student("Buffer",23);
		Student student2 = new Student("Banlance",22);
		Student student3 = new Student("Buffer",23);
		
		System.out.println(student1.equals(student2));
		System.out.println(student1.equals(student3));

		System.out.println(student1.hashCode());
		System.out.println(student2.hashCode());
		System.out.println(student3.hashCode());	
	}
}
```

结果

```shell
false
true
1892650872
247063595
1892650872
```

student1 和 student3 的 equals 方法返回值是 true ，所以他们的 hashCode 值相同

## 3. 异常

### 3.1 Throwable 类

Throwable 类是Java语言中所有错误和异常的顶级父类，直接子类为 Error 和 Exception

#### 3.1.1 构造方法

```java
无参构造：构造一个新的 throwable 对象，其详细信息为null
public Throwable()
    
有参构造：使用指定的详细信息(message)构造一个新的 throwable 对象
public Throwable(String message)
```

#### 3.1.2 成员方法

```java
// 返回此 throwable 对象的详细信息字符串
public String getMessage()

// 返回一个简要信息描述
public String toString()
    
// 打印此 throwable 对象及其详细信息字符串到标准错误流(控制台)
public void printStackTrace()
```

测试

```java
public class Test {
	public static void main(String[] args) {
		Throwable throwable1 = new Throwable();
				
		System.out.println(throwable1.getMessage());
		System.out.println(throwable1.toString());
		throwable1.printStackTrace();
		
		Throwable throwable2 = new Throwable("错误信息！！！");
		
		System.out.println(throwable2.getMessage());
		System.out.println(throwable2.toString());
		throwable2.printStackTrace();
	}
}
```

结果

```java
null
java.lang.Throwable
java.lang.Throwable
错误信息！！！
java.lang.Throwable: 错误信息！！！
	at code.throwable.Test.main(Test.java:5)
java.lang.Throwable: 错误信息！！！
	at code.throwable.Test.main(Test.java:11)
```

### 3.2 Error

Error 类是 Throwable 的子类，它指出了一个合理的应用程序不应该试图捕捉的严重问题

Error 结尾的是严重问题，无法解决

### 3.3 Exception

Exception 类及其子类是一种 Throwable 的子类，指示了一个合理的应用程序可能想要捕获的条件。

Exception 结尾的是我们可以处理的

```shell
RuntimeException	 运行期异常，我们需要修正代码
非RuntimeException 	编译期异常，必须处理的，否则程序编译不通过
```



