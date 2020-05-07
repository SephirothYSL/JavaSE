# Java中参数的传递

## 1. 形参与实参

### 1.1 形参

用来接收调用该方法时传递的参数。只有在被调用的时候才分配内存空间，一旦调用结束，就释放内存空间。因此仅仅在方法内有效。是一个局部变量

### 1.2 实参

传递给被调用方法的值，预先创建并赋予确定值。

## 2. 基本数据类型的传参：值传递

```java
public class Test1 {
    public static void main(String[] args) {
        int i = 10;
        int j = 5;

        System.out.println("i：" + i + "\tj：" + j);
        swap(i, j);
        System.out.println("i：" + i + "\tj：" + j);
    }
 
    public static void swap(int a, int b) {
        int temp = a;
        a = b;
        b = temp;
        System.out.println("a：" + a + "\tb：" + b);
    }
}
```

执行的结果如下：

![https://p.pstatp.com/origin/fe9a00017f52035dc529](https://p.pstatp.com/origin/fe9a00017f52035dc529)

因为基本类型传递参数，是将实参的值复制一份传递给形参，然后由形参去参与方法内的代码执行，当方法执行到最后一行，形参被销毁，方法结束。此时全程只有形参的值发生了改变，而实参却没有改变。

## 3. 引用数据类型的传参：引用传递，传递的是地址

```java
public class Test2 {
    public static void main(String[] args) {
        Test test = new Test();
        Data data = new Data();
        System.out.println("data.i："+data.i+" data.j："+data.j);
        
        swap(data);
        System.out.println("data.i："+data.i+" data.j："+data.j);

    }

    public static void swap(Data data) {
        int temp = data.i;
        data.i = data.j;
        data.j = temp;
    }
}

class Data {
    int i = 10;
    int j = 5;
}
```

执行的结果如下：

![https://p.pstatp.com/origin/ffc80000e152a2f54985](https://p.pstatp.com/origin/ffc80000e152a2f54985)

在传递引用调用中，如果传递的参数是引用数据类型，参数视为实参。在调用的过程中，将实参的地址传递给了形参，形参上对于对象的所有改变都发生在实参上。所以 i 和 j 实现了数据的交换

## 4. Java中只有值传递

在做练习题的时候，我遇到这样一种情况，这里我用代码简单描述一下：

```java
class Test3 {
	public static void main(String[] args) {		
		
		int[] array1 = new int[3];
		int[] array2 = new int[5];
		
		method(array1, array2);
		
		System.out.println(array1.length);	// 3
		System.out.println(array2.length);	// 5
	}
	
	public static void method(int[] array1, int[] array2) {
		array1 = array2;
	}
}
```

我得到的结果是 3 和 5 ，这个时候我就有了一个疑问，引用数据类型作为参数传递的是地址，形参的所有更改不应该都作用到实参上才对吗？结果应该是5 和 5 啊！

但其实这种理解是错误的。这里举一个形象的例子来帮助理解值传递和引用传递

你有一把钥匙，当你的朋友想要去你家的时候，如果你直接把你的钥匙给他了，这就是引用传递。这种情况下，如果他对这把钥匙做了什么事情，比如他在钥匙上刻下了自己名字，那么这把钥匙还给你的时候，你自己的钥匙上也会多出他刻的名字。

你有一把钥匙，当你的朋友想要去你家的时候，你复刻了一把新钥匙给他，自己的还在自己手里，这就是值传递。这种情况下，他对这把钥匙做什么都不会影响你手里的这把钥匙。

但是，不管上面哪种情况，你的朋友拿着你给他的钥匙，进到你的家里，把你家的电视砸了。那你说你会不会受到影响？而我们在讨论 Test2 的代码里的 swap 方法，不就是在“砸电视”吗？swap 方法改变的不是那把钥匙，而是钥匙打开的房子

现在我们对值传递和引用传递是不是有了一些不一样的理解？

其实我们的 method 方法里的形参，是把实际参数的引用的地址复制了一份，传递给了形式参数。**所以，上面的参数其实是值传递，把实参对象引用的地址当做值传递给了形式参数**

**引用传递实际上是对形式参数的地址所指向的堆内元素的引用**，这个时候才会影响实参，而对形式参数的地址做修改并不会影响到实参本身。这就好像你朋友砸了你家的电视和在复刻的钥匙上刻字的区别

通过代码表示就是Test3 和 Test2 的区别，Test3 只是作用于形式参数，并没有对其地址指向堆内数据发生改变，所以实参并不会发生改变；而 Test2 直接作用于其地址指向的堆内数据，所以实参也会发生改变

## 5. 总结

**Java中只有值传递(复制地址再传递)，对于引用类型参数，值的内容是对象的引用。当形参引用的对象发生改变，才会影响到实参(引用传递)**
