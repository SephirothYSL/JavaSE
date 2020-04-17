# 理解Java中逻辑表达式的短路机制

关于运算符优先级与执行顺序的问题：

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



结论：

​	1、Java 中优先级高的表达式会被视为一个整体（如小括号相较于其他运算符，或 && 相较于 || ），但是执行顺序还是从左到右

​	2、在满足一的前提下，再执行短路原则



————————————————
版权声明：本文为CSDN博主「桑汤奈伊伏」的原创文章，遵循 CC 4.0 BY-SA 版权协议，转载请附上原文出处链接及本声明。
原文链接：https://blog.csdn.net/libertine1993/java/article/details/47378427