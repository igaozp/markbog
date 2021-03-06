#### 前言

前段时间阿里出了关于 Java 的 《阿里巴巴 Java 开发手册》，阿里作为国内 Java 技术领域内的带头者，其技术手册不管时对初学者还是从业者都是一份不可多得的材料。手册涉及大量的由一线开发人员总结的经验，我不可能将所有的内容读懂理解或者运用到实践中，这要涉及到大量的多个领域的工程实践。所以我将从一个初级或者中级的 Java 程序员的视角从手册中选取适当的内容进行归纳总结，同时由于内容比较多我将会分成多篇文章归纳。

#### 命名规范

变量或者函数命名也许是开发中最艰难的一个过程，这一部分并不教你如何命名，而是教你如何将变量或者函数名称变得既通俗易懂同时又符合规范。这里可以推荐一个网站也许可以解决你的命名烦恼 👉 [CODELF](https://unbug.github.io/codelf/)

1. 类名使用 `UpperCamelCase` （大驼峰）风格，除领域模型的相关命名如：`DO` `DTO` 等

2. 方法名、参数名、成员变量、局部变量统一使用 `lowerCamelCase` （小驼峰）风格

3. 接口类中的方法和属性不要加任何修饰符号（`public` 也不要加），以保持代码的简洁性，并附加有效的 `Javadoc` 注释，尽量不要在接口中定义 变量

4. `Service / DAO` 层方法命名规范

   {0}. 获取单个对象的方法用 `get` 做前缀
   {0}. 获取多个对象的方法用 `list` 做前缀
   {0}. 获取统计值的方法用 `count` 做前缀
   {0}. 插入的方法用 `save`（推荐）或 `insert` 做前缀
   {0}. 删除的方法用 `remove`（推荐）或 `delete` 做前缀
   {0}. 修改的方法用 `update` 做前缀

5. 领域模型命名规约

   {0}.  数据对象：`xxxDO`，`xxx` 即为数据表名
   {0}.  数据传输对象：`xxxDTO`，`xxx` 为业务领域相关的名称
   {0}.  展示对象：`xxxVO`，`xxx` 一般为网页名称
   {0}.  `POJO` 是 `DO / DTO / BO / VO` 的统称，禁止命名成 `xxxPOJO`

#### 格式规范

代码的格式规范可以在 IDE 里进行相应的设定，利用 IDE 的自动格式化便可以完成。这里的代码风格可能与你之前的习惯有一些出入，也许是有的地方没有注意到，或者习惯于另一种写法，最好从现在开始改变一些习惯，当完成过渡之后你会发现这会让你的代码更加条理，更加符合业内规范、更加优雅（雾

1. 大括号使用规范。如果是大括号内为空，则简洁地写成 {} 即可，不需要换行。如果 是非空代码块则：

   - 左大括号前不换行
   - 左大括号后换行
   - 右大括号前换行
   - 右大括号后还有 `else` 等代码则不换行；表示终止右大括号后必须换行

2.  左括号和后一个字符之间不出现空格；同样，右括号和前一个字符之间也不出现空 格

3. `if / for / while / switch / do` 等保留字与左右括号之间都必须加空格

4. 任何运算符左右必须加一个空格

5. 缩进采用 4 个空格，禁止使用 `tab` 字符。如果使用 `tab` 缩进，必须设置 1 个 `tab` 为 4 个空格。IDEA 设置 `tab` 为 4 个空格时， 请勿勾选 Use tab character

   ```java
   public static void main(String args[]) { 
       // 缩进 4 个空格
       String say = "hello"; 
       // 运算符的左右必须有一个空格 
       int flag = 0; 
       // 关键词 if 与括号之间必须有一个空格，括号内的 f 与左括号，0 与右括号不需要空格 
       if (flag == 0) {
   	    System.out.println(say); 
       }

   	// 左大括号前加空格且不换行；左大括号后换行 
       if (flag == 1) {
   	    System.out.println("world");
   	    // 右大括号前换行，右大括号后有 else，不用换行
   	} else { 
       	System.out.println("ok");
   	    // 在右大括号后直接结束，则必须换行 
       }
   }
   ```

6. 单行字符数限制不超过 120 个，超出需要换行，换行时遵循如下原则：

   - 第二行相对第一行缩进 4 个空格，从第三行开始，不再继续缩进
   - 运算符与下文一起换行
   - 方法调用的点符号与下文一起换行
   - 在多个参数超长，逗号后进行换行
   - 在括号前不要换行

   ```java
   正例：

   StringBuffer sb = new StringBuffer(); 
   //超过 120 个字符的情况下，换行缩进 4 个空格，并且方法前的点符号一起换行
   sb.append("zi").append("xin")... 
       .append("huang")... 
       .append("huang")... 
       .append("huang");

   反例：

   StringBuffer sb = new StringBuffer(); 
   //超过 120 个字符的情况下，不要在括号前换行
   sb.append("zi").append("xin")...append 
       ("huang");

   //参数很多的方法调用可能超过 120 个字符，不要在逗号前换行 
   method(args1, args2, args3, ...
       , argsX);
   ```

7. 方法参数在定义和传入时，多个参数逗号后边必须加空格

   ```java
   method("a", "b", "c");
   ```

8. IDE 的 text file encoding 设置为 UTF-8；IDE 中文件的换行符使用 Unix 格式，不要使用  Windows 格式

9. 方法体内的执行语句组、变量的定义语句组、不同的业务逻辑之间或者不同的语义 之间插入一个空行。相同业务逻辑和语义之间不需要插入空行，没有必要插入多行空格进行隔开

#### OOP 规范

这个没啥可说的，毕竟是无数人的踩坑经历，阅读全文并背诵（逃

1. 避免通过一个类的对象引用访问此类的静态变量或静态方法，无谓增加编译器解析成 本，直接用类名来访问即可

2. 所有的覆写方法，必须加 `@Override` 注解

3. 不能使用过时的类或方法

4. `Object` 的 `equals` 方法容易抛空指针异常，应使用常量或确定有值的对象来调用 `equals`

5. 所有的相同类型的包装类对象之间值的比较，全部使用 `equals` 方法比较

6. `POJO` 类必须写 `toString` 方法，如果继承了另一个 `POJO` 类，注意在前面加一下 `super.toString`

7. 当一个类有多个构造方法，或者多个同名方法，这些方法应该按顺序放置在一起， 便于阅读

8. 类内方法定义顺序依次是：公有方法或保护方法 > 私有方法 > `getter/setter` 方法

9. `setter` 方法中，参数名称与类成员变量名称一致，`this.成员名=参数名`

10. 循环体内，字符串的联接方式，使用 `StringBuilder` 的 `append` 方法进行扩展

11. `final` 可提高程序响应效率，声明成 `final` 的情况：
    
    - 不需要重新赋值的变量，包括类属性、局部变量
    - 对象参数前加 `final`，表示不允许修改引用的指向
    - 类方法确定不允许被重写

12. 类成员与方法访问控制从严：
    
    - 如果不允许外部直接通过 `new` 来创建对象，那么构造方法必须是 `private`
    - 工具类不允许有 `public` 或 `default` 构造方法
    - 类非 `static` 成员变量并且与子类共享，必须是 `protected`
    - 类非 `static` 成员变量并且仅在本类使用，必须是 `private`
    - 类 `static` 成员变量如果仅在本类使用，必须是 `private`
    - 若是 `static` 成员变量，必须考虑是否为 `final`
    - 类成员方法只供类内部调用，必须是 `private`
    - 类成员方法只对继承类公开，那么限制为 `protected`
    - 慎用 `Object` 的 `clone` 方法来拷贝对象，对象的 `clone` 方法默认是浅拷贝，若想实现深拷贝需要重写 `clone` 方法实现属性对象 的拷贝
    - 构造方法里面禁止加入任何业务逻辑，如果有初始化逻辑，请放在 `init` 方法中