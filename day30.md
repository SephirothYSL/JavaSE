## 1. 反射

### 1.1 获取类对象

```shell
Class Class.forName(String 完整的包名.类名); √
	根据用户提供的完整包名.类名，获取对应的Class类对象，【并且该方法可以强制加载对应的.class文件。】
	
Class 类名.class;
	通过类名获取对应的Class对象属性
	
Class 类对象.getClass();
	通过类对象，获取对应的Class类对象。
```

【注意】**三种方式创建出来的对象是同一个对象，因为指向的同一个 .class 字节码文件(只加载一次)**

```java
public class Test {
	public static void main(String[] args)
			throws ClassNotFoundException, InstantiationException, IllegalAccessException, IllegalArgumentException,
			InvocationTargetException, NoSuchMethodException, SecurityException {
		
        Class<?> className = Class.forName("code.reflect.Person");

		Class<Person> className2 = Person.class;

		Class<? extends Person> className3 = new Person().getClass();

		System.out.println(className);

		System.out.println(className2);

		System.out.println(className3);
	}
}
```

### 1.2 忽略访问修饰符方法

```java
void setAccessible(boolean flag);
	该方法是可以通过【Constructor构造方法，Method成员方法，Field成员变量】调用，给予暴力反射私有化内容类外操作权限。
```

### 1.3 获取构造方法类对象

```java
Constructor[] getConstructors();
	获取当前Class类对象内所有的非私有化构造方法类对象数组。

Constructor[] getDeclaredConstructors();
	获取当前Class类对象内所有的构造方法类对象数组，包括私有化构造方法。【暴力反射】

Constructor getConstructor(Class... initParameterTypes); 【重点】
	获取指定参数数据类型，顺序，个数的非私有化构造方法Constructor类对象。
	例如:
		public Person(int id, String name) {}
		Class类对象.getConstructor(int.class, String.class);
		int.class, String.class 这里需要的构造方法参数类型是(int, String)
		
		public Person(int id) {}
		Class类对象.getConstructor(int.class);
		
		public Person() {}
		Class类对象.getConstructor();
	Class...
		1. 这里需要的参数类型是Class类对象，用于约束当前方法所需的数据类型
		2. ... 是不定长参数，参数个数不限制

Constructor getDeclaredConstructor(Class... initParameterTypes);
	获取指定参数类型，顺序，个数对应的构造方法，可以获取私有化构造方法Constructor对象【暴力反射】
	案例操作同上！！！
	例如:
		private Person(String name);
		Class类对象.getDeclaredConstructor(String.class);
```

【注意】构造方法是依赖参数区分的，根据参数的类型，个数，顺序来选择执行对应的构造方法

```java
public class Test {
	public static void main(String[] args)
			throws ClassNotFoundException, InstantiationException, IllegalAccessException, IllegalArgumentException,
			InvocationTargetException, NoSuchMethodException, SecurityException {
		Class<?> className = Class.forName("code.reflect.Person");

		Constructor<?>[] constructors = className.getConstructors();
		
		for (Constructor<?> constructor : constructors) {
			System.out.println(constructor);
		}
		
		System.out.println("----------------------------");
		
		Constructor<?>[] declaredConstructors = className.getDeclaredConstructors();
		
		for (Constructor<?> constructor : declaredConstructors) {
			System.out.println(constructor);
		}
		
		System.out.println("----------------------------");
		
		Person person1 = (Person) className.getConstructor().newInstance();

		System.out.println(person1);
		
		System.out.println("----------------------------");
		
		Constructor<?> dc = className.getDeclaredConstructor(String.class);
	
		dc.setAccessible(true);
		
		Person person2 = (Person) dc.newInstance("Buffer");
		
		System.out.println(person2);
	}
}
```

### 1.4 获取成员方法类对象并调用

