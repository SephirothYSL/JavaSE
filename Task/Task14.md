## 类与类之间的调用

引擎类：

```java
public class Engine {
    // 成员方法 Field
	private String type;
	private int displacement;

    // 无参构造 Constructor
	public Engine() {
		super();
	}

    // 两参构造 Constructor
	public Engine(String type, int displacement) {
		super();
		this.type = type;
		this.displacement = displacement;
	}

	public String getType() {
		return type;
	}

	public void setType(String type) {
		this.type = type;
	}

	public int getDisplacement() {
		return displacement;
	}

	public void setDisplacement(int displacement) {
		System.out.println("调整引擎排量中~~~");
		this.displacement = displacement;
	}
}
```

轮胎类：

```java
public class Tyre {
    // 成员变量 Field
	private String type;
	private float size;

    // 无参构造 Constructor
	public Tyre() {
		super();
	}

    // 两参构造 Constructor
	public Tyre(String type, float size) {
		super();
		this.type = type;
		this.size = size;
	}

	public String getType() {
		return type;
	}

	public void setType(String type) {
		this.type = type;
	}

	public float getSize() {
		return size;
	}

	public void setSize(float size) {		
		this.size = size;
	}
}
```

汽车类：

```java
public class Car {
    // 成员变量 Field
	private Engine engine;
	private Tyre tyre;

    // 无参构造 Constructor
	public Car() {
		super();
	}

    // 两参构造 Constructor
	public Car(Engine engine, Tyre tyre) {
		super();
		this.engine = engine;
		this.tyre = tyre;
	}

    /*
     * 展示引擎和轮胎的成员变量方法
     */
	public void show() {
		System.out.println("引擎种类：" + engine.getType() + " 引擎排量：" + engine.getDisplacement());
		System.out.println("轮胎种类：" + tyre.getType() + " 轮胎尺寸：" + tyre.getSize());
	}

    /*
     * 飙车方法
     *
     * 当引擎排量大于等于800，且轮胎尺寸大于等于55时飙车，否则不飙车
     */
	public void race() {
		if (engine.getDisplacement() >= 800 && tyre.getSize() >= 55.0) {
			System.out.println("硬件达到了，速度上去了，飙车走起...");
		} else {
			System.out.println("还差点意思，算了吧");
		}
	}

	public Engine getEngine() {
		return engine;
	}

	public void setEngine(Engine engine) {
		this.engine = engine;
	}

	public Tyre getTyre() {
		return tyre;
	}

	public void setTyre(Tyre tyre) {
		System.out.println("更换新轮胎~~~");
		this.tyre = tyre;
	}
}
```

测试类：

```java
public class TestCar {
	public static void main(String[] args) {
        // 造一个引擎
		Engine engine = new Engine("一般的引擎",500);
        // 造一个轮胎
		Tyre tyre = new Tyre("垃圾轮胎",50.0F);
		
        // 把引擎和轮胎装上车
		Car car = new Car(engine, tyre);
		
        // 展示引擎和轮胎的成员变量方法
		car.show();
		
        // 飙车
		car.race();
		
		System.out.println("--------------------------------------");
		
        // 调整引擎排量
		engine.setDisplacement(800);

        // 造一个新轮胎
		Tyre tyre2 = new Tyre("垃圾轮胎",55.0F);
        // 新轮胎替换 car 的旧轮胎
		car.setTyre(tyre2);
		
        // 展示引擎和轮胎的成员变量方法
		car.show();
		
        // 飙车
		car.race();
		
		System.out.println("--------------------------------------");
		
        // 匿名对象创建 car2
		Car car2 = new Car(new Engine("最好的引擎",1000), new Tyre("米其林轮胎",60.0F));
		
        // 展示引擎和轮胎的成员变量方法
		car2.show();
		
        // 飙车
		car2.race();
	}
}
```
