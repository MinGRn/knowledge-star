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

# JAVA Class 类转 Map

这是一个工具类，在使用时需要保证 JDK 版本至少为 1.8。在 `transBean2Map(T clazz, String fields, Boolean isValNotNull)` 方法使用了 Lambda 表达式。
Lambda 表达式是 1.8 的新特性，之前的版本是没有的。

另外，在工具类中判断字符不为 NULL 使用的是 `commons-lang3` 依赖包。如果没有该依赖包请在 POM 依赖中引入该依赖。或者直接不使用 `commons-lang3` 工具类：

`if (isValNotNull && StringUtils.isBlank((CharSequence) value))` 直接写成 `if (isValNotNull && value != null)`。

工具类如下所示：

```java
import org.apache.commons.lang3.StringUtils;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.beans.BeanInfo;
import java.beans.Introspector;
import java.beans.PropertyDescriptor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;
import java.util.Arrays;
import java.util.HashMap;
import java.util.Map;

/**
 * Operations clazz that transition to {@link java.util.Map}
 * </p>
 * If you want to use this util, please check JDK {@since 1.8} or later.
 * The Lambda is a feature that only comes with JDK {@since 1.8}.
 * In addition, StringUtils come from org.apache.commons.lang3, if no dependence
 * please download or add it in pom.
 * </p>
 * <a href="http://mvnrepository.com/artifact/org.apache.commons/commons-lang3">
 * download or copy commons-lang dependence
 * </a>
 *
 * @author MinGRn <br> MinGRn97@gmail.com
 * @since 1.8
 */
public class BeanUtils {

	private BeanUtils() {
	}

	private static Logger LOGGER = LoggerFactory.getLogger(BeanUtils.class);


	public static void main(String[] args) {
		MoveCarCustomer moveCarCustomer = new MoveCarCustomer();
		moveCarCustomer.setBackLinkmanName("MinGRn");
		moveCarCustomer.setBackLinkmanPhone("199********");
		moveCarCustomer.setBackLinkmanRelation("不明");
		Map<String, Object> map = transBean2Map(moveCarCustomer, "updateUser", false);
		for (String s : map.keySet()) {
			System.out.printf("key: %s \nVal: %s", s, map.get(s) + "\n\n");
		}
	}


	/**
	 * Transition Class to Map
	 * </p>
	 * Use Introspector{@link java.beans.Introspector} and PropertyDescriptor{@link java.beans.PropertyDescriptor}
	 * transition Class Object to Map{@link java.util.Map}
	 * </p>
	 * if parameter {@code isValNotNull} is TRUE return field only not null of class, else return all
	 *
	 * @param clazz class
	 * @param isValNotNull the value is not null
	 * @return java.util.Map
	 */
	@SuppressWarnings("unchecked")
	public static <T> Map<String, Object> transBean2Map(T clazz, Boolean isValNotNull) {
		Map<String, Object> map = new HashMap<>(10);
		try {
			String clazzStr = "class";
			BeanInfo beanInfo = Introspector.getBeanInfo(clazz.getClass());
			PropertyDescriptor[] propertyDescriptors = beanInfo.getPropertyDescriptors();
			for (PropertyDescriptor property : propertyDescriptors) {
				String key = property.getName();
				if (!key.equals(clazzStr)) {
					Method getter = property.getReadMethod();
					Object value = getter.invoke(clazz);
					if (isValNotNull && StringUtils.isBlank((CharSequence) value)) {
						continue;
					}
					map.put(key, value);
				}
			}
		} catch (Exception e) {
			LOGGER.error("BeanUtils.transBean2Map Error ====>", e);
		}
		return map;
	}


	/**
	 * Gets the value of the required field to the map
	 *
	 * @param clazz class
	 * @param fields get one or more, multiple is separated by ","
	 * @param isValNotNull the value is not null
	 * @since 1.8
	 */
	@SuppressWarnings("unchecked")
	public static <T> Map transBean2Map(T clazz, String fields, Boolean isValNotNull) {
		Map<String, Object> map = new HashMap<>(10);
		Class bean = clazz.getClass();
		Arrays.stream(bean.getDeclaredFields())
				.filter(field -> fields.contains(field.getName()))
				.forEach(field -> setField2Map(field, clazz, map, isValNotNull));
		return map;
	}

	/**
	 * set field 2 map
	 *
	 * @param field clazz field
	 * @param isValNotNull 值不允许为空
	 */
	private static <T> void setField2Map(Field field, T clazz, Map<String, Object> map, Boolean isValNotNull) {
		field.setAccessible(true);
		try {
			Object fieldValue = field.get(clazz);
			if (isValNotNull && StringUtils.isBlank((CharSequence) fieldValue)) {
				return;
			}
			map.put(field.getName(), fieldValue);
		} catch (IllegalAccessException e) {
			LOGGER.error("BeanUtils.transBean2Map.setMap Error ====>", e);
		}
	}
}
```

