## 第一题

```java
public class Task1 {
	public static void main(String[] args) {
		MyClass mc = new MyClass();

		int value = 5;

		final int fvalue = 10;
		mc.print(fvalue);
		mc.print(value);
		mc.changeValue(fvalue);
		mc.changeValue(value);
	}
}

class MyClass {

	public void print(final int value) {
		System.out.println(value);
	}

	public void changeValue(int value) {
		value = 2 * value;
		System.out.println(value);
	}
}
```

结果

```shell
10
5
20
10
```

【注意】值传递不影响实参值

## 第二题

```java
public class Task2 {
	public static void main(String[] args) {
		final MyValue myValue = new MyValue();

		myValue.value = 100;

		System.out.println(myValue.value);
	}
}

class MyValue {
	int value;
}
```

结果

```java
100
```

【注意】final修饰的对象不能更改地址指向，但是堆内存中的数据不受影响
