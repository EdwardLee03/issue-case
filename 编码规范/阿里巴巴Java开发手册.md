

# 阿里巴巴Java开发手册

## 前言
《阿里巴巴Java开发手册》是阿里巴巴集团**技术团队的集体经验总结，经历了多次大规模一线实战的检验**及不断的完善，反馈给广大开发者。
现代软件行业的高速发展对开发者的综合素质要求越来越高，
因为不仅是编程知识点，其它维度的知识点也会影响到软件的最终交付质量。
比如：数据库的表结构和索引设计缺陷可能带来软件上的架构缺陷或性能风险；
工程结构混乱导致后续维护艰难；没有鉴权的漏洞代码易被黑客攻击等等。  
所以本手册以 _Java开发者_ 为中心视角，划分为**编程规约、异常日志、MySQL数据库、
工程结构、安全规约**五大块，再根据内容特征，细分成若干二级子目录。
根据**约束力强弱及故障敏感性**，规约依次分为**强制、推荐、参考**三大类。
对于规约条目的延伸信息中，“说明”对内容做了引申和解释；
**“正例”提倡什么样的编码和实现方式；“反例”说明需要提防的雷区，以及真实的错误案例**。

本手册的*愿景*是**码出高效、码出质量**。代码的字里行间流淌的是**软件生命中的血液**，
**质量的提升**是**尽可能少踩坑，杜绝踩重复的坑，切实提升 _质量意识_**。
另外，现代软件架构都需要**协同开发**完成，*高效协作*即**降低协同成本，提升沟通效率**，
所谓**无规矩不成方圆，无规范不能协作**。众所周知，制订*交通法规*表面上是要限制行车权，
实际上是**保障公众的人身安全**。试想如果没有限速，没有红绿灯，谁还敢上路行驶。
对*软件*来说，*适当的规范和标准*绝不是消灭代码内容的创造性、优雅性，
而是**限制过度个性化**，以一种普遍认可的**统一方式一起做事，提升协作效率**。

自己的理解：
```
"质量的提升是尽可能少踩坑，杜绝踩重复的坑，切实提升质量意识。"，这句怎么理解？
首先，最重要的是质量意识的提升，这是前提；其次，就是如何做到"尽可能少踩坑，杜绝踩重复的坑"。
我自己的做法是和别人一起解决别人遇到的问题，这样别人踩到的坑就是我们一起踩的，一起真正地掌握某些知识点；
还有一个技巧，善用搜索引擎的订阅功能，如“Google快讯 - 随时跟踪网上是否有您感兴趣的新内容”，可以将别人遇到的线上问题总结的文章主动推送给你。
```

《阿里巴巴Java开发手册》，开放包容地认真听取社区、博客、论坛的反馈，及时修正，保持与时俱进。
请关注手册末页的“阿里技术”和“云栖社区”公众号获取最新版本。



### 目录
```
前言
一、编程规约
    （一）命名风格
    （二）常量定义
    （三）代码格式
    （四）OOP规约
    （五）集合处理
    （六）并发处理
    （七）控制语句
    （八）注释规约
    （九）其它
二、异常日志
    （一）异常处理
    （二）日志规约
三、MySQL数据库
    （一）建表规约
    （二）索引规约
    （三）SQL语句
    （四）ORM映射
四、工程结构
    （一）应用分层
    （二）二方库依赖
    （三）服务器
五、安全规约
附 1：版本历史
附 2：本手册专有名词
```

很有价值的章节，值得仔细揣摩：
```
一、编程规约
    (一) 命名风格：6、11、12、13、15
    (二) 常量定义：2、3
    (三) 代码格式：5、8
    (四) OOP规约：2、8、9、10、12、17、20
    (五) 集合处理：9、11、12
    (六) 并发处理：2、4、5、6、7、8、9、13、14
    (七) 控制语句：1、3、7、8
    (八) 注释规约：1、2、6、7、9、10、11
    (九) 其它：6、7
二、异常日志
    (一) 异常处理：1、3、4、6、9、10、11、12
    (二) 日志规约：1、6、7、8
三、MySQL 数据库
    (一) 建表规约：5、8、9、14
    (二) 索引规约：1、4、6、9、10、11
    (三) SQL 语句：1
    (四) ORM 映射：1、7
四、工程结构
    (一) 应用分层：1、2、3
    (二) 二方库依赖：3、6、7、8
    (三) 服务器：1、2、3
五、安全规约
```



### 一、编程规约
#### (一) 命名风格
2. 【强制】 _代码中的命名_严禁使用拼音与英文混合的方式，更不允许直接使用中文的方式。
```
说明：正确的英文拼写和语法可以让阅读者易于理解，避免歧义。
正例：alibaba / taobao / hangzhou 等国际通用的名称，可视同英文。
反例：DaZhePromotion [打折] / getPingfenByName() [评分] / int 某变量 = 3
```

3. 【强制】*类名*使用 **Upper**CamelCase 风格，必须遵从**驼峰**形式，
但以下情形例外：DO / BO / DTO / VO / AO
```
正例：MarcoPolo / UserDO / XmlService / TcpUdpDeal / TaPromotion
反例：macroPolo / UserDo / XMLService / TCPUDPDeal / TAPromotion
```

4. 【强制】*方法名、参数名、成员变量、局部变量*都统一使用 **lower**CamelCase 风格，必须遵从**驼峰**形式。
```
正例：localValue / getHttpMessage() / inputUserId
```

5. 【强制】*常量*命名**全部大写，单词间用下划线隔开**，力求语义表达完整清楚，不要嫌名字长。
```
正例：MAX_STOCK_COUNT
反例：MAX_COUNT
```

6. 【`强制`】*抽象类*命名使用 **Abstract** 或 Base 开头；*异常类*命名使用 **Exception** 结尾；
*测试类*命名**以它要测试的类的名称开始，以 Test 结尾**。

8. 【强制】POJO 类中*布尔类型的变量*，都不要加 is，否则部分框架解析会引起**序列化错误**。
```
反例：定义为基本数据类型 Boolean isDeleted 的属性，它的方法也是 isDeleted()，
RPC框架在反向解析的时候，“以为”对应的属性名称是 deleted，导致属性获取不到，进而抛出异常。
```

9. 【强制】*包名*统一使用**小写，点分隔符之间有且仅有一个自然语义的英语单词**。
包名统一使用**单数**形式，但是类名如果有复数含义，类名可以使用复数形式。
```
正例：应用工具类包名为 com.alibaba.open.util、类名为 MessageUtils（此规则参考 Spring 的框架结构）
```

10. 【强制】杜绝完全不规范的*缩写*，避免望文不知义。
```
反例：AbstractClass“缩写”命名成 AbsClass；condition“缩写”命名成 condi，
此类随意缩写严重降低了代码的可阅读性。
```

11. 【`推荐`】如果使用了*设计模式*，建议**在类名中体现出具体模式**。
```
说明：将设计模式体现在名字中，有利于阅读者快速理解架构设计思想。
正例：public class OrderFactory;
     public class LoginProxy;
     public class ResourceObserver;
```
**白话**
```
Spring 框架最能体现这一点
```

12. 【`推荐`】*接口类中的方法和属性***不要加任何修饰符号（public 也不要加），保持代码的简洁性，并加上有效的 Javadoc 注释**。
尽量不要在接口里定义变量，如果一定要定义变量，肯定是与接口方法相关，并且是整个应用的基础常量。
```
正例：接口方法签名：void f();
    接口基础常量表示：String COMPANY = "alibaba";
反例：接口方法定义：public abstract void f();
说明：JDK8 中接口允许有默认实现，那么这个 default 方法，是对所有实现类都有价值的默认实现。
```

13. *接口和实现类*的命名有两套规则：
    1）【`强制`】对于 _Service 和 DAO 类_，基于 **SOA 的理念，暴露出来的服务一定是接口，内部的实现类用 Impl 的后缀与接口区别**。
```
正例：CacheServiceImpl 实现 CacheService 接口
```
    2）【推荐】如果是*形容能力的接口名称*，取对应的形容词做接口名（通常是–able 的形式）。
```
正例：AbstractTranslator 实现 Translatable
```

14. 【参考】*枚举类*名建议带上 **Enum** 后缀，*枚举成员名称*需要**全大写，单词间用下划线隔开**。
```
说明：枚举其实就是特殊的常量类，且构造方法被默认强制是私有的。
正例：枚举名字：DealStatusEnum，成员名称：SUCCESS / UNKOWN_REASON。
```

15. 【`参考`】**各层命名**规约：  
    A) **Service/DAO 层方法**命名规约  
        1） 获取**单个对象**的方法用 **get** 做前缀  
        2） 获取**多个对象**的方法用 **list** 做前缀  
        3） 获取**统计值**的方法用 count 做前缀  
        4） **插入**的方法用 **save**（推荐）或 insert 做前缀  
        5） **修改**的方法用 **update** 做前缀  
        6） **删除**的方法用 **remove**（推荐）或 delete 做前缀  
    B) **领域模型**命名规约  
        1） 数据对象：xxxDO，xxx 即为**数据表名**  
        2） 数据传输对象：xxxDTO，xxx 为**业务领域相关的名称**  
        3） 展示对象：xxxVO，xxx 一般为**网页名称**  
        4） POJO 是 DO/DTO/BO/VO 的统称，禁止命名成 xxxPOJO  

