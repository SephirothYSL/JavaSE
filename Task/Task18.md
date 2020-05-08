## 作业(接口)

```shell
教练和运动员案例
	排球运动员和篮球运动员。
	排球教练和篮球教练。
	为了出国交流，跟排球相关的人员都需要学习英语。
```

### 说英语接口

```java
public interface SpeakEnglish {
	void speak(); 
}
```

### 教练类

```java
abstract class Coach {
	String name;
	int age;

	public abstract void teach(); 
}

class BasketballCoach extends Coach {
	@Override
	public void teach() {
		System.out.println("篮球教练教篮球");
	}

}

// 实现说英语接口，重写speak()方法
class VolleyballCoach extends Coach implements SpeakEnglish{
	@Override
	public void teach() {
		System.out.println("排球教练教排球");
	}

	@Override
	public void speak() {
		System.out.println("排球教练会说英语");
	}
}
```

### 运动员类

```java
abstract class Player {
	String name;
	int age;

	public abstract void train();
}

class BasketballPlayer extends Player {
	@Override
	public void train() {
		System.out.println("篮球运动员训练篮球");
	}

}

// 实现说英语接口，重写speak()方法
class VolleyballPlayer extends Player implements SpeakEnglish {
	@Override
	public void train() {
		System.out.println("排球运动员训练排球");
	}

	@Override
	public void speak() {
		System.out.println("排球运动员会说英语");
	}

}
```

### 测试类

```java
public class Test {
	public static void main(String[] args) {
		BasketballCoach basketballCoach = new BasketballCoach();
		
		basketballCoach.teach();
		
		VolleyballCoach volleyballcoach = new VolleyballCoach();
		
		volleyballcoach.teach();
		volleyballcoach.speak();
		
		BasketballPlayer basketballPlayer = new BasketballPlayer();
		
		basketballPlayer.train();
		
		VolleyballPlayer volleyballPlayer = new VolleyballPlayer();
		
		volleyballPlayer.train();
		volleyballPlayer.speak();
	}
}
```

### 结果

```shell
篮球教练教篮球
排球教练教排球
排球教练会说英语
篮球运动员训练篮球
排球运动员训练排球
排球运动员会说英语
```

