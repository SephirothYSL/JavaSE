## 第一题

> 龟兔赛跑
>
> 乌龟和兔子进行1000米赛跑。兔子前进5米，乌龟前进1米。但是兔子每隔20米，就需要休息0.5秒；乌龟每隔100米，就需要休息0.5秒。请用多线程实现，并得出谁赢了！

兔子

```java
public class Rabbit implements Runnable {
	long startTime = System.currentTimeMillis();

	int count = 0;
    
	@Override
	public void run() {
		while (count != 1000) {
			count += 5;

			if (0 == count % 20) {
				try {
					Thread.sleep(500);
					// System.out.println("兔子休息0.5秒");
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			}
		}

		long endTime = System.currentTimeMillis();

		System.out.println("兔子跑到终点，用时 : " + (endTime - startTime));
	}
}
```

乌龟

```java
public class Tank implements Runnable{
	long startTime = System.currentTimeMillis();
	
	int count = 0;

	@Override
	public void run() {
		while (count != 1000) {
			count += 1;

			if (0 == count % 100) {
				try {
					Thread.sleep(500);
					// System.out.println("乌龟休息0.5秒");
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			}
		}

		long endTime = System.currentTimeMillis();

		System.out.println("乌龟跑到终点，用时 : " + (endTime - startTime));
	}
}
```

测试

```java
public class Task {
	public static void main(String[] args) {
		Thread rabbit = new Thread(new Rabbit());

		Thread tank = new Thread(new Tank());

		rabbit.start();

		tank.start();
	}
}
```

结果

```java
乌龟跑到终点，用时 : 5004
兔子跑到终点，用时 : 25022
```

## 第二题

>计算100以为的质数

```java
public class Task2 {
	public static void main(String[] args) {

		Thread thread1 = new Thread(new Runnable() {

			@Override
			public void run() {
				getNums(1, 50);
			}
		});

		Thread thread2 = new Thread(new Runnable() {

			@Override
			public void run() {
				getNums(51, 100);
			}
		});

		thread1.start();
		thread2.start();
	}

	/**
	 * 获取指定范围内的质数
	 * @param start 开始范围
	 * @param end 结束范围
	 */
	public static void getNums(int start, int end) {

		if (start <= 2 && 2 < end) {
			System.out.println(2);
		}

		for (int i = start; i <= end; i++) {
			for (int j = 2; j < i; j++) {
				if (i % j == 0) {
					break;
				}

				if (j == i - 1) {
					System.out.println(i);
				}
			}
		}
	}
}
```

## 第三题

>计算200-300之间可被7整除的数字

```java
public class Task3 {
	public static void main(String[] args) {
		Thread thread1 = new Thread(new Runnable() {

			@Override
			public void run() {
				getNums(200, 250);
				try {
					Thread.sleep(2000);
				} catch (InterruptedException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
		});

		Thread thread2 = new Thread(new Runnable() {

			@Override
			public void run() {
				getNums(250, 300);
				try {
					Thread.sleep(2000);
				} catch (InterruptedException e) {
					// TODO Auto-generated catch block
					e.printStackTrace();
				}
			}
		});

		thread1.setPriority(6);
		thread2.setPriority(9);

		thread1.start();
		thread2.start();

	}

	public static void getNums(int start, int end) {
		for (int i = start; i <= end; i++) {
			if (0 == i % 7) {
				System.out.println(i);
			}
		}
	}
}
```