**白话**
```
很有价值，值得遵守。
```


#### (二) 常量定义
1. 【强制】不允许任何*魔法值*（即未经定义的常量）直接出现在代码中。
```
反例：String key = "trade.id:" + tradeId;
     cache.put(key, value);
```

2. 【`强制`】*long 或者 Long 初始赋值*时，必须使用**大写的 L**，不能是小写的 l，
小写容易跟数字 1 混淆，造成误解。
```
说明：Long a = 2l; 写的是数字的 21，还是 Long 型的 2?
```

3. 【`推荐`】不要使用一个常量类维护所有*常量*，应该**按常量功能进行归类，分开维护**。
如：缓存相关的常量放在类：CacheConst 下；系统配置相关的常量放在类：ConfigConst 下。
```
说明：大而全的常量类，非得使用查找功能才能定位到修改的常量，不利于理解和维护。
```
**白话**
```
程序局部性原理
```

4. 【推荐】*常量的复用*层次有五层：跨应用共享常量、应用内共享常量、子工程内共享常量、
包内共享常量、类内共享常量。  
    1） **跨应用**共享常量：放置在**二方库**中，通常是 client.jar 中的 constant 目录下。  
    2） **应用内**共享常量：放置在**一方库**的 modules 中的 constant 目录下。
    ```
    反例：易懂变量也要统一定义成应用内共享常量，两位攻城师在两个类中分别定义了表示“是”的变量：
        类 A 中：public static final String YES = "yes";
        类 B 中：public static final String YES = "y";
        A.YES.equals(B.YES)，预期是 true，但实际返回为 false，导致线上问题。
    ```
    5） 类内共享常量：直接在类内部 private static final 定义。

5. 【推荐】如果**变量值仅在一个范围内变化**，且**带有名称之外的延伸属性**，定义为*枚举类*。
下面正例中的数字就是延伸信息，表示星期几。
```
正例：public Enum { MONDAY(1), TUESDAY(2), WEDNESDAY(3), THURSDAY(4), FRIDAY(5),
SATURDAY(6), SUNDAY(7);}
```


#### (三) 代码格式
5. 【`强制`】*缩进*采用 **4 个空格**，禁止使用 tab 字符。
```
说明：如果使用 tab 缩进，必须设置 1 个 tab 为 4 个空格。
IDEA 设置 tab 为 4 个空格时，请勿勾选 Use tab character；
而在 eclipse 中，必须勾选 insert spaces for tabs。
```

6. 【强制】**单行字符数**限制不超过 _120_ 个，超出需要换行，换行时遵循如下原则：  
    1） 第二行相对第一行缩进 4 个空格，从第三行开始，不再继续缩进。  
    2） 运算符与下文一起换行。  
    3） 方法调用的点符号与下文一起换行。

8. 【`强制`】IDE 的 text _file encoding_ 设置为 **UTF-8**;
IDE 中文件的*换行符*使用 **Unix 格式**，不要使用 windows 格式。

10. 【推荐】方法体内的执行语句组、变量的定义语句组、不同的业务逻辑之间或者不同的语义之间插入一个空行。
```
说明：没有必要插入多个空行进行隔开。
```


#### (四) OOP规约
1. 【强制】避免通过一个类的对象引用访问此**类的静态变量或静态方法**，无谓增加编译器解析成本，直接用**类名**来访问即可。

2. 【`强制`】所有的*覆写方法*，必须加 **@Override** 注解。
```
说明：getObject() 与 get0bject() 的问题。一个是字母的 O，一个是数字的 0，加 @Override 可以准确判断是否覆盖成功。另外，如果在抽象类中对方法签名进行修改，其实现类会马上编译报错。
```

3. 【强制】相同参数类型，相同业务含义，才可以使用 Java 的*可变参数*，避免使用 Object。
```
说明：可变参数必须放置在参数列表的最后。（提倡同学们尽量不用可变参数编程）
正例：public List<User> listUser(String type, Integer... ids) {...}
```

4. 【强制】外部正在调用或者二方库依赖的接口，不允许修改方法签名，避免对接口调用方产生影响。
*接口过时*必须加 @Deprecated 注解，并清晰地说明采用的新接口或者新服务是什么。

5. 【强制】不能使用过时的类或方法。
```
说明：java.net.URLDecoder 中的方法 decode(String encodeStr) 这个方法已经过时，
应该使用双参数 decode(String source, String encode)。
接口提供方既然明确是过时接口，那么有义务同时提供新的接口；
作为调用方来说，有义务去考证过时方法的新实现是什么。
```

6. 【强制】Object 的 equals 方法容易抛*空指针异常*，应使用常量或确定有值的对象来调用 equals。
```
正例： "test".equals(object);
反例： object.equals("test");
说明：推荐使用 java.util.Objects#equals （JDK7 引入的工具类）
```

7. 【强制】所有相同类型的**包装类对象之间值的比较**，全部使用 _equals_ 方法比较。
```
说明：对于 Integer var = ? 在-128 至 127 范围内的赋值，Integer 对象是在 IntegerCache.cache 产生，会复用已有对象，这个区间内的 Integer 值可以直接使用 == 进行判断，
但是这个区间之外的所有数据，都会在堆上产生，并不会复用已有对象，这是一个大坑，推荐使用 equals 方法进行判断。
```

8. 关于**基本数据类型与包装数据类型的使用标准**如下：  
    1） 【强制】所有的 **POJO 类属性**必须使用**包装**数据类型。  
    2） 【强制】**RPC 方法的返回值和参数**必须使用**包装**数据类型。  
    3） 【推荐】所有的**局部变量**使用**基本**数据类型。
    ```
    说明：POJO 类属性没有初始值是提醒使用者在需要使用时，必须自己显式地进行赋值，任何 NPE 问题，或者入库检查，都由使用者来保证。
    正例：数据库的查询结果可能是 null，因为自动拆箱，用基本数据类型接收有 NPE 风险。
    反例：比如显示成交总额涨跌情况，即正负 x%，x 为基本数据类型，
    调用的 RPC 服务，调用不成功时，返回的是默认值，页面显示：0%，这是不合理的，应该显示成中划线-。
    所以包装数据类型的 null 值，能够表示额外的信息，如：远程调用失败，异常退出。
    ```

9. 【`强制`】定义 DO/DTO/VO 等 *POJO 类*时，**不要设定**任何**属性默认值**。
```
反例：POJO 类的 gmtCreate 默认值为 new Date(); 但是这个属性在数据提取时并没有置入具体值，
在更新其它字段时又附带更新了此字段，导致创建时间被修改成当前时间。
```

10. 【`强制`】*序列化类新增属性*时，请**不要修改 serialVersionUID** 字段，避免反序列失败；
如果完全不兼容升级，避免反序列化混乱，那么请修改 serialVersionUID 值。
```
说明：注意 serialVersionUID 不一致会抛出序列化运行时异常。
```

11. 【强制】*构造方法*里面**禁止加入任何业务逻辑**，如果有初始化逻辑，请放在 init 方法中。

12. 【`强制`】*POJO 类*必须写 _toString_ 方法。使用 IDE 的中工具：source > generate toString 时，
如果继承了另一个 POJO 类，注意在前面加一下 super.toString()。
```
说明：在方法执行抛出异常时，可以直接调用 POJO 的 toString() 方法打印其属性值，便于排查问题。
```

13. 【推荐】使用索引访问用 String 的 split 方法得到的数组时，
需做最后一个分隔符后有无内容的检查，否则会有抛 IndexOutOfBoundsException 的风险。
```
说明：
    String str = "a,b,c,,";
    String[] ary = str.split(",");
    // 预期大于 3，结果是 3
    System.out.println(ary.length);
```

14. 【推荐】当一个类有多个构造方法，或者*多个同名方法*，这些方法应该按顺序放置在一起，便于阅读。

15. 【推荐】*类内方法定义顺序*依次是：公有方法或保护方法 > 私有方法 > getter/setter 方法。
```
说明：公有方法是类的调用者和维护者最关心的方法，首屏展示最好；
保护方法虽然只是子类关心，也可能是“模板设计模式”下的核心方法；
而私有方法外部一般不需要特别关心，是一个黑盒实现；
因为方法信息价值较低，所有 Service 和 DAO 的 getter/setter 方法放在类体最后。
```

16. 【推荐】setter 方法中，参数名称与类成员变量名称一致，this.成员名 = 参数名。
在 _getter/setter_ 方法中，不要增加业务逻辑，增加排查问题的难度。

17. 【`推荐`】**循环体内，字符串的连接**方式，使用 StringBuilder 的 append 方法进行扩展。
```
说明：反编译出的字节码文件显示每次循环都会 new 出一个 StringBuilder 对象，然后进行 append 操作，最后通过 toString 方法返回 String 对象，造成内存资源浪费。
反例：
    String str = "start";
    for (int i = 0; i < 100; i++) {
        str = str + "hello";
    }
```

