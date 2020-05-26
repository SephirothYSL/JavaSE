## 电影院卖票

> Ticket 类

```java
public class Ticket implements Runnable {
	// 票号
	private int num = 0;

	@Override
	public void run() {
		// 当票号小于100时卖票
		while (num < 100) {

			// synchronized 锁，锁对象为当前 Ticket 对象
			synchronized (this) {
				// 双重验证
				if (num < 100) {
					num++;
					// 打印出票信息
					StringBuilder printInfor = Tools.printInfor(num);

					try {
						// 保存至文件
						Tools.save(printInfor);
					} catch (IOException e1) {
						e1.printStackTrace();
					}

					try {
						// 睡0.1秒
						Thread.sleep(100);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
				}

			}

		}
	}

}
```

> 工具类

```java
public class Tools {

	/**
	 * 将可变长字符串保存到文件中
	 * @param sb 传入一个 StringBuilder 类型的参数
	 * @throws IOException
	 */
	public static void save(StringBuilder sb) throws IOException {

		BufferedOutputStream bos = new BufferedOutputStream(
				new FileOutputStream(new File("./src/task/Test.txt"), true));

		bos.write(new String(sb).getBytes());
		bos.write('\n');
		bos.close();
	}

	/**
	 * 打印信息，包括出票窗口、票号、时间、座位号和提示语
	 * @param num 传入票号
	 * @return 返回一个 StringBuilder 类型的参数
	 */
	public static StringBuilder printInfor(int num) {

		String str = "欢迎光临直播间\n";

		StringBuilder sb = new StringBuilder(str + getTicket(num) + getDate() + getSeat(num) + "\n");

		System.out.println(sb);

		return sb;
	}

	/**
	 * 获取出票窗口及票号
	 * 
	 * @param num 传入票号
	 * @return 返回一个字符串
	 */
	private static String getTicket(int num) {
		return "出票窗口为：" + Thread.currentThread().getName() + "\t票号为：" + num + "\n";
	}

	/**
	 * 获取时间
	 * 
	 * @return 返回一个字符串
	 */
	private static String getDate() {
		Date date = new Date();

		SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy年MM月dd日 HH:mm:ss");

		String s = dateFormat.format(date);

		return "出票日期为：" + s;
	}

	/**
	 * 获取座位
	 * 
	 * @param num 传入票号
	 * @return 返回一个字符串
	 */
	private static String getSeat(int num) {
		int line = num / 21 + 1;

		int list = num % 20;

		if (0 == list) {
			list = 20;
		}

		return "\n座位为： 第 " + line + " 排  " + "第 " + list + " 列";
	}
}
```

> 测试类

```java
public class Test {
	public static void main(String[] args) {
		Ticket ticket = new Ticket();
		
		Thread th1 = new Thread(ticket);
		Thread th2 = new Thread(ticket);
		Thread th3 = new Thread(ticket);		
		
		th1.setName("Nico's 窗口");
		th2.setName("Balance's 窗口");
		th3.setName("Amy's 窗口");
		
		th1.start();
		th2.start();
		th3.start();
	}
}
```

