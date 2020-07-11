### 正文

在一次 codding 的过程中，我需要用一个空字符串，于是我就这样定义了：

```java
String nullStr = null;
```

然后我在使用过程中发现这样定义并不能达到我想要的效果，因为我想显示的是空字符，而不是显示"null"，于是我重新定义了新的字符串：

```java
String nullStr = "";
```

才实现了我想要的效果，即显示一个空字符串，而不是"null"。

因为这个案例给我造成了困惑，所以我研究了一下 Java 中关于字符串拼接的问题，样例代码如下

```java
public class Test {
    public static void main(String[] args) {
        String s1 = "";
        String s2 = null;

        System.out.println(s1);
        System.out.println(s2);
        System.out.println(s1 + s1);
        System.out.println(s2 + s2);
        System.out.println(s1 + s2);
    }
}
```

打印结果如下：

```java
null

nullnull
null
```

我们先来看一下反编译的 class 文件

```java
public class Test
{

	public Test()
	{
	}

	public static void main(String args[])
	{
		String s1 = "";
		String s2 = null;
		System.out.println(s1);
		System.out.println(s2);
		System.out.println((new StringBuilder()).append(s1).append(s1).toString());
		System.out.println((new StringBuilder()).append(s2).append(s2).toString());
		System.out.println((new StringBuilder()).append(s1).append(s2).toString());
	}
}
```

这时我们可以发现，字符串用 + 拼接实际上是创建了一个 StringBuilder 对象然后再调用 append 方法逐一进行拼接，我们再来看 StringBuilder 的源码：

```java
public final class StringBuilder extends AbstractStringBuilder{
    private transient char[] toStringCache;
    
    @Override
    public synchronized StringBuilder append(Object obj) {
        toStringCache = null;
        super.append(String.valueOf(obj));
        return this;
    }
    
    @Override
    public synchronized String toString() {
        if (toStringCache == null) {
            toStringCache = Arrays.copyOfRange(value, 0, count);
        }
        return new String(toStringCache, true);
    }
}
```

这里我们主要看两个方法，append 方法和 toString 方法。

首先，append 方法默认调用了父类的 append 方法，传入的参数还经过了 String 类的 valueOf 方法进行了包装，那我们再来看一眼这个方法：

```java
public static String valueOf(Object obj) {
        return (obj == null) ? "null" : obj.toString();
}
```

这里就是给我造成困惑的原因所在，可以看到这个方法就是对传入的参数做了一次判断，**如果为null，就返回字符串"null"**，我之前定义的 null 字符串在这里就已经变成了 "null"，所以后面会打印出 null 也是理所应当的。

回到 append 方法，此时我们传递了一个 "null" 字符串给父类的 append 方法，那我们再深入到父类中去一探究竟：

```java
abstract class AbstractStringBuilder{
    char[] value;
    
    int count;
    
    private void ensureCapacityInternal(int minimumCapacity) {
        // overflow-conscious code
        if (minimumCapacity - value.length > 0) {
            value = Arrays.copyOf(value,
                    newCapacity(minimumCapacity));
        }
    }
    
    public void getChars(int srcBegin, int srcEnd, char dst[], int dstBegin) {
        if (srcBegin < 0) {
            throw new StringIndexOutOfBoundsException(srcBegin);
        }
        if (srcEnd > value.length) {
            throw new StringIndexOutOfBoundsException(srcEnd);
        }
        if (srcBegin > srcEnd) {
            throw new StringIndexOutOfBoundsException(srcEnd - srcBegin);
        }
        System.arraycopy(value, srcBegin, dst, dstBegin, srcEnd - srcBegin);
    }
    
    private AbstractStringBuilder appendNull() {
        int c = count;
        ensureCapacityInternal(c + 4);
        final char[] value = this.value;
        value[c++] = 'n';
        value[c++] = 'u';
        value[c++] = 'l';
        value[c++] = 'l';
        count = c;
        return this;
    }
    
    public AbstractStringBuilder append(String str) {
        if (str == null)
            return appendNull();
        int len = str.length();
        ensureCapacityInternal(count + len);
        str.getChars(0, len, value, count);
        count += len;
        return this;
    }
}
```

父类中有两个变量比较重要，一个是 value ，这个 value 其实就是字符串本身了，是以字符数组的形式存在的；另一个变量是 count ，存储的是字符串的长度，（同时也是字符数组 value 的容量，其实都是一回事）。这两个变量都会传递给 StringBuilder 的 toString 方法。

这时候我们再看 append 方法，首先对传入的字符串进行判断，如果是 null 就执行 appendNull 方法，这个方法就是给 value 赋上 'n' 'u' 'l' 'l' ，再给 count 赋上4就大功告成了。当然如果传入的字符串不为空，就执行 ensureCapacityInternal 方法和 getChars 方法给 count 和 value 赋上对应的值。

这个时候 append 方法已经执行完毕了，我们在父类中得到了带有值的 value 和 count。我们回到 StringBuilder 类中看 toString 方法，因为这个方法才是最终打印结果到控制台要执行的方法：

```java
@Override
public synchronized String toString() {
    if (toStringCache == null) {
        toStringCache = Arrays.copyOfRange(value, 0, count);
    }
    return new String(toStringCache, true);
}
```

进来先对 toStringCache 这个变量进行一下判断，这里是一定等于 null 的，因为我们的 append 方法中一开始就将这个字段设置为 null 了。

```java
@Override
public synchronized StringBuilder append(Object obj) {
    toStringCache = null;
}
```

所以结果一定为真，将 toStringCache 赋上值，这里用到了父类的 value 和 count（我们刚刚已经给这两个变量赋上值了）。接下来就是将 toStringCache  转成字符串了，用到了 String 类中的方法：

```java
public String(char value[], int offset, int count) {
    if (offset < 0) {
        throw new StringIndexOutOfBoundsException(offset);
    }
    if (count <= 0) {
        if (count < 0) {
            throw new StringIndexOutOfBoundsException(count);
        }
        if (offset <= value.length) {
            this.value = "".value;
            return;
        }
    }
    // Note: offset or count might be near -1>>>1.
    if (offset > value.length - count) {
        throw new StringIndexOutOfBoundsException(offset + count);
    }
    this.value = Arrays.copyOfRange(value, offset, offset+count);
}
```

被转为字符串的 toStringCache  输出到控制台中，于是我们看到了上面案例中的结果：

```java
null

nullnull
null
```

这时就能完全理解了，不管有多少字符串使用 + 拼接，都是 new 了一个 StringBuilder 重复调用 append 方法而已。

### 补充

```java
String s1 = "";
String s2 = new String();
```

这个案例中的 s1 和 s2 是完全相同的，可见 String 类的源码：

```java
public final class String
    public String() {
            this.value = "".value;
    }
}
```

当调用无参构造时，默认传递的字符串为 ""