18. 【推荐】 _final_ 可以声明类、成员变量、方法、以及本地变量，下列情况使用 final 关键字：  
    1） 不允许**被继承的类**，如：String 类。  
    2） 不允许**修改引用的域对象**，如：POJO 类的域变量。  
    3） 不允许**被重写的方法**，如：POJO 类的 setter 方法。  
    4） 不允许运行过程中重新赋值的局部变量。  
    5） 避免**上下文重复使用一个变量**，使用 final 描述可以强制重新定义一个变量，方便更好地进行重构。

19. 【推荐】慎用 Object 的 _clone_ 方法来*拷贝对象*。
```
说明：对象的 clone 方法默认是浅拷贝，若想实现深拷贝需要重写 clone 方法实现属性对象的拷贝。
```

20. 【`推荐`】*类成员与方法访问*控制从严：  
    1） 如果**不允许外部直接通过 new 来创建对象**，那么构造方法必须是 private。  
    2） **工具类**不允许有 public 或 default 构造方法。  
    3） 类非 static 成员变量并且与子类共享，必须是 protected。  
    4） 类非 static 成员变量并且**仅在本类使用**，必须是 private。  
    5） 类 static 成员变量如果仅在本类使用，必须是 private。  
    6） 若是 **static 成员变量**，必须考虑是否为 _final_。  
    7） 类成员方法只供**类内部调用**，必须是 private。  
    8） 类成员方法只对继承类公开，那么限制为 protected。
    ```
    说明：任何类、方法、参数、变量，严控访问范围。过于宽泛的访问范围，不利于模块解耦。
    思考：如果是一个 private 的方法，想删除就删除，可是一个 public 的 service 方法，
    或者一个 public 的成员变量，删除一下，不得手心冒点汗吗？
    变量像自己的小孩，尽量在自己的视线内，变量作用域太大，如果无限制地到处跑，那么你会担心的。
    ```


#### (五) 集合处理
1. 【强制】关于 _hashCode 和 equals_ 的处理，遵循如下规则：  
    1） **只要重写 equals，就必须重写 hashCode**。  
    2） 因为 _Set_ 存储的是**不重复的对象，依据 hashCode 和 equals 进行判断**，所以 Set 存储的对象必须重写这两个方法。  
    3） 如果**自定义对象做为 Map 的键**，那么必须重写 hashCode 和 equals。
    ```
    说明：String 重写了 hashCode 和 equals 方法，所以我们可以非常愉快地使用 String 对象作为 key 来使用。
    ```

2. 【强制】ArrayList 的 _subList 结果不可强转成 ArrayList_，否则会抛出 ClassCastException 异常：
java.util.RandomAccessSubList cannot be cast to java.util.ArrayList ;
```
说明：subList 返回的是 ArrayList 的内部类 SubList，并不是 ArrayList ，
而是 ArrayList 的一个视图，对于 SubList 子列表的所有操作最终会反映到原列表上。
```

3. 【强制】 在 subList 场景中，**高度注意**对*原集合元素个数的修改*，会导致子列表的遍历、增 加、删除均产生 _ConcurrentModificationException_ 异常。

4. 【强制】使用*集合转数组*的方法，必须使用**集合的 toArray(T[] array)**，传入的是类型完全一样的数组，大小就是 list.size()。
```
说明：使用 toArray 带参方法，入参分配的数组空间不够大时，toArray 方法内部将重新分配内存空间，并返回新数组地址；
如果数组元素大于实际所需，下标为[list.size()]的数组元素将被置为 null，其它数组元素保持原值，因此最好将方法入参数组大小定义与集合元素个数一致。
正例：
    List<String> list = new ArrayList<String>(2);
    list.add("guan");
    list.add("bao");
    String[] array = new String[list.size()];
    array = list.toArray(array);
反例：直接使用 toArray 无参方法存在问题，此方法返回值只能是 Object[] 类，若强转其它类型数组将出现 ClassCastException 错误。
```

5. 【强制】使用工具类 _Arrays.asList()_ 把*数组转换成集合*时，不能使用其*修改集合*相关的方法，它的 add/remove/clear 方法会抛出 UnsupportedOperationException 异常。
```
说明：asList 的返回对象是一个 Arrays 内部类，并没有实现集合的修改方法。
Arrays.asList 体现的是适配器模式，只是转换接口，后台的数据仍是数组。
    String[] str = new String[] { "a", "b" };
    List list = Arrays.asList(str);
第一种情况：list.add("c"); 运行时异常。
第二种情况：str[0] = "gujin"; 那么 list.get(0) 也会随之修改。
```

6. 【强制】*泛型通配符*<? extends T>来接收返回的数据，此写法的泛型集合不能使用 add 方法，
而<? super T>不能使用 get 方法，做为接口调用赋值时易出错。
```
说明：扩展说一下 PECS(Producer Extends Consumer Super)原则：
1）频繁往外读取内容的，适合用上界 Extends。2）经常往里插入的，适合用下界 Super。
示例：Collections.copy(List<? super T> dest, List<? extends T> src)
```

7. 【强制】不要在 _foreach_ 循环里进行元素的 _remove/add_ 操作。remove 元素请使用 Iterator 方式，如果并发操作，需要对 Iterator 对象加锁。
```
正例：
    Iterator<String> it = a.iterator();
    while (it.hasNext()) {
        String temp = it.next();
        if (删除元素的条件) {
            it.remove();
        }
    }
反例：
    List<String> a = new ArrayList<String>();
    a.add("1");
    a.add("2");
    for (String temp : a) {
        if ("1".equals(temp)) {
            a.remove(temp);
        }
    }
说明：以上代码的执行结果肯定会出乎大家的意料，那么试一下把“1”换成“2”，会是同样的结果吗？
```

8. 【强制】在 JDK7 版本及以上， _Comparator_ 要满足如下*三个条件*，不然 Arrays.sort，Collections.sort 会报 IllegalArgumentException 异常。
```
说明：
    1） x，y 的比较结果和 y，x 的比较结果相反。(对称性)
    2） x>y，y>z，则 x>z。(传递性)
    3） x=y，则 x，z 比较结果和 y，z 比较结果相同。(等价性)
反例：下例中没有处理相等的情况，实际使用中可能会出现异常：
    new Comparator<Student>() {
        @Override
        public int compare(Student o1, Student o2) {
            return o1.getId() > o2.getId() ? 1 : -1;
        }
    };
```

9. 【`推荐`】*集合初始化*时，指定**集合初始值大小**。
```
说明：HashMap 使用 HashMap(int initialCapacity) 初始化
正例：initialCapacity = (需要存储的元素个数 / 负载因子) + 1。
注意负载因子（loader factor）默认为 0.75，如果暂时无法确定初始值大小，请设置为 16。
反例：HashMap 需要放置 1024 个元素，由于没有设置容量初始大小，随着元素不断增加，容量 7 次被迫扩大，resize 需要重建 hash 表，严重影响性能。
```

10. 【推荐】使用 **entrySet** 遍历 _Map_ 类集合 KV，而不是 keySet 方式进行遍历。
```
说明：keySet 其实是遍历了 2 次，一次是转为 Iterator 对象，另一次是从 hashMap 中取出 key 所对应的 value。而 entrySet 只是遍历了一次就把 key 和 value 都放到了 entry 中，效率更高。如果是 JDK8，使用 Map.foreach 方法。
正例：values() 返回的是 V 值集合，是一个 List 集合对象；keySet() 返回的是 K 值集合，是一个 Set 集合对象；entrySet() 返回的是 K-V 值组合集合。
```

11. 【`推荐`】高度注意 _Map_ 类集合 K/V 能不能存储 _null_ 值的情况，如下表格：

| 集合类              | Key          | Value        | Super       | 说明      |
| --------           | --------     | ---------    | --------    | --------  |
| Hashtable          | 不允许为 null | 不允许为 null | Dictionary  | 线程安全   |
| _ConcurrentHashMap_  | 不允许为 null | _不允许为 null_ | AbstractMap | _分段锁技术_ |
| TreeMap            | 不允许为 null | 允许为 null   | AbstractMap | 线程不安全 |
| _HashMap_            | _允许为 null_   | 允许为 null   | AbstractMap | _线程不安全_ |

```
反例：由于 HashMap 的干扰，很多人认为 ConcurrentHashMap 是可以置入 null 值，
而事实上， 存储 null 值时会抛出 NPE 异常。
```

12. 【`参考`】合理利用好*集合的有序性(sort)和稳定性(order)*，
避免集合的无序性(unsort)和不稳定性(unorder)带来的负面影响。
```
说明：有序性是指遍历的结果是按某种比较规则依次排列的。稳定性是指集合每次遍历的元素次序是一定的。
如：ArrayList 是 order/unsort；HashMap 是 unorder/unsort；TreeSet 是 order/sort。
```

