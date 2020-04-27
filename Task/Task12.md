## 十二生肖

```java
package task;

public class TestChineseZodiac {
	public static void main(String[] args) {
		Mouse mouse = new Mouse();

		mouse.age = 2;
		mouse.length = 12.0;
		mouse.weight = 20.0;

		System.out.println("鼠：" + mouse.age + " " + mouse.length + " " + mouse.weight);

		mouse.eat();
		mouse.sleep();
		mouse.burrow();

		Cattle cattle = new Cattle();
		
		cattle.age = 4;
		cattle.breed = "花花牛";
		cattle.weight = 300;
		
		System.out.println("牛：" + cattle.age + " " + cattle.breed + " " + cattle.weight);
		
		cattle.eat();
		cattle.sleep();
		cattle.work();

		Tiger tiger = new Tiger();
		
		tiger.age = 6;
		tiger.breed = "华南虎";
		tiger.color = "虎皮色";
		
		System.out.println("虎：" + tiger.age + " " + tiger.breed + " " + tiger.color);
		
		tiger.eat();
		tiger.sleep();
		tiger.catchAndHunt();

		Rabbit rabbit = new Rabbit();
		
		rabbit.age = 3;
		rabbit.color = "白色";
		rabbit.weight = 20.0;
		
		System.out.println("兔：" + rabbit.age + " " + rabbit.color + " " + rabbit.weight);
		
		rabbit.eat();
		rabbit.sleep();
		rabbit.run();

		Dragon dragon = new Dragon();
		
		dragon.age = 1000;
		dragon.color = "黑色";
		dragon.length = 40;
		
		System.out.println("龙：" + dragon.age + " " + dragon.color + " " + dragon.length);
		
		dragon.eat();
		dragon.fly();
		dragon.sleep();

		Snake snake = new Snake();
		
		snake.age = 10;
		snake.color = "青色";
		snake.weight = 20.0;
		
		System.out.println("蛇：" + snake.age + " " + snake.color + " " + snake.weight);
		
		snake.eat();
		snake.sleep();
		snake.climb();

		Horse horse = new Horse();
		
		horse.age = 10;
		horse.color = "黄色";
		horse.weight = 200.0;
		
		System.out.println("马：" + horse.age + " " + horse.color + " " + horse.weight);
		
		horse.run();
		horse.eat();
		horse.sleep();

		Sheep sheep = new Sheep();
		
		sheep.age = 5;
		sheep.color = "白色";
		sheep.weight = 200.0;
		
		System.out.println("羊：" + sheep.age + " " + sheep.color + " " + sheep.weight);
		
		sheep.eat();
		sheep.sleep();
		sheep.run();

		Monkey monkey = new Monkey();
		
		monkey.age = 3;
		monkey.breed = "猴哥";
		monkey.color = "黄色";
		
		System.out.println("猴：" + monkey.age + " " + monkey.color + " " + monkey.breed);
		
		monkey.eat();
		monkey.sleep();
		monkey.climb();

		Chook chook = new Chook();
		
		chook.breed = "打鸣鸡";
		chook.sex = '公';
		chook.weight = 15;
		
		System.out.println("鸡：" + chook.sex + " " + chook.breed + " " + chook.weight);
		
		chook.eat();
		chook.sleep();
		chook.run();

		Dog dog = new Dog();
		
		dog.age = 5;
		dog.breed = "中华田园犬";
		dog.color = "黄色";
		
		System.out.println("狗：" + dog.age + " " + dog.color + " " + dog.breed);
		
		dog.eat();
		dog.sleep();
		dog.run();

		Pig pig = new Pig();
		
		pig.age = 2;
		pig.breed = "家猪";
		pig.weight = 500.0;
		
		System.out.println("猪：" + pig.age + " " + pig.breed + " " + pig.weight);
		
		pig.eat();
		pig.sleep();
		pig.arch();
	}
}

class Mouse {
	double length;
	double weight;
	int age;

	public void eat() {
	}

	public void sleep() {
	}

	public void burrow() {
	}
}

class Cattle {
	int age;
	double weight;
	String breed;

	public void eat() {
	}

	public void sleep() {
	}

	public void work() {
	}
}

class Tiger {
	String breed;
	int age;
	String color;

	public void eat() {
	}

	public void sleep() {
	}

	public void catchAndHunt() {
	}
}

class Rabbit {
	String color;
	int age;
	double weight;

	public void eat() {
	}

	public void sleep() {
	}

	public void run() {
	}
}

class Dragon {
	int age;
	String color;
	double length;

	public void fly() {
	}

	public void eat() {
	}

	public void sleep() {
	}
}

class Snake {
	int age;
	String color;
	double weight;

	public void climb() {
	}

	public void eat() {
	}

	public void sleep() {
	}
}

class Horse {
	int age;
	String color;
	double weight;

	public void run() {
	}

	public void eat() {
	}

	public void sleep() {
	}
}

class Sheep {
	int age;
	String color;
	double weight;

	public void eat() {
	}

	public void sleep() {
	}

	public void run() {
	}
}

class Monkey {
	int age;
	String breed;
	String color;

	public void climb() {
	}

	public void eat() {
	}

	public void sleep() {
	}
}

class Chook {
	String breed;
	char sex;
	double weight;

	public void eat() {
	}

	public void sleep() {
	}

	public void run() {
	}
}

class Dog {
	int age;
	String breed;
	String color;

	public void eat() {
	}

	public void sleep() {
	}

	public void run() {
	}
}

class Pig {
	String breed;
	int age;
	double weight;

	public void eat() {
	}

	public void sleep() {
	}

	public void arch() {
	}
}
```

