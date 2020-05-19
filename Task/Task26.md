## 获取10个1~20之间的元素，要求不能重复

```java
public class Test {
	public static void main(String[] args) {
		HashSet<Integer> hashSet = new HashSet<Integer>();

		while (11 != hashSet.size()) {
			hashSet.add((int) (Math.random() * 20));
		}

		System.out.println(hashSet);	// [16, 1, 17, 2, 3, 4, 8, 9, 11, 12, 15]

	}
}
```