13. 【参考】利用 *Set 元素唯一*的特性，可以快速对一个集合进行去重操作，避免使用 List 的 contains 方法进行遍历、对比、去重操作。


#### (六) 并发处理
1. 【强制】获取*单例对象*需要保证*线程安全*，其中的方法也要保证线程安全。
```
说明：资源驱动类、工具类、单例工厂类都需要注意。
```

2. 【`强制`】创建**线程或线程池**时请指定**有意义的线程名称**，_方便出错时回溯_。
```
正例：
    public class TimerTaskThread extends Thread {
        public TimerTaskThread() {
            super.setName("TimerTaskThread");
            ...
        }
    }
说明：Guava 的 ThreadFactoryBuilder
```

3. 【强制】**线程资源**必须通过**线程池**提供，不允许在应用中自行显式创建线程。
```
说明：使用线程池的好处是减少在创建和销毁线程上所花的时间以及系统资源的开销，解决资源不足的问题。
如果不使用线程池，有可能造成系统创建大量同类线程而导致消耗完内存或者执行上下文“过度切换”的问题。
```

4. 【`强制`】**线程池**不允许使用 Executors 去创建，而是通过 _ThreadPoolExecutor_ 的方式，
这样的处理方式让写的同学更加明确**线程池的运行规则**，规避**资源耗尽的风险**。
```
说明：Executors 返回的线程池对象的弊端如下：
1）FixedThreadPool 和 SingleThreadPool:
    允许的请求队列长度为 Integer.MAX_VALUE，可能会堆积大量的请求，从而导致 OOM。
2）CachedThreadPool 和 ScheduledThreadPool:
    允许的创建线程数量为 Integer.MAX_VALUE，可能会创建大量的线程，从而导致 OOM。
```

5. 【`强制`】 _SimpleDateFormat_ 是**线程不安全**的类，一般不要定义为 static 变量，
如果定义为 static，必须加锁，或者使用 DateUtils 工具类。
```
正例：注意线程安全，使用 DateUtils。亦推荐如下处理：
    private static final ThreadLocal<DateFormat> df = new ThreadLocal<DateFormat>() {
            @Override protected DateFormat initialValue() {
                return new SimpleDateFormat("yyyy-MM-dd");
            }
    };
说明：如果是 JDK8 的应用，可以使用 Instant 代替 Date，LocalDateTime 代替 Calendar，
DateTimeFormatter 代替 Simpledateformatter，官方给出的解释：simple beautiful strong immutable thread-safe。
```

6. 【`强制`】**高并发**时，**同步调用**应该去考量**锁的性能损耗**。能用**无锁数据结构**，就不要用锁；
能**锁区块**，就不要锁整个方法体；能用**对象锁**，就不要用类锁。
```
说明：尽可能使加锁的代码块工作量尽可能的小，避免在锁代码块中调用 RPC 方法。
```

7. 【`强制`】对**多个资源、数据库表、对象同时加锁**时，需要保持一致的**加锁顺序**，否则可能会造成**死锁**。
```
说明：线程一需要对表 A、B、C 依次全部加锁后才可以进行更新操作，那么线程二的加锁顺序也必须是 A、B、C，否则可能出现死锁。
```

8. 【`强制`】**并发修改同一记录**时，避免更新丢失，需要**加锁**。
要么在**应用层**加锁，要么在**缓存**加锁，要么在**数据库层**使用**乐观锁**，使用 version 作为更新依据。
```
说明：如果每次访问冲突概率小于 20%，推荐使用乐观锁，否则使用悲观锁。
乐观锁的重试次数不得小于 3 次。
```

9. 【`强制`】*多线程并行处理定时任务*时， _Timer_ 运行多个 _TimeTask_ 时，只要其中之一**没有捕获抛出的异常**，其它任务便会自动终止运行，使用 _ScheduledExecutorService_ 则没有这个问题。

10. 【推荐】使用 _CountDownLatch_ 进行**异步转同步**操作，
每个线程退出前必须调用 countDown 方法，线程执行代码注意 catch 异常，确保 countDown 方法可以执行，避免主线程无法执行至 await 方法，直到超时才返回结果。
```
说明：注意，子线程抛出异常堆栈，不能在主线程 try-catch 到。
```

11. 【推荐】避免 _Random_ 实例被多线程使用，虽然共享该实例是线程安全的，但**会因竞争同一 seed 导致的性能下降**。
```
说明：Random 实例包括 java.util.Random 的实例或者 Math.random() 的方式。
正例：在 JDK7 之后，可以直接使用 ThreadLocalRandom，而在 JDK7 之前，需要编码保证每个线程持有一个实例。
```

12. 【推荐】在并发场景下，通过*双重检查锁（double-checked locking）*实现*延迟初始化*的优化问题隐患
(可参考 The "Double-Checked Locking is Broken" Declaration)，推荐问题解决方案中较为简单一种（适用于 JDK5 及以上版本），将目标属性声明为 volatile 型。

13. 【`参考`】 _volatile_ 解决**多线程内存不可见问题**。对于**一写多读**，是可以解决**变量同步问题**，
但是如果**多写**，同样**无法解决线程安全问题**。如果是 count++ 操作，使用如下类实现：
_AtomicInteger_ count = new AtomicInteger(); count.addAndGet(1);
如果是 JDK8，推荐使用 _LongAdder_ 对象，比 AtomicLong 性能更好（减少**乐观锁**的重试次数）。

14. 【`参考`】 _HashMap_ 在容量不够进行 resize 时由于**高并发可能出现死链**，导致 **CPU 飙升**，在开发过程中可以使用其它数据结构或加锁来规避此风险。
```
说明：ConcurrentHashMap
```

15. 【参考】 _ThreadLocal_ 无法解决**共享对象的更新问题**，ThreadLocal 对象建议使用 static 修饰。
这个变量是针对一个线程内所有操作共有的，所以设置为静态变量，所有此类实例共享此静态变量，
也就是说在类第一次被使用时装载，只分配一块存储空间，所有此类的对象(只要是这个线程内定义的)都可以操控这个变量。


#### (七) 控制语句
1. 【`强制`】在一个 _switch_ 块内，每个 case 要么通过 _break/return_ 等来终止，要么注释说明程序将继续执行到哪一个 case 为止；
在一个 switch 块内，都必须包含一个 default 语句并且放在最后，即使它什么代码也没有。

2. 【强制】在 _if/else/for/while/do_ 语句中必须使用*大括号*。即使只有一行代码，
避免使用单行的形式：if (condition) statements;

3. 【`推荐`】表达**异常的分支**时，少用 if-else 方式，这种方式可以改写成：
```
    if (condition) {
        ...
        return obj;
    }
    // 接着写 else 的业务逻辑代码;
说明：如果非得使用 if()...else if()...else...方式表达逻辑，【强制】避免后续代码维护困难，请勿超过 3 层。
正例：逻辑上超过 3 层的 if-else 代码可以使用卫语句，或者状态模式来实现。
```

4. 【推荐】除常用方法（如 getXxx/isXxx）等外，不要在条件判断中执行其它复杂的语句，将复杂逻辑判断的结果赋值给一个有意义的布尔变量名，以提高可读性。
```
说明：很多 if 语句内的逻辑相当复杂，阅读者需要分析条件表达式的最终结果，才能明确什么样的条件执行什么样的语句，那么，如果阅读者分析逻辑表达式错误呢？
```

5. 【推荐】 _循环体中的语句_要考量性能，以下操作尽量移至循环体外处理，如定义对象、变量、获取数据库连接，进行不必要的 try-catch 操作（这个 try-catch 是否可以移至循环体外）。

6. 【推荐】 _接口入参保护_，这种场景常见的是用于做批量操作的接口。

7. 【`参考`】下列情形，**需要**进行**参数校验**：  
    1） 调用频次低的方法。  
    2） **执行时间开销很大的方法**。此情形中，参数校验时间几乎可以忽略不计，
但如果因为参数错误导致中间执行回退，或者错误，那就得不偿失。  
    3） 需要**极高稳定性和可用性的方法**。  
    4） **对外提供的开放接口**，不管是 RPC/API/HTTP 接口。  
    5） **敏感权限入口**。

**白话**
```
很有价值，值得遵守。
```

8. 【`参考`】下列情形，**不需要**进行**参数校验**：  
    1） 极有可能**被循环调用的方法**。但在方法说明里必须注明外部参数检查要求。  
    2） **底层调用频度比较高的方法**。毕竟是像纯净水过滤的最后一道，参数错误不太可能到底层才会暴露问题。
一般 DAO 与 Service 层都在同一个应用中，部署在同一台服务器中，所以 DAO 的参数校验，可以省略。  
    3） 被声明成 **private** 只会被自己代码所调用的**方法**，如果能够确定调用方法的代码传入参数已经做过检查或者肯定不会有问题，此时可以不校验参数。