```java
Method[] getMethods();
	获取类内的所有非私有化成员方法，包括从父类继承而来的子类可以使用的成员方法。

Method[] getDeclaredMethods(); 
	获取类内的所有方法，包含私有化成员方法，但是不包括父类继承到子类成员方法。【暴力反射】

Method getMethod(String methodName, Class... parameterTypes);
	根据指定的方法名，和对应的参数类型，个数，顺序获取对应的成员方法Method类对象,
可以获取类内的非私有化成员方法，和父类继承到子类的成员方法。
	methodName 是方法名
	Class... 不定长参数，根据方法的数据类型来选择对应的成员方法。
	例如:
		public void game();
		Class类对象.getMethod("game");
		
		public void game(String game);
		Class类对象.getMethod("game", String.class);

Method getDeclaredMethod(String methodName, Class... parameterTypes);
	根据指定的方法名，和对应的参数类型，个数，顺序，获取类内的成员方法，包含私有化成员方法，但是不包括父类继承到子类的方法。【暴力反射】
	操作方式同上！！！
        
Object invoke(Object obj, Object... parameters);【用的很多】
	obj: 
		执行调用当前方法的类对象
	parameters:
		不定长参数，当前方法执行所需的实际参数，要求符合形式参数列表要求参数类
		型，个数和顺序。
	返回值类型 Object
		方法执行过程中可能会存在返回值，也有可能是void，Object表示所有，后期使
		用过程中可以按照自己的需求进行数据类型强制转换
```

```java
public class TestMethod {
	public static void main(String[] args) throws ClassNotFoundException, NoSuchMethodException, SecurityException,
			IllegalAccessException, IllegalArgumentException, InvocationTargetException, InstantiationException {
                
		Class<?> className = Class.forName("code.reflect.Person");

		Method[] methods = className.getMethods();

		for (Method method : methods) {
			System.out.println(method);
		}

		System.out.println("--------------------");

		Method[] dms = className.getDeclaredMethods();

		for (Method method : dms) {
			System.out.println(method);
		}

		System.out.println("--------------------");

		Object person = className.getConstructor().newInstance();

		Method method = className.getMethod("play");

		method.invoke(person);

		System.out.println("--------------------");

		Method dm = className.getDeclaredMethod("eat", String.class);

		dm.setAccessible(true);

		dm.invoke(person, "烤羊排");
	}
}
```

### 1.5 获取成员变量类对象及调用

```java
Field[] getFields();
	获取类内所有非私有化成员变量数组
Field[] getDeclaredFields();
	获取类内所有成员变量数组，包括私有化成员变量【暴力反射】
Field getField(String fieldName);
	根据成员变量名字，获取类内非私有化成员变量
Field getDeclaredField(String fieldName);
	根据成员变量名字，获取类内任意权限修饰成员变量，包含私有化成员变量【暴力反射】
	
void set(Object obj, Object value);
	通过Field类对象调用，第一个参数是指定哪一个类对象中使用，第二个参数是对应当前成员变量的赋值数据。

Object get(Objec obj);
	通过Field类对象调用，需要的参数是明确当前操作的是哪一个类对象中的成员变量
```

```java
public class Test {
	public static void main(String[] args)
			throws ClassNotFoundException, InstantiationException, IllegalAccessException, IllegalArgumentException,
			InvocationTargetException, NoSuchMethodException, SecurityException, NoSuchFieldException {
                
		Class<?> className = Class.forName("code.reflect.Person");

		Object person = className.getConstructor().newInstance();

		Field[] fields = className.getFields();

		for (Field field : fields) {
			System.out.println(field);
		}

		System.out.println("------------------------------");

		Field[] dfs = className.getDeclaredFields();

		for (Field field : dfs) {
			System.out.println(field);
		}

		System.out.println("------------------------------");

		Field sex = className.getField("sex");

		System.out.println(sex);

		System.out.println("------------------------------");

		Field age = className.getDeclaredField("age");

		age.setAccessible(true);

		age.set(person, 23);

		System.out.println("age.get() : " + age.get(person));

		System.out.println(person);
	}
}
```

