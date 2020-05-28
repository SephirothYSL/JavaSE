## 1. 多线程

### 1.1 线程控制

#### 1.1.1 方法

```java
线程休眠(运行-->阻塞)：
	public static void sleep(long millis)

线程加入(运行-->阻塞)：
	public final void join()
    
线程礼让(运行-->就绪)：    
	public static void yield()
```

#### 1.1.2 sleep()

在指定的毫秒数内让当前正在执行的线程休眠（暂停执行）

```java
public class Test {
	public static void main(String[] args) {
		Thread th1 = new Thread(new Runnable() {
			int count = 0;

			@Override
			public void run() {
				while (count < 10) {
					System.out.print(count);	// 0123456789
					count++;
					try {
						Thread.sleep(500);
					} catch (InterruptedException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}
				}
			}
		});

		th1.start();
		System.out.println("主线程");	// 主线程
	}
}
```

#### 1.1.3 join()

> 在当前线程中，执行另一个线程的join方法，然后当前线程就会阻塞，等待插入的线程执行完毕之后，才会从阻塞状态进入到就绪状态，重新参与CPU抢夺！

> 就绪状态的线程的抢占发生在任意时期

```java
public class TestJoin {
	public static void main(String[] args) {
		Thread thread1 = new Thread(new Runnable() {
			int count = 0;

			@Override
			public void run() {
				while (count < 10) {
					System.out.println("插入线程 ：" + count);
					count++;
					try {
						Thread.sleep(500);
					} catch (InterruptedException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}
				}
			}
		});

		Thread thread2 = new Thread(new Runnable() {
			int count = 0;

			@Override
			public void run() {

				while (count < 5) {
					System.out.println("Thread2： " + count);
					count++;

					try {
						Thread.sleep(500);
					} catch (InterruptedException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}

					if (2 == count) {
						try {
							thread1.join();
						} catch (InterruptedException e) {
							// TODO Auto-generated catch block
							e.printStackTrace();
						}
					}
				}
			}
		});

		thread2.start();
		thread1.start();
		System.out.println("主线程");
	}
}
```

结果

```java
主线程
插入线程 ：0
Thread2： 0
插入线程 ：1
Thread2： 1
插入线程 ：2
插入线程 ：3
插入线程 ：4
插入线程 ：5
插入线程 ：6
插入线程 ：7
插入线程 ：8
插入线程 ：9
Thread2： 2
Thread2： 3
Thread2： 4
```

#### 1.1.4 yidle()

> 可以让当前正在运行的线程暂停，，并执行其他线程。但是不会让当前线程阻塞，而且让当前的线程进入到就绪状态。

> 实际上：线程执行yield之后，只有比当前线程的优先级更高或者相同的才有机会参与抢夺CPU,而且当前线程也会参与抢夺

```java
public class TestYield {
	public static void main(String[] args) {
		Thread thread1 = new Thread(new Runnable() {
			int count = 0;

			@Override
			public void run() {
				while (count < 5) {
					System.out.println("线程一: " + (++count));

					try {
						Thread.sleep(1000);
					} catch (InterruptedException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}

					if (3 == count) {
						System.out.println("线程一礼让~~~");
						Thread.yield();
					}
				}
			}
		});

		Thread thread2 = new Thread(new Runnable() {
			int count = 0;

			@Override
			public void run() {
				while (count < 10) {
					System.out.println("线程二: " + (++count));

					try {
						Thread.sleep(1000);
					} catch (InterruptedException e) {
						// TODO Auto-generated catch block
						e.printStackTrace();
					}
				}
			}
		});

		thread1.start();
		thread2.start();

		System.out.println("主线程");
	}
}
```

结果

```java
主线程
线程二: 1
线程一: 1
线程一: 2
线程二: 2
线程二: 3
线程一: 3
线程一礼让~~~
线程一: 4
线程二: 4
线程二: 5
线程一: 5
线程二: 6
线程二: 7
线程二: 8
线程二: 9
线程二: 10
```

### 1.2 线程相关方法

