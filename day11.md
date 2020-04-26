## 1. 数组

### 1.1 选择排序算法

把每一个元素分别和第一个元素比较

```java
import java.util.Arrays;

public class TestSelectSort {
	public static void main(String[] args) {
		int[] array = { 42, 2, 1, 34, 53, 36, 84, 2, 13, 16, 46, 84 };

		System.out.println("排序前：" + Arrays.toString(array));

		selectSort(array);

		System.out.println("排序后：" + Arrays.toString(array));
	}

	/**
	 * 选择排序算法 从大到小
	 * 
	 * @param array 传入一个数组
	 */
	public static void selectSort(int[] array) {
		for (int i = 1; i < array.length; i++) {
			for (int j = 0; j < array.length - 1; j++) {
				if (array[j] < array[i]) {
					int temp = array[i];
					array[i] = array[j];
					array[j] = temp;
				}
			}
		}
	}
}
```

### 1.2 冒泡排序算法

相邻两元素两两比较

```java
import java.util.Arrays;

public class TestBubbleSort {

	public static void main(String[] args) {
		int[] array = { 42, 22, 1, 34, 53, 36, 89, 2, 13, 16, 46, 84 };

		bubbleSort(array);

		System.out.println(Arrays.toString(array));

	}

	/**
	 * 冒泡排序算法
	 * @param array 传入一个数组
	 */
	public static void bubbleSort(int[] array) {
		for (int i = 1; i < array.length; i++) {
			for (int j = 0; j < array.length - i; j++) {
				if (array[j] < array[j + 1]) {
					int temp = array[j + 1];
					array[j + 1] = array[j];
					array[j] = temp;
				}

			}
		}

	}
}
```

## 2. Eclipse

### 2.1 快捷键

```shell
ctrl + shift + L：快捷键提示
ctrl + d：删除选中行
alt + ? 或 alt + /：自动补全代码
ctrl + 1：弹出错误修复 / Quick fix
ctrl + o：快速outline视图
ctrl + e：快速切换选项卡
ctrl + shift + r：打开资源列表
ctrl + shift + f：代码格式化
ctrl + shift + o：自动导包删包
ctrl + M：全屏代码区
shift + enter 及 ctrl + shift + enter： 在当前行上或者下创建空白行
Alt + 上下：移动选中行
ctrl + Alt + 上下：复制选中行
ctrl + /：注释选中行（//形式）
ctrl + shift + /：注释选中行（/**/形式，使用ctrl+shift+\取消）
ctrl + H 查找文件
ctrl + shift + X和 ctrl + shift + y：大小写转换（常用于SQL语句）
选中类 + F3：查看源码
选中类 + F4：显示继承关系
```

### 2.2 常用操作

```shell
窗口复位：
	Window -- Perspective-- Reset Perspective 
	
修改代码区字体大小：
	Window -- Preferences -- General -- Appearance -- Colors and Fonts -- Basic --  Text Font - Edit
	
修改字符集：
	默认情况下 Eclipse 字符集为 GBK，但现在很多项目采用的是 UTF-8，这是我们就需要设置我们的 Eclipse 开发环境字符集为 UTF-8，
    设置步骤如下：在菜单栏选择 Window -> Preferences -> General -> Workspace -> Text file encoding，在 Text file encoding 中点击 Other，选择 UTF-8
	
设置自动提示的配置：
	window -- Preferences -- Java -- Editor -- Content Assist -- Auto Activation -- Auto activation triggers for Java
	输入 "." 后出现自动提示的内容有：
 • 类变量
 • 类方法
 • 超类方法
 • 其他相关类
	
自定义代码模板：
	Eclipse 还提供了非常多的代码模板，我们可以通过 Windows->Preferences->Java->Editor->Templates (你可以在搜索框中输入Templates查找)看到所有已定义的代码模板列表。
```

【注意】如果有些快捷键用不了，可能是发生了快捷键冲突，关闭QQ和输入法中有冲突的快捷键即可

