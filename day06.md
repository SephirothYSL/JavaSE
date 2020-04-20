## 1. for 循环

```shell
格式：
	for (循环条件初始化条件;循环条件判断;循环条件变更) {
		代码块
	}
	
执行流程
	1、首先进行循环条件初始化
	2、循环条件判断，为真就执行代码块，为假则退出循环
	3、循环条件变更
	4、回到2
```

```java
class TestFor3 {
	public static void main(String[] args) {
		for (char ch = 'A' ; ch <= 'Z' ; ch++) {
			System.out.print(ch);
		}
	}
}
```

【注意】for 死循环

```java
for (;;) {
    
}
```

## 2. 流程控制关键字

### 2.1 break

用于switch分支结构和循环结构，跳出当前循环（就近原则）

```java
class TestBreak2 {
	public static void main(String[] args) {
		for (int i = 1 ; i <= 100 ; i++) {
			
			if (50 == i) {
				System.out.println("执行了break");
				break;
			}
			
			System.out.println(i);
		}
	}
}
```

### 2.2 continue

用于跳过当次循环，直接执行下次循环

```java
class TestContinue2 {
	public static void main(String[] args) {
		for (int i = 1 ; i <= 10 ; i++) {
			
			if (i == 5) {
				System.out.print("continue±»Ö´ĞĞ");
				continue;
			}
			
			System.out.print(i + " ");
		}
	}
}
```

【注意】continue 在 while 循环、do while循环中使用时，循环条件变更需要在 continue 前执行，否则可能会造成死循环