```shell
static Thread currentThread();
	返回对当前正在执行的线程对象的引用

long getId();
	返回该线程的标识符。线程 ID 是一个正的 long 数，在创建该线程时生成。线程 ID 是唯一的，并终生不变。线程终止时，该线程 ID 可以被重新使用 

String getName();
	返回该线程的名称
	
Thread.State getState();
	返回该线程的状态
	
int getPriority();
	返回线程的优先级。
	
boolean isAlive();
	测试线程是否处于活动状态
	
boolean isDaemon();
	测试该线程是否为守护线程
	
void setDaemon(boolean on);
	将该线程标记为守护线程或用户线程，该方法必须在启动线程前调用
	
void setName(String name);
	改变线程名称，使之与参数 name 相同
	
void setPriority(int newPriority);
	更改线程的优先级

boolean isInterrupted();
	测试线程是否已经中断
	
void interrupt();
	中断线程
	
static boolean interrupted();
	测试当前线程是否已经中断。线程的中断状态由该方法清除。
```

```java
public class Test {
	public static void main(String[] args) {
		Thread thread = new Thread(new Runnable() {
			int count = 0;

			@Override
			public void run() {

				System.out.println("当前线程的状态为：" + Thread.currentThread().getState());

				while (count < 10) {
					System.out.println(++count);

					if (5 == count) {
						Thread.currentThread();
						boolean interrupted1 = Thread.interrupted();
						System.out.println("子线程是否中断：" + interrupted1); // 子线程是否中断：true

						Thread.currentThread();
						boolean interrupted2 = Thread.interrupted();
						System.out.println("子线程是否中断：" + interrupted2); // 子线程是否中断：false
					}
				}
			}
		});

		thread.setName("子线程");
		System.out.println("线程的名称为：" + thread.getName()); // 线程的名称为：子线程

		thread.setPriority(8);
		System.out.println("优先级为：" + thread.getPriority()); // 优先级为：8

		System.out.println("线程的Id为：" + thread.getId()); // 线程的Id为：11

		System.out.println("当前线程是否处于活动状态：" + thread.isAlive()); // 当前线程是否处于活动状态：false

		thread.setDaemon(true);
		System.out.println("判断当前线程是否是守护线程：" + thread.isDaemon()); // 判断当前线程是否是守护线程：true

		thread.start();

		thread.interrupt();
		System.out.println("当前线程是否中断：" + thread.isInterrupted()); // 当前线程是否中断：true

		System.out.println("当前线程是否处于活动状态：" + thread.isAlive()); // 当前线程是否处于活动状态：true
	}
}
```

### 1.3 线程安全

#### 1.3.1 出现的原因

> 线程的抢占发生在任意时期
>
> 当多个线程操作同一个数据源的时候吗，并且都涉及到了修改，那么就有可能发生数据重复的问题，这种现象就成为线程安全的问题。

#### 1.3.2 导致线程安全问题的因素

> 1、多个线程
>
> 2、同时操作临界资源 共享资源

#### 1.3.3 如何解决线程安全的问题

##### 1.3.3.1 Synchronized

###### 1.3.3.1.1 同步代码块

```java
格式：
	synchronized (对象) {
		需要被同步的代码;
	}
```

【注意】同步代码块的锁对象可以是任意对象

```java
public class Test {
	public static void main(String[] args) {
		Runnable runnable = new Runnable() {

			int count = 0;

			@Override
			public void run() {
				while (count < 10) {
					synchronized (this) {
						if (count < 10) {
							System.out.println(Thread.currentThread().getName() + " : " + (++count));
						}
					}
					
					try {
						Thread.sleep(500);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
				}
			}
		};

		Thread thread1 = new Thread(runnable);
		Thread thread2 = new Thread(runnable);

		thread1.start();
		thread2.start();
	}
}
```

###### 1.3.3.1.2 同步方法

```java
格式：
    访问修饰符 synchronized 返回值 方法名(参数列表){
    	需要被同步的代码;
	}
```

【注意】同步方法的锁对象是 this

```java
public class Test2 {
	public static void main(String[] args) {
		Runnable runnable = new Runnable() {
			int count = 0;

			public synchronized void print() {

				if (count < 10) {
					System.out.println(Thread.currentThread().getName() + " : " + (++count));
				}

				try {
					Thread.sleep(100);
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			}

			@Override
			public void run() {
				while (count < 10) {
					print();
				}
			}
		};

		Thread thread1 = new Thread(runnable);
		Thread thread2 = new Thread(runnable);

		thread1.setName("子线程--1");
		thread2.setName("子线程--2");

		thread1.start();
		thread2.start();
	}
}
```

