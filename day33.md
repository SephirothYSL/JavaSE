## 1. 多线程

### 1.1 线程通信

线程通信：有一个缓冲区的仓库，生产者线程，不断往仓库存储内容，消费者线程不断从仓库中获取内容。为了解决生产者和消费者的动态调节的问题，可以使用线程通信机制，来保护生产者和消费中的同步

```java
void wait();
	在其他线程调用此对象的 notify() 方法或 notifyAll() 方法前，导致当前线程等待
        线程 状态从 运行 变更为 阻塞

void notify();
	唤醒在此对象监视器上等待的单个线程
        只能唤醒因为wait阻塞的线程。线程的状态从 阻塞 变更为 就绪
        
void notifyAll();
	唤醒在此对象监视器上等待的所有线程
        只能唤醒因为wait阻塞的线程。线程的状态从 阻塞 变更为 就绪
```

> **wait、notify、notifyall 都是Object的方法、都需要使用在同步方法中**

```java
class Restaurant {
	int count = 0;

	public synchronized void make() {
		if (count < 10) {
			System.out.println(Thread.currentThread().getName() + "做了一道菜，当前还有" + (count + 1) + "道菜");
			count++;
			notifyAll();
		} else {
			try {
				System.out.println("做完了赶紧卖");
				wait();
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}

	public synchronized void sell() {
		if (count > 0) {
			System.out.println(Thread.currentThread().getName() + "卖了一道菜，当前还有" + (count - 1) + "道菜");
			count--;
			notify();
		} else {
			try {
				System.out.println("卖完了赶紧做");
				wait();
			} catch (InterruptedException e) {
				e.printStackTrace();
			}

		}

	}
}

public class TestRestaurant {
	public static void main(String[] args) {
		Restaurant res = new Restaurant();

		Thread th1 = new Thread(new Runnable() {

			@Override
			public void run() {
				while (true) {
					res.make();
					Thread.yield();
				}
			}
		});

		Thread th2 = new Thread(new Runnable() {

			@Override
			public void run() {
				while (true) {
					res.make();
					Thread.yield();
				}
			}
		});

		Thread th3 = new Thread(new Runnable() {

			@Override
			public void run() {
				while (true) {
					res.sell();
					Thread.yield();
				}
			}
		});
		
		Thread th4 = new Thread(new Runnable() {

			@Override
			public void run() {
				while (true) {
					res.sell();
					Thread.yield();
				}
			}
		});

		th1.setName("做饭小伙");
		th2.setName("做饭姑娘");
		th3.setName("卖饭小伙");
		th4.setName("卖饭姑娘");

		th1.start();
		th2.start();
		th3.start();
		th4.start();
	}
}
```

### 1.2 线程池

线程池：有效并充分利用线程，合理分配资源

>程序启动一个新线程成本是比较高的，因为它涉及到要与操作系统进行交互。而使用线程池可以很好的提高性能，尤其是当程序中要创建大量生存期很短的线程时，更应该考虑使用线程池

>线程池里的每一个线程代码结束后，并不会死亡，而是再次回到线程池中成为空闲状态，等待下一个对象来使用

#### 1.2.1 线程池的优点

> 1、控制线程数量
>
> 2、避免了频繁的创建和销毁线程
>
> 3、对线程进行统一的管理

#### 1.2.2 Executors

Executors Java封装的创建线程池的工具类  现在已经被淘汰 因为很容易引起 OOM 异常

```java
newFixedThreadPool(int nThreads);  
    创建一个可重用的，具有固定线程数的线程池

newSingleThreadExecutor();
	创建一个只有单线程的线程池，相当于上个方法的参数是1 

newCachedThreadPool();
	创建一个没有上限的线程池

newScheduledThreadPool();
    创建一个固定线程数量的线程池，这个线程池具备延迟、定时重复执行

newWorkStealingPool();
    创建一个抢占式
```

#### 1.2.3 ThreadPoolExecutor 类

目前推荐手动创建线程池

```java
ThreadPoolExecutor(int corePoolSize,  int maximumPoolSize, long keepAliveTime, TimeUnit unit, BlockingQueue<Runnable> workQueue)
    用给定的初始参数和默认的线程工厂及被拒绝的执行处理程序创建新的 ThreadPoolExecutor
    	corePoolSize - 设置最小线程数量。池中所保存的线程数，包括空闲线程。
		maximumPoolSize - 池中允许的最大线程数。
		keepAliveTime - 当线程数大于核心时，此为终止前多余的空闲线程等待新任务的最长时间。
		unit - keepAliveTime 参数的时间单位。
		workQueue - 执行前用于保持任务的队列。此队列仅保持由 execute 方法提交的 Runnable 任务
```

运行线程池

```java
execute(Runnable command)；
    在将来某个时间执行给定任务
```

```java
public class TestThreadPool {
	public static void main(String[] args) {
		ThreadPoolExecutor tpe = new ThreadPoolExecutor(3, 5, 1000, TimeUnit.SECONDS,
				new ArrayBlockingQueue<Runnable>(10));

		tpe.execute(new Runnable() {
			int count = 0;

			@Override
			public void run() {
				while (count < 5) {
					try {
						System.out.println("111");
						count++;
						Thread.sleep(1000);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
				}
			}
		});

		tpe.execute(new Runnable() {
			int count = 0;

			@Override
			public void run() {
				while (count < 5) {
					try {
						System.out.println("222");
						count++;
						Thread.sleep(1000);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
				}
			}
		});

		tpe.execute(new Runnable() {
			int count = 0;

			@Override
			public void run() {
				while (count < 5) {
					try {
						System.out.println("333");
						count++;
						Thread.sleep(1000);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
				}
			}
		});

		tpe.shutdown();
	}
}
```

## 2. 网络基础

### 2.1 网络

计算机网络：就是把分布在不同区域的计算机，与专门的外部设备通信互联成为一个规模巨大，而且功能强大，网络系统，从而达到计算机之间可用相互通信，交换资源、共享信息等。

> 网络的分类：根据网络的范围可用分为：广域网、域域网、局域网

> 网络编程就是用 Java 语言实现计算机间数据的信息传递和资源共享

### 2.2 网络模型

> OSI：Open System Interconnect 开放式系统互联. 参考 ISO(国际标准化组织)制定一种通用 计算机通信标准体系。七层模型。

> TCP/IP的四层模型：应用层、传输层、网络层、数据链路层
>
> 应用层(应用层、表示层、会话层)：程序实现的细节 
>
> 传输层：实现传输的通信，提供端对端的通信，只支持2种协议：TCP、UDP
>
> 数据链路层(数据链路层、物理层)：驱动程序、网络接口卡等 硬件

### 2.3 IP

> IP：IP地址是指互联网中的地址：Internet Protocol Address.
>
> 是互联网设备与互联网之间的唯一标记。同一个网段中，IP地址唯一。
>
> IP地址的组成：是数字类型，是一个32位的整数。通常是为4个8进制的数字，每8位之间使用.隔开。
>
> 但是为了方便查看和传输IP地址，一般都是讲进制转换十进制。8个二进制转换为十进制：0-255之间。
>
> eg:127.0.0.1  192.168.1.1 
>
> IP协议分为：IP4、IP6
>
> IP地址分类：广域网

| 类型     | 范围                       | 作用           |
| -------- | -------------------------- | -------------- |
| A类地址  | 1.0.0.1~126.255.255.254    | 保留给政府机构 |
| B类地址  | 128.0.0.1~ 191.255.255.254 | 分配大中型企业 |
| C类地址  | 192.0.0.1~ 223.255.255.254 | 任何人         |
| D类地址  | 224.0.0.1~239.255.255.254  | 组播地址       |
| E类地址  | 240.0.0.1~255.255.255.254  | 实验地址       |
| 回环地址 | 127.0.0.1                  | 本机           |

### 2.4 端口

端口是应用程序的标识

> IP地址可以定位计算机(手机、有网络的设备)，那么端口就是定位具体的软件的

#### 2.4.1 端口号

端口号用来唯一标记通信实体上运行的程序。同一个机器上，一个端口号只能对应一个运行程序。数据的发送和接收都需要通过端口出入计算机。

##### 2.4.1.1 范围：

0-65535

##### 2.4.1.2 分类：

> 公共端口：0-1023  国际上被认证的端口号  
>
> ​		比如：http： 协议	80	https：	443	dns：	53
>
> 注册端口：1024~49151 这块端口我们可以使用，但是个人建议使用10000以后的
>
> 动态、私有端口：49152~65535 

##### 2.4.1.3 常用软件对应的端口号：

```shell
Tomcat	8080

Mysql	3306

Oracle	1521

ftp		21

SSH		22

Redis	6379
```

### 2.5 Java的IP类

Java 提供了操作 IP 地址的类，InetAddress

```java
InetAddress getByAddress(byte[] addr);
	在给定原始 IP 地址的情况下，返回 InetAddress 对象

String getHostAddress();
	返回 IP 地址字符串（以文本表现形式）。 

String getHostName();
	获取此 IP 地址的主机名
        
InetAddress[] getAllByName(String host);
	在给定主机名的情况下，根据系统上配置的名称服务返回其 IP 地址所组成的数组        
```

```java
public class Test {
	public static void main(String[] args) throws UnknownHostException {
		InetAddress localHost = InetAddress.getLocalHost();

		System.out.println(localHost);	// PC-Buffer/192.168.2.100

		System.out.println(localHost.getHostAddress());	// 192.168.2.100

		System.out.println(localHost.getHostName());	// PC-Buffer

		InetAddress[] allByName = InetAddress.getAllByName("www.baidu.com");

		for (InetAddress inetAddress : allByName) {
			System.out.println(inetAddress);
		}
	}
}
```
