# JAVA 生成指定范围的随机数

获取指定数值之间的数据可以利用 `java.util.Random()` 类。

`new Random().nextInt(maxVal)` 表示生成 `[0,maxVal]` 之间的随机数，我们再通过 (maxVal - minVal + 1) 计算，进行取模即可生成指定区间之间的随机数。

以生成 `[10,20]` 随机数为例，首先生成 0-20 的随机数 `new Random().nextInt(20)`，然后对(20-10+1)取模 `new Random().nextInt(20)%(20-10+1)` 得到 `[0-10]` 之间的随机数。

然后加上 minVal =10，最后生成的是 10-20 的随机数！

**示例：**

```java
import java.util.Random;
public class RandomTest {
    public static void main(String[] args) {
        int minVal = 10,maxVal = 20;

        int randomVal = new Random().nextInt(maxVal)%(maxVal - minVal + 1) + minVal;
        
        System.out.println(randomVal);
    }
}
```

# JAVA 获取本地环境属性与值

在 `com.lang.System()` 类中提供了许多与计算机相关的静态方法，其中 `System.getProperty(String key)` 静态方法就是获取计算机属性值的方法。

要想获取属性值我们首先需要知道具体属性。同样的，在不知道有哪些时同样的可以调用 `System.getProperties()` 即可获取所有属性，接着再调用 `properties.propertyNames()` 进行遍历 Key 即可。

**示例：**

```java
import java.util.Enumeration;
import java.util.Properties;
public class RandomTest {
	public static void main(String[] args) {
		Properties properties = System.getProperties();
		Enumeration enumeration = properties.propertyNames();
		while (enumeration.hasMoreElements()) {
			String key = (String) enumeration.nextElement();
			System.out.printf("Key: %s  System.getProperty(%s): %s\n", key, key, System.getProperty(key));
		}
	}
}
```

属性与值示例如下：

|属性 | 值 | 释义|
|:---|:---|:---|
|java.runtime.name|Java(TM) SE Runtime Environment| JAVA运行环境 |
|sun.boot.library.path|D:\JDK\JDK8\jdk1.8.0_152\jre\bin|JAVA依赖包地址|
|java.vm.version|25.152-b16|JVM 版本|
|java.vm.vendor|Oracle Corporation|JAVA供应商|
|java.vendor.url|`http://java.oracle.com/`|JAVA供应商地址|
|path.separator|;|操作系统地址分隔符|
|java.vm.name|Java HotSpot(TM) 64-Bit Server VM|JVM 名称|
|file.encoding.pkg|sun.io||
|user.script||用户脚本|
|user.country|GB||
|sun.java.launcher|SUN_STANDARD||
|sun.os.patch.level|||
|java.vm.specification.name|Java Virtual Machine Specification||
|user.dir|D:\IntelliJIDEA\workspace\yilutong.com\microService|用户当前目录|
|java.runtime.version|1.8.0_152-b16|JAVA运行版本|
|java.awt.graphicsenv|sun.awt.Win32GraphicsEnvironment||
|java.endorsed.dirs|D:\JDK\JDK8\jdk1.8.0_152\jre\lib\endorsed||
|os.arch|amd64||
|java.io.tmpdir|C:\Users\MinGR\AppData\Local\Temp\||
|line.separator||系统行分隔符|
|java.vm.specification.vendor|Oracle Corporation||
|user.variant|||
|os.name|Windows 10|操作系统名称|
|sun.jnu.encoding|GBK||
|java.specification.name|Java Platform API Specification||
|java.class.version|52.0|JAVA编译版本|
|sun.management.compiler|HotSpot 64-Bit Tiered Compilers||
|os.version|10.0|操作系统版本|
|user.home|C:\Users\MinGR|当前系统用户目录|
|user.timezone|Asia/Shanghai|用户时间分区|
|java.awt.printerjob|sun.awt.windows.WPrinterJob||
|file.encoding|UTF-8|文件编码格式|
|java.specification.version|1.8||
|user.name|MinGR|操作系统登录用户|
|java.vm.specification.version|1.8||
|sun.arch.data.model|64||
|java.home|D:\JDK\JDK8\jdk1.8.0_152\jre|JDK安装目录|
|sun.java.command|com.yilutong.wechat.web.h5games.H5AuthorizeController||
|java.specification.vendor|Oracle Corporation||
|user.language|en||
|awt.toolkit|sun.awt.windows.WToolkit||
|java.vm.info|mixed mode||
|java.version|1.8.0_152|JAVA版本号|
|java.ext.dirs|D:\JDK\JDK8\jdk1.8.0_152\jre\lib\ext;C:\WINDOWS\Sun\Java\lib\ext||
|java.vendor|Oracle Corporation||
|file.separator| \\ |文件分隔符|
|java.vendor.url.bug|`http://bugreport.sun.com/bugreport/`||
|sun.cpu.endian|little||
|sun.io.unicode.encoding|UnicodeLittle||
|sun.desktop|windows|操作系统|
|sun.cpu.isalist | amd64 | |