# JAVA 根据经纬度计算两点距离

在地图上计算两点之间的距离其实就是计算地球弧度距离，将用角度表示的角转换为近似相等的用弧度表示的角。

首先需要获取某个地点的经纬度，这里可以借用百度地图 API 进行计算得到。

## 通过百度 API 求取距离

```java
import org.apache.http.client.methods.HttpUriRequest;
import org.apache.http.client.methods.RequestBuilder;
import org.apache.http.impl.client.CloseableHttpClient;
import org.apache.http.impl.client.HttpClientBuilder;

import java.io.BufferedReader;
import java.io.IOException;
import java.io.InputStream;
import java.io.InputStreamReader;

/**
 * 百度 API 经纬度计算位置
 * </p>
 * 发送 GET 请求借助 httpclient,需要在 POM 中引入:
 * <a href="http://mvnrepository.com/artifact/org.apache.httpcomponents/httpclient"></a>
 *
 * @author MinGRn <br > MinGRn97@gmail.com
 * @date 01/10/2018 15:17
 */
public class DistanceUtil {

	/**
	 * 百度获取位置经纬度 URL
	 */
	private static final String LNG_LAT_POINT_URL = "http://api.map.baidu.com/geocoder/v2/?output=json&ak=RguGdBfvanKG10lrLHtUAtka&address=";

	/**
	 * 百度Map距离求取 URL
	 */
	private static final String WAY_POINTS_DISTANCE_URL = "http://api.map.baidu.com/telematics/v3/distance?output=json&ak=RguGdBfvanKG10lrLHtUAtka&waypoints=";


	/**
	 * 获取具体位置的经纬度
	 * </p>
	 * 如: location = 上海市徐汇区零陵小区
	 * result:{"status":0,"result":{"location":{"lng":121.45078363819293,"lat":31.193489388753848},"precise":1,"confidence":70,"comprehension":100,"level":"地产小区"}}
	 *
	 * @param location 地理位置
	 */
	private static void getLngAndLat(String location) {
		try (CloseableHttpClient httpClient = HttpClientBuilder.create().build()) {
			HttpUriRequest uriRequest = RequestBuilder.get(LNG_LAT_POINT_URL + location).build();
			result(httpClient, uriRequest);
		} catch (IOException e) {
			// TODO: 01/10/2018 IOException ...
		}
	}


	/**
	 * 计算两个坐标点的距离
	 *
	 * @param startLng 起点经度
	 * @param startLat 起点纬度
	 * @param endLng 终点经度
	 * @param endLat 终点纬度
	 * @return 距离（米）
	 */
	private static void twoLocationDistance(Double startLng, Double startLat, Double endLng, Double endLat) {
		try (CloseableHttpClient httpClient = HttpClientBuilder.create().build()) {
			StringBuilder builderPoint = new StringBuilder(String.valueOf(startLng))
					.append(",").append(startLat).append(";").append(endLng).append(",").append(endLat);
			HttpUriRequest uriRequest = RequestBuilder.get(WAY_POINTS_DISTANCE_URL + builderPoint).build();
			result(httpClient, uriRequest);
		} catch (IOException e) {
			// TODO: 01/10/2018 IOException ...
		}
	}

	private static String result(CloseableHttpClient httpClient, HttpUriRequest uriRequest) {
		StringBuilder stringBuilder = new StringBuilder();
		try (InputStream inputStream = httpClient.execute(uriRequest).getEntity().getContent()) {
			String line;
			BufferedReader br = new BufferedReader(new InputStreamReader(inputStream));
			while ((line = br.readLine()) != null) {
				stringBuilder.append(line);
			}
			System.out.println(stringBuilder.toString());
		} catch (IOException e) {
			// TODO: 01/10/2018 IOException ...
		}
		return stringBuilder.toString();
	}
}
```