#### (八) 注释规约
1. 【`强制`】*类、类属性、类方法的注释*必须使用 _Javadoc 规范_，使用/\*\*内容\*/格式，不得使用 //xxx 方式。
```
说明：在 IDE 编辑窗口中，Javadoc 方式会提示相关注释，生成 Javadoc 可以正确输出相应注释；
在 IDE 中，工程调用方法时，不进入方法即可悬浮提示方法、参数、返回值的意义，提高阅读效率。
```

2. 【`强制`】所有的*抽象方法*（包括*接口中的方法*）必须要用 **Javadoc 注释**、
除了**返回值、参数、异常说明**外，还必须指出**该方法做什么事情，实现什么功能**。
```
说明：对子类的实现要求，或者调用注意事项，请一并说明。
```

3. 【强制】所有的*类*都必须添加**创建者和创建日期**。

5. 【强制】所有的**枚举类型字段**必须要有注释，**说明每个数据项的用途**。

6. 【`推荐`】与其“半吊子”英文来**注释**，不如用中文注释**把问题说清楚**。专有名词与关键字保持英文原文即可。
```
反例：“TCP 连接超时”解释成“传输控制协议连接超时”，理解反而费脑筋。
```

7. 【`推荐`】代码修改的同时，注释也要进行相应的修改，尤其是**参数、返回值、异常、核心逻辑**等的修改。
```
说明：代码与注释更新不同步，就像路网与导航软件更新不同步一样，如果导航软件严重滞后，就失去了导航的意义。
```

8. 【参考】合理处理注释掉的代码。在上方详细说明，而不是简单的注释掉。如果无用，则删除。
```
说明：代码被注释掉有两种可能性：1）后续会恢复此段代码逻辑。2）永久不用。
前者如果没有备注信息，难以知晓注释动机。后者建议直接删掉（代码仓库保存了历史代码）。
```

9. 【`参考`】对于*注释*的要求：第一、能够**准确反应设计思想和代码逻辑**；
第二、能够**描述业务含义**，使别的程序员能够迅速了解到代码背后的信息。
完全没用注释的大段代码对于阅读者形同天书，注释是给自己看的，即使隔很长时间，也能清晰理解当时的思路；
注释也是给继任者看的，使其能够快速接替自己的工作。

10. 【`参考`】**好的命名、代码结构**是**自解释**的， _注释力求精简准确、表达到位_。
避免出现注释的一个极端：过多过滥的注释，代码的逻辑一旦修改，修改注释是相当大的负担。
```
反例：
    // put elephant into fridge
    put(elephant, fridge);
方法名 put，加上两个有意义的变量名 elephant 和 fridge，已经说明了这是在干什么，
语义清晰的代码不需要额外的注释。
```

11. 【`参考`】 _特殊注释标记_，请注明标记人与标记时间。注意及时处理这些标记，通过标记扫描，经常清理此类标记。
**线上故障**有时候就是来源于这些标记处的代码。  
    1） 待办事宜（*TODO*）:（标记人，标记时间，[预计处理时间]）  
      表示需要实现，但目前还未实现的功能。这实际上是一个 Javadoc 的标签，目前的 Javadoc 还没有实现，但已经被广泛使用。  
      只能应用于类，接口和方法（因为它是一个 Javadoc 标签）。  
    2） 错误，不能工作（*FIXME*）:（标记人，标记时间，[预计处理时间]）  
      在注释中用 FIXME 标记某代码是错误的，而且不能工作，需要及时纠正的情况。


#### (九) 其它
1. 【强制】在使用*正则表达式*时，利用好其预编译功能，可以有效加快正则匹配速度。
```
说明：不要在方法体内定义：Pattern pattern = Pattern.compile(规则);
```

2. 【强制】Velocity 调用 POJO 类的属性时，建议直接使用属性名取值即可，
模板引擎会自动按规范调用 POJO 的 getXxx()，如果是 Boolean 基本数据类型变量（Boolean 命名不需要加 is 前缀），会自动调用 isXxx()方法。
```
说明：注意如果是 Boolean 包装类对象，优先调用 getXxx()的方法。
```

3. 【强制】后台输送给页面的变量必须加\$!{var}——中间的感叹号。
```
说明：如果 var=null 或者不存在，那么${var}会直接显示在页面上。
```

4. 【强制】注意 _Math.random()_ 这个方法返回是 double 类型，注意取值的范围 0≤x<1（能够取到零值，注意除零异常），
如果想获取**整数类型的随机数**，不要将 x 放大 10 的若干倍然后取整，直接使用 Random 对象的 _nextInt_ 或者 _nextLong_ 方法。

5. 【强制】获取*当前毫秒数* _System.currentTimeMillis()_; 而不是 new Date().getTime();
```
说明：如果想获取更加精确的纳秒级时间值，使用 System.nanoTime() 的方式。
在 JDK8 中，针对统计时间等场景，推荐使用 Instant 类。
```

6. 【`推荐`】不要在视图模板中加入任何复杂的逻辑。
```
说明：根据 MVC 理论，视图的职责是展示，不要抢模型和控制器的活。(APP的职责是展示数据)
组件、模块、服务职责清晰
```

7. 【`推荐`】任何*数据结构的构造或初始化*，都应**指定大小**，避免**数据结构无限增长吃光内存**。

8. 【推荐】对于“明确停止使用的代码和配置”，如方法、变量、类、配置文件、动态配置属性等要坚决从程序中清理出去，避免造成过多垃圾。



### 二、异常日志
#### (一) `异常处理`
1. 【`强制`】Java 类库中定义的一类 _RuntimeException_ 可以通过**预先检查**进行规避，而不应该通过 catch 来处理，比如：IndexOutOfBoundsException，NullPointerException 等等。
```
说明：无法通过预检查的异常除外，如在解析一个外部传来的字符串形式数字时，通过 catch NumberFormatException 来实现。
正例：if (obj != null) {...}
反例：try { obj.method() } catch (NullPointerException e) {...}
```

2. 【强制】*异常*不要用来做流程控制，条件控制，因为异常的处理效率比条件分支低。

3. 【`强制`】对*大段代码*进行 _try-catch_，这是不负责任的表现。catch 时请分清**稳定代码和非稳定代码**，
稳定代码指的是无论如何不会出错的代码。对于非稳定代码的 catch 尽可能进行**区分异常类型，再做对应的异常处理**。

4. 【`强制`】**捕获异常**是为了处理它，**不要捕获了却什么都不处理而抛弃之**，如果不想处理它，请将该异常抛给它的调用者。
**最外层的业务使用者**，必须**处理异常**，将其**转化为用户可以理解的内容**。

5. 【强制】有 try 块放到了事务代码中，catch 异常后，如果需要回滚事务，一定要注意手动回滚事务。

6. 【`强制`】 _finally_ 块必须**对资源对象、流对象进行关闭**，有异常也要做 try-catch。
```
说明：如果 JDK7 及以上，可以使用 try-with-resources 方式。
```

7. 【强制】不能在 finally 块中使用 return，finally 块中的 return 返回后方法结束执行，不会再执行 try 块中的 return 语句。

8. 【强制】 _捕获异常与抛异常_，必须是完全匹配，或者捕获异常是抛异常的父类。
```
说明：如果预期对方抛的是绣球，实际接到的是铅球，就会产生意外情况。
```

9. 【`推荐`】*方法的返回值*可以为 null，不强制返回空集合，或者空对象等，
必须**添加注释充分说明什么情况下会返回 null 值**。调用方需要进行 null 判断防止 NPE 问题。
```
说明：本手册明确防止 NPE 是调用者的责任。
即使被调用方法返回空集合或者空对象，对调用者来说，也并非高枕无忧，必须考虑到远程调用失败、序列化失败、运行时异常等场景返回 null 的情况。
```

10. 【`推荐`】防止 _NPE_，是程序员的基本修养，注意 _NPE 产生的场景_：
    1）返回类型为基本数据类型，return 包装数据类型的对象时，**自动拆箱**有可能产生 NPE。  
```
反例：public int f() { return Integer 对象}， 如果为 null，自动解箱抛 NPE。
```

    2） **数据库的查询结果**可能为 null。  
    3） **集合里的元素**即使 isNotEmpty，取出的数据元素也可能为 null。  
    4） **远程调用返回对象**时，一律要求进行空指针判断，防止 NPE。  
    5） 对于 Session 中获取的数据，建议 NPE 检查，避免空指针。  
    6） **级联调用** obj.getA().getB().getC()；一连串调用，易产生 NPE。
    ```
    正例：使用 JDK8 的 Optional 类来防止 NPE 问题。
    ```

**白话**
```
很有价值，值得遵守。
```

11. 【`推荐`】定义时区分 _unchecked/checked 异常_，避免直接抛出 new RuntimeException()，更不允许抛出 Exception 或者 Throwable，应使用**有业务含义的自定义异常**。
推荐业界已定义过的自定义异常，如：DAOException / ServiceException 等。

