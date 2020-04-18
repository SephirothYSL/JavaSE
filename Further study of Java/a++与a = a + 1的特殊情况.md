# a++ 、++a 、  a += 1 、 a = a + 1 之间的特殊情况

## 1、首先需要明确一点：

```shell
a++ 、++a 、  a += 1 、 a = a + 1
这四个操作都是对 a 进行加1操作，数据类型相同的情况下单独成行使用没有任何区别
```

```java
class Test {
	public static void main (String[] args) {
		int num1 = 5;
		num1++;
		System.out.println(num1);	// 6
		System.out.println("----------");
		
		int num2 = 5;
		++num2;
		System.out.println(num2);	// 6
		System.out.println("----------");
		
		int num3 = 5;
		num3 += 1;
		System.out.println(num3);	// 6
		System.out.println("----------");
		
		int num4 = 5;
		num4 = num4 + 1;
		System.out.println(num4);	// 6
		System.out.println("----------");
	}
}
```

这里用了一个最简单的例子，能说明在数据类型相同的情况下 (int) 四个操作都是对 a 进行了加1操作，结果都为6

### 1.1 但是如果 a 的数据类型为 char 类型，就会有一些区别：

```java
class Test {
	public static void main (String [] args) {
		char ch1 = 'A';
		ch1++;
		System.out.println(ch1);	// B
		System.out.println("----------");
		
        char ch2 = 'A';
		++ch2;
		System.out.println(ch2);	// B
		System.out.println("----------");
		
        char ch3 = 'A';
		ch3 += 1;
		System.out.println(ch3);	// B
		System.out.println("----------");
		
        char ch4 = 'A';
		ch4 = ch4 + 1;
		System.out.println(ch4);	// 不兼容的类型: 从int转换到char可能会有损失
		System.out.println("----------");		
	}
}
```

我们会发现前三个操作的结果都为 B ，但是一旦编译 a = a + 1 相关的代码就会报错，报错内容为：不兼容的类型: 从int转换到char可能会有损失

```shell
这个时候我们发现 ch4 = ch4 + 1; 这行代码确实存在这样的问题，ch4 是字符型变量，1是默认的 int 类型常量，字符型占用2个字节空间，int 型占用4个字节空间，Java会默认分配出一个 int 型的变量来接收这个结果，但是我们用字符型变量来接收就可能会导致精度缺失的问题。而其他三个操作会进行默认的自动类型转换。
```

### 1.2 最后，讨论一中比较特殊的情况：

```java
class Test {
	public static void main(String[] args) {
		int i = 0;
		int count1 = 0;
        int count2 = 0;
        int count3 = 0;
        int count4 = 0;
		
		while (i < 5){
			count1 = ++count1;
            count2 = count2++;
            count3 += count3;
            count4 = count4 + 1;
			i++;
		}		
		
		System.out.println("count1："+count1);	// 5
        System.out.println("count2："+count2);	// 0
        System.out.println("count3："+count3);	// 5
        System.out.println("count4："+count4);	// 5
	}
}
```

这个时候我们发现 a++ 操作的结果和其他三种不同，按照我们的思考，四个操作的结果都应该为5才对

如果我们在循环的内层加上一句打印就能发现每次循环 count 的值都是0，自始至终都没有进行 +1操作

```java
class Test {
	public static void main(String[] args) {
		int i = 0;
        int count = 0;
		
		while (i < 5){

            count = count++;
			System.out.println("count："+count);
			i++;
		}		
	}
}
```

![image-20200418154206686](C:\Users\CJF\AppData\Roaming\Typora\typora-user-images\image-20200418154206686.png)

对于 count = count++; 这个操作，按照 Java 的运行机制，可以这样简单的理解

```java
int temp = count;
count = count + 1;
count = temp;
```

这样子就很容易理解了，根据 count++ 先赋值后运算的规则，用 temp 这个中间变量来接收 count 的值，此时参与运算的就是 temp ！然后再对 count 进行加1操作，最后一步，赋值操作，这个时候是把 temp 赋值给 count ！因为 temp 的值是 count 还没有进行自增操作前的值0，所以这个时候进行过自增操作的 count 被赋了0这个值，结果为0。

count 实际上进行的操作为先自增1，然后被赋值为0，但是 count 的结果实际上并没有发生改变

## 2、总结

```java
1、
    a++ 、++a 、  a += 1 、 a = a + 1
	这四个操作都是对 a 进行加1操作，数据类型相同的情况下单独成行使用没有任何区别
  
2、
    字符型操作 a = a + 1 时会报错，可能会缺失精度
    
3、
    a = a++;	
	这个操作是无效操作，a 的值并不会发生任何改变
```