现在进行测试：
```java
public static void main(String[] args){
  getLngAndLat("上海市徐汇区零陵小区");
}
```

输出结果为：
```json
result:{"status":0,"result":{"location":{"lng":121.45078363819293,"lat":31.193489388753848},"precise":1,"confidence":70,"comprehension":100,"level":"地产小区"}}
```

这样就可以得到具体某个位置的经纬度了，得到两个地区的经纬度后调用 `twoLocationDistance(Double startLng, Double startLat, Double endLng, Double endLat)` 方法来获取距离信息：
```java
public static void main(String[] args){
  twoLocationDistance(121.455244, 31.234076, 121.488301, 31.237534);
}
```

可以看到具体数据结果为：`{"status":"Success","results":[3166.3643236737]}`。说明两点距离是 3166 米。

## 通过弧度角进行求取距离

现在来看下怎么自己通过计算地球弧度距离，直接看如下这个工具类：

```java
import java.math.BigDecimal;
import java.math.RoundingMode;

/**
 * 根据圆周率计算两点地图经纬度距离
 * </p>
 *
 * @author MinGRn <br > MinGRn97@gmail.com
 */
public class GoogleMapHelper {

	/**
	 * 地球半径(km)
	 */
	private static final double EARTH_RADIUS = 6378.137;

	/**
	 * 等同于 Math.toRadians(),将用角度表示的角转换为近似相等的用弧度表示的角
	 * </p>
	 * JS 没有 Math.toRadians(),如在 JS 直接使用该方法即可。
	 * eg:java
	 * Math.toRadians(startLat);
	 * eg:js
	 * radians(startLat)
	 *
	 * @param angle 角度
	 */
	private static double radians(double angle) {
		return angle * Math.PI / 180.0;
	}

	/**
	 * 计算两个坐标点的距离
	 * </p>
	 * 距离四舍五入保留一位小数,单位KM
	 *
	 * @param startLng 起点经度
	 * @param startLat 起点纬度
	 * @param endLng 终点经度
	 * @param endLat 终点纬度
	 * @return 距离（千米）
	 */
	private static double twoLocationDistance(double startLng, double startLat, double endLng, double endLat) {
		double startRadLat = Math.toRadians(startLat), endRadLat = Math.toRadians(endLat);
		double radLatDiff = startRadLat - endRadLat, radLngDiff = Math.toRadians(startLng) - Math.toRadians(endLng);

		double distance = 2 * Math.asin(Math.sqrt(Math.pow(Math.sin(radLatDiff / 2), 2) +
				Math.cos(startRadLat) * Math.cos(endRadLat) * Math.pow(Math.sin(radLngDiff / 2), 2)));

		distance = distance * EARTH_RADIUS;
		//distance = Math.round(distance * 10000) / 10000;
		//距离四舍五入保留一位小数
		distance = new BigDecimal(distance).setScale(1, RoundingMode.HALF_UP).doubleValue();
		return distance;
	}
}
```

进行测试：
```java
public static void main(String[] args) {
	long startTime = System.currentTimeMillis();
	System.out.println("耗时：" + (System.currentTimeMillis() - startTime) + "毫秒");
	double dist = twoLocationDistance(121.455244, 31.234076, 121.488301, 31.237534);
	System.out.println("两点相距：" + dist + "千米");
}
```

可以看到输出结果为：`耗时：0毫秒 两点相距：3.2千米`。可以看到两个结果相同，只是这里进行了四舍五入处理。所以，计算两个经纬度的距离可以直接使用该工具类进行计算。

另外，如果通过调用百度 API 进行求取需要发送 GET 请求，这里借助的工具是 `httpclient` 可以在 MAVEN 中央仓库进行下载:

```xml
<dependency>
    <groupId>org.apache.httpcomponents</groupId>
    <artifactId>httpclient</artifactId>
    <version>4.5.6</version>
</dependency>
```

