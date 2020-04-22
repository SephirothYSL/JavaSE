## 完成对于循环点菜代码的方法封装

```java
import java.util.Scanner;

class Task {
	static int total = 0;
	
	public static void main(String[] args) {		
		
		System.out.println("-----欢迎来到Buffer's Food Store-----");
		showMenu();	
	}
	
	/**
	* 展示菜谱，然后跳到input方法
	*/
	public static void showMenu() {
		System.out.println("1 煎饼果子 2 芙蓉蛋卷 3 馍夹菜 4 麦多馅饼 5 臭豆腐 6 臊子面 7 笼香楼 8 烙馍卷菜 9 火锅 0 结账");
		input();
	}
	
	/**
	* 点菜：键盘录入并（带有合法性判断），如果用户输入了非法的数据，将跳回展示菜谱方法
	* 		如果正确录入，则跳到 showFood 方法
	*/
	public static void input() {
		Scanner scanner = new Scanner(System.in);
		
		System.out.println("请点菜（0~9）：");
		int num = scanner.nextInt();
		
		if (num < 0 || num > 9) {
			System.out.println("您输入了非法的数据，请重新输入：");
			showMenu();
		} 
		
		showFood(num);		
	}
	
	/**
	* 展示用户点的菜品，如果客人不选择结账就跳回showMenu方法展示菜品，
	* 如果客人结账，则跳到 pay 方法，pay方法执行完后终止
	*
	* @param num 传入用户输入的数字，int类型
	*/
	public static void showFood(int num) {
						
		switch (num) {
			case 1:
				System.out.println("菜品1 煎饼果子一份 6RMB");
				total += 6;
				break;
			case 2:
				System.out.println("菜品2 芙蓉蛋卷一份 6RMB");
				total += 6;
				break;
			case 3:
				System.out.println("菜品3 馍夹菜一份 5RMB");
				total += 5;
				break;
			case 4:
				System.out.println("菜品4 麦多馅饼一份 4RMB");
				total += 4;
				break;
			case 5:
				System.out.println("菜品5 臭豆腐一份 5RMB");
				total += 5;
				break;
			case 6:
				System.out.println("菜品6 臊子面一份 10RMB");
				total += 10;
				break;
			case 7:
				System.out.println("菜品7 笼香楼一份 100RMB");
				total += 100;
				break;
			case 8:
				System.out.println("菜品8 烙馍卷菜一份 80RMB");
				total += 80;
				break;
			case 9:
				System.out.println("菜品9 火锅一份 200RMB");
				total += 200;
				break;
			case 0:
				System.out.println("结账");
				pay(total);	
				return;
		}
		
		showMenu();						
	}
	
	/**
	* 结账
	*
	* @param total 总结 int类型
	*/
	public static void pay(int total) {
		System.out.println("您一共消费：" + total + "元");
	}
}
```

