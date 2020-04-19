## 1. 相同点

三目运算符有三个操作数，第一个为表达式，剩下两个为值，当表达式条件为真时取第一个值，当条件为假时取第二个值。

```java
class Test {
	public static void main (String[] args) {
		System.out.println(2 == 2 ? 1 : 2);	// 1
	}
}
```

三目运算符的判断表达式值为真，故取第一个值打印，结果为1

如果用 if else 同样能实现相同的效果

```java
class Test {
	public static void main (String[] args) {
        if (2 == 2) {
            System.out.println(1);
        } else {
            System.out.println(2);
        }		
	}
}
```

if 的判断结果为真，执行后面的代码，打印的结果为1

## 2. 不同点

其实很多时候三元运算符可以和if-else语句进行互换，它们两个可以等价的实现判断的效果。但是三元运算符与if-else语句也还是有不同之处的

第一：两者之间对于返回值有不同的要求，三元运算符是必须要有返回值要求，其运算后一定会有一个结果返回供程序开发人员使用；而 if else 语句并不一定有返回值，其执行结果可能是赋值语句或者打印输出语句

第二：两者的性能不同，三元运算符的运算性能相对于 if else 语句来说要高一些，但大多数情况下可以忽略不计

第三：三目运算符会进行数据类型转换（低转高）

```java
class Test {
	public static void main (String[] args) {
		char ch = 'a';
		int num = 5;
		
		System.out.println(2 == 2 ? num : 9.0);	// 5.0
		
		System.out.println("----------------");
		
		System.out.println(2 == 2 ? 97 : ch); 	// a
		
		System.out.println("----------------");	
		
		System.out.println(2 == 2 ? ch : num);	// 97
		
		System.out.println("----------------");	
		
		System.out.println(2 == 2 ? 99 : 9.0);	// 99.0
		
		System.out.println("----------------");
		
		System.out.println(2 == 2 ? 99 : 'a');	// c
	}
}
```

【注意】

```shell
而jvm在给数值分配数据类型的时候会选取刚好能装下该数据大小精度的数据类型进行分配（99为byte/short）
在java中常见数据类型其范围从小到大（精度由高到低）：byte short char int long float double 
```