参看资料：
- [坐标拾取系统](http://api.map.baidu.com/lbsapi/getpoint/index.html) 
- [经纬度距离计算](http://www.hhlink.com/%E7%BB%8F%E7%BA%AC%E5%BA%A6) 
- [用百度地图api计算两个地方的距离](https://blog.csdn.net/JackRen_Developer/article/details/72859630) 
- [谷歌地图计算两经纬度坐标点的距离](http://happyqing.iteye.com/blog/2236103)

# JAVA 抢红包算法

## 方法一：二倍均值法

```java
import java.math.BigDecimal;
import java.util.ArrayList;
import java.util.List;
import java.util.Random;

/**
 * 抢红包
 * </p>
 * <a href="https://juejin.im/post/5af80310f265da0b8636585e">参考</p>
 *
 * @author MinGRn <br > MinGRn97@gmail.com
 * @date 10/10/2018 09:48
 */
public class DivideRedPackage {

	/**
	 * 发红包算法,金额参数以分为单位
	 */
	private static List<Integer> divideRedPackage(Integer totalAmount, Integer totalPeopleNum) {
		List<Integer> amountList = new ArrayList<>();
		Integer restAmount = totalAmount;
		Integer restPeopleNum = totalPeopleNum;
		Random random = new Random();
		for (int i = 0; i < totalPeopleNum - 1; i++) {
			/*
			 *随机范围：[1，剩余人均金额的两倍),左闭右开
			 */
			int amount = random.nextInt(restAmount / restPeopleNum * 2 - 1) + 1;
			restAmount -= amount;
			restPeopleNum--;
			amountList.add(amount);
		}
		amountList.add(restAmount);
		return amountList;
	}


	public static void main(String[] args) {
		List<Integer> amountList = divideRedPackage(5000, 30);
		for (Integer amount : amountList) {
			System.out.println("抢到金额：" + new BigDecimal(amount).divide(new BigDecimal(100)));
		}
	}
}
```

参考: 
- [漫画：如何实现抢红包算法?](https://juejin.im/post/5af80310f265da0b8636585e)

## 方法二：

```java
import java.util.Random;

/**
 * 抢红包
 * </p>
 * <a href="https://blog.csdn.net/lb_383691051/article/details/79379384">参考</p>
 *
 * @author MinGRn <br > MinGRn97@gmail.com
 * @date 10/10/2018 12:17
 */
public class DivideRedPackage {
	public static void main(String[] args) {
		Integer count = 10;
		Boolean isHave = true;
		MoneyPackage moneyPackage = new MoneyPackage((double) 100, 10);
		while (isHave) {
			if ((--count) <= 0) {
				isHave = false;
			}
			System.out.println(divideRedPackage(moneyPackage));
		}
	}

	/**
	 * 随机获取红包
	 *
	 * @param moneyPackage 红包
	 */
	private static double divideRedPackage(MoneyPackage moneyPackage) {
		if (moneyPackage.peopleNum == 1) {
			moneyPackage.peopleNum--;
			return (double) Math.round(moneyPackage.amount * 100) / 100;
		}
		double min = 0.01, max = moneyPackage.amount / moneyPackage.peopleNum * 2;
		double money = new Random().nextDouble() * max;
		money = money <= min ? min : money;
		money = Math.floor(money * 100) / 100;
		moneyPackage.peopleNum--;
		moneyPackage.amount -= money;
		return money;
	}

	static class MoneyPackage {
		/**
		 * 红包总额
		 */
		Double amount;

		/**
		 * 红包数
		 */
		Integer peopleNum;

		public Double getAmount() {
			return amount;
		}

		public void setAmount(Double amount) {
			this.amount = amount;
		}

		public Integer getPeopleNum() {
			return peopleNum;
		}

		public void setPeopleNum(Integer peopleNum) {
			this.peopleNum = peopleNum;
		}

		MoneyPackage(Double amount, Integer peopleNum) {
			this.amount = amount;
			this.peopleNum = peopleNum;
		}
	}
}
```
参考：
- [画家丶](https://blog.csdn.net/lb_383691051/article/details/79379384)