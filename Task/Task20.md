# 常量接口

灯状态接口：

定义了红黄绿三种颜色的灯分别用1、2、3来表示

```java
public interface LightStatus {
	// 1 --> 红灯
	public static final int RED = 1;
	// 2 --> 黄灯
	public static final int YELLOW = 2;
	// 3 --> 绿灯
	public static final int GREEN = 3;
}
```

测试类

```java
public class TestLights {
	public static void main(String[] args) {
        // 定义当前灯的状态
		int currentLightState = 3;

        /*
         * 当前灯的状态为红灯时，跳转到绿灯
         * 当前灯的状态为绿灯时，跳转到黄灯
         * 当前灯的状态为黄灯时，跳转到红灯
         */
		if (currentLightState == LightStatus.RED) {
			currentLightState = LightStatus.GREEN;
		} else if (currentLightState == LightStatus.GREEN) {
			currentLightState = LightStatus.YELLOW;
		} else { 
			currentLightState = LightStatus.RED;
		}

		System.out.println(currentLightState); // 2
	}
}
```

常量接口的写法方便，代码简洁可读性高，生成的 .class 文件小，没有构造方法和其他类似重载和重写的特性，因此比较高效；但是需要注意常量接口可以被继承
