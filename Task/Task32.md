## 电影院卖票

> Ticket 类

```java
public class Ticket implements Runnable {
	// 票号
	private int num = 0;

	private static final int MAX_COUNT = 100;

	@Override
	public void run() {
		// 当前窗口卖的票数
		int count = 0;

		// 当票号小于100时卖票
		while (num < MAX_COUNT) {

			// synchronized 锁，锁对象为当前 Ticket 对象
			synchronized (this) {
				// 双重验证
				if (num < MAX_COUNT) {
					num++;
					// 打印出票信息
					String printInfor = Tools.printInfor(num);

					// 当前窗口卖的票自增
					++count;

					try {
						// 保存至文件
						Tools.save(printInfor);

						// 睡0.1秒
						Thread.sleep(100);
					} catch (IOException e1) {
						e1.printStackTrace();
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
				}
			}
		}

		// 打印当前窗口卖的总票数
		System.out.println(Thread.currentThread().getName() + "一共卖了：" + count + " 张票");
	}

}
```

> 工具类

```java
public class Tools {

	private static final Long CURRENT_TIME = System.currentTimeMillis();

	/**
	 * 将可变长字符串保存到文件中
	 * 
	 * @param sb 传入一个 StringBuilder 类型的参数
	 * @throws IOException
	 */
	public static void save(String str) throws IOException {

		BufferedOutputStream bos = new BufferedOutputStream(
				new FileOutputStream(new File("./src/task/Test.txt"), true));

		bos.write(new String(str).getBytes());
		bos.write('\n');
		bos.close();
	}

	/**
	 * 打印信息
	 * 
	 * @param num 传入票号
	 * @return 返回一个 StringBuilder 类型的参数
	 */
	public static String printInfor(int num) {

		String title = "欢迎光临直播间\n";

		StringBuilder sb = new StringBuilder(title);
		sb.append(getTicket(num));
		sb.append(getDate());
		sb.append(getSeat(num));
		sb.append("\r\n观影时间为 ： ");
		sb.append(getCalendar(CURRENT_TIME));
		sb.append("\r\n");

		System.out.println(sb);

		return sb.toString();
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
	 * 获取出票时间
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

	/**
	 * 获取观影日期
	 * @param time 当前时间，final修饰不可更改
	 * @return 返回一个字符串：包含年、月、日、时、分的日期
	 */
	private static String getCalendar(Long time) {

		Calendar cal = Calendar.getInstance();

		cal.setTimeInMillis(time);

		cal.add(Calendar.DAY_OF_MONTH, +3);

		Date date = cal.getTime();

		SimpleDateFormat dateFormat = new SimpleDateFormat("yyyy年MM月dd日 HH:mm");

		String s = dateFormat.format(date);

		return s;
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