12. 【`参考`】在代码中使用“*抛异常*”还是“*返回错误码*”，对于**公司外的 HTTP/API 开放接口**必须使用“**错误码**”；
而**应用内部**推荐**异常抛出**；**跨应用间 RPC 调用**优先考虑使用 _Result 方式_，
**封装 isSuccess() 方法、“错误码”、“错误简短信息”**。
```
说明：关于 RPC 方法返回方式使用 Result 方式的理由：
    1）使用抛异常返回方式，调用方如果没有捕获到就会产生运行时错误。
    2）如果不加栈信息，只是 new 自定义异常，加入自己的理解的 error message，对于调用端解决问题的帮助不会太多。
    如果加了栈信息，在频繁调用出错的情况下，数据序列化和传输的性能损耗也是问题。
```

**白话**
```
很有价值，值得遵守。
```

13. 【`参考`】避免出现*重复的代码*（Don’t Repeat Yourself），即 _DRY 原则_。
```
说明：随意复制和粘贴代码，必然会导致代码的重复，在以后需要修改时，需要修改所有的副本，容易遗漏。必要时抽取共性方法，或者抽象公共类，甚至是共用模块。
正例：一个类中有多个 public 方法，都需要进行数行相同的参数校验操作，这个时候请抽取：
    private boolean checkParam(DTO dto) {...}
```


#### (二) 日志规约
1. 【`强制`】应用中不可直接使用日志系统（Log4j、Logback）中的 API，而应依赖使用**日志框架 SLF4J 中的 API**，使用*门面模式的日志框架*，有利于维护和各个类的日志处理方式统一。
```
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    private static final Logger logger = LoggerFactory.getLogger(Abc.class);
```

2. 【强制】日志文件推荐至少保存 15 天，因为有些异常具备以“周”为频次发生的特点。

3. 【强制】应用中的**扩展日志**（如打点、临时监控、访问日志等）**命名**方式：appName_logType_logName.log。
logType:日志类型，推荐分类有 stats/desc/monitor/visit 等；logName:日志描述。
这种命名的好处：通过文件名就可知道**日志文件属于什么应用，什么类型，什么目的**，也有利于归类查找。
```
正例：mppserver 应用中单独监控时区转换异常，如： mppserver_monitor_timeZoneConvert.log
说明：推荐对日志进行分类，如将错误日志和业务日志分开存放，便于开发人员查看，也便于通过日志对系统进行及时监控。
```

4. 【强制】对 _trace/debug/info_ 级别的日志输出，必须使用条件输出形式或者使用**占位符**的方式。
```
说明：logger.debug("Processing trade with id: " + id + " symbol: " + symbol);
如果日志级别是 warn，上述日志不会打印，但是会执行字符串拼接操作，
如果 symbol 是对象，会执行 toString() 方法，浪费了系统资源，执行了上述操作，最终日志却没有打印。
正例：（条件）
    if (logger.isDebugEnabled()) {
        logger.debug("Processing trade with id: " + id + " symbol: " + symbol);
    }
正例：（占位符）
    logger.debug("Processing trade with id: {} symbol : {} ", id, symbol);
```

5. 【强制】避免*重复打印日志*，浪费磁盘空间，务必在 log4j.xml 中设置 additivity=false。
```
正例：<logger name="com.taobao.dubbo.config" additivity="false">
```

6. 【`强制`】**异常信息**应该包括两类信息：**案发现场信息**和**异常堆栈信息**。
如果不处理，那么通过关键字 _throws_ 往上抛出。
```
正例：logger.error(各类参数或者对象 toString + "_" + e.getMessage(), e);
```

7. 【`推荐`】谨慎地*记录日志*。生产环境禁止输出 debug 日志；有选择地输出 _info_ 日志；
如果使用 warn 来记录刚上线时的业务行为信息，一定要注意**日志输出量的问题**，避免**把服务器磁盘撑爆**，并记得及时删除这些观察日志。
```
说明：大量地输出无效日志，不利于系统性能提升，也不利于快速定位错误点。
记录日志时请思考：这些日志真的有人看吗？看到这条日志你能做什么？能不能给问题排查带来好处？
```

8. 【`参考`】可以使用 _warn_ 日志级别来记录**用户输入参数错误**的情况，避免用户投诉时，无所适从。
注意*日志输出的级别*， _error_ 级别只记录**系统逻辑出错、异常**等重要的错误信息。
如非必要，请不要在此场景打出 error 级别。

**白话**
```
很有价值，值得遵守。
```



### 三、MySQL 数据库
#### (一) 建表规约
1. 【强制】表达*是与否*概念的字段，必须使用 **is_xxx** 的方式命名，数据类型是 unsigned tinyint （1 表示是，0 表示否）。
```
说明：任何字段如果为非负数，必须是 unsigned。
正例：表达逻辑删除的字段名 is_deleted，1 表示删除，0 表示未删除。
```

2. 【强制】*表名、字段名*必须使用*小写字母*或数字，禁止出现数字开头，禁止两个下划线中间只出现数字。
数据库字段名的修改代价很大，因为无法进行预发布，所以字段名称需要慎重考虑。
```
正例：getter_admin，task_config，level3_name
反例：GetterAdmin，taskConfig，level_3_name
```

3. 【强制】*表名*不使用*复数名词*。
```
说明：表名应该仅仅表示表里面的实体内容，不应该表示实体数量，对应于 DO 类名也是单数形式，符合表达习惯。
```

4. 【强制】禁用*保留字*，如 desc、range、match、delayed 等，请参考 MySQL 官方保留字。

5. 【`强制`】**主键索引名**为 **pk_字段名**；**唯一索引名**为 **uk_字段名**；**普通索引名**则为 **idx_字段名**。
```
说明：pk_ 即 primary key；uk_ 即 unique key；idx_ 即 index 的简称。
```

6. 【强制】*小数类型*为 decimal，禁止使用 float 和 double。
```
说明：float 和 double 在存储的时候，存在精度损失的问题，很可能在值的比较时，得到不正确的结果。
如果存储的数据范围超过 decimal 的范围，建议将数据拆成整数和小数分开存储。
```

8. 【`强制`】**varchar** 是可变长字符串，不预先分配存储空间，长度不要超过 5000，
如果存储长度大于此值，定义字段类型为 text，独立出来一张表，用主键来对应，避免影响其它字段索引效率。

9. 【`强制`】表必备三字段：**id, gmt_create, gmt_modified**。
```
说明：其中 id 必为主键，类型为 unsigned bigint、单表时自增、步长为 1。
gmt_create, gmt_modified 的类型均为 date_time 类型。
```

10. 【推荐】*表的命名*最好是加上“业务名称_表的作用”。
```
正例：tiger_task / tiger_reader / mpp_config
```

11. 【推荐】*库名*与应用名称尽量一致。

12. 【推荐】如果修改字段含义或对字段表示的状态追加时，需要及时更新*字段注释*。

13. 【推荐】*字段*允许适当*冗余*，以*提高查询性能*，但必须考虑*数据一致*。冗余字段应遵循：  
    1）不是频繁修改的字段。  
    2）不是 varchar 超长字段，更不能是 text 字段。
```
正例：商品类目名称使用频率高，字段长度短，名称基本一成不变，
可在相关联的表中冗余存储类目名称，避免关联查询。
```

14. 【`推荐`】**单表行数**超过 **500 万行**或者**单表容量**超过 **2GB**，才推荐进行**分库分表**。
```
说明：如果预计三年后的数据量根本达不到这个级别，请不要在创建表时就分库分表。
```

15. 【参考】合适的*字符存储长度*，不但节约*数据库表空间*、节约*索引存储*，更重要的是**提升检索速度**。
```
正例：如下表，其中无符号值可以避免误存负数，且扩大了表示范围。
```


#### (二) 索引规约
1. 【`强制`】**业务上具有唯一特性**的字段，即使是多个字段的组合，也必须建成**唯一索引**。
```
说明：不要以为唯一索引影响了 insert 速度，这个速度损耗可以忽略，但提高查找速度是明显的；
另外，即使在应用层做了非常完善的校验控制，只要没有唯一索引，根据墨菲定律，必然有脏数据产生。
```

2. 【强制】超过三个表禁止 join。需要 join 的字段，数据类型必须绝对一致；多表关联查询时，保证被关联的字段需要有索引。
```
说明：即使双表 join 也要注意表索引、SQL 性能。
```

3. 【强制】在 _varchar_ 字段上建立索引时，必须指定*索引长度*，没必要对全字段建立索引，根据实际文本区分度决定索引长度即可。
```
说明：索引的长度与区分度是一对矛盾体，一般对字符串类型数据，长度为 20 的索引，区分度会高达 90% 以上，可以使用 count(distinct left(列名, 索引长度))/count(*)的区分度来确定。
```

4. 【`强制`】页面搜索严禁**左模糊**或者全模糊，如果需要请走**搜索引擎**来解决。
```
说明：索引文件具有 B-Tree 的最左前缀匹配特性，如果左边的值未确定，那么无法使用此索引。
```

5. 【推荐】如果有 _order by_ 的场景，请注意利用*索引的有序性*。order by 最后的字段是*组合索引*的一部分，并且放在*索引组合顺序的最后*，避免出现 file_sort 的情况，影响查询性能。
```
正例：where a=? and b=? order by c; 索引：a_b_c
反例：索引中有范围查找，那么索引有序性无法利用，如：WHERE a>10 ORDER BY b; 索引 a_b 无法排序。
```