###### 1.3.3.1.3 静态同步方法

```java
格式：
    访问修饰符 static synchronized 返回值 方法名(参数列表){
    	需要被同步的代码;
	}
```

【注意】同步静态方法的锁对象是当前类的字节码文件对象

```java
public class StaticMehtod implements Runnable {

	private static int count = 0;

	public static synchronized void print() {

		if (count < 300) {
			System.out.println(Thread.currentThread().getName() + " : " + (++count));
		}

	}

	@Override
	public void run() {
		while (count < 300) {
			StaticMehtod.print();
		}
	}

}
```

```java
public class Test3 {
	public static void main(String[] args) {
		StaticMehtod staticMehtod = new StaticMehtod();
		
		Thread th1 = new Thread(staticMehtod);
		Thread th2 = new Thread(staticMehtod);
		Thread th3 = new Thread(staticMehtod);
	
		th1.start();
		th2.start();
		th3.start();
	}
}
```

###### 注意

>1、锁修饰的内容只能是引用类型对象，一般都是使用this
>
>2、锁的位置很关键，一般都是锁定是引起线程安全的部分
>
>3、锁会自动释放，内部代码执行完毕之后
>
>4、多个线程必须使用同一把锁

###### 1.3.3.1.4 Synchronized 用法的区别

>1、同步代码块 锁的粒度可以很小
>
>锁的粒度来讲：同步代码块 <  同步方法 <  同步静态方法
>
>粒度 也就是锁的范围  粒度越小越好
>
>2、同步代码块 锁的对象可以是：引用类型属性、this、字节码对象
>
>同步方法 锁的对象只能是当前类的实例 this
>
>3、同步静态方法 锁的对象是 当前类的字节码对象

##### 1.3.3.2 Lock

Lock锁的性能要比 synchronized 高，但是lock要求必须手动释放锁

```java
格式：
	private final ReentrantLock lock = new ReentrantLock();

	public void method() { 
		lock.lock();  // block until condition holds
     	try {
       		// ... method body
     	} finally {
       		lock.unlock()
     	}
   	} 
```

```java
public class Test {
	public static void main(String[] args) {
		Runnable runnable = new Runnable() {
			int count = 0;

			private Lock lock = new ReentrantLock();

			@Override
			public void run() {
				while (count < 200) {
					try {
						lock.lock();
						
						if (count < 200) {
							System.out.println(Thread.currentThread().getName() + " : " + (++count));
							Thread.sleep(50);
						}
					} catch (InterruptedException e) {
						e.printStackTrace();
					} finally {
						lock.unlock();
					}
				}
			}
		};

		Thread th1 = new Thread(runnable);
		Thread th2 = new Thread(runnable);
		Thread th3 = new Thread(runnable);

		th1.start();
		th2.start();
		th3.start();
	}
}
```

#### 1.3.4 死锁

两个或两个以上的线程在争夺资源的过程中，发生的一种相互等待的现象

##### 1.3.4.1 产生的原因

> 1、2个以上的线程
>
> 2、2个以上的锁
>
> 3、同步代码块嵌套同步代码块

自定义锁对象

```java
class MyLock {
	// 第一把锁
	public static Object LOCK1 = new Object();
	// 第二把锁
	public static Object LOCK2 = new Object();
}
```

死锁类

```java
public class DeadLock implements Runnable {

	boolean flag;

	public DeadLock(boolean flag) {
		this.flag = flag;

	}

	@Override
	public void run() {
		if (flag) {
			synchronized (MyLock.LOCK1) {
				System.out.println("if LOCK1");
				synchronized (MyLock.LOCK2) {
					System.out.println("if LOCK2");
				}
			}
		} else {
			synchronized (MyLock.LOCK2) {
				System.out.println("else LOCK2");
				synchronized (MyLock.LOCK1) {
					System.out.println("else LOCK1");
				}
			}
		}

	};
}
```

测试类

```java
public class Test {
	public static void main(String[] args) {
		Thread th1 = new Thread(new DeadLock(false));
		Thread th2 = new Thread(new DeadLock(true));

		th1.start();
		th2.start();
	}
}
```

结果

```java
else LOCK2
if LOCK1
```

