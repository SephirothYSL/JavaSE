## 1. 多线程

### 1.1 进程和线程

#### 1.1.1 进程

>概述：
>
>​		正在运行的程序，是系统进行资源分配和调用的独立单位
>
>​		每一个进程都有它自己的内存空间和系统资源
>
>
>
>特点：
>
>​		1、独立性
>
>​		2、动态性
>
>​		3、并发性

#### 1.1.2 线程

>概述：		
>
>​		是进程中的单个顺序控制流，是一条执行路径
>
>​		一个进程如果只有一条执行路径，则称为单线程程序
>
>​		一个进程如果有多条执行路径，则称为多线程程序
>
>
>
>特点：
>
>​		1、线程是CPU的最小调度单位，CPU可以很快的在多个线程间实现切换。
>
>​		2、运行时的线程，随时都可以被CPU给挂起。
>
>​		3、线程的抢占发生在任意时期

#### 1.1.3 进程与线程的区别

>1、一个程序，可以有多个进程
>
>2、一个进程可以有多个线程。但是必须要有一个主线程
>
>3、进程间不能共享资源，但是线程间可以共享资源。

### 1.2 线程的使用

#### 1.2.1 创建及启动

```java
创建线程：
    Thread thread = new Thread();

启动线程：
    thread.start();
```

#### 1.2.2 实现 Runnable 接口

```java
public static void main(String[] args) {
		Runnable runnable = new Runnable() {
			
			@Override
			public void run() {
				System.out.println("Test Thread~~~");	// Test Thread~~~	
			}
		};
		
		Thread thread = new Thread(runnable);
		thread.start();
	}
```

#### 1.2.3 继承 Thread 类并重写 run 方法

```java
public class Test2 extends Thread {
	@Override
	public void run() {
		System.out.println("Test Thread");	// Test Thread
	}

	public static void main(String[] args) {
		Test2 test2 = new Test2();
		
		test2.start();
	}
}
```

#### 1.2.4 实现 Callable 接口

>可以有返回值
>
>可以抛出异常

```java
public class Test3 {
	public static void main(String[] args) throws InterruptedException, ExecutionException {
		Callable<Integer> cal = new Callable<Integer>() {
			int count = 0;

			@Override
			public Integer call() throws Exception {
				count++;

				System.out.println(" Test :" + count);	//  Test :1

				return count;
			}
		};

		FutureTask<Integer> future = new FutureTask<Integer>(cal);

		Thread thread = new Thread(future);

		thread.start();

		System.out.println("返回值为：" + future.get());	// 返回值为：1
	}
}
```

#### 1.2.5 三种创建方式的区别

> 继承 Thread 类：
>
> ​		编写简单、单继承，所以这种类无法再继承其他类、无法实现多个线程的资源共享、扩展性无

> 实现 Runnable 接口：
>
> ​		编写复杂一点，接口可以多实现，可以实现多个线程的资源共享  推荐使用

> 实现 Callable 接口：
>
> ​		编码复杂，可以实现线程执行完之后进行值的返回

> 开发中，需要线程返回值，就使用 Callable，不需要返回值的就可以 Runnable 

### 1.3 线程调度

#### 1.3.1 分时调度模型

所有线程轮流使用 CPU 的使用权，平均分配每个线程占用 CPU 的时间片

#### 1.3.2 抢占式调度模型

优先让优先级高的线程使用 CPU，如果线程的优先级相同，那么会随机选择一个，优先级高的线程获取的 CPU 时间片相对多一些

>Java 采用的是抢占式调度模型

#### 1.3.3 优先级

线程的优先级就是线程获得CPU的概率，优先级越高，获取CPU的概率越大

> Java中共有10种优先级，从小到大，1-10之间。10是优先级最高，默认的优先级是5

#### 1.3.4 优先级方法

```java
获取当前线程的优先级：
	public final int getPriority()
    
设置当前线程的优先级：
	public final void setPriority(int newPriority)
```

```java
public class Test {
	public static void main(String[] args) {
		Runnable runnable = new Runnable() {
			@Override
			public void run() {
				System.out.println(Thread.currentThread().getName());
			}
		};

		Thread th1 = new Thread(runnable);

		Thread th2 = new Thread(runnable);

		th1.setPriority(6);
		th2.setPriority(9);

		th1.start();	// Thread-0
		th2.start();	// Thread-1

		System.out.println("th1的优先级为： " + th1.getPriority());	// th1的优先级为： 6
		System.out.println("th2的优先级为： " + th2.getPriority());	// th2的优先级为： 9
	}
}
```

【注意】设置优先级需要在 start 方法之前设置

### 1.4 线程的生命周期

线程有五大状态，分别是新建、就绪、运行、阻塞、销毁

新建：

> 当我们实例化线程对象的时候，线程就是新建状态

就绪：

> 当我们调用线程的start方法之后，线程就会进入就绪状态
>
> 处于该状态的线程，随时都可以获取CPU调度

运行：

> 线程获取CPU的调度之后，线程抢到了时间片，可以用来运行自己任务

阻塞：

> 当线程因为资源竞争，或主动方法调用，让线程进入到阻塞。
>
> 常见：sleep、wait、join等等

销毁：

> 当线程的run方法执行结束之后，就会进入到销毁状态

【注意】程序的结束就是指的内部多的所有线程全部进入到了销毁状态

![](https://ae01.alicdn.com/kf/H76e24cca11a7448baf5c4cdcf5d93588Y.jpg)

### 1.5 守护线程

线程分为：用户线程和守护线程，Java中默认创建的线程就是用户线程

#### 1.5.1 特点

当守护的用户线程销毁的时候，守护线程也会跟着消亡。无论守护线程是否执行结束都会随着用户线程一起销毁

#### 1.5.2 方法

```java
当传入 true 时，将当前线程设置为守护线程：
	public final void setDaemon(boolean on)
```

```java
public class Test {
	public static void main(String[] args) {
		Thread thread1 = new Thread(new Runnable() {

			@Override
			public void run() {
				System.out.println("守护线程");	// 守护线程
			}
		});

		thread1.setDaemon(true);

		Thread thread2 = new Thread(new Runnable() {

			@Override
			public void run() {
				System.out.println("子线程");	// 子线程
			}
		});
		
		thread1.start();
		thread2.start();
		System.out.println("主线程");	// 主线程
	}
}
```

【注意】主线程和 GC（**garbage collection **垃圾回收机制） 线程就是一对用户线程与守护线程，GC 守护主线程
