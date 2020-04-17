# 理解Java中逻辑表达式的短路机制

### 关于运算符优先级与执行顺序的问题：

​		运算符优先级高的表达式在执行时会被视为一个整体,  但是对于除赋值符外的所有二元运算符来说,  执行的顺序始终是从左到右执行的

```java
/*
* 测试运算符的优先级是否与执行顺序有关 
*/
public class TestOrder{
	public static int test(int para){
	System.out.println("called with para = " + para);
        return para;
    }
	 
    public static void main(String[] args){
	int i = test(0) + test(1) - test(2) * test(3);
	System.out.println("-------------------------");
		 
	i =test(0) + test(1) + test(2) + ( test(3) - test(4) );
	System.out.println("-------------------------");
		 
	i = ( test(0) - test(1) ) + test(2) + test(3) *  test(4);
    } 
}
```

输出结果：

![img](https://img-blog.csdn.net/20150809201638752)

第一个表达式 " test(2) * test(3)" 拥有较高的优先级, 所以会被视为一个整体, 但是程序的执行顺序还是从左到右, 因此调用的顺序是 test(0), test(1), test(2), test(3) 

第二个表达式理同第一个

第三个表达式执行顺序是 (整体) , test(2), test(3), test(4)

对于++, --,这种运算符的解释, 也一样 a + ++b 的执行顺序是从左往右, a + (整体), 整体是++b

可以明确Java运算符优先级高的表达式会被视为整体, 但是执行顺序还是从左到右！！！



### 逻辑表达式的短路机制:

​		在 Java 中, 在已经能够确定整个逻辑表达式的值的情况下, 就会对整个逻辑表达式进行求值, 也就是说会有部分的条件不会被判断到, 因为我们已经能够确定整个逻辑表达式的值了(当然这种机制仍然要遵循表达式执行的顺序)

```java
import java.util.*;
 
public class ShortCircuit{
    public static boolean test(int para){
	    System.out.println("test is called with para = " + para);
		return para > 5;
	}  
	
	public static void main(String[] args){		
		System.out.println("----------------------------------------");
		if(test(8) || test(1) && test(4)){}
		
		System.out.println("----------------------------------------");
        //嵌套的逻辑表达式, 短路的判断会逐级别判断
        if( (test(9) || test(6) || test(7)) || test(8) && test(1)){}
        /*内层逻辑表达式  test(8) && test(1) */		
	}
}
```

![img](https://img-blog.csdn.net/20150809205148704)

第一个表达式中, &&的优先级高 (关于&&的优先级高于||, 有疑惑的请拉至最下方, 参考来自Sun的官方文档给出的优先级表格),  所以test(1) && test(4) 会被当成整体, 外层的逻辑表达式是 test(8) || (整体), 故因为test(8) 为真, 整个逻辑表达式的值已确定为真, 故发生短路, 只判断了test(8)的条件

第二个表达式说明, 短路机制的判断会发生在每一层的逻辑表达式当中(当然仍然得遵循执行顺序).内层表达式 test(9) || test(6) || test(7) 只判断了test(9) 就短路，不再执行优先级更高的判断



### Java官方文档运算符优先级:

![img](https://img-blog.csdn.net/20150809202734977)



### 结论：

​	1、Java 中优先级高的表达式会被视为一个整体（如小括号相较于其他运算符，或 && 相较于 || ），但是执行顺序还是从左到右

​	2、在满足一的前提下，再执行短路原则



————————————————

版权声明：本文摘自CSDN博主「桑汤奈伊伏」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/libertine1993/java/article/details/47378427