6. 【`推荐`】利用**覆盖索引**来进行查询操作，避免**回表**。
```
说明：如果一本书需要知道第 11 章是什么标题，会翻开第 11 章对应的那一页吗？
目录浏览一下就好，这个目录就是起到覆盖索引的作用。
正例：能够建立索引的种类：主键索引、唯一索引、普通索引，而覆盖索引是查询的一种效果，用 explain 的结果，extra 列会出现：using index。
```

7. 【推荐】利用延迟关联或者子查询优化超多*分页场景*。
```
说明：MySQL 并不是跳过 offset 行，而是取 offset+N 行，然后返回放弃前 offset 行，返回 N 行，
那当 offset 特别大的时候，效率就非常的低下，要么控制返回的总页数，要么对超过特定阈值的页数进行 SQL 改写。
正例：先快速定位需要获取的 id 段，然后再关联：
    SELECT a.* FROM 表 1 a, (select id from 表 1 where 条件 LIMIT 100000,20 ) b where a.id=b.id
```

8. 【推荐】*SQL 性能优化*的目标：至少要达到 range 级别，要求是 ref 级别，如果可以是 consts 最好。
```
说明：
1）consts 单表中最多只有一个匹配行（主键或者唯一索引），在优化阶段即可读取到数据。
2）ref 指的是使用普通的索引（normal index）。
3）range 对索引进行范围检索。
反例：explain 表的结果，type=index，索引物理文件全扫描，速度非常慢，这个 index 级别比较 range 还低，与全表扫描是小巫见大巫。
```

9. 【`推荐`】建**组合索引**的时候，*区分度最高*的**在最左边**。
```
正例：如果 where a=? and b=? ，a 列的几乎接近于唯一值，那么只需要单建 idx_a 索引即可。
说明：存在非等号和等号混合判断条件时，在建索引时，请把等号条件的列前置。如：where a>? and b=? 那么即使 a 的区分度更高，也必须把 b 放在索引的最前列。
```

10. 【`推荐`】防止因*字段类型不同*造成的隐式转换，导致**索引失效**。

11. 【`参考`】**创建索引**时避免有如下极端误解：  
    1）**宁滥勿缺**。误认为一个查询就需要建一个索引。  
    2）**宁缺勿滥**。误认为索引会消耗空间、严重拖慢更新和新增速度。  
    3）抵制唯一索引。误认为业务的唯一性一律需要在应用层通过“先查后插”方式解决。


#### (三) SQL 语句
1. 【`强制`】不要使用 count(列名)或 count(常量)来替代 **count(\*)**，count(\*)是 SQL92 定义的标准统计行数的语法，跟数据库无关，跟 NULL 和非 NULL 无关。
```
说明：count(*)会统计值为 NULL 的行，而 count(列名)不会统计此列为 NULL 值的行。
```

4. 【强制】使用 ISNULL() 来判断是否为 NULL 值。注意：NULL 与任何值的直接比较都为 NULL。

5. 【强制】 在代码中写*分页查询*逻辑时，若 count 为 0 应直接返回，避免执行后面的分页语句。

6. 【强制】不得使用*外键与级联*，一切**外键概念**必须在**应用层**解决。

7. 【强制】禁止使用*存储过程*，存储过程难以调试和扩展，更没有移植性。

8. 【`强制`】*数据订正*时，删除和修改记录时，要先 select，避免出现误删除，确认无误才能执行更新语句。

9. 【推荐】*in 操作*能避免则避免，若实在避免不了，需要仔细评估 in 后边的集合元素数量，控制在 1000 个之内。

10. 【参考】如果有全球化需要，所有的字符存储与表示，均以 **UTF-8 编码**，注意字符统计函数的区别。
```
说明：如果要使用表情，那么使用 utfmb4 来进行存储，注意它与 UTF-8 编码的区别。
```


#### (四) ORM 映射
1. 【`强制`】在表查询中，一律不要使用 * 作为查询的字段列表，**需要哪些字段必须明确写明**。
```
说明：1）增加查询分析器解析成本。2）增减字段容易与 resultMap 配置不一致。
```

2. 【强制】*POJO 类的布尔属性*不能加 is，而数据库字段必须加 is_，要求在 resultMap 中进行字段与属性之间的映射。
```
说明：参见定义 POJO 类以及数据库字段定义规定，在 <resultMap> 中增加映射，是必须的。
在 MyBatis Generator 生成的代码中，需要进行对应的修改。
```

3. 【强制】不要用 resultClass 当返回参数，即使所有类属性名与数据库字段一一对应，也需要定义；反过来，每一个表也必然有一个与之对应。
```
说明：配置映射关系，使字段与 DO 类解耦，方便维护。
```

4. 【强制】sql.xml **配置参数**使用：*#{}*，#param# 不要使用 ${} 此种方式容易出现 _SQL 注入_。

6. 【强制】不允许直接拿 HashMap 与 Hashtable 作为*查询结果集*的输出。
```
说明：resultClass=”Hashtable”，会置入字段名和属性值，但是值的类型不可控。
```

7. 【`强制`】*更新数据表记录*时，必须同时更新记录对应的 *gmt_modified* 字段值为**当前时间**。

8. 【推荐】不要写一个大而全的数据更新接口，传入为 POJO 类，不管是不是自己的目标更新字段，都进行 update table set c1=value1,c2=value2,c3=value3; 这是不对的。
执行 SQL 时，**不要更新无改动的字段**，一是易出错；二是效率低；三是增加 binlog 存储。

9. 【参考】*@Transactional 事务*不要滥用。事务会影响数据库的 QPS，
另外使用事务的地方需要考虑各方面的**回滚方案**，包括**缓存回滚、搜索引擎回滚、消息补偿、统计修正等**。

10. 【参考】\<isEqual>中的 compareValue 是与属性值对比的常量，一般是数字，表示相等时带上此条件；\<isNotEmpty>表示不为空且不为 null 时执行；\<isNotNull>表示不为 null 值时执行。



### 四、工程结构
#### (一) `应用分层`
1. 【`推荐`】图中默认上层依赖于下层，箭头关系表示可直接依赖，如：开放接口层可以依赖于 Web 层，也可以直接依赖于 Service 层，依此类推：  
![应用分层](./应用分层.jpg)

 * **开放接口**层：可直接**封装 Service 方法**暴露成 _RPC 接口_；通过 **Web** 封装成 _HTTP 接口_；进行**网关安全控制、流量控制**等。
 * 终端显示层：各个端的模板渲染并执行显示的层。当前主要是 velocity 渲染，JS 渲染， 移动端展示等。
 * **Web** 层：主要是对**访问控制**进行转发，各类基本**参数校验**，或者不复用的业务简单处理等。
 * **Service** 层：相对**具体的业务逻辑服务**层。
 * **Manager** 层：**通用业务处理**层，它有如下特征：  
    1） **对第三方平台封装**的层，预处理返回结果及转化异常信息；  
    2） 对 **Service 层通用能力**的下沉，如缓存方案、中间件通用处理；  
    3） 与 DAO 层交互，对多个 DAO 的组合复用。
 * **DAO** 层：**数据访问**层，与底层 MySQL、Oracle、HBase 进行数据交互。
 * **外部接口**或**第三方平台**：包括*其它部门 RPC 开放接口，基础平台，其它公司的 HTTP 接口*。

**白话**
```
很有价值，值得遵守。
```

2. 【`参考`】 （*分层异常处理*规约）在 **DAO 层**，产生的异常类型有很多，无法用细粒度的异常进行 catch，使用 catch(Exception e) 方式，并 throw new DAOException(e)，不需要打印日志，因为*异常*在 **Manager/Service 层**一定需要**捕获并打到日志文件**中去，如果同台服务器再打日志，浪费性能和存储。  
在 **Service 层**出现异常时，必须**记录出错日志**到磁盘，尽可能带上**参数信息**，相当于保护*案发现场*。  
如果 **Manager 与 Service 层**同机部署，日志方式与 DAO 层处理一致，如果是单独部署，则采用与 Service 一致的处理方式。  
**Web 层**绝不应该继续往上抛异常，因为已经处于顶层，无继续处理异常的方式，如果意识到这个异常将导致页面无法正常渲染，那么就应该直接跳转到友好错误页面，加上**友好的错误提示信息**。  
**开放接口层**要将*异常*处理成**错误码和错误信息**方式返回。

**白话**
```
很有价值，值得遵守。
```

3. 【`参考`】*分层领域模型*规约：
 * DO（Data Object）：与*数据库表*结构一一对应，通过 _DAO_ 层向上传输*数据源对象*。
 * DTO（Data Transfer Object）：*数据传输对象*，*Service 和 Manager* 层向外传输的对象。
 * BO（Business Object）：*业务对象*。可以由 *Service* 层输出的*封装业务逻辑的对象*。
 * Query：数据查询对象，各层接收上层的查询请求。注：超过 2 个参数的查询封装，禁止使用 Map 类来传输。
 * VO（View Object）：*显示层对象*，通常是 _Web_ 向模板渲染引擎层传输的对象。


