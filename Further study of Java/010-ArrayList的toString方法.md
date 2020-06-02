# ArrayList 的 toString 方法源码

```java
public class Test {
	public static void main(String[] args) {
		ArrayList<String> arrayList = new ArrayList<String>();
		
		arrayList.add("Hello");
		arrayList.add("World");
		arrayList.add("Java");
		
		System.out.println(arrayList);
	}
}
```

结果

```java
[Hello, World, Java]
```

直接打印集合本身，调用其 toString 方法，没有输出地址值，说明重写了 toString 方法，但是ArrayList中没有重写 toString 方法，其父类 AbstractList 类中也重写没有这个方法，再往上的父类 AbstractCollection 中发现重写了 toString 方法

```java
public abstract class AbstractCollection<E> implements Collection<E> {
	public String toString() {
        Iterator<E> it = iterator();	// 这里其实省略了 this ，完整写法为：this.iterator()
        if (! it.hasNext())				// 如果集合为空直接打印[]
            return "[]";

        StringBuilder sb = new StringBuilder();		// 创建一个 StringBuilder 
        sb.append('[');
        for (;;) {
            E e = it.next();	// 获取迭代器指向的元素
            sb.append(e == this ? "(this Collection)" : e);	// 如果这个元素不等于当前集合，就打印
            if (! it.hasNext())	// 当没有下一个元素就打印 ]
                return sb.append(']').toString();
            sb.append(',').append(' ');
        }
    }
}
```

> 对 this 的理解

```java
public class Test {
	public static void main(String[] args) {
		ArrayList<ArrayList<?>> al = new ArrayList<ArrayList<?>>();
		al.add(al);
		System.out.println(al);
	}
}
```

结果

```java
[(this Collection)]
```

当集合的泛型为其本身，且添加元素也为自身时才会输出 [(this Collection)] ，避免自己添加自己成为死循环
