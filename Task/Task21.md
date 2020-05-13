## 作业

需求

```shell
验证哥德巴赫猜想

输入一个大于6的偶数，请输出这个偶数能被分解为那两个质数的和

如：10=3+7
```

```java
public class Test {
	public static void main(String[] args) {
		get(100);
	}

	/**
	 * 验证哥德巴赫猜想
	 * 
	 * @param num 传入的数
	 */
	public static void get(int num) {
		// 合法性判断，必须是大于6的偶数
		if (num <= 6 || num % 2 != 0) {
			System.out.println("Input parameter is valied!");
			return;
		}

		for (int i = 2; i < num; i++) {
			if (isNum(i)) {
				if (isNum(num - i) && 0 != (num - i) % 2) {
					System.out.println("第一个数为：" + i + "第二个数为：" + (num - i));
					return;
				}
			}
		}
	}

	/**
	 * 判断是否为质数，
	 * 
	 * @param num 传入一个数
	 * @return 如果是返回true，否则返回false
	 */
	public static boolean isNum(int num) {
		for (int i = 2; i < num; i++) {
			if (0 == num % i) {
				return false;
			}

		}

		return true;
	}
}
```

结果

```shell
第一个数为：3第二个数为：97
```