#### (二) 二方库依赖
1. 【强制】定义 GAV 遵从以下规则：  
    1） GroupID 格式：com.{公司/BU}.业务线.[子业务线]，最多 4 级。
```
说明：{公司/BU} 例如：alibaba/taobao/tmall/aliexpress 等BU一级；子业务线可选。
正例：com.taobao.jstorm 或 com.alibaba.dubbo.register
```

    2） ArtifactID 格式：**产品线名-模块名**。语义不重复不遗漏，先到中央仓库去查证一下。  
```
正例：dubbo-client / fastjson-api
```

    3） Version：详细规定参考下方。

2. 【强制】*二方库版本号命名*方式：主版本号.次版本号.修订号  
    1） 主版本号：当做了不兼容的 API 修改，或者增加了能改变产品方向的新功能。  
    2） 次版本号：当做了向下兼容的功能性新增（新增类、接口等）。  
    3） 修订号：修复 bug，没有修改方法签名的功能加强，保持 API 兼容性。
```
说明：注意：起始版本号必须为：1.0.0，而不是 0.0.1 正式发布的类库必须先去中央仓库进行查证，使版本号有延续性，正式版本号不允许覆盖升级。
```

3. 【`强制`】*线上应用*不要依赖 _SNAPSHOT 版本_（安全包除外）。
```
说明：不依赖 SNAPSHOT 版本是保证应用发布的幂等性。另外，也可以加快编译时的打包构建。
```

4. 【强制】*二方库的新增或升级*，保持除功能点之外的其它 *jar 包仲裁*结果不变。如果有改变，必须明确评估和验证，建议进行 dependency:resolve 前后信息比对，如果仲裁结果完全不一致，那么通过 dependency:tree 命令，找出差异点，进行 <excludes> 排除 jar 包。

5. 【强制】二方库里可以定义*枚举类型*，参数可以使用枚举类型，但是*接口返回值*不允许使用枚举类型或者包含枚举类型的 POJO 对象。

6. 【`强制`】依赖于一个*二方库群*时，必须定义一个**统一的版本变量**，避免**版本号不一致**。
```
说明：依赖 springframework-core,-context,-beans，它们都是同一个版本，可以定义一个变量来保存版本：${spring.version}，定义依赖的时候，引用该版本。
```

7. 【`强制`】禁止在*子项目的 pom 依赖*中出现相同的 GroupId 和 ArtifactId，但是不同的 Version。
```
说明：在本地调试时会使用各子项目指定的版本号，但是合并成一个 war，只能有一个版本号出现在最后的 lib 目录中。
可能出现线下调试是正确的，发布到线上却出故障的问题。
```

8. 【`推荐`】所有 pom 文件中的*依赖声明*放在 <dependencies> 语句块中，所有*版本仲裁*放在 <dependencyManagement> 语句块中。
```
说明：<dependencyManagement> 里只是声明版本，并不实现引入，因此子项目需要显式的声明依赖，version 和 scope 都读取自父 pom。
而 <dependencies> 所有声明在主 pom 的 <dependencies> 里的依赖都会自动引入，并默认被所有的子项目继承。
```

9. 【推荐】二方库不要有*配置项*，最低限度地不要再增加配置项。

10. 【参考】为避免*应用二方库的依赖冲突问题*，二方库发布者应当遵循以下原则：  
    1）**精简可控**原则。移除一切不必要的 API 和依赖，只包含 Service API、必要的*领域模型对象*、Utils 类、常量、枚举等。如果依赖其它二方库，尽量是 provided 引入，让二方库使用者去依赖具体版本号；无 log 具体实现，只依赖日志框架。  
    2）**稳定可追溯**原则。每个版本的变化应该被记录，二方库由谁维护，源码在哪里，都需要能方便查到。除非用户主动升级版本，否则公共二方库的行为不应该发生变化。


#### (三) 服务器
1. 【`推荐`】*高并发服务器*建议调小 *TCP 协议的 time_wait 超时时间*。
```
说明：操作系统默认 240 秒后，才会关闭处于 time_wait 状态的连接，
在高并发访问下，服务器端会因为处于 time_wait 的连接数太多，可能无法建立新的连接，所以需要在服务器上调小此等待值。
正例：在 linux 服务器上请通过变更 /etc/sysctl.conf 文件去修改该缺省值(秒)：net.ipv4.tcp_fin_timeout = 30
可能会使应用线程被打爆
```

2. 【`推荐`】调大*服务器所支持的最大文件句柄数*（File Descriptor，简写为 fd）。
```
说明：主流操作系统的设计是将 TCP/UDP 连接采用与文件一样的方式去管理，即一个连接对应于一个 fd。
主流的 linux 服务器默认所支持最大 fd 数量为 1024，当并发连接数很大时很容易因为 fd 不足而出现“open too many files”错误，导致新的连接无法建立。
建议将 linux 服务器所支持的最大句柄数调高数倍（与服务器的内存数量相关）。
```

3. 【`推荐`】给 JVM 设置-XX:+HeapDumpOnOutOfMemoryError 参数，让 JVM 碰到 *OOM 场景*时输出 **dump 信息**。
```
说明：OOM 的发生是有概率的，甚至有规律地相隔数月才出现一例，出现时的现场信息对查错非常有价值。
```

4. 【参考】服务器内部重定向使用 forward；外部重定向地址使用 URL 拼装工具类来生成，
否则会带来 URL 维护不一致的问题和潜在的安全风险。



### 五、`安全规约`
1. 【`强制`】隶属于*用户个人*的页面或者功能必须进行*权限控制校验*。
```
说明：防止没有做水平权限校验就可随意访问、修改、删除别人的数据，比如查看他人的私信内容、修改他人的订单。
```

2. 【`强制`】*用户敏感数据*禁止直接展示，必须对展示数据进行*脱敏*。
```
说明：查看个人手机号码会显示成：158****9119，隐藏中间 4 位，防止隐私泄露。
```

3. 【`强制`】用户输入的 *SQL 参数*严格使用*参数绑定*或者 METADATA 字段值限定，防止 **SQL 注入**，禁止字符串拼接 SQL 访问数据库。

4. 【`强制`】*用户请求*传入的任何*参数*必须做**有效性验证**。
忽略参数校验可能导致：
 * page size 过大导致内存溢出
 * 恶意 order by 导致数据库慢查询
 * 任意重定向
 * SQL 注入
 * 反序列化注入
 * 正则输入源串拒绝服务 ReDoS
```
说明：Java 代码用正则来验证客户端的输入，有些正则写法验证普通用户输入没有问题，
但是如果攻击人员使用的是特殊构造的字符串来验证，有可能导致死循环的结果。
```

5. 【`强制`】禁止向 HTML 页面输出*未经安全过滤或未正确转义的用户数据*。

6. 【`强制`】*表单、AJAX 提交*必须执行 _CSRF 安全过滤_。
```
说明：CSRF(Cross-site request forgery)跨站请求伪造是一类常见编程漏洞。
对于存在 CSRF 漏洞的应用/网站，攻击者可以事先构造好 URL，只要受害者用户一访问，后台便在用户不知情情况下对数据库中用户参数进行相应修改。
```

7. 【`强制`】在使用*平台资源*，譬如**短信、邮件、电话、下单、支付**，必须实现正确的*防重放限制*，
如**数量限制、疲劳度控制、验证码校验**，避免被**滥刷、资损**。
```
说明：如注册时发送验证码到手机，如果没有限制次数和频率，那么可以利用此功能骚扰到其它用户，并造成短信平台资源浪费。
```

8. 【`推荐`】**发贴、评论、发送即时消息**等*用户生成内容的场景*必须实现**防刷、文本内容违禁词过滤等风控策略**。



### 附 1：版本历史



### 附 2：本手册专有名词
1. POJO（Plain Ordinary Java Object）：在本手册中，POJO 专指只有 setter/getter/toString 的简单类，
包括 DO/DTO/BO/VO 等。
2. DO（Data Object）：本手册指数据库表一一对应的 POJO 类。
3. GAV（GroupId、ArtifactId、Version）：Maven 坐标，是用来唯一标识 jar 包。
4. OOP（Object Oriented Programming）: 本手册泛指类、对象的编程处理方式。
5. ORM（Object Relation Mapping）: 对象关系映射，**对象领域模型与底层数据之间的转换**，
本文泛指 iBATIS, MyBatis 等框架。
6. NPE（java.lang.NullPointerException）: 空指针异常。
7. SOA（Service-Oriented Architecture）: _面向服务架构_，它可以根据需求通过网络
对*松散耦合的粗粒度应用组件*进行分布式部署、组合和使用，有利于提升**组件可重用性，可维护性**。
8. 一方库：本工程内部子项目模块依赖的库（jar 包）。
9. 二方库：公司内部发布到中央仓库，可供公司内部其它应用依赖的库（jar 包）。
10. 三方库：公司之外的开源库（jar 包）。


