# 一、java基础

### 1.JVM、JRE和JDK之间有什么区别

#### JVM

JVM是Java虚拟机的缩写。它是用来运行Java字节码文件的虚拟机（虚拟机实际上是一个应用软件）。JVM一般是由c或者c++来写成的，所以它有不同的实现。**JVM在各个操作系统上面的实现是不同的，但是相同的java代码，在各个操作系统上JVM上运行结果是一样的**。字节码在其中起到了关键的作用，这就是为什么java可以”一次编译，到处运行“的原理所在。我们平常用的最多的JVM是HotSpot VM。

#### JRE

JRE是Java Runtime Environment的缩写，即Java运行环境。顾名思义，任何用Java语言写成的程序都要在上面运行，如果没有这个运行环境，那么用Java写成的程序将无法运行。它包括了JVM和一些java的基础类库和基本组件。

#### JDK

JDK是Java Development Kit 的缩写，即Java 开发工具，它包含了JRE和编译器（javac）和一些工具（javadoc)。程序员必须依赖于JDK才能够写出java程序出来。我们常用的JDK版本通常是JDK-8。



### 2.Java八大基础数据类型有哪些？

* 整数类型：**int**（4字节）,**long**（8字节）,**short**（2字节）,**byte**（1字节）

* 浮点数类型：**float**（4字节），**double**（8字节）

* 字符类型：**char**(2字节)

* 布尔类型：**boolean**(长度不确定，厂商有不同实现)

**注意：**如果使用long类型的数据，那么一定要在数值后面加上**L**，不然会被解析成整数。



### 3.成员变量和局部变量的区别？

成员变量是属于类的，他可以被访问修饰符==public,private,protected==和==static==修饰。如果该成员变量用static修饰，那么他是属于类变量，随着对象的创建和销毁而创建和销毁。如果成员变量没有用static修饰，那么它就是实例变量。成员变量如果没有赋予初值，那么系统会自动赋予。

局部变量是在方法或者代码块里面的变量，他不能够用访问修饰符和static修饰，且局部变量如果后面的代码中需要用到，那么就必须设置初值，不然编译就会报错。局部变量随着方法的调用和销毁自动调用和销毁。



### 4.静态变量的作用？

静态变量是用static修饰的变量，它属于类变量。它可以被该类的所有对象共享，并且我们通常用==final==关键字来修饰它。



### 5.静态方法和实例方法有什么不一样？

在我们调用静态方法时，可以使用==类名.方法名==的方式，也可以使用==这个类的对象名.方法名==的方式。但是我们一般是不推荐使用后面的这种方式，因为这样容易造成混淆。因为静态方法是属于这个类的，而不是属于这个对象的。**所以我们在使用静态方法时是可以不创建对象的。**

同时静态方法只可以访问静态成员（静态变量和静态方法），而实例方法既可以访问静态成员，也可以访问实例成员（实例方法和实例变量）。



### 6.重载和重写的区别

#### 重载

重载是发生在同一个类里面。要求**方法名相同，参数类型不同，顺序不同，参数个数不同**，方法返回值和修饰符可以不同。重载可以发生在任何方法上，包括构造方法。

需要注意的是，**重载发生在编译期**，是编译器针对不同的参数来选择执行哪个方法。

#### 重写

重写一般发生在子类和父类之间。子类一般去重写父类的方法，要求**方法名相同，参数类型相同，顺序相同，参数个数相同。方法的返回类型必须小于等于父类的返回类型（如果父类方法返回的是==void==和==基本数据类型==，那么子类也必须返回相同的类型），抛出的异常范围必须小于等于父类抛出的异常范围，方法的修饰符必须要大于等于父类方法的修饰符**，这就是说如果父类的方法用==private==修饰，那么子类是无法重写父类的方法的。同时如果父类方法用==final==和==static==来修饰，子类也是无法重写父类的方法的。

需要注意的是，**重写发生在运行期**，是子类对父类方法的内部改造。



### 7.什么是可变长参数？

从Java5开始支持可变长参数，即在调用方法的时候可以允许传入不确定长度的参数。比如下面这个方法就可以传入0个或多个参数：

```java
public void function(String ... args){

}
```

另外，可变长参数只能放在参数列表中的最后一位，或者也可以可变长参数前面没有任何参数。如下面这个函数：

```java
public void function1(String str,String ... args){

}
```

如果固定参数的方法和可变长参数的方法发生重载了怎么办呢？编译器会优先选择固定参数的方法。

另外，**可变长参数实际上会被转换成一个数组。**



### 8.基本类型和包装类型的区别是什么？

* 如果是成员变量，那么基本类型有默认值，但是包装类型如果不赋值的话就是**null**。
* 如果是局部变量，那么基本类型存在于java虚拟机栈中的局部变量表里。如果是成员变量（且未被==static==修饰）,那么基本类型存在于java虚拟机的堆中。



### 9.自动装箱和拆箱了解过吗？原理是什么？

* **装箱**：将基本数据类型用他们对应的引用类型包装起来；
* **拆箱**：将引用类型转化成基本数据类型；

如下代码所示：

```java
Integer i = 10;     //装箱
int a = i;      //拆箱
```

原理：**装箱实际上是调用了包装类型的==valueOf()==方法，拆箱实际上是调用了==xxxValue()==方法。**

所以以上代码的本质是：

* ==Integer i = 10== 等价于 ==Integer.valueOf()==
* ==int a = i== 等价于 ==i.intValue()==

同时还需要注意的是：**应该避免频繁的装箱和拆箱，因为这样会影响系统的性能。**



### 10.包装类型的缓存机制了解过吗？

**java的基本数据类型的包装类型基本上都使用了缓存机制来提升性能。**

在java中，==**Byte,Integer,Long,Short**== 这四种包装类型都创建了数值为【-128,127】的数据，==Character== 则创建了数值为【0,127】的数据，==Boolean== 则直接返回 ==False== 或者 ==True==  。

Integer缓存源码如下：

```java
public static Integer valueOf(int i) {
   if (i >= IntegerCache.low && i <= IntegerCache.high)
       //如果是在-128~127之间，那么返回的是直接创建好的对象
       return IntegerCache.cache[i + (-IntegerCache.low)];    
   return new Integer(i);
}

private static class IntegerCache {
	static final int low = -128;
	static final int high;
    static final Integer cache[];
	static {
		int h = 127;
        cache = new Integer[(high - low) + 1];
        int j = low;
        for(int k = 0; k < cache.length; k++)
            cache[k] = new Integer(j++);
    }
}
```

其他类型的源码大同小异。如果超出范围内仍然会去创建新的对象。

两种浮点数的包装类型==Float== 和 ==Double== 并没有实现缓存机制。

```java
Integer i1 = 10;
Integer i2 = 10;
System.out.println(i1==i2);  //输出true

Float f1 = 333f;
Float f2 = 333f;
System.out.println(f1==f2);   //输出false

Double d1 = 1.2;
Double d2 = 1.2;
System.out.println(d1==d2);  //输出false
```

如下代码，输出的是false还是true呢？

```java
Integer i1 = 40;
Integer i2 = new Integer(40);
System.out.println(i1==i2);   
```

让我们来分析分析，第一行代码等价于 ==Integer.valueOf(40)==，使用的是缓存内的对象；第二行代码则会创建一个新的对象；所以两者实际上不是同一个对象。因此上面的输出应该是为 ==false==。

**记住：所有整型包装类对象之间值的比较，全部采用equals方法。**

在阿里巴巴开发手册中这样写道：

![image-20230307144512310](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230307144512310.png)

因此我们在开发时应该格外注意。



### 11.为什么浮点数在计算时会有精度丢失的风险？

```java
float a = 2.0f - 1.9f;
float b = 1.8f - 1.7f;
System.out.println(a==b);  //输出false
```

我们都知道，在计算机中数字是有二进制来表示的，因此他的宽度是有限的。在无限小数的存储上，无法精确表示，只能采用截断的方式，因此会出现精度丢失的风险。

#### 如何解决浮点数运算时精度丢失的问题？

使用==BigDecimal== 可以解决这个问题，不会造成精度丢失。通常情况下，大部分需要计算浮点数的场景（比如支付或涉及到钱的场景）都是通过BigDecimal来做的。



### 12.面向对象三大特征？

#### 封装

封装指的是把一个对象的状态信息（或者属性）隐藏在这个对象的内部，不允许外部直接访问我们的内部信息。但是可以提供一些方法来给外部来访问，如果外部访问不了的话，那么这个类就没有任何意义了。

#### 继承

不同类型的对象，相互之间有一些共同点，因此我们可以在使用已存在的类的定义作为基础建立新的类，该类可以使用父类的功能，可以拥有父类的属性。这样子就可以提高开发效率，提高代码的可用性。

关于继承需要记住以下几点：

* **子类可以拥有父类的所有属性和方法（包括私有的），**但是私有的属性和方法子类是不能够使用的，只是==拥有==。
* 子类可以有自己的属性和方法，即子类可以对父类进行拓展。

#### 多态

顾名思义，多态的意思是一个对象具有多种形态。具体的来说，就是**父类的引用指向子类的对象。**

多态的特点如下：

* 对象类型和引用类型之间是继承（类）/实现（接口）的关系。
* 引用类型变量发出的方法调用的到底是哪个类的方法，必须在运行期才能确定。
* 如果子类重写了父类的方法，那么真正执行的是子类的覆盖方法，如果没有重写，那么执行的是父类的方法。
* 多态不能调用“只在子类中存在而不在父类中存在”的方法。



### 13.接口和抽象类有什么区别？

#### 共同点

* 都不能被实例化。
* 都可以包含有抽象方法。

#### 区别

* 一个类只能继承一个抽象类，但是可以实现多个接口。

* 接口主要是对类的行为进行约束，实现了某个接口就说明有了接口具体的行为。抽象类主要用于代码复用，强调的是所属关系。

* 接口中的成员变量都是用==public stati final== 修饰的，不能被修改且必须有初始值，而抽象类的成员变量默认是==default== ，可在子类中被重新定义，也可以被重新赋值。

  

### 14.深拷贝和浅拷贝有什么区别？什么是引用拷贝？

#### 浅拷贝

浅拷贝会在堆上创建一个新的对象，不过如果原对象中的属性是引用类型的话，浅拷贝会直接复制内部对象的引用地址，也就是说拷贝对象和原对象共用同一个内部对象。

#### 深拷贝

深拷贝会完整地复制整个对象，包括这个对象中的内部对象。

#### 引用拷贝

**引用拷贝就是两个不同的引用指向同一个对象。**



### 15.Object类

#### Object类的常见方法有哪些？

Object类是所有类的父类，它主要提供了以下的方法：

```java
//用于返回当前运行时对象的Class对象，用final修饰，所以不允许子类重写
public final native Class<?> getClass()

//用于返回对象的哈希码
public native int hashCode()

//用于比较两个对象的内存地址是否相等
public boolean equals(Object obj)

//用于创建并返回当前对象的拷贝
protected native Object clone() throws CloneNotSupportedException;

//返回类的实例的名字的哈希码的16进制的字符串，建议所有的子类都重写该方法
public String toString();

//唤醒一个线程
public final native void notify();

//唤醒所有的线程
public final native void notifyAll();

//暂停线程的执行，并且释放锁,有下面三个方法：
public final native void wait(long timeout) throws InterruptedException;

public final void wait(long timeout, int nanos) throws InterruptedException;

public final void wait() throws InterruptedException;

//实例被垃圾回收器回收时进行的操作
protected void finalize() throws Throwable;
```

#### == 跟equals()的区别

**==**对于引用类型和基本数据类型是不同的：

* 对于基本数据类型，==比较的是值。
* 对于引用数据类型，==比较的是两个对象的内存地址。

equals()有两种使用方法：

* **类没有重写equals()方法**：通过比较两个对象时，等价于直接用“==”来比较两个对象，因为如果没有重写，那么调用的实际上是父类的equals()方法，而equals()方法的实现如下：

  ```java
  public boolean equals(Object obj) {
  	return (this == obj);
  }
  ```

* **类重写了equals()方法：**一般我们都重写这个方法，用来比较两个对象中的属性是否相等，如果相等，那么我们就返回true（即我们认为这两个对象相等）。



#### hashCode()

hashCode()的作用是获取哈希码（==int== 整数），这个哈希码的作用是为了知道某个对象在散列表中的位置。hashCode()是一个本地方法，是由c或者c++实现的，该方法通常是得到对象的内存地址然后转换成整数得来的。

#### 为什么在equals()方法时必须重写hashCode()方法？

我们在重写equal()方法时一般是用来判断两个对象是否是相等的。如果两个对象是相等的，那么他们的==hashCode==就必须相等。如果重写了equals()而不重写hashCode()方法，那么就有可能出现两个对象相等，但是他们的hashCode却不相等的情况，这是不对的。

简单的来说：

* 如果两个对象相等，那么它们的hashCode一定相等；
* 如果两个对象的hashCode相等，这两个对象并不一定相等，因为会存在哈希冲突；
* 如果两个对象的hashCode不相等，那么直接就认为这两个对象不相等。



### 16.String类

#### String、StringBuilder、StringBuffer的区别？

String是不可变的，因为它使用==final==关键字修饰字符串数组来保存字符串，因此可以将String理解为常量，**线程安全**。

StringBuilder是可变的，该类继承父类==AbstractStringBuilder==，使用字符串数组来保存字符串，但是没有对方法加上同步锁，因此是**线程不安全**的。

StringBuffer是可变的，它也是继承父类==AbstractStringBuilder==，使用字符串数组来保存字符串，但是它对方法加上了同步锁，因此是**线程安全**的。

总结下来就是说：

* **操作少量的数据**：用`String`；
* **单线程下操作大量数据**：用`StringBuilder`;
* **多线程下操作大量数据**：用`StringBuffer`;



#### 字符串拼接用“+”还是StringBuilder?

建议用**StringBuilder**。因为字符串通过“+”的方式进行拼接，实际上是调用了`StringBuilder`的`append`方法，拼接之后通过`toString`方法得到一个`String`对象。

另外需要注意的是，在循环内使用“+”进行字符串拼接的话，存在明显的缺陷：**编译器不会创建单个`StringBuilder`以复用，而是每次都会创建`StringBuilder`对象**。因此应该避免在循环内使用“+”进行字符串拼接，这样会导致创建过多的`StringBuilder`对象，从而影响性能。



#### String s1 = new String("abc");这句话创建了⼏个字符串对象？

答案是1个或2个。

底层原理分析：

```java
String str1 = "abc";    //在常量池中

String str2 = new String("abc");  //在堆上
```

对于第一行代码，当直接赋值时，“abc"会存储在字符串常量池中，此时的赋值操作就相当于创建0个或1个对象。原因如下：

* 如果此时在字符串常量池中已经存在“abc”，那么这个时候不会再创建对象，而是直接将引用赋值给str1。
* 如果此时在字符创常量池中不存在“abc"，那么这个时候就创建一个对象，并将引用赋值给str1。

对于第二行代码，此时会创建1个或2个对象。原因如下：

* 如果此时在字符串常量池中已经存在“abc”，那么就只会在堆内创建一个String对象。此过程中创建了1个对象。
* 如果此时在字符创常量池中不存在“abc"，那么会先在常量池中创建这样一个字符串，然后再执行new操作，会在堆中创建一个“abc"的字符串对象，并将引用赋值给str2。此过程中创建了2个对象。



#### intern方法有什么用？

该方法的作用是：**如果字符串s在字符串常量池中存在对应字面量，那么就返回这个字面量的地址；如果不存在，则创建一个对应的字面量，并返回该字面量的地址。**



#### String类型的变量做“+”运算时发生了什么？

对于不用`final`修饰的Stinge类型来说：

```java
String str1 = "str";    //字符串常量
String str2 = "ing";
String str3 = "str" + "ing";    //常量池中的对象
String str4 = str1 + str2;    //在堆上创建一个新的对象
String str5 = "string";      //常量池中的对象
System.out.println(str3 == str4);//false
System.out.println(str3 == str5);//true
System.out.println(str4 == str5);//false
```



在编译期可以确定值的字符串，**jvm会将其放入字符串常量池中，并且字符串常量在拼接时得到的字符串常量也会被放进字符串常量池中去。**这个得益于编译器的优化。

也就是说：对于`String str3 = "str" + "ing"`，编译器会优化成`String str3 = "string"`。

而对于`String str4 = str1 + str2`，编译器实际上是调用了`StringBuilder`的`append`方法来实现的，因此对于`String str4 = str1 + str2`，它实际上等价于：

```java
String str4 = new StringBuilder().append(str1).append(str2).toString();
```



而对于用`final`修饰的String类型来讲：

```java
final String str1 = "str";
final String str2 = "ing";
// 下⾯两个表达式其实是等价的
String c = "str" + "ing";// 常量池中的对象
String d = str1 + str2; // 常量池中的对象
System.out.println(c == d);// true
```

被`final`修饰的`String`会被编译器当做常量来处理，因为在编译期编译器就可以确定它的值。

如果编译器在编译器无法确定它的值，那么是无法被优化的，如下所示：

```java
final String str1 = "str";
final String str2 = getStr();   //str2在运行时才可以知道它的值
String c = "str" + "ing";// 常量池中的对象
String d = str1 + str2; // 在堆上创建的新的对象
System.out.println(c == d);// false
public static String getStr() {
	return "ing";
}
```

#### String类能被继承吗？为什么？

首先，String类被final修饰，所以它不能被继承。

原因：

* 效率性，String类作为最常用的类之一，禁止被继承和重写，可以提高效率。
* 安全性，String类中有很多调用底层的本地方法，调用了操作系统的API，如果方法可以重写，可能会被植入恶意代码，破坏程序。



#### String类常用的方法都有哪些？

* indexOf（）：返回指定字符的索引。
* spilt（）：分割字符串，返回一个分割后的字符串数组。
* charAt（）：返回指定索引处的字符。
* length（）：返回字符串的长度。
* substring（）：截取字符串。
* trim（）：去掉字符串两端的空白。
* equsl（）：字符串比较。
* toLowerCase（）：将字符串转成小写字母。
* toUpperCase（）：将字符串转成大写字母。
* replace（）：字符串替换。



### 17.Exception和Error有什么区别？

在java中，所有的异常都有一个共同的祖先，那就是`java.lang`包中的`Throwable`类。`Throwable`类有两个重要的子类：

* `Error`: 属于程序无法处理的错误。比如说：java虚拟机运行错误、虚拟机内存不够错误（outOfMemoryError）、类定义错误等（NoClassDefFoundError）等。发生这些错误时，java虚拟机一般会终止线程的运行。
* `Exception`：程序本身可以处理的异常。可以通过`catch`来进行处理。`Exception`一般又分为两类：**受检查异常**，必须处理，**不受检查异常**，可以不处理。

 

### 18.Checked EXception和 Unchecked Exception有什么区别？

Checked EXception即**受检查异常**，java代码在编译过程中，如果受检查异常没有被`catch`或者`throw`的话，就没有办法通过编译。

除了`RuntimeException`及其子类之外，其他`Exception`类及其子类都是**受检查异常**，常见的受检查异常有：`IO相关的异常`、`ClassNotFoundException`、`SQLException`等。 

`UnChecked Exception` 即**不受检查异常**，java代码在编译过程中，不处理异常也不会报错。

`RuntimeException`及其子类都属于不受检查异常，常见的有：

* `NullPointerException`（空指针异常）

* `ArrayIndexOutOfBoundsException`（数组越界异常）

* `ClassCastException`（类型转换异常）

* `IllegalArgumentException`（参数错误异常）

* `ArithmeticException`（算术异常）

  

### 19.Throwalbe类常用的方法有哪些？

* `String getMessage()`：返回异常发生时的简要信息。
* `String  toString()`：返回异常发生时的详细信息。
* `String getLocalizedMessage()`：返回异常对象的本地化信息。使⽤ Throwable 的⼦类覆盖这个⽅ 法，可以⽣成本地化信息。如果⼦类没有覆盖该⽅法，则该⽅法返回的信息与 getMessage() 返 回的结果相同。
* `void printStackTrack()`：在控制台上打印`Throwale`对象封装的信息。



### 20.try-catch-finally如何使用？

* `try块`：用于捕获异常。其后可以接0个或多个`catch`，如果没有`catch`，则必须跟`finally`块。
* `cathc块`：用于处理try捕获到的异常。
* `finally块`：无论是否捕获或处理异常，`finally`块里面的代码都会执行。**当在`try`或者`catch`中出现`return`，则`finally`将在方法返回之前执行。**

**不要再fianlly语句块中使用return！**当 try 语句和 finally 语句中都有 return 语句时，try 语句 块中的 return 语句会被忽略。这是因为 try 语句中的 return 返回值会先被暂存在⼀个本地变量中， 当执⾏到 finally 语句中的 return 之后，这个本地变量的值就变为了 finally 语句中的 return 返回值。



### 21.什么是反射？反射的优缺点？

反射机制允许我们在java代码运行时分析类以及执行类中的方法的能力。**通过反射你可以获取到任意一个类的所有属性和方法，你还可以调用这些方法和属性。**

反射可以使我们的代码更加灵活，它是各种框架的灵魂。

但是使用反射也增加了安全问题，破坏了封装性，同时反射的性能也要稍微差一点。

#### 获取Class对象的方法：

* **知道具体类的情况下可以使用：**

  ```java
  Class alunbarClass = TargetObject.class;
  ```

* **通过Class.forName()传入类的全路径获取：**

  ```java
  Class alunbarClass1 = Class.forName("cn.javaguide.TargetObject");
  ```

* **通过对象实例`instance.getClass()`获取：**

  ```java
  TargetObject o = new TargetObject();
  Class alunbarClass2 = o.getClass();
  ```

* **通过类加载器`xxxClassLoader.loadClass()`传入类路径获取:**

  ```java
  ClassLoader.getSystemClassLoader().loadClass("cn.javaguide.TargetObject");
  ```

  





### 22.什么是序列化？什么是反序列化？

**如果我们需要持久化java对象，比如说将java对象保存到文件中，或者在网络中传输java对象，这些都需要用到序列化。**

* **序列化**：将对象转换成二进制字节流的过程。
* **反序列化：**将二进制字节流转化成对象的过程。



### 23.如果有些字段不想被序列化怎么办？

可以使用关键字`transient`。`transient`关键字的作用是：**阻止变量序列化**。

关于`transient`还有几点需要注意：

* `transient`只修饰变量，不修饰方法和类。
* `transient`修饰的变量，在反序列化都会变成类型的默认值。比如说`int`类型的变量反序列后的值为`0`。
* `static`变量不属于任何对象，无论有没有`transient`修饰，均不会被序列化。



### 24.java IO流了解过吗？

IO即input/output，输入和输出。数据从外部设备输入到内存称为**输入**，从内存输出到外部设备（文件、数据库、远程主机）称为**输出**。IO流在java中按照方向可以分为`输入流`和 `输出流`，按照数据处理的方式可以分为`字节流`和`字符流`。

java IO流的40多个类都是从以下四个抽象基类派生出来的：

* **InputStream/Reader:** 所有输入流的基类，前者是字节输入流，后者是字符输入流。
* **OutputStream/Writer:** 所有输出流的基类，前者是字节输出流，后者是字符输入流。



### 25.I/O流为什么还要分为字节流和字符流呢？

因为字节流要转换成字符流，过程很耗时。如果你必须使用字符流，但是你只得到了字节流，那么你必须经历这个转换，其中的编码也很容易出现问题。

所以就把字符流单独作为了一部分，从而提高使用字符流的效率。



### 26.java中常见的三种IO模型

**BIO** ：

属于**同步阻塞IO模型**。是指一个线程在进行IO操作时，如果数据没有准备好，会一直阻塞，直到数据准备好为止。

在这种情况下，一个线程只能处理一个IO操作，如果有很大的IO并发，那就需要创建多个线程来处理，这会导致系统资源的浪费。



**NIO** ：

属于**IO多路复用模型** ， 也有人说是**同步非阻塞IO模型**。 

同步非阻塞IO模型中，应用程序会一直发起 read调用，等待数据从内核空间拷贝到用户空间的这段时间里，线程依然是阻塞的，直到准备好数据。这样的IO模型存在问题：**应用程序不断进行IO系统调用轮询数据是否已经准备好，这个操作是非常消耗CPU资源的**。 

IO多路复用模型中，线程首先发起select调用，询问内核数据是否准备好，等内核把数据准备好了，用户线程再发起 read 调用。read 调用的过程（数据从内核空间 -> 用户空间）还是阻塞的。

目前支持 IO 多路复用的系统调用，有 select，epoll 等等。select 系统调用，目前几乎在所有的操作系统上都有支持。

- **select 调用** ：内核提供的系统调用，它支持一次查询多个系统调用的可用状态。几乎所有的操作系统都支持。
- **epoll 调用** ：linux 2.6 内核，属于 select 调用的增强版本，优化了 IO 的执行效率。

**IO 多路复用模型，通过减少无效的系统调用，减少了对 CPU 资源的消耗。** 



**AIO** ：

属于**异步IO模型** 。线程操作完成之后，会立即返回，不会堵塞在那里。当后台准备好数据后，操作系统会通知相应的线程来进行后续的操作。



另外面经的答案：

* BIO：线程发起IO请求，不管内核是否准备好IO操作，从发起请求起，线程一直阻塞，直到操作完成。

* NIO：线程发起IO请求，立即返回。内核在做好IO操作准备之后，通过调用注册回调函数通知线程做IO操作，线程开始阻塞，直到操作完成。

* AIO：线程发起IO请求，立即返回。内存做好IO操作准备之后，做IO操作，直到操作完成或者失败，通过调用注册回调函数通知线程做IO操作完成或者失败。

  

### 27.类的实例化顺序？

父类静态代码块/静态域 -> 子类静态代码块/静态域  -> 父类非静态代码块 ->  父类构造器  ->子类非静态代码块 ->子类构造器



### 28.java中创建对象有几种方式？

* 用new 语句来创建对象。
* 调用 对象的 clone() 方法。（浅拷贝）
* 利用反射机制。
* 利用反序列化。
* 使用Unsafe。



### 29.try-with-resources了解吗？

try-with-resources是Java SE 7中引入的一种语法结构，用于确保在代码块结束时关闭资源，无论代码块是正常结束还是抛出异常。在try-with-resources结构中，资源必须实现java.lang.AutoCloseable或java.io.Closeable接口，这样在代码块结束时，可以自动调用资源的close()方法来关闭资源。

```java
try (BufferedReader br = new BufferedReader(new FileReader(file))) {
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    e.printStackTrace();
}

```



### 30.面向对象和面向过程的区别？

* **面向过程**：分析解决问题的步骤，然后用函数把这些步骤一步一步去实现，然后在使用的时候调用函数即可。
* **面向对象** ：把构成问题的事物分解成各个对象，用对象去描述某个事物在解决整个问题上的过程中发生的行为。更容易维护和复用，也更容易拓展。但是性能比较低。



### 31.为什么有了基本数据类型之后还要有包装类？

* 为了迎合java中“万物皆对象”的观点，所以让基本数据类型也有了包装类。

* 有了包装类之后，可以提供更丰富的操作，可以将数据存在在集合里面，因为集合里面存储的数据都是对象类型的。

  

### 32.请你讲一下lamada表达式？

Lambda表达式是Java 8引入的一种新的语言特性，它允许以更简洁、更函数式的方式来编写匿名函数。Lambda表达式本质上是一个函数式接口的实现，它可以**用于替代只有单一抽象方法的接口的匿名内部类**的写法。

Lambda表达式的语法格式如下：

```
rustCopy code(parameters) -> expression
或
(parameters) -> { statements; }
```

其中，parameters表示Lambda表达式的参数列表，可以为空或包含多个参数；expression或statements表示Lambda表达式的方法体，可以是一个表达式或一个代码块。

Lambda表达式可以在许多场合中使用，例如在**集合的遍历、排序、筛选**等操作中，简化了代码的编写，提高了代码的可读性和简洁性。Lambda表达式还可以与Java的函数式接口（Functional Interface）一起使用，用于实现回调、事件处理、并发编程等场景。

Lambda表达式的主要特点包括：

1. 简洁性：相比于传统的匿名内部类，Lambda表达式可以更加简洁地表示一个函数式接口的实现，减少了代码量。
2. 代码可读性：Lambda表达式通过提供更加直观的语法，可以使代码更加易读和易懂。
3. 函数式编程：Lambda表达式支持函数式编程，即将函数作为参数传递、将函数作为返回值返回、在函数中定义函数等高级用法，使得Java在函数式编程方面更加强大和灵活。





### 33.泛型中的extends和super的区别？

* `extends`：用于限定通配符可以接受的最上限的类型，即只能接受指定类型及其子类型。
* `super`：用于限定通配符可以接受的最下限的类型，即只能接受指定类型及其父类型。

```java
public class Animal {
    public static void main(String[] args) {
        List<? extends Animal> list1 = new ArrayList<Animal>();
        List<? extends Animal> list2 = new ArrayList<Mammal>();
        List<? extends Animal> list3 = new ArrayList<Fish>();

        List<? super Animal> list4 = new ArrayList<Animal>();
        List<? super Animal> list5 = new ArrayList<Object>();

    }
}

class Fish extends Animal{}
class Mammal extends Animal{ }
```

```java
public class Box<T extends Number> {
    private T content;

    public Box(T content) {
        this.content = content;
    }

    public T getContent() {
        return content;
    }

    public void setContent(T content) {
        this.content = content;
    }

    // 使用 extends 限定通配符，表示类型参数 T 必须是 Number 或 Number 的子类
    public void printNumber(Box<? extends Number> box) {
        Number content = box.getContent();
        System.out.println("Number: " + content);
    }

    // 使用 super 限定通配符，表示类型参数 T 必须是 Number 或 Number 的父类
    public void setNumber(Box<? super Number> box, Number content) {
        box.setContent(content);
    }
}

```

















# 二、java集合

### 1.什么是java集合？

java集合，也叫作容器，主要由两大接口派生而来，一个是`Collection`接口，**主要用于存放单一元素**；一个是`Map`接口，主要**用于存放键值对**。对于`Collection`接口，下面又有三个子接口：`Set`，`List`，`Queue`。

![image-20230314225236447](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230314225236447.png)



![image-20230314225314698](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230314225314698.png)

### 2.说说List,Set,Queue,Map四者的区别？

* `List`: 存储元素是有序的，可重复的。

* `Set`: 存储元素是无序的，不可重复的。

* `Queue`: 按照特定的排队顺序，有序的，可重复的。

* `Map` : 存储key-value键值对，key是无序的，不可重复的,value是无序的，可重复的。

  

### 3.说说集合底层的数据结构？

#### List

* `ArrayList` : Object[] 数组。
* `LinkedList` : 双向链表（ JDK1.6之前为循环链表，JDK 1.7取消了循环）。
* `Vector` : Object[] 数组。

 #### Set

* `HashSet` （无序，唯一）: 基于`HashMap` 实现，底层基于`HashMap` 来保存元素。
* `LinkedHashSet` : 是`HashSet`的子类，内部通过`LinkedHashMap` 来实现。
* `TreeSet` （有序，唯一）: 红黑树（自平衡的排序二叉树）。

#### Queue

* `PriortyQueue` : Object[] 数组来实现二叉堆。
* `ArrayQueue` : Object[] 数组+双指针。

#### Map

* `HashMap` : JDK1.8以前是**数组加链表**来实现的，数组是`HashMap` 的主体，链表是为了解决哈希冲突而存在的（“拉链法”解决冲突）；JDK1.8以后是**数组+链表+红黑树** 来实现的，当链表长度大于阈值（默认为8）时，会将链表转化为红黑树，以减少搜索时间。（将链表转化成红黑树之前会先判断数组的长度是否大于等于64，如果不大于等于，那么会先对数组进行扩容，而不是转化为红黑树）。
* `HashTable` : 数组+链表来实现的，数组是`HashTable` 的主体，链表则是为了解决哈希冲突而存在的。
* `LinkedHashMap` : 底层基于`HashMap` ,只不过是在数组+链表+红黑树的基础上，多了一条双向链表，使得上面的结构可以保持键值对的插入顺序。同时通过对链表进⾏相应的操作，实现 了访问顺序相关逻辑。
* `TreeMap` : 红黑树（自平衡的排序二叉树）



### 4.如何选用集合？

**需要存键值对时**：

* 需要排序用`TreeMap`
* 不需要排序用`HashMap`
* 需要保证线程安全用`ConcurrentHashMap`

**需要存单一元素时：** 

* 需要保证元素唯一就选`TreeSet` 或`HashSet`
* 不需要保证元素唯一就选`ArrayList` 或`LinkedList`

### 5.ArrayList 和 Vector的区别？

* `ArrayList` 是`List` 的主要实现类，底层用Object[] 数组存储，**适合频繁的查找工作，线程不安全**。
* `Vector` 是`List` 的古老实现类，底层用Object[] 数组存储，**线程安全**。

 

### 6.ArrayList 和 LinkedList 的区别？

* **是否线程安全** ：两者都是线程不安全的。
* **底层数据结构** ： ArrayList 是 Object类型的数组，LinkedList 使用的是**双向链表**（JDK1.6之前为循环链表，JDK1.7之后取消了循环）。
* **插入、删除元素的位置** ：`ArrayList` 采用数组存储，如果插入在最后一位，那么时间复杂度是`O(1)`，但是如果要在某个位置插入或删除元素，那么会涉及到元素的移动，时间复杂度是`O(n)` 。`LinkedList` 采用链表存储，如果要在头尾插入或删除，时间复杂度是`O(1)`，但是要在指定位置插入或删除，那么需要先移动到指定的位置，因此时间复杂度是`O(n)` 。
* **是否支持随机访问** ：`ArrayList` 支持随机访问，`LinkedList` 不支持。
* **内存空间占用** ：`LinkedList` 每一个元素会比`ArrayList` 多占用内存空间，因为每一个节点都要存储直接前驱和直接后继和数据部分；`ArrayList` 内存空间浪费主要在于列表结尾会预留一定的空间。



### 7.说一说ArrayList 扩容机制？

以无参方法创建`ArrayList` 时，实际上初始化的是一个空的数组，当真正对数组添加元素时，才真正分配容量。即向数组中添加第一个元素时，数组容量扩为10。

当添加元素时，如果容量不够，那么会先扩容（**一般是扩容为原来数组长度的1.5倍**），然后进行原数组的拷贝。因此是很消耗性能的。



### 8.Queue和Deque的区别？

`Queue`是单端队列，只能从一端插入元素（称为队尾），从另一端删除元素（称为对头），遵循先进先出原则。

Queue 扩展了 Collection 的接⼝，根据 因为容量问题⽽导致操作失败后处理⽅式的不同 可以分为 两类⽅法: ⼀种在操作失败后会抛出异常，另⼀种则会返回特殊值。

![image-20230315142341261](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230315142341261.png)

`Deque` 是双端队列，在队列两端都可以插入或者删除元素。

Deque 扩展了 Queue 的接⼝, 增加了在队⾸和队尾进⾏插⼊和删除的⽅法，同样根据失败后处理 ⽅式的不同分为两类。

![image-20230315142517087](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230315142517087.png)

事实上， Deque 还提供有 push() 和 pop() 等其他⽅法，可⽤于模拟栈。

### 9.HashMap和HashTable的区别？

* `HashMap` 是非线程安全的，`HashTable`是线程安全的（因为内部方法基本都使用`synchronized`关键字修饰）
* `HashMap`效率高，`HashTable`效率低，因此现在已经弃用了。
* `HashMap` 可以存储 null 的 key 值，并且只能存储一个，null作为值可以存储多个；`HashTable` 不可以存储null 键和 null值。
* 如果不给定初始容量，`HashMap` **默认初始化大小是16，后面每次扩容，都会变为原来的2倍**。`HashTable`默认大小则为11，之后每次扩充，都会变成原来的2n+1；如果给定初始容量，**那么`HashMap` 会将其扩充为2的幂次方大小**。`HashTalbe`则会使用原来的大小。
* `HashMap` 底层是**数组+链表+红黑树**，`HashTable`底层是**数组+链表**。



### 10.HashMap和TreeMap的区别？

TreeMap 和 HashMap 都继承⾃ **AbstractMap** ，但是需要注意的是 TreeMap 它还实现了 **NavigableMap** 接⼝和 **SortedMap** 接口。

实现`NavigableMap` 接口让`TreeMap` 有了对集合内元素搜索的能力。



实现`SortedMap` 接口让`TreeMap` 有了对集合中的元素根据key 排序的能力。



### 11.HashSet如何检查重复？

当把对象加入到`HashSet`中时，`HashSet` 会先根据对象的 hashcode 值来判断加入对象的位置，同时也会和其他加入的对象的 hashcode 值做比较，如果没有相同的hashcode 值，`HashSet` 会假设该对象没有重复出现。但是如果发现有重复的 hashcode值，那么就会调用 equals() 方法来检查 hashcode 相等的对象是否真的相等。如果两者相同，`HashSet` 就不会让它加入成功。



### 12.HashMap的长度为什么是2的幂次方？

目的是为了让`HashMap `存储高效，尽量减少碰撞，也就是要尽量把数据分配均匀。

Hash值的范围值是 -2147483648 到 2147482647 ,前后加起来大概有40亿的映射空间，只要哈希表映射得比较均匀，一般是不会出现冲突的。但问题是一个40亿长度的数组，内存是放不下的，所以我们还要**对数组的长度进行取模运算**，**得到的余数才是要存放的位置**。这个数组下标的计算方法是 **（n-1）& hash** 。 其中n是数组的长度。

**取余(%)操作中如果除数是 2 的 幂次则等价于与其除数减⼀的与(&)操作（也就是说 hash%length==hash&(length-1)的前提是 length 是 2 的 n 次⽅；）** 。并且使用二进制操作 & ，相比于 % 能更加提高效率，这就是为什么说HashMap的长度是2的幂次方。



### 13.HashMap的底层实现？

#### JDK1.8之前

底层数据结构是：**数组+链表** 的形式。HashMap通过 key 的 `hashcode` 经过扰动函数处理后得到 hash 值，然后通过 `(n-1)& hash` 得到存放元素的位置下标（这里的 n 指的是 数组的长度），如果当前存在元素的话，就判断该元素与要存入的元素的 hash 跟key是否相同，如果相同的话，直接覆盖，不相同的话就通过拉链法来解决。

所谓的扰动函数就是 HashMap 中的 `hash()` 方法。使用`hash() ` 方法可以防止一些实现的比较差的 `hashCode()` 方法，从而减少碰撞的概率。

JDK1.7 的`hash() `  方法：

```java
static int hash(int h) {
    // This function ensures that hashCodes that differ only by
    // constant multiples at each bit position have a bounded
    // number of collisions (approximately 8 at default load factor).
    h ^= (h >>> 20) ^ (h >>> 12);
    return h ^ (h >>> 7) ^ (h >>> 4);
}
```

JDK 1.8中的 `hash()` 方法：

```java
static final int hash(Object key) {
	int h;
    // key.hashCode()：返回散列值也就是hashcode
    // ^ ：按位异或
    // >>>:⽆符号右移，忽略符号位，空位都以0补⻬
    return (key == null) ? 0 : (h = key.hashCode()) ^ (h >>> 16);
}
```

JDK 1.8 的`hash()` 方法比 1.7 的性能要好不少。

**1.7链表插入使用的是头插法** 。



#### JDK 1.8之后

相比于之前的版本，JDK 1.8在解决哈希冲突的时候有了一些改变。当链表长度大于阈值（默认为8）（将链表转换成红⿊树前会判断，如果当前数组的⻓度⼩于 64，那么会选择先进⾏数组扩容，而 不是转换为红⿊树）时，将链表转化为红黑树，以减少搜索时间。

**1.8链表插入使用的是尾插法** 。因为1.8中插入key和value需要判断链表元素个数，所以需要遍历链表统计链表元素个数，所以正好就使用尾插法。



### 14.HashMap多线程导致死循环问题？

JDK1.8之前，在并发环境下，HashMap采用**头插法** 插入节点，这样会形成循环链表，因此会造成死循环。JDK 1.8之后，采用**尾插法** 插入节点，但是任然会存在数据丢失的问题。所以我们推荐使用`ConcurrentHashMap` 。



### 15.HashMap有哪几种遍历方式？

从大的方向来说，可以分为4类：

1. 迭代器（Iterator） 方式遍历
2. For Each 方式遍历
3. Lamada表达式遍历（JDK 1.8+）
4. Stream API 遍历（JDK 1.8+）

但是具体又划分为以下7种：

* 使用**迭代器 EntrySet** 方式遍历：

  ```java
  Iterator<Map.Entry<Integer, String>> iterator = map.entrySet().iterator();
  while (iterator.hasNext()) {
      Map.Entry<Integer, String> entry = iterator.next();
      System.out.println(entry.getKey());
      System.out.println(entry.getValue());
  }
  ```

* 使用**迭代器 KeySe**t 方式遍历：

  ```java
  Iterator<Integer> iterator = map.keySet().iterator();
  while (iterator.hasNext()) {
      Integer key = iterator.next();
      System.out.println(key);
      System.out.println(map.get(key));
  }
  ```

* 使用 **ForEach EntrySet** :

  ```java
  for (Map.Entry<Integer, String> entry : map.entrySet()) {
      System.out.println(entry.getKey());
      System.out.println(entry.getValue());
  }
  ```

* 使用 **ForEach KeySet**：

  ```java
  for (Integer key : map.keySet()) {
      System.out.println(key);
      System.out.println(map.get(key));
  }
  ```

* **Lamada 表达式** 

  ```java
  map.forEach((key, value) -> {
      System.out.println(key);
      System.out.println(value);
  });
  ```

* **Stream API 单线程**

  ```java
  map.entrySet().stream().forEach((entry) -> {
      System.out.println(entry.getKey());
      System.out.println(entry.getValue());
  });
  ```

* **Stream API 多线程** 

  ```java
  map.entrySet().parallelStream().forEach((entry) -> {
      System.out.println(entry.getKey());
      System.out.println(entry.getValue());
  });                                                                                                                                                                       
  ```



### 16.ConcurrentHashMap 和 HashTable 的区别？

* **底层数据结构** ：JDK 1.7 的 `ConcurrentHashMap ` 底层采用 **分段的数组+链表** 实现，JDK1.8采用的数据结构跟 1.8 的`HashMap` 的是一样的，**数组+链表/红黑树** ；`HashTable` 则是 用**数组+链表** 的形式。
* **实现线程安全的方式** ：
  * 在JDK 1.7 的时候，`ConcurrentHashMap` 对整个数组桶进行**分组分段**（`Segment`，分段锁） ，每一把锁只锁其中的一部分数据，多线程访问容器里不容的数据段的数据，就不会存在锁竞争，提高并发访问率。
  * 到了JDK 1.8的时候，`ConcurrentHashMap ` 已经抛弃了 `Segment` 的概念，而是直接用 `Node` 数组+链表+红黑树的数据结构来实现，**并发控制使用`synchronized` 和CAS 来操作**。
  * `HashTalbe` ：使用`synchronized` 来保证线程安全，效率非常低下。当一个线程访问同步方法时，其他线程也访问同步方法，这个时候可能会进入阻塞或者轮询状态，如使用 put 方法来添加元素，这个时候另外的线程不能用put 来添加元素，也不能用 get 来获取元素。

![image-20230319215531549](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230319215531549.png)

`ConcurrentHashMap` 是由 `Segment` 数据结构和 `HashEntry` 构成。

`Segment` 数组中的每个元素包含一个小数组，这个小数组中的每个元素如果后面发生冲突则会变为链表。



![image-20230319220738736](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230319220738736.png)

JDK 1.8 的`ConcurrentHashMap` 采用 **Node 数组+ 链表/红黑树** 。不过，Node 只用于链表的情况，红黑树的情况需要使用 **TreeNode** ，当链表达到一定成都时，会转化成红黑树。



### 17.ConcurrentHashMap 的具体实现方式

#### JDK 1.8之前

首先将数据分为一段一段（就是 “segment”）的存储，然后给每个数据段分配一把锁，当一个线程占用锁访问其中一个数据段时，那么其他线程也可以访问其他的数据段。

`Segment` 继承了`ReentranLock` ，所以 **`Segment` 是一个可重入锁**，扮演锁的角色。一个 `ConcurrentHashMap` 包含一个`Segment` 数组，`Segment`的个数一旦初始化就不能被改变。`Segment` 数组的大小默认是16，也就是说同时支持16个线程并发写。

#### JDK 1.8之后

取消`Segment`分段锁，采用 `Node+ CAS + synchronized` 来保证并发安全。跟`HashMap` 1.8的结构类似，都是**数组+链表+红黑二叉树** 。java 8在链表超过阈值（8）时，会将链表转化为红黑树。

在java 8中，锁粒度更细，`synchronized` 只锁定当前链表或红黑二叉树的首节点，这样只要hash不冲突，就不会产生并发，就不会影响到其他Node的读写，效率大幅提升。



### 18.JDK1.7 和JDK 1.8的ConcurrentHashMap实现有什么不同？

* **线程安全的实现方式** ：JDK 1.7使用 `Segment` 来保证安全，`Segment` 继承自 `ReentranLock` 。JDK1.8 采用 `Node + CAS +synchronized` 保证线程安全，锁粒度更细，`synchronized` 只锁住当前链表或红黑二叉树的头结点。
* **Hash碰撞方法** ：JDK 1.7采用拉链法，JDK 1.8采用拉链法+红黑二叉树。
* **并发度** ：JDK 1.7最大并发度是 `segment` 的个数，默认是16个。JDK 1.8最大并发度是 Node数组的大小，并发度更大。



### 19.解决哈希冲突的方法有哪些？

* **链地址法** ：将哈希桶设计成链表或其他数据结构，当发生哈希冲突时，将冲突的键值对添加到对应哈希桶的链表中。
* **开发地址法** ：当发生哈希冲突时，不再使用相同哈希桶，而是在哈希表的其他位置寻找空的哈希桶，直到找到一个合适的位置。
  * 线性探测（Linear Probing）：当发生哈希冲突时，沿着哈希表的线性序列向后寻找空闲哈希桶，直到找到一个空闲位置。
  * 二次探测（Quadratic Probing）：当发生哈希冲突时，按照二次探测的公式向后寻找空闲哈希桶，直到找到一个空闲位置。
  * 双重哈希（Double Hashing）：当发生哈希冲突时，使用第二个哈希函数计算出一个增量，将哈希桶的位置向后移动增量个位置，直到找到一个空闲位置。

* **再哈希法** ：当哈希冲突发生频繁时，可以重新设计哈希函数，或者使用另一个哈希函数进行再哈希，以期望减少冲突的发生。



### 20.Collection和Collections有什么区别？

* Colletction是最基本的集合接口，它派生了三大子接口，list,set,queue。
* Colletcions是一个包装类，它包含各种有关集合操作的静态方法（对集合的搜索、排序、线程安全化等）。此类不能实例化，就像一个工具类一样，服务与Collection框架。



### 21.hashmap的扩容机制？

1. hashmap**初始化**时会指定初始化大小以及扩展阈值，如果不指定就使用默认值为null。

2. 当向hashmap中**存值**时，

   如果为**空**就开始第一次扩容，创建初始化数组大小，默认为16，

   如果链表当前**长度**大于8且数组长度大于64时，将链表转为红黑树结构，

   如果添加的元素达到了**阈值的0.75**，就进行扩容（默认加载因子是0.75，比如16的容量，就会在16*0.75=12的时候进行扩容）

   **扩容使用resize方式**，每次扩容都是之前的两倍，是使用新数组代替原=原来的旧数组，将原数组的数据迁移到新数组中使用尾插法。

 



### 22.说说hashmap的put方法？

1. 根据key通过哈希算法与与运算得出数组下标。

2. 如果数组下标位置元素为空，则将key好value封装成Entry对象（JDK1.7是Entry对象，JDK1.8是Node对象）并放入该位置。

3. 如果数组小标不为空：则要分情况讨论：

   a. 如果是jdk 1.7,则先判断是否需要扩容，如果扩容就进行扩容，如果不用扩容就生成entry对象，并使用头插法添加到当前位置的链表中。

   b. 如果是jdk 1.8，则会先判断当前位置上的Node类型，看是红黑树Node，还是链表Node。

   ​	i. 如果是红黑树Node，则key和value封装成一个红黑树节点并添加到红黑树中去，在这个过程中会判断红黑树是否存在当前

   ​		key，如果存在，则只是更新value。

   ​	ii. 如果是链表的Node，则将key和value封装到一个链表Node并通过尾插法插入到最后的位置上，同时还会判断是否存在相		同的key，如果存在就只更新value。插入到链表后，会判断当前链表个数，如果大于等于8，则会将该链表转化为红黑树



# 三、多线程

### 1.什么是进程？什么是线程？

* **进程** ：进程是程序的一次执行过程，是操**作系统分配资源的最小单位**， 进程是动态的。
* **线程** ：线程跟进程类似，是一个比进程更小的执行单位，是**操作系统调度资源的最小单位**，一个进程可以有多个线程，所以线程也被称为轻量级的进程。**一个java程序的运行是 main线程和其他线程同时运行。**

### 2.说说线程和进程的关系？

从 JVM角度来看，一个进程可以有多个线程，多个线程共享进程里的堆和方法区资源，每个线程有自己独立的虚拟机栈、本地方法栈和程序计数器。

总结：线程是进程划分为更小的运行单位。线程和进程的最大不同在于基本上进程是独立的，但是线程却不一定，有可能线程之间会相互影响。**线程执行开销小，但不利于资源的管理和保护，进程相反。**



### 3.并发和并行的区别？

* **并发** ：两个或两个以上的作业在**同一时间段**执行。 
* **并行** ：两个或两个以上的作业在**同一时刻** 执行。



### 4.同步和异步的区别？

* **同步** ：一个进程在执行某个请求的时候，若该请求需要一段时间才能返回，那么这个进程会一直等待下去，直到收到返回信息才继续执行下去。**同步是阻塞模式。** 
* **异步** ：异步是指进程不需要一直等下去，而是继续执行下面的操作，不管其他进程的状态。当有消息返回时系统会通知进程继续处理，这样就可以提高执行的效率。**异步是非阻塞模式。** 

对同步的理解：比如说客户端给服务端发送请求，在等待服务端响应的请求时，客户端不做其他的事情。当服务端做完了才返回给客户端。这样的话需要客户端一直等待，对用户很不友好。

对异步的理解：比如说客户端给服务端发送请求，在等待服务端响应的请求时，客户端可以去做其他的事情，这样既节约了时间，也提高了效率。



### 5.说说线程的声生命周期和状态？

从操作系统层面上来讲，线程有5种状态：**创建，就绪，运行，阻塞，终止。** 

从java层面来讲，有以下6种：

* **NEW** ：初始状态，线程被创建出来但是没有被调用`start()`。
* **RUNNALBE** ：运行状态，线程被调用了，即使用方法`start()` 。
* **BLOCKED** ：阻塞状态，需要等待锁释放。
* **WAITING** ：等待状态，表示该线程需要等待别的线程做出一些特定的动作（通知或中断）。
* **TIME_WAITING** ：超时等待状态，可以在指定的时间后自行返回而不是像WAITING那样。
* **TERMINATED** ：终止状态，表示该线程已经运行完毕。



### 6.什么是上下文切换？

线程在执行过程中会有自己的运行条件和状态（简称上下文），比如说提到的程序计数器，栈等。当线程切换时，需要保存当前线程的上下文，留着线程下次调用CPU的时候恢复现场。并加载下一个线程的上下文。这就是上下文切换。



### 7.什么是线程死锁？产生死锁的必要条件是什么？如何预防和避免死锁？

死锁：多个线程同时被阻塞，他们中的一个或多个都在等待某个资源被释放。由于线程无限期的被阻塞，所以程序不可能正常终止。

举个例子，线程A和线程B都需要对方手里的资源才能运行，但是双方都不释放资源，从而相互等待，进入死锁状态。

产生死锁的四个必要条件是：

* **互斥条件** ：该资源任意时刻只能由一个线程占用。
* **请求和保持条件** ：一个线程因请求资源而阻塞时，对已占有资源保持不放。
* **不剥夺条件** ：线程已占有的资源在未使用完之前不得被其他线程强行剥夺，只有自己使用完毕后才释放资源。
* **循环等待条件** ：若干个线程之间形成一种头尾相接的循环等待资源的关系。

那么如何预防死锁呢？破坏死锁的产生的必要条件即可：

* **破坏请求和保持条件** ：一次性申请所有资源。
* **破坏不剥夺条件** ：占用部分资源的线程如果在申请不到别的资源时，可以将已占有的资源主动释放。
* **破坏循环等待条件** ：按照一定的顺序来申请资源，比如说，申请资源的时候顺序，释放资源的时候反序。

那么如何避免死锁呢？

避免死锁就是在对资源进行分配时，借助于算法（比如说银行家算法）对资源分配进行评估，使其进入安全状态。



### 8.sleep()方法和wait()方法对比

**共同点** ：两者都可以暂停线程的执行。

**区别** ：

* **sleep()** **没有释放锁**，**但是 wait()方法释放了锁**。
* sleep() 方法用于暂停线程，wait() 方法一般用于线程之间的交互/通信。
* sleep() 方法执行完成后，会自动苏醒。但是 wait() 方法执行完后，线程不会自动苏醒，需要调用 notify() 或者 notifyAll() 方法来唤醒线程。
* sleep() 方法是 **Thread 类**的方法，而 wait() 方法是 **Object 类**的方法。



### 9.可以直接调用Thread类中的 run() 方法吗？

new一个 Thread，线程进入了新建状态。调用 start() 方法，会启动一个线程并让它进入到就绪状态，当分配到时间片后就可以直接运行了。start() 方法会准备相应的工作，然后自动去执行 run() 方法，这才是真正的多线程工作。

但是，如果直接运行 run() 方法，那么会被当成一个普通的方法去执行，不是开启多线程。



### 10.什么是线程池？为什么要使用线程池？

顾名思义，线程池就是管理一系列线程的资源池。当有任务要处理时，直接从线程池中获取线程来处理，处理完之后线程并不会被销毁，而是等待下一个任务。

为什么要使用线程池？

* **降低资源消耗** ：通过重复利用已经创建好的线程降低线程创建和销毁造成的消耗。
* **提高响应速度** ：当任务到达时，任务不需等到线程创建就能立即执行。
* **提高线程的可管理性** ：线程是稀缺资源，如果无限制的创建，不仅会消耗系统资源，还会降低系统的稳定性，使用线程池可以进行统一的分配，调优和监控。



### 11.如何创建线程池

**方式一：通过`ThreadPoolExecutor` 构造函数来创建。** 

![image-20230320233715751](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230320233715751.png)

**方式二 ：通过 `Executor` 框架的工具类`Executor` 来创建** 。

java中的线程池主要有以下类型：

1. **固定线程数线程池（FixedThreadPool）**：该线程池维护固定数量的线程，当有任务提交时，如果线程池中的线程都在执行任务，新提交的任务会被放入队列中等待执行，直到有空闲线程。
2. **可缓存线程池（CachedThreadPool）**：该线程池的线程数可以根据任务的数量动态调整，线程数不固定，如果有任务提交时，如果有空闲线程则直接使用，如果没有空闲线程则创建新的线程执行任务，而当线程空闲时间较长时，线程池会自动回收线程。
3. **单线程线程池（SingleThreadExecutor）**：该线程池只维护一个线程，所有提交的任务都会按照顺序依次执行，适合需要顺序执行的任务场景。
4. **定时任务线程池（ScheduledThreadPool）**：该线程池用于执行定时任务和周期性任务，可以指定任务的执行时间、延迟时间和执行周期。
5. **自定义线程池**：除了上述几种类型的线程池外，Java还支持通过ThreadPoolExecutor类来自定义线程池，可以根据业务需求自行配置线程池的参数，例如核心线程数、最大线程数、队列类型、拒绝策略等。





### 12.线程池的参数？

* `corePoolSize` ：核心线程数。线程池维护的最小线程数量，核心线程数在创建后不会被回收。
* `maximumPoolSize` ：线程池允许创建的最大线程数。
* `keepAliveTime` ：空闲线程存活时间。
* `unit` ：空闲线程存活时间的单位。
* `workQueue` ：工作队列。存放待执行任务的队列。
* `threadFactory` ：线程工厂。创建线程的工厂，可以设定线程名，线程编号等。
* `handler` ：拒绝策略。当线程池线程数已满，并且工作队列达到限制时，新提交的任务就会使用拒绝策略来处理。



### 13.线程池处理任务的流程了解吗？

![image-20230322002519249](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230322002519249.png)

1. 如果当前线程数<核心线程数，那么会新创建一个线程来执行任务。

2. 如果当前线程数 > =核心线程数，但是 小于 最大线程数，那么任务会被放置到任务队列中。

3. 如果当前任务队列已满，但是当前运行线程数小于最大线程数，那么会创建一个线程来执行任务。

4. 如果当前运行线程数量已经等于最大线程数了，那么当前的任务会被拒绝。

   

### 14.线程池的拒绝策略有哪些？

* **AbortPolicy（默认）**：直接抛出RejectedExecutionException异常，阻止新任务的提交。
* **CallerRunsPolicy**：将任务回退给提交任务的线程去执行，即由提交任务的线程自己执行新提交的任务。
* **DiscardPolicy**：直接丢弃新提交的任务，不做任何处理。
* **DiscardOldestPolicy**：丢弃队列中最早提交的任务，然后将新提交的任务加入队列。
* **自定义拒绝策略**：可以通过实现RejectedExecutionHandler接口来自定义拒绝策略，根据业务需求自行处理无法接受新任务的情况。



### 15.线程池常用的阻塞队列有哪些？

* ArrayBlockingQueue：基于数组实现的有界阻塞队列，按照先进先出（FIFO）的顺序进行存取。

* LinkedBlockingQueue：基于链表实现的可选有界或无界阻塞队列，按照先进先出（FIFO）的顺序进行存取。可以指定容量大小，也可以不指定，默认为无界。搭配使用的线程池是`FixedThreadPool` 和 `SingleThreadExcutor` 。**因为不限制大小，所以如果任务很多，那么会不断放到队列中，可能会造成OOM。**

* SynchronousQueue：不存储元素的阻塞队列，每个插入操作必须等待一个相应的删除操作，用于直接传递任务的情况。搭配使用的线程池是`CachedThreadPool` 。

* PriorityBlockingQueue：带有优先级的无界阻塞队列，元素按照优先级进行排序。



### 16.synchronized是什么？有什么用？

`synchronized` 是java中的一个关键字，翻译成中文是同步的意思。主要问题是**解决多个线程之间访问资源的同步性**，可以保证被它修饰的**方法或代码块**在任意时刻只能有一个线程执行。



### 17.如何使用 synchronized？

* **修饰实例方法** ：给当前对象实例加锁，进入同步代码块前获得当前对象实例的锁。**锁住的是当前对象实例。**

  ```java
  synchronized void method() {
      //业务代码
  }
  ```

* **修饰静态方法** ：给当前类加锁，进入同步代码块前需要获得当前类的锁。**锁住的是当前类。**

  ```java
  synchronized static void method() {
      //业务代码
  }
  ```

* **修饰代码块**： 对括号里指定的对象/类加锁：

  * `synchronized(object)` 表示进入同步代码块前要获得 **给定对象的锁**。

  * `synchronized(类.class)` 表示进入同步代码块前要获得 **给定 Class 的锁**。

    ```java
    synchronized(this) {
        //业务代码
    }
    ```



### 18.synchronized的底层原理知道吗？

* **synchronized修饰代码块** ：使用的是 `monitorenter` 和`monitorexit` 指令。前者指向同步代码块开始的位置，后者指向同步代码块结束的位置。
* **synchronized修饰方法** ：使用 `ACC_SYNCHRONIZED` 标识，该标识表明该方法是一个同步方法。

两者的本质都是对对象监视器`monitor` 的获取。



### 19.JDK1.6 之后的 synchronized 底层做了哪些优化？

在早期的java版本中，`synchronized` 属于重量级锁，效率低下。这是因为监视器锁（monitor） 依赖于操作系统底层的`Mutex Lock` 来实现的。

在java 6之后，`synchronized` 引入了大量的优化，如偏向锁，轻量级锁，自旋锁，适应性自旋锁，锁消除，锁粗化等技术来减少操作的开销。

锁主要存在四种状态，依次是：**无锁状态，偏向锁状态，轻量级锁状态，重量级锁状态**。 他们会随着竞争的激烈而逐渐升级，注意锁只可以升级，不可以降级。这种策略是为了提高获得锁和释放锁的效率。

**多线程下`synchronized` 的加锁就是对同一个对象的对象头中的 mark word中的变量进行 CAS操作。**

* **偏向锁** ：针对于只有一个线程访问同步块的情况，该锁能够在进入同步块时，将锁对象标记为偏向锁，并且将对象头中的线程ID设置为当前线程的ID，这样下次再进来，无需再次获取锁。
* **自旋锁** ：当线程获取锁失败后，会尝试自旋一段时间（进行一个忙循环，让线程等待），等待锁的释放。
* **锁消除** ：对于代码中存在的一些无法竞争的锁，java虚拟机会对其进行锁消除，就是消除锁，避免无所谓的竞争。
* **轻量级锁** ：对于短时间内只有一个线程获取锁的情况，java虚拟机引入了轻量级锁的概念。当一个线程获取锁时，会将锁对象头部中的信息复制到线程栈帧的锁记录中，此时其他线程尝试获取锁时，需要先自旋等待，等待时间过长或者获取失败后，才会升级为重量级锁。
* **重量级锁** ：使用操作系统互斥量（mutex） 来实现的。当对所有锁的优化都失败时，将退回到重量级锁。



下面，我们再从实际场景出发，来具体说说锁升级的过程。

1. 一开始，没有任何线程访问同步块，此时同步块处于**无锁状态**。
2. 然后，线程1首先访问同步块，它以CAS的方式修改Mark Word，尝试加**偏向锁**。由于此时没有竞争，所以偏向锁加锁成功，此时Mark Word里存储的是线程1的ID。
3. 然后，线程2开始访问同步块，它以CAS的方式修改Mark Word，尝试加偏向锁。由于此时存在竞争，所以偏向锁加锁失败，于是线程2会发起撤销偏向锁的流程（清空线程1的ID），于是同步块从偏向线程1的状态恢复到了可以公平竞争的状态。
4. 然后，线程1和线程2共同竞争，它们同时以CAS方式修改Mark Word，尝试加**轻量级锁**。由于存在竞争，只有一个线程会成功，假设线程1成功了。但线程2不会轻易放弃，它认为线程1很快就能执行完毕，执行权很快会落到自己头上，于是线程2继续**自旋加锁**。
5. 最后，如果线程1很快执行完，则线程2就会加轻量级锁成功，锁不会晋升到重量级状态。也可能是线程1执行时间较长，那么线程2自旋一定次数后就放弃自旋，并发起锁膨胀的流程。届时，锁被线程2修改为**重量级锁**，之后线程2进入阻塞状态。而线程1重复加锁或者解锁时，CAS操作都会失败，此时它就会释放锁并唤醒等待的线程。



### 20.ReentrantLock是什么？

`ReentrantLock` 实现了`Lock` 接口，是一个可重入且独占式的锁，和`synchronized` 类似。不过`ReentrantLock` 更加灵活，更加强大，增加了轮询、超时、中断、公平锁和非公平锁等高级功能。

```java
public class ReentrantLock implements Lock, java.io.Serializable {}
```

![image-20230322153831634](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230322153831634.png)



`ReentrantLock` 默认使用非公平锁，也可以通过构造器来显式指定公平锁。

```java
// 传入一个 boolean 值，true 时为公平锁，false 时为非公平锁
public ReentrantLock(boolean fair) {
    sync = fair ? new FairSync() : new NonfairSync();
}
```



### 21.公平锁和非公平锁的区别？

* **公平锁** ：锁被释放后，先申请的线程先得到锁。性能较差，因为公平锁保证了时间上的绝对顺序。
* **非公平锁** ：锁被释放后，后申请的线程可能也会得到锁，是随机或者按照其他优先级排的，性能更好，但是可能造成有些线程永远无法获取锁。



### 22.synchronized跟ReentrantLock有什么区别？

1. **两者都是可重入锁** 

   可重入锁：线程可以在此获取自己的内部锁。比如一个线程获得了某个对象的锁，此时这个对象还没有释放锁，这个时候这个线程想要再次获得这个对象锁还是可以的。如下面代码所示：

   ```java
   public class ReentrantLockDemo {
       public synchronized void method1() {
           System.out.println("方法1");
           method2();
       }
   
       public synchronized void method2() {
           System.out.println("方法2");
       }
   }
   ```

   当一个线程执行`method1() `方法时，获得该对象实例的锁，在`method1()` 方法中又调用了`method2()` ,因为`synchronized` 是可重入锁，所以可以在此获得该对象实例的锁，所以不会发生死锁。

2. **synchronized依赖于JVM而reentrantLock依赖于API**

   `synchronized`依赖于底层的JVM，但是`ReentrantLock` 依赖于API层面（**需要`Lock()`和`unLock()` 方法配合 try/fianlly语句块来完成**）。

3. **reentrantLock比 synchronized多了一些功能**

   * **可实现公平锁** 。（synchronized是非公平锁）
   * **等待可中断** ：正在等待的线程可以放弃等待，转去处理别的事情。
   * **可实现选择性通知**（锁可以绑定多个条件） ：`synchronized`关键字与`wait()`和`notify()`/`notifyAll()`方法相结合可以实现等待/通知机制。`ReentrantLock`类当然也可以实现，但是需要借助于`Condition`接口与`newCondition()`方法。



### 23.可中断锁和不可中断锁有什么区别？

* **可中断锁** ：获取锁的过程可以被中断，不需要一直等到获取锁，可以去处理别的逻辑。`ReentrantLock` 就属于中断锁。
* **不可中断锁** ：获取锁的过程不可以被中断，只能等到获取锁了之后才能去处理别的逻辑。`synchronized` 就属于不可中断锁。





### 24.创建线程有哪几种方式？

* 通过**继承 Thread** 类。

  ```java
  public class Thread1 extends Thread {
      public static void main(String[] args) {
          Thread1 thread1 = new Thread1();
          thread1.start();
  
      }
  
      @Override
      public void run() {
          System.out.println("hello world");
  
      }
  }
  ```

* 通过**实现 Runnable 接口**。

  ```java
  public class Thread2 {
      public static void main(String[] args) {
          Thread thread = new Thread(() -> System.out.println("hello world"));//使用了lamada表达式
          thread.start();
      }
  }
  ```

* 通过**实现 Callable 接口**。

  ```java
  public class Thread3{
  
      public static void main(String[] args) throws ExecutionException, InterruptedException {
          FutureTask<String> futureTask = new FutureTask<>(()->{   //使用了lamada表达式
              return "hello world";
          });
          Thread thread = new Thread(futureTask);
          thread.start();
          String s = futureTask.get();  //获取返回结果
          System.out.println(s);
      }
  }
  ```

  **实现 `Runnable` 接口没有返回值，实现`Callable` 方法可以有返回值和可以抛出异常。** 这两者都可以采用`start()` 方法来启动线程。

  

* 通过线程池来创建。

  ```java
  public class Thread4 {
      public static void main(String[] args) {
          ThreadPoolExecutor executor = new ThreadPoolExecutor(2, 4, 10, TimeUnit.SECONDS
                  , new LinkedBlockingDeque<>(10), Executors.defaultThreadFactory(), new ThreadPoolExecutor.AbortPolicy());
   //阿里巴巴java开发手册中不允许使用Excutors来创建线程池
   //而应该使用 ThreadPoolExcutor的方式，这样的处理方式能让同学们明白线程池的运行规则，规避资源耗尽的风险。
          executor.execute(()->{
              System.out.println("hello world");
          });
      }
  }
  ```

  



### 25.如何停止一个正在运行的线程？

* **使用标志变量停止线程** ：在`run` 方法中，可以在循环迭代的时候每次检查这个标志变量，并在需要停止的地方将变量修改，然后线程可以在下一个迭代中退出并停止运行。

  ```java
  class MyThread extends Thread {
      private volatile boolean isRunning = true;
  
      public void stopThread() {
          isRunning = false;
      }
  
      public void run() {
          while (isRunning) {
              // 线程执行的代码
              //达到某个条件可以停止线程
          }
      }
  }
  
  ```

* **使用`interrupt()` 方法停止线程** ：在需要停止线程时，可以使用`interrupt` 方法来向线程发送中断信号。在线程中检查`Thread.interruput()` 方法的返回值，以确定是否应该停止线程。

  ```java
  class MyThread extends Thread {
      public void run() {
          while (!Thread.interrupted()) {
              // 线程执行的代码
          }
      }
  }
  
  MyThread thread = new MyThread();
  thread.start();
  thread.interrupt();
  ```

  

### 26.notify() 和notifyAll() 有什么区别？

* **notify()** ：唤醒在此对象监视器上等待的单个线程。如果有多个线程在等待，那么会唤醒其中一线程，具体由操作系统调度决定。
* **notifyAll()** ：唤醒在次对象监视器上等待的所有线程，让他们重新进入竞争状态。

需要注意的是：**notify()可能会导致死锁，notifyAll() 不会导致死锁。**

notify() 可能会导致死锁的一个场景是：如果两个线程A和B，他们都在同一个对象监视器上等待，但是`notify()` 方法只唤醒了线程A，没有唤醒线程B，那么线程B就会永远等待下去，造成死锁。**一个线程在等待的时候，如果不唤醒，那么它是不会被cpu调度的，会一直沉睡。**



### 27.为什么wait，notify或者notifyAll 方法要在同步块中调用？

* 因为这些方法针对的是某个对象，线程在调用时只有获得了某个对象的锁，才能够调用这些方法。
* 如果你没有获得对象监视器的锁，调用这些方法会抛出`IllegalMonitorStateException` 异常。



### 28.有三个线程T1,T2,T3,如何保证顺序执行？

* 使用`join()` 方法：

```java
public class Main {
    public static void main(String[] args) throws InterruptedException {
        // 创建三个线程
        Thread t1 = new Thread(() -> {
            System.out.println("线程T1开始执行");
            // T1的逻辑代码
            System.out.println("线程T1执行完毕");
        });

        Thread t2 = new Thread(() -> {
            try {
                // T2在等待T1执行完毕之后才能执行
                t1.join();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("线程T2开始执行");
            // T2的逻辑代码
            System.out.println("线程T2执行完毕");
        });

        Thread t3 = new Thread(() -> {
            try {
                // T3在等待T2执行完毕之后才能执行
                t2.join();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("线程T3开始执行");
            // T3的逻辑代码
            System.out.println("线程T3执行完毕");
        });

        // 启动三个线程
        t1.start();
        t2.start();
        t3.start();

        // 等待所有线程执行完毕
        t3.join();
        System.out.println("主线程执行");
    }
}
```

上面代码的执行结果是：

```java
线程T1开始执行
线程T1执行完毕
线程T2开始执行
线程T2执行完毕
线程T3开始执行
线程T3执行完毕
主线程执行
```



* 使用 `CountDownLatch` 类

  ```java
  public class Main {
      public static void main(String[] args) throws InterruptedException {
          CountDownLatch latch1 = new CountDownLatch(1);    //计数器为1
          CountDownLatch latch2 = new CountDownLatch(1);    //计数器为1
  
          Thread t1 = new Thread(() -> {
              // code for T1
              System.out.println("t1");
              latch1.countDown();   //latch1中的计数器减1
          });
          Thread t2 = new Thread(() -> {
              try {
                  latch1.await();
              } catch (InterruptedException e) {
                  e.printStackTrace();
              }
              // code for T2
              System.out.println("t2");
              latch2.countDown();
          });
          Thread t3 = new Thread(() -> {
              try {
                  latch2.await();
              } catch (InterruptedException e) {
                  e.printStackTrace();
              }
              // code for T3
              System.out.println("t3");
          });
  
          t1.start();
          t2.start();
          t3.start();
      }
  }
  ```

  **CountDownLatch 是 Java 提供的一个同步工具类**，**它可以让一个或多个线程等待其他线程完成操作后再执行**。

  在这里，我们创建了两个 CountDownLatch 对象，分别是 latch1 和 latch2。latch1 的初始计数器为 1，latch2 的初始计数器也为 1。在 t1 线程中，执行完 T1 的代码后，调用了 latch1.countDown() 方法，将 latch1 的计数器减 1。在 t2 线程中，调用了 latch1.await() 方法，让 t2 线程等待 latch1 的计数器为 0，即 t1 线程执行完 T1 的代码后。当 latch1 的计数器为 0 时，t2 线程才会继续执行 T2 的代码，并调用 latch2.countDown() 方法，将 latch2 的计数器减 1。在 t3 线程中，调用了 latch2.await() 方法，让 t3 线程等待 latch2 的计数器为 0，即 t2 线程执行完 T2 的代码后。当 latch2 的计数器为 0 时，t3 线程才会继续执行 T3 的代码。



### 29.Thread类中的yield方法有什么作用？

yield 方法可以暂停当前正在执行的线程，让其他有相同优先级的线程执行。它是一个静态方法，它只保证暂停CPU的使用权，但是其他线程不一定能占用CPU，因为在进行线程调度时，还有可能会再次轮到执行 yield 方法的线程。



### 30.并发编程的三个重要特性是什么，展开讲一讲？

* **原子性** ：一个操作是不可中断的，要么都执行，要么都不执行。在java中，使用`synchronized` 或者 `lock` 接口来保证方法或代码块的原子性。
* **可见性** ：一个线程修改了共享变量的值，那么其他线程能够立即看到修改后的值。在java中，可以使用`volatile`关键字或者`synchronized`来保证共享变量的可见性。如果我们将变量声明为`volatile` ，这就指示JVM，这个变量是共享的且不稳定，每次我们获取到他们都要到主存中去获取。
* **有序性** ：程序执行的顺序按照代码的先后顺序执行。在java中，可以使用`volatile` 关键字来禁止**指令重排序**。



### 31.volatile关键字的作用？

`volatile` 可以用来修饰变量，被它修饰的变量具有可见性和有序性，但是不具有原子性。

具体来说，当一个线程修改了一个`volatile` 的值时，其他线程能够立即看到这个修改。

此外，使用`volatile` 修饰的变量的读写操作会被禁止重排序，这意味着这些操作会按照程序中的顺序执行。

`volatile` 关键字可以保证数据的可见性，不能保证数据的原子性。`synchronized` 关键字两者都能保证。



### 32.什么是乐观锁？使用场景是什么？

顾名思义，乐观锁就是总是设想最好的场景，认为每次访问共享资源的时候不会被别人修改，线程可以不停的去执行，也不需要加锁。只是在修改数据的时候需要去检测对应的数据是否被其他线程修改过了。

使用场景：乐观锁多**用于写比较少的情况**（多读场景） ，避免频繁加锁影响性能，大大提高了系统的吞吐量。



### 33.乐观锁的实现方式是什么？

#### 版本号机制

一般是在数据表加上一个数据版本号`version` 字段，表示数据被修改的次数，当数据被修改时，`version`字段加一。当线程A要更新数据值时，在读取数据的同时也会读取`version` 的值，然后再提交更新时，会将数据库中的`version`字段与刚才读出来的 `version` 字段的值做比较，如果相等才可以更新成功，如果不相等，那么会尝试更新操作，直到更新成功。

常见的版本号生成方式有：自增序列，时间戳，UUID等。UUID生成的字符串较长，不建议使用。时间戳需要使用更高精度的时间戳（毫秒或微妙级别）。自增序列会耗尽。



#### CAS机制

CAS的全称是**Compare And Swap（比较与交换）** ，用于实现乐观锁。被广泛应用在各大框架中。CAS的思想很简单，就是用一个预期的值和要更新的值作为比较，两者相等才进行更新。

CAS涉及到三个操作数：**要更新的值、预期值和新的值**。它通过比较在内存中的值（要更新的值）和预期值是否相等，如果相等，那么就会将新的值写入。如果不相等，那么会重新尝试。



### 34.CAS操作存在哪些问题？

**ABA问题** ：

如果一个线程初次读取值的时候是A，并且在准备赋值的时候发现也是A，那么能说明这个值没有被修改过吗？

很明显不能，因为如果在这期间其他线程修改了这个值，然后又把这个值改回A，那么CAS会认为该值从来没有修改过。

JDK1.5以后的 `AtomicStampedReference` 类就是用来解决ABA问题的。

**循环开销时间大** ：

CAS通常会通过自旋来进行重试操作，也就是说如果不成功那就一直循环，直到成功为止。如果长时间不成功，那么会给CPU带来很大的开销。

**只能保证一个共享变量的原子性操作** ：

CAS只对单个变量有效，当涉及到多个变量时CAS无效。



### 35.什么是悲观锁？使用场景是什么？

悲观锁总是设想最坏的情况，认为每次访问共享资源的时候，其他线程会进来修改数据，所以在每次获取资源操作时候都会进行上锁。这样其他线程想要拥有资源只能等到当前线程释放锁，不然就会一直阻塞。

像java中的`synchronized` 和`ReentrantLock` 等独占锁就是悲观锁的实现。

使用场景：悲观锁多**用于多写**的场景，避免频繁失败和重试影响性能。









# 四、JVM

### 1.JVM内存模型？

* **线程私有** ：程序计数器、虚拟机栈、本地方法栈。
* **线程共享** ：方法区、堆。



#### 虚拟机栈

又称方法栈，是线程私有的。线程执行方法都会创建一个栈帧，用来存储局部变量表，操作数栈、动态链接、方法出口等信息。调用方法时执行入栈、方法返回时出栈。

#### 本地方法栈

跟虚拟机栈类似，但是是用来执行`native` 方法（本地方法）的。

#### 程序计数器

保存着当前线程执行的字节码的位置，每个线程都有独立的程序计数器，只为java方法服务。上下文切换时，会根据程序计数器来继续执行这个线程。

**当执行natvie 方法时，程序技术栈为空。**

#### 方法区

用于存储已被虚拟机加载的**类信息，常量，静态变量，即时编译器优化后的代码**等数据。

**1.7的永久代和1.8的元空间都是对方法区的一种实现。** 

#### 堆

是java虚拟机中管理内存最大的一块，**且是线程共享的，基本上所有的对象实例和数组都存储在这里**。当堆没有可用空间时，会抛出OOM（Out Of Memory）异常。根据对象的存活周期不同，JVM把对象分代管理，用垃圾回收器回收垃圾。



### 2.说说类的加载和卸载？

系统加载类文件主要需要三步：**加载 -> 链接 -> 初始化。** 其中链接又分为三步：**验证 -> 准备 -> 解析**。

* **加载** ：通过类的完全限定名，查找此类字节码文件，利用字节码文件创建 Class对象。
* **验证** ：确保Class文件符合当前虚拟机的要求，不会危害到虚拟机本身。
* **准备** ：进行内存分配，为`static` 修饰的类变量分配内存，并设置初始值（0或者 null ）。**不包含 final修饰的静态变量，因为final变量在编译时分配。**
* **解析** ：将常量池中的符号引用替换为直接引用的过程。直接引用为直接指向目标的指针或者相对偏移量。
* **初始化** ：主要完成静态块执行以及静态变量的赋值，先初始化父类，再初始化当前类。只有对类主动使用时才会初始化。触发条件包括：**创建类的实例时，访问类的静态方法或者静态变量时，使用`Class.forName` 反射类的时，某个子类初始化时。**
* **卸载** ：该类的Class对象被GC。java自带的加载器加载的类，在虚拟机声明周期是不会被加载的，只有用户自定义的加载器加载的类才可以被卸。



### 3.讲一下双亲委派模型？有什么好处？

先来了解一下类加载器,自底向上分别为：

* 自定义加载器：用户可以自定义的加载器。
* 应用程序类加载器（Application ClassLoader）： 面向我们的加载器，负责加载classPath下的jar包和类。
* 扩展类加载器（Extension ClassLoader）: 主要负责加载 `%JAVA_HOME%/lib/ext` 下的jar 包。
* 启动类加载器（Bootstrap ClassLoader）: 主要负责加载`%JAVA_HOME%J/lib`下的核心类库。

双亲委派模型，即类加载器在加载类的时候，先把请求委托给它的父类加载器来加载，一直到最顶层的父类，如果能够加载就成功返回，如果不能子类加载器自己就加载。总的来说，就是“向上委托，向下查找”。

![image-20230317232240589](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230317232240589.png)

双亲委派模型的好处：

* 避免类的重复加载
* 防止java的核心API被篡改



### 4.说说堆和栈的区别？

* **功能不同** ：栈用来存储局部变量和方法的调用，堆则是用来存放对象实例和数组的。不管是成员变量还是类变量，或者是局部变量，他们指向的对象都存储在堆内存中。
* **共享性不同** ：栈是线程私有的，堆是所有线程共享的。
* **异常错误不同** ：无论是栈还是对，当空间不足时都会抛出异常。栈空间不足抛出`StackOverFlow(SOF)`  ,堆空间不足抛出`OutOfMemory(OOM)` 。
* **空间大小不同** ：堆的空间是要远远大于栈的。



### 5.说说堆空间的基本结构？

在 JDK7 跟 JDK7 之前，堆空间主要分为三个部分：

* **新生代**（Young Generation）：包含 **Eden** 区， **S0**区， **S1**区。
* **老年代**（Old Generation）
* **永久代**（Permanent Generation）

在 JDK 1.8 之后永久代就变成了**元空间（MetaSpace）** 。

![image-20230317234428306](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230317234428306.png)



### 6.说说对象分配规则？

* 对象优先被分配在 Eden 区，如果 Eden 区没有足够的空间，那么虚拟机会进行一次 **Minor GC**。 
* **大对象直接进入老年代**（大对象是指那些需要大量连续内存空间的对象）。这样做的目的是为了避免在 Eden 区和S0区，S1区之间大量的内存拷贝（新生代采用的是复制算法收集内存）。
* **长期存活的对象进入老年代**。JVM会为每个对象定义一个年龄计数器，当发生一次 Minor GC 的时候，对象会进入 Sruvivor 区（即S0跟S1区） ，然后每进行一次 Minor GC,年龄计数器就会加一，直到达到阈值（一般默认为15）就会进入老年代。
* 动态判断对象的年龄。如果 Survivor 区中相同年龄的所有对象的大小超过Survivor 区的 50%，年龄大于或等于该年龄的对象将直接进入老年代。
* 空间分配担保。每次进行Minor GC 时，JVM会计算 Survivor 区移至老年区的对象的平均大小，如果这个值大于老年区的剩余值大小则进行一次Full GC ,如果小于的话检查 HandlePromotionFailure设置, 如果是 true，那么只进行 Mionor GC ，如果是false，则进行 Full GC。



### 7.说说java对象创建的过程？

* 检查类是否已经被加载，如果没有就加载类
* 为对象分配内存空间
* 将对象头外的对象内存空间初始化为0
* 对对象头进行必要设置



### 8.简述java的对象结构？

java对象由三个部分组成：**对象头，实例数据，对齐填充**。

**对象头**包含两个（三个）部分：

* **markword** ：包含对象自身的运行时数据，包括哈希码，GC分代年龄，锁标识状态，线程持有的锁，偏向锁ID（一般是32/64 bit） 。
* **Kclass** : 指针类型，指向对象的类元数据类型（即对象代表哪个类）。
* **数组长度** ：如果是数组对象，那么对象头还有一部分用来记录数组的长度。

**实例数据** 是用来存储对象真正的有效信息（包括父类继承下来的和自己定义的）。

**对齐填充** 起着占位符的作用，因为JVM要求对象的起始地址必须是8字节的整数倍。



### 9.如何判断对象可以被回收？

* **引用计数法** ：每个对象都有一个计数器，**新增一个引用时计数器加一**，**引用释放时计数器减一**，**计数器为0时可以进行回收**。这个方法虽然简单，但是不能够解决**循环依赖**的问题。比如说A引用B，B又引用A，那么他们各自的计数器永远不为0，所以就永远无法被回收掉。

* **可达性分析** ：从 GC roots 开始 向下搜索，搜索走过的路径被称为引用链。当对象到 GC roots 没有任何引用链相连时，则证明这个对象是不可达的，可以进行回收。

  

### 10.说一说java中的引用类型有几种？

* **强引用** ： 这是最普遍的引用，如果一个对象具有强引用，就类似于**必不可少的日用品**，垃圾回收器绝对不会去回收他们，宁愿抛出OOM错误，使程序终止异常，也不会去回收。
* **软引用** ：如果一个对象具有软引用，那就**类似于可有可无的日用品**，当内存空间不够时，垃圾回收器会回收它，当内存空间足够，垃圾回收器不会回收它。
* **弱引用** ：如果一个对象具有弱引用，那就类似于可有可无的日用品。它跟软引用的区别在于：只具有弱引用的对象拥有更短暂的生命周期。当垃圾回收线程启动，**发现只具有弱引用的对象，那么不管内存空间够不够，垃圾回收器都会回收它。**
* **虚引用** ：顾名思义，就是形同虚设的引用，它的主要作用在于**跟踪对象被垃圾回收的活动。**



### 11.哪些对象可以作为GC Roots？

* 虚拟机栈（栈中的本地变量表）中引用的对象
* 本地方法栈中引用的对象
* 方法区中类静态属性引用的对象
* 方法区中常量引用的对象
* 所有被同步锁持有的对象



### 12.你知道哪些垃圾回收算法？

GC最基础的垃圾回收算法就是三个：标记-清除算法，标记-复制算法，标记-整理算法。

* **标记-清除算法** ：分为两个阶段，首先标出所有**不需要回收**的对象，在标记完成后统一回收掉**没被标记**的对象。（**标记清除产生大量不连续的碎片**）
* **标记-复制算法** ：**为了解决标记清除算法的内存碎片问题，产生了复制算法**。它将内存空间按容量分为相等的两块，每次只使用其中的一块，当一块的内存空间用完了，就将还存活的对象复制到另外一块上去，然后再把已经使用过的空间一次性清理掉。（**标记复制浪费大量的空间，效率跟存活对象的个数有关**）
* **标记-整理算法** ：跟标记-清除算法一样，但是后续步骤不是直接对可回收对象进行回收，而是让所有存活的对象往一端移动，直接清理掉端边界以外的内存。

最后还有一个**分代回收算法** ，把堆分为新生代和老年代，然后根据各个年代的特点选择合适的垃圾回收算法。

比如在新生代中，每次收集都会有大量对象死去，所以可以选择”标记-复制“算法，只需要付出少量对象的复制成本就可以完成每次垃圾收集。而**老年代的对象存活几率是比较高**的，而且没有额外的空间对它进行分配担保，所以我们必须选择“**标记-清除”或“标记-整理”**算法进行垃圾收集。



### 13.JVM调优命令有哪些？

JDK 命令行工具，这些命令安装在jdk 安装目录下 的 `bin` 目录：

* jps : 查看所有java进程。
* jstat : 监视虚拟机各种运行的状态，可以显示进程中的类信息，内存，垃圾回收，JIT编译等运行数据。
* jinfo : 实时查看和调整虚拟机运行参数。
* jmap : 生成堆转储快照，即生成 head dump文件
* jhat ： 和 jmap 搭配使用，用于分析head dump文件，它会建立一个 HTML/HTTP服务器，让用户可以在浏览器上查看分析结果。
* jstack ：生成虚拟机当前时刻的线程快照。线程快照就是当前虚拟机内每一条线程正在执行的方法堆栈的集合。



### 14.JVM调优工具有哪些？

* jconsole : 从 java 5开始，在 JDK中自带的java监控和管理程序，用于对JVM中内存、线程、类等的监控。
* jvisualvm : JDK 自带全能工具，可以分析内存快照，线程快照，监控内存变化，GC变化等。



### 15.你知道哪些JVM性能调优参数

* **设定堆内存大小** ：`-Xmx` 。

* **设定新生代大小** 。新生代不宜过小，否则会有大量对象涌入老年代。

  `-XX:NewSize` :新生代大小

  `-XX:NewRatio` :新生代和老年代之比

  `-XX:SurvivorRatio` : 伊甸园空间和幸存者空间的占比

* **设定垃圾回收器** ：

  新生代用`-XX:+UserParNewGC` ,老年代用`-XX:+UserConcMarkSweepGC` 。



### 16.对象一定分配在堆中吗？有没有了解过逃逸分析技术？

不一定。JVM会通过`逃逸分析` 技术，那些逃不出方法的对象会在栈上进行分配。逃逸分析，通俗的讲，就是**如果一个对象的指针被多个方法或者线程引用时，那么我们就成这个对象的指针发生了逃逸。**

逃逸分析的好处：

* 栈上分配，可以降低垃圾回收器运行的频率。
* 减少内存使用，因为不用生成对象头。



### 17.为什么使用元空间代替永久代？

永久代的方法区，和堆使用的物理空间上是连续的，因此永久代空间配置有限。

但是在JDK 1.8之后，永久代改为元空间，物理空间不再与堆连续，因此元空间可以`内存有多大，元空间就有多大` 。

所以在使用元空间后，就不用再受制于永久代的大小了，避免发生OOM异常。



### 18.说一说JVM有哪些垃圾回收器？

下图展示了7种作用于不同分代的收集器，其中作用于新生代的收集器包括：Serial 、PraNew 、Parallel Scavenge ，老年代的收集器包括：Serial Old ，Paraller Old ,CMS ，还有作用于回收整个Java堆的垃圾回收器。不同回收器之间连线代表他们可以搭配使用。

![image-20230318160700167](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230318160700167.png)



* Serial 收集器（标记复制算法） ：新生代**单线程**收集器，标记和清理都是单线程，优点是简单高效。
* ParNew 收集器（标记复制算法）：新生代**并行**收集器，实际上是 Serial 收集器的多线程版本，在多核CPU下会有更高效的表现。
* Parallel Scavenge收集器（标记复制算法）：新生代**并行**收集器，追求高吞吐量，高效利用CPU。
* Serial Old收集器（标记整理算法）：老年代**单线程**收集器，是Serial 收集器的老年代版本。
* Parallel Old 收集器（标记整理算法）：老年代**并行**收集器，吞吐量有限，是 Paraller Scavenge 收集器的老年代版本。
* CMS 收集器（标记清除算法）：老年代**并行**收集器，具有高并发，低停顿的特点，追求最短GC回收停顿时间。
* G1 收集器（标记整理算法）：**java堆并行收集器**，回收范围包括新生代和老年代。



### 19.什么时候会触发 Full GC?

* **调用 System.gc()** : 只是建议虚拟机去执行 Full GC, 但是不一定会去执行。不建议使用这种方式，而是让虚拟机去管理内存。

* **未指定新生代和老年代的大小** ：堆伸缩时会产生full GC，所以一定要配置`-Xmx` ,`-Xms` 。

* **老年代空间不足** ：常见场景：大对象、大数组直接进入老年代，长期存活的对象进入老年代等。

* **永久代空间满** ：永久代中存在着一些Class信息，常量，静态变量等数据，到系统中要加载的类、反射的类和调用的方法太多时，永久代可能会被占满，所以会发生 Full GC。

* **空间分配担保失败** ：

  1. 每次晋升的对象的平均大小>老年代剩余空间
  2. Minor GC后存活的对象超过了老年代剩余空间

  注意GC日志中是否有promotion failed和concurrent mode failure两种状况，当出现这两种状况的时候就有可能会触发Full GC。

  promotion failed 是在进行 Minor GC时候，survivor space空间放不下只能晋升老年代，而此时老年代也空间不足时发生的。

  concurrent mode failure 是在进行CMS GC过程，此时有对象要放入老年代而空间不足造成的，这种情况下会退化使用Serial Old收集器变成单线程的，此时是相当的慢的。

### 20.你知道哪些JVM调优参数？

堆栈内存相关：

* -Xms 设置初始堆的大小
* -Xmx 设置最大堆的大小
* -Xmn 设置新生代大小
* **-Xss 设置每个线程的栈大小**

垃圾回收器相关：

* -XX:+UseParallelGC  选择垃圾回收器为并行收集器
* -XX：ParallelGCThreads=20   配置并行收集器的线程数

辅助信息相关：

* -XX:+PrintGCDetails 打印GC详细信息
* -XX:+DisableExplicitGC 禁止系统使用 System.gc()，防止手动误触发 Full GC 造成问题。



### 21.JVM包含哪几部分？

* 类加载子系统：可以根据指定的全限定名来载入类或接口。
* 执行引擎：负责执行那些包含在被载入类的方法中的指令。
* 运行时数据区：当程序运行时，JVM需要内存来存储许多内容，例如：字节码、对象、参数、返回值、局部变量、运算的中间结果，等等，JVM会把这些东西都存储到运行时数据区中，以便于管理。而运行时数据区又可以分为方法区、堆、虚拟机栈、本地方法栈、程序计数器。



### 22.什么是stw?

在 Java 中，STW (Stop-The-World) 指的是**垃圾回收器在执行垃圾回收**操作时，会导致整个应用程序的执行被暂停或阻塞的现象。在 STW 发生期间，所有线程都会被暂停，不再执行任何任务，直到垃圾回收操作完成。

需要注意的是，并不是所有的垃圾回收操作都会导致 STW，现代的 JVM 在进行垃圾回收时通常会采用一些并发和并行的技术，以减少 STW 的发生。例如，**CMS (Concurrent Mark and Sweep) 垃圾回收器**和 **G1 (Garbage-First) 垃圾回收器**都是**并发垃圾回收器**，可以在不完全暂停应用程序的情况下执行部分或全部垃圾回收操作，从而减少 STW 的发生时间，提高应用程序的性能和响应时间。























# 五、MySQL数据库



### 1.什么是数据库、数据库管理员、数据库管理系统、数据库系统？

* **数据库**：数据库（DataBase 简称DB），是信息的集合，或者说是我们储存数据的地方。
* **数据库管理系统**：数据库管理系统（DataBase Management System 简称DBMS），是用来管理数据库的一种大型软件，通常用于建立、使用和维护数据库。注意：**我们常说mysql，oracle等这些都是数据库管理系统，而不是数据库**。
* **数据库管理员**：数据库管理员（DataBase Administrator 简称DBA）,负责管理数据库系统的操作人员。
* **数据库系统：**数据库系统（DataBase System 简称DBS）,通常由软件，数据库和数据库管理系统组成。



### 2.什么是元组、码、候选码、主码、外码、主属性、非主属性？

* **元组**：关系是一张表，表中的每一行（即数据库中的每条记录）称为一个元组，每列就是一个属性。
* **码**：码就是唯一标志实体的属性，对应表中的列。
* **候选码：**若关系中的某一属性或某一属性组的值能唯一标志一个元组，⽽其任何、⼦集都不能再标识，则称该属性组为候选码。例如：在学⽣实体中，“学号”是能唯⼀的区分学⽣实体的，同时 ⼜假设“姓名”、“班级”的属性组合⾜以区分学⽣实体，那么{学号}和{姓名，班级}都是候选码。
* **主码**：主码也叫做主键。主码是从候选码中挑选出来的。一个实体集只能有一个主码，但是可以有多个候选码。
* **外码：**外码也叫做外键。如果一个关系中的一个属性是另外一个关系的主码，那么这个属性叫做外码。
* **主属性：**候选码中出现过的属性称为主属性。⽐如关系 ⼯⼈（⼯号，身份证号，姓名，性别， 部⻔）. 显然⼯号和身份证号都能够唯⼀标示这个关系，所以都是候选码。⼯号、身份证号这两 个属性就是主属性。如果主码是⼀个属性组，那么属性组中的属性都是主属性。
* **非主属性：**不包含在任何⼀个候选码中的属性称为⾮主属性。⽐如在关系——学⽣（学号，姓 名，年龄，性别，班级）中，主码是“学号”，那么其他的“姓名”、“年龄”、“性别”、“班级”就都可以称为⾮主属性。



### 3.主键和外键有什么区别？

* **主键：**主键唯一标志一个元组，不能重复，也不能为空。一个表只能有一个主键。
* **外键：**外键是另外一个关系中的主键，外键可以有多个，也可以有重复的，也可以是空值。一个表可以有多个外键。



### 4.为什么不推荐使用外键与级联？

在阿里巴巴开发手册中这样写道：

不得使用外键与级联，一切外键概念都必须在应用层解决。这是为什么呢？

比如说以学生表和成绩表为例，`student_id`是学生表中的主键，那么成绩表中的`student_id`就是外键。如果学生表中的`student_id`更新，同时触发成绩表中`student_id`更新，即为级联更新。**外键与级联更新适用于单机低并发，不适合分布式，高并发集群；级联更新更是强阻塞，存在更新风暴的风险；外键影响数据库插入的速度。**



### 5.数据库范式了解过吗？

* **1NF（第一范式）：**属性（对应表中的字段）不能再被分割，也就是这个字段只能是一个值，不能再分为其他字段了。**1NF是所有关系型数据库的最基本要求。**

* **2NF（第二范式）：**2NF在1NF的基础上，**消除了非主属性对于码的部分函数依赖。**第二范式要求在数据库中的每个表，**非主属性键必须完全依赖于主属性，而不是依赖于主属性的一部分。**

  部分函数依赖：一个非主属性键只依赖于主键的一部分，而不是整个主键。例如，在一个订单表中，如果订单号和产品号联合形成了主键，但是产品名称只依赖于产品号而不依赖于订单号，则存在部分函数依赖关系。

  为了遵守第二范式，需要将表分解为多个表，其中每个表都具有一个主键和完全依赖于该主键的属性集。在上述例子中，可以将订单表分解为订单表和产品表，使得产品名称属性只存在于产品表中，而不是与订单号和产品号一起存在于订单表中，这样可以消除部分函数依赖。

* **3NF（第三范式）**：3NF在2NF的基础上，**消除了非主属性对于码的传递函数依赖。**符合3NF的数据库设计，基本上解决了数据冗余过大，插入异常，修改异常，删除异常的问题。

  第三范式要求在数据库的每个表中，每个非主键属性都不依赖于其他非主属性。换句话来说，**任何非主属性都不能依赖于其他非主属性，而是必须依赖于主属性。**

  传递函数依赖是指存在非主属性A、B和C的关系，其中A依赖于主键，B依赖于A，C依赖于B而不是主键。例如，在一个订单表中，如果订单地址取决于顾客城市，而顾客城市又取决于顾客国家，则存在传递函数依赖关系。 

  为了遵守第三范式，需要将表分解为多个表，其中每个表都具有一个主键和与该主键直接相关的属性集。在上述例子中，可以将订单表分解为三个表：订单表、顾客表和国家表。这样，订单地址将从订单表中移动到顾客表中，而顾客城市和顾客国家将分别存在于顾客表和国家表中。这种分解可以消除传递函数依赖。



### 6.drop、delete、truncate有什么区别？

* **drop(丢失数据)**：`drop table 表名`，直接将表删除，包括表定义，索引，约束触发器等。
* **truncate(清空数据)**：`truncate table 表名`,删除表中的数据，**再插入数据的时候自增id又从1开始**。该语句并不会把表的定义，索引，约束，触发器等删除，而是将表的数据也重新初始化，但是由于它重置表，所以不能保留表的特定状态或日志。也就是说，**不支持回滚**的操作。
* **delete(删除数据)：**`delete from 表名 where 列名 = 值`，删除某一行的数据，如果不加`wehere`字句，那么效果跟`truncate`类似。表的结构，索引，约束等将保留，同时**支持回滚**操作。

注意：**turncate和delete只是删除表中的数据，不会删除表的结构，但是使用drop不仅删除表的数据，而且连表的结构也一并删除了。**



### 7.MyISAM和InnoDB的区别是什么？

* **是否支持行级锁**：MyISAM只支持表级锁，不支持行级锁；而InnoDB既支持表级锁，也支持行级锁。
* **是否支持事务：**MyISAM不支持事务，而InnoDB支持事务。
* **是否支持外键：**MyISAM不支持外键，而InnoDB支持外键。但是不建议使用外键。
* **是否支持数据库异常崩溃后的数据恢复：**MyISAM不支持，而InnoDB支持。InnoDB在数据库异常崩溃后，重新启动会保证恢复到数据库之前的状态，这依赖于`redo log`。
* **索引实现不一样：**虽然两者都是使用**B+树作为索引结构，**但是两者的实现方式是不一样的。

综上所述，MyISAM存储引擎适用于读取密集型的应用，如数据仓库、日志系统等。而InnoDB存储引擎适用于写入密集型和事务性的应用，如电子商务网站、银行系统等。



### 8.何为事务？事务的ACID特性指什么？

一言蔽之，事务就是一组逻辑上的操作，**要么都执行，要么都不执行。**

事务的ACID特性如下：

* **原子性**（Atomicity）:事务是最小的执行单位，不允许分割。事务的原子性确保动作要么都执行，要么都不执行。
* **一致性**（Consistency）:事务的执行前后，数据应该要保持一致。从一个一致性状态转换到另外一个一致性状态。
* **隔离性**（Isolation）:事务之间是隔离的，一个事务不能被其他事务干扰，每个事务之间应该是独立的。
* **持久性**（Durability）:一个事务被提交之后，它对数据库的改变是永久的，即使数据库发生故障也不对其有任何影响。

同时要注意的是：**只有保证了事务的原子性、隔离性和持久性，才能够保证事务的一致性。**

```sql
# 开启一个事务
START TRANSACTION;
# 多条 SQL 语句
SQL1,SQL2...
## 提交事务
COMMIT;
```



### 9.并发事务带来了那些问题？

* **脏读：**当一个事务正在访问数据并且对数据做了修改，但是此时这个事务并没有提交。在这个时候如果另外一个事务也来访问这条数据，那么就会出现访问到的是“脏的”数据，因为另外一个事务想访问的应该是未被修改前的数据，所以此时会造成不正确的结果。

* **丢失修改：**当一个事务对某条数据进行修改后，另外一个事务也对这个数据进行了修改，那么第一个事务的修改结果就会发生改变，称为丢失修改。

* **不可重复读：**当一个事务访问某条数据时，另外一个事务也访问这个数据并且对这条数据做了修改，那么当我前一个事务想继续访问这条数据时，得到的是不一样的结果（因为前一个事务原本想访问的是没有被修改的数据），称为不可重复读。

* **幻读**：当一个事务访问某个表时，另外一个事务对这个表插入了几条数据，当前一个事务想要来访问这个表时，发现多了几条数据，得到的是不一样的结果，这称为幻读。

  

### 10.MySQL的隔离级别有哪些？

* **读取未提交（read-uncommitted）**:允许读取尚未提交的数据，可能会导致脏读，幻读或不可重复读。这是最低的隔离级别。
* **读取已提交（read-committed）：**允许读取已经提交的数据，可以防止脏读，但是可能会导致幻读或者不可重复读。
* **可重复读（repeatable-reda）**：对同一字段的多次读取结果是一样的，可以防止脏读和不可重复读，但是可能会导致幻读。**可重复读也是mysql 默认的隔离级别。**
* **可串行化（serializable）：**所有事务逐个执行，这样事务之间就不存在干扰，可以防止脏读、不可重复读和幻读。这是最高的隔离级别。

示意图如下：

![image-20230309001250987](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230309001250987.png)



### 11.MySQL的隔离级别是基于什么实现的？

**MySQL的隔离级别是通过锁和MVCC共同实现的。**

**除了最高级别的SERIALIZABLE是通过锁来实现的，其他级别都是通过MVCC来实现的**。不过， SERIALIZABLE 之外的其他隔离级别可能也需要⽤到锁机制，就⽐如 REPEATABLE-READ 在当前读情况下需要使⽤加锁读来保证不会出现幻读。



### 12.表级锁和行级锁有什么区别？

* **表级锁**：是MySQL中锁粒度最大的一种锁，**是针对非索引字段的锁**，即对当前的这张表加锁，实现简单，资源消耗也最小,并发力度小。MyISAM和InnoDB都支持这种锁。
* **行级锁**：是MySQL中锁粒度最小的一种锁，**是针对索引字段的锁**，只针对当前的行记录进行上锁即可，并发度高，可能会出现死锁。



### 13.行级锁的使用有什么注意事项？

InnoDB中的行级锁是针对索引字段加的锁。当我们执行`delete`、`update`这样的语句时，如果`where`条件后面的字段没有命中唯一索引或者索引失效的话，就会导致扫描全表，从而对全表中的所有记录进行加锁。



### 14.什么是共享锁和排他锁？

不管是行级锁和表级锁，它们都有排它锁和共享锁两类：

* **共享锁（S锁）**：又称读锁，事务在读取记录的时候获取共享锁，允许多个事务同时获取。

* **排他锁（X锁）**：又称写锁，事务在修改记录的时候获取排它锁，不允许其他事务同时获取。**如果一个记录加了排他锁，那么其他事务不能对这条记录再加任何其他类型的锁（排它锁不兼容）。**

  

### 15.意向锁有什么用？

如果要用到表锁的话，那么如何判断表中的记录有没有加行锁呢？一遍一遍遍历肯定不行，性能太差了。这就需要用到意向锁。意向锁也有两类：

* **意向共享锁：**事务有意向表中的某些加共享锁，在此之前必须要获得该表的意向共享锁。
* **意向排他锁：**事务有意向表中的某些记录加排他锁，在此之前必须要获得该表的意向排他锁。

意向锁是有数据引擎⾃⼰维护的，⽤户⽆法⼿动操作意向锁，在为数据⾏加共享 / 排他锁之前， InooDB 会先获取该数据⾏所在在数据表的对应意向锁。



### 16.InnoDB有哪几类行锁？

* **记录锁**：属于单个记录上的锁。
* **间隙锁**：锁定一个范围，不包括记录本身。
* **临键锁：**锁定一个范围，包括记录本身。



### 17.索引是什么，有什么优缺点？

**索引是一种快速查询和检索数据的数据结构**，索引的作用就是相当于一本字典的目录，当我们想要查询某个字的时候，我们直接打开目录，然后翻到对应的那一页就行了。

常见的索引结构有：B树、B+树和Hash、红黑树等。**在MySQL和 MyISAM中，都使用B+树来作为索引结构。**

**优点** ：

* 查询速度快，这也是创建索引的最主要的原因
* 通过创建唯一性索引，可以保证数据库表中的每一行数据的独一性

**缺点** ：

* 创建索引和维护索引需要耗费很多时间。当对表中的数据进行增删改时，如果数据有索引，那么对应的索引也会动态该表，影响SQL执行的效率。
* 索引需要使用物理文件存储，也会耗费一定的空间。



### 18.使用索引一定能提高查询性能吗？

**不一定**。在大部分情况下，索引查询都是比全表扫描要快的，但是如果数据量不大的情况下，使用索引并不会带来很大的提升，而且还会浪费内存空间，影响运行效率。

### 19.索引底层数据结构

#### 哈希表

就是散列表，可以通过键值找到对应的value值，时间复杂度接近O(1) 。这里不赘述了。

#### B树 & B+树

B树也称**多路平衡查找树** ，B+树是B树的一种变体。目前大部分数据库系统和文件系统都使用B+树作为索引结构。

**B树和B+树有什么区别呢？** 

* B树的所有节点既存放**键（key）**，也存放**数据（data）**，**而B+树只有叶子节点存放key 和 data，内节点只存放 key。**
* B树的叶子节点是独立的，B+树的叶子节点之间有一条引用链指向与它相邻的叶子节点。
*  树的检索的过程相当于对范围内的每个节点的关键字做二分查找，可能还没有到达叶子节点，检索就结束了。而 B+树的检索效率就很稳定了，任何查找都是从根节点到叶子节点的过程，叶子节点的顺序检索很明显。



### 20.什么是主键索引（Primary Key）

数据库表中的主键列使用的就是主键索引。一**张数据库表只能有一个主键，并且不能为 null ，而且也不允许重复。**

在MySQL的InnoDB表中，如果没有显示的指定主键，那么InnoDB首先会查询表中是否含有唯一索引且值不为 null 的字段，如果有，那么会指定该字段为主键。如果没有，那么InnoDB会自动生成一个6字节的自增主键。

![image-20230315174504068](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230315174504068.png)



### 21.什么是聚簇索引？有什么优缺点。

**聚簇索引是索引结构和数据一起存放的索引，并不是一种单独的索引类型。InnodDB中的主键索引就是聚簇索引。**

在MySQL中，InnoDB引擎的表的`.ibd`文件就包含了该表的索引和数据。对于InnoDB引擎表来说，**该表的索引（B+树）的每个非叶子节点存储索引，叶子节点存储索引和索引对应的数据。**

**优点** ：

* **查询速度非常快** ： 因为B+树本身是一颗多路平衡二叉树，同时节点也是排好序的，定位到索引，就相当于定位到了数据，因为索引跟数据是放在一块的。相比于非聚簇索引，**聚簇索引少了一次读取数据的I/O操作。**
* **对排序查找和范围查找优化** ： 聚簇索引对于主键的排序查找和范围查找速度非常快。

**缺点** ：

* **依赖于有序的数据：** B+树是多路平衡树，如果索引不是有序的，那么就需要在插入的时候排序，如果是整形数据还好，如果是字符串或者UUID这种长的数据，那么排序是非常慢的。
* **更新代价大** ：如果对应列的数据被修改时，那么对应的索引也会被修改，修改代价很大。所以对于主键索引来说，主键一般是不可被修改的。

### 22.什么是非聚簇索引？有什么优缺点？

**非聚簇索引是索引结构跟数据分开存放的索引，并不是一种单独的索引类型。二级索引（辅助索引）就属于非聚簇索引。** MySQL的MyISAM存储引擎，不管是主键还是非主键，使用的都是非聚簇索引。

非聚簇索引的叶子节点（data域中）并不一定存放数据的指针，因为**二级索引的叶子节点（data域中）就存放的是主键，根据主键再回表查数据。**

**优点** ：

更新代价比聚簇索引小。

**缺点** ：

* **依赖有序的数据**。
* **可能会造成二次查询（回表）** ： 这应该是非聚簇索引的最大的缺点了。当查到索引对应的指针或主键后，可能还需要再根据指针或主键到数据文件或表中去查询。

聚簇索引和非聚簇索：

![image-20230315184325698](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230315184325698.png)



**非聚簇索引一定会造成回表吗？**

不一定。

试想这样一种情况，用户准备查询用户名，而用户名字段刚好建立了索引，

```sql
SELECT name FROM table WHERE name='guang19';
```

那么这个索引的key本身就是name，查到对应的name直接返回就行了，无需回表查询。

如果SQL查询就是主键呢？

```sql
SELECT id FROM table WHERE id=1;
```

主键索引本身的key就是主键，查到返回就行了。这种情况被称为**覆盖索引**。



### 23.覆盖索引和联合索引

如果一个索引包含（或者说覆盖）所有需要查询的字段的值，我们就称之为"覆盖索引" 。我们知道在InnoDB中，如果不是主键索引，那么最终还是要回表，也就是说通过主键再查找一次，这样就会比较慢。

**覆盖索引即需要查询的字段正好是索引的字段（也就是key），那么直接根据该索引，就可以查到数据了，而无需回表查询。** 

如主键索引，如果一条 SQL 需要查询主键，那么正好根据主键索引就可以查到主键。

再如普通索引，如果一条SQL语句要查询name，name字段正好有索引，那么直接根据这个索引就可以查到数据。

![image-20230315204759138](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230315204759138.png)



**联合索引** ：使用表中的多个字段建立索引，就是联合索引，也叫作组合索引或者复合索引。

注意：**innodb中的联合索引是非聚簇索引。** 这意味着索引中存储的是键值和对应的行地址（**主键**），而不是实际的数据行。



### 24.什么是二级索引（辅助索引）？

**二级索引又称为辅助索引，是因为二级索引的叶子节点存储的数据是主键**。也就是说，通过二级索引，可以定位主键的位置。

唯一索引，普通索引，前缀索引等索引属于二级索引。

1. **唯一索引(Unique Key)** ：唯一索引也是一种约束。**唯一索引的属性列不能出现重复的数据，但是允许数据为 NULL，一张表允许创建多个唯一索引。** 建立唯一索引的目的大部分时候都是为了该属性列的数据的唯一性，而不是为了查询效率。
2. **普通索引(Index)** ：**普通索引的唯一作用就是为了快速查询数据，一张表允许创建多个普通索引，并允许数据重复和 NULL。**
3. **前缀索引(Prefix)** ：前缀索引只适用于字符串类型的数据。**前缀索引是对文本的前几个字符创建索引**，相比普通索引建立的数据更小， 因为只取前几个字符。
4. **全文索引(Full Text)** ：全文索引主要是为了检索大文本数据中的关键字的信息，是目前搜索引擎数据库使用的一种技术。Mysql5.6 之前只有 MYISAM 引擎支持全文索引，5.6 之后 InnoDB 也支持了全文索引。



### 25.索引类型的总结

按照底层存储方式划分 ：

* **聚簇索引** ：索引结构和数据一起存放的索引，InnoDB中的主键索引就属于聚簇索引。

* **非聚簇索引** ：索引结构和数据分开存放的索引，二级索引（辅助索引）就属于非聚簇索引。MySQL的MyISAM,不管是主键还是非主键，使用的都是聚簇索引。

  

按照引用维度划分：

* 主键索引：加速查询+列值唯一（不可以有null）+表中只用一个。
* 普通索引：仅加速查询。
* 唯一索引：加速查询+列值唯一（可以有null）。
* 覆盖索引：一个索引包含所有需要查询的字段的值。
* 联合索引：表中的多个字段组成一个索引。



### 26.什么是最左前缀匹配原则？

最左前缀原则指的是，在使用**联合索引**时，Mysql会根据联合索引中的字段顺序，从左到右依次去查询条件中去匹配，**如果查询条件中存在与联合索引最左侧字段相匹配的字段，则会用这个字段过滤一些数据，直至联合索引中全部字段匹配完成**，或者说在执行过程中遇到范围查询（如`<`，`>`） 才会停止匹配。 

对于`>=` ,`<=` ,`between` ,`like` 前缀匹配的范围查询，MySQL并不会停止匹配。

所以我们在使用联合索引时，可以将区分度高的字段放在最左边，这可以过滤更多的数据。



### 27.应该在哪些字段上建立索引？

* **不为NULL的字段** ：索引字段的数据应该尽量不为NULL，因为对于这样的字段，数据库比较难优化。
* **被频繁查询的字段** 。
* **被作为条件查询的字段** ：被作为where条件查询的字段，应该建立索引。
* **频繁需要排序的字段** ：索引已经排好序，这样可以利用索引的排序，加快查询时间。
* **被经常频繁用于连接的字段** ：经常用于连接的字段可能是一些外键列，对于外键列并不一定要建立外键，只是说该列涉及到表与表之间的联系。对于被频繁连接的字段，可以考虑建立索引，提高多表连接查询的效率。



### 28.正确使用索引的一些建议？

* **被频繁更新的字段应该慎重建立索引**

* **限制每张表上的索引数量**：索引并不是越多越好，建议单张表索引不超过5个！

* **尽可能考虑建立联合索引而不是单列索引** 

* **注意避免建立冗余索引** ：冗余索引指的是索引的功能相同，能够命中索引(a, b)就肯定能命中索引(a) ，那么索引(a)就是冗余索引。如（name,city ）和（name ）这两个索引就是冗余索引，能够命中前者的查询肯定是能够命中后者的 。在大多数情况下，都应该尽量扩展已有的索引而不是创建新索引。

  

### 29.索引失效的情况

* 使用`select *` 查询

* 创建组合索引，但查询条件未遵守最左前缀匹配原则

* 在索引列上进行**计算、函数、类型转换**等

* 以 % 开头的 LIKE 语句查询，比如说：`liek %abc` 。但是像`like abc%` 这样的会走一部分索引。

* 查询条件中使用or，且or的前后条件有一个列没有索引，涉及的索引都不会被使用到

* 索引字段上使用 `!=` 、`<>` 、`not in` 时，索引可能会失效

* 索引字段上使用`is null`，`is not null` ，可能导致索引失效

* mysql估计使用全表查询比使用索引要快，则不使用索引

  

### 30.如何获取执行计划？

`explain` 执行计划支持`select` ,`delete` ,`insert` ,`update` 等语句。我们一般多用于分析`select` 查询语句，使用起来非常简单，语法如下：

```sql
EXPLAIN + SELECT 查询语句；
```

我们简单来看下一条查询语句的执行计划：

```mysql
explain SELECT * FROM dept_emp WHERE emp_no IN (SELECT emp_no FROM dept_emp GROUP BY emp_no HAVING COUNT(emp_no)>1);
```

结果如下：

```sql
+----+-------------+----------+------------+-------+-----------------+---------+---------+------+--------+----------+-------------+
| id | select_type | table    | partitions | type  | possible_keys   | key     | key_len | ref  | rows   | filtered | Extra       |
+----+-------------+----------+------------+-------+-----------------+---------+---------+------+--------+----------+-------------+
|  1 | PRIMARY     | dept_emp | NULL       | ALL   | NULL            | NULL    | NULL    | NULL | 331143 |   100.00 | Using where |
|  2 | SUBQUERY    | dept_emp | NULL       | index | PRIMARY,dept_no | PRIMARY | 16      | NULL | 331143 |   100.00 | Using index |
+----+-------------+----------+------------+-------+-----------------+---------+---------+------+--------+----------+-------------+
------

```

可以看到，执行计划结果中共有12列，各列代表含义总结如下：

![image-20230315220633920](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230315220633920.png)

有几个重要的字段需要特别注意：

* key : 表示实际用到的索引，如果为NULL，则表示未用到索引。
* type : 描述了查询是如何执行的。所有值的顺序从优到最差排序为：**system > const > eq_ref > ref > fulltext > ref_or_null > index_merge > unique_subquery > index_subquery > range > index > ALL** 。其中all代表全表扫描，性能最差。
* Extra : 额外信息，通过这些信息，可以更准确的理解MySQL是如何执行的。



### 31.MySQL三大日志

MySQL InnoDB存储引擎使用 **redo log（重做日志）** 保证事务的持久性，使用  **undo log（回滚日志）** 来保证事务的原子性。MySQL数据库的数据备份、主备、主主、主从都离不开`binlog` ，需要依靠 **bin log** 来同步数据，保证数据一致性。



### 32.SQL优化手段有哪些？

* **select** 中尽量不要使用 *。
* 尽量减少子查询，用关联查询替代（left join , right join, inner join）。
* 减少 in 或者 not in 的使用，尽量使用 **exists ,not extsts** 替代。
* or 的查询尽量使用 **union 或者 union all**代替（当不用考虑重复数据或者不需要剔除重复数据时，使用 union all 效率 更好）。
* 应该尽量**避免在 where 子句中使用 != 或者 < >操作符**，不会走索引而是会走全表扫描。
* where 字句中尽量不要出现对字段进行 null 值判断，否则将不走索引而是走全表扫描。可以将对应的字段设置为0，确保该字段没有 null 值。



### 33.什么是内连接、左外连接、右外连接？

* 内连接（inner join）：匹配两张表中关联的记录。
* 左外连接（left join）：除了匹配两张表中关联的记录外，还会匹配左表中剩余的记录，同时右表中未匹配的字段用NULL来表示。
* 右外连接（right join）：除了匹配两张表中关联的记录外，还会匹配右表中剩余的记录，同时左表中未匹配到的字段用NULL来表示。



### 34.说一说MySQL中一条查询语句是如何查询的？

* 取得连接，检查是否有权限。
* 查询缓存（不建议使用缓存，在MySQL 8.0 已经去除）。
* 分析器进行词法分析和语法分析，检查语法是不是有错误。
* 优化器，使用优化算法来优化sql语句。
* 执行器，在这一步还要进行权限校验，如果校验通过那么就去存储引擎中执行语句，并返回结果。



### 35.varchar 和 char的区别？

* char 是**固定长度**的类型，varchar 是**可变长度**的类型。
* varchar(30) 表示最多存放30个字符。一个字符串 “hello” ，varchar(30) 和varchar(150) 所占的空间一样，但是后者要比前者在排序时消耗更多内存。
* 对效率要求高使用char，对空间要求高使用varchar。



### 36.MyISAM和InnoDB中的索引有什么异同呢？

**两者里面的索引的底层数据结构都是B+树。**

* 在myisam中，b+树的叶子节点的data域存放的是数据记录的地址。在查找索引时，如果指定的key存在，那么取出data域里面的值，然后以data域的值为地址读取相应的数据记录。这称为”**非聚簇索引**“。

* 在innodb中，b+树的叶子节点的data域存放的是完整的数据记录。这个索引的key就是数据表的主键，这称为”**聚簇索引**“ 。

* 其余的索引则称为“**辅助索引**” ，辅助索引的data域存储相应记录主键的值而不是地址，这也是和myisam不同的地方，在根据辅助索引查找时，则需要先取出主键的值，再走一遍主索引。

  

### 37.什么是索引下推？

索引下推（Index Condition Pushdown）是一种数据库查询优化技术，它在查询时将过滤条件下推至存储引擎层面进行处理，可以减少从存储引擎返回的数据量，从而提高查询性能。

在传统的查询优化中，数据库会先使用索引进行数据筛选，然后再根据其他过滤条件进行筛选。但是，有些过滤条件并不是所有的数据都满足的，**传统的查询优化方法会将这些不符合条件的数据都查出来，再在内存中进行过滤，这样会造成大量不必要的I/O操作，导致查询性能下降。**

而索引下推则会将过滤条件下推至存储引擎层面，让存储引擎来处理不符合条件的数据，减少了从存储引擎返回的数据量，从而提高查询性能。具体实现方式是在查询过程中，**将所有的过滤条件都下推至存储引擎层面进行处理，这样存储引擎只需要将满足条件的数据返回给数据库即可，减少了不必要的I/O操作和内存开销。**

需要注意的是，索引下推适用于某些特定的查询场景，如多表连接、分组查询、排序查询等。在其他查询场景下，索引下推可能并不会带来明显的性能提升，因此需要根据实际情况来选择使用。 



### 38.MySQL的三大日志了解吗？

* redo log （重做日志）
* binlog （归档日志）
* undo log（回滚日志）

![image-20230329012955255](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230329012955255.png)

### 39.请你说说redo log日志？

redo log日志是innodb 存储引擎特有的，它让MySQL拥有了崩溃恢复的能力。

比如说MySQL实例宕机了，**重启时，innodb引擎会使用`redo log`恢复数据，保证数据的持久性与完整性。**

MySQL中的数据以页为单位（通常是16kb），查询一条记录，会从硬盘里面把一页数据加载出来，加载出来的数据叫做数据页，会放入到`Buffer pool` 中，后续的查询都是去`Buffer Pool` 中找，没有命中再去硬盘加载，减少硬盘 `IO` 开销，提升性能。

更新数据的时候，发现 `Buffer Pool` 里存在要更新的数据，就直接在 `Buffer Pool` 里更新。

然后会把“某个数据页上做了什么修改”记录到重做日志缓存（redo log buffer）里，接着刷盘到`redo log`文件里。

![image-20230329013809095](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230329013809095.png)



**刷盘时机** ：

理想情况下，事务一提交就会进行刷盘操作，但实际上，刷盘是根据策略来选择的。

`InnoDB` 存储引擎为 `redo log` 的刷盘策略提供了 `innodb_flush_log_at_trx_commit` 参数，它支持三种策略：

* 0：表示每次事务提交不进行刷盘操作
* 1：表示每次事务提交都进行刷盘操作（默认值）
* 2：表示每次事务提交时都只把 redo log buffer 内容写入 page cache

`innodb_flush_log_at_trx_commit` 参数默认为 1 ，也就是说当事务提交时会调用 `fsync` 对 redo log 进行刷盘。

`InnoDB` 存储引擎有一个后台线程，每隔`1` 秒，就会把 `redo log buffer` 中的内容写到文件系统缓存（`page cache`），然后调用 `fsync` 刷盘。

![image-20230329014420550](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230329014420550.png)

也就是说，一个没有提交事务的 redo log 记录，也会进行刷盘。



### 40.请你说说binlog日志？

`binlog` 是逻辑日志，记录内容是语句的原始逻辑，类似于“给 ID=2 这一行的 c 字段加 1”，属于`MySQL Server` 层。

不管用什么存储引擎，只要发生了表数据更新，都会产生 `binlog` 日志。

那 `binlog` 到底是用来干嘛的？

可以说`MySQL`数据库的**数据备份、主备、主主、主从**都离不开`binlog`，需要依靠`binlog`来同步数据，保证数据一致性。

![image-20230413215910345](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230413215910345.png)

`binlog`会记录所有涉及更新数据的逻辑操作，并且是顺序写。



**记录格式**

`binlog` 日志有三种格式，可以通过`binlog_format`参数指定。

- **statement**

- **row**

- **mixed**

  

**写入机制**

`binlog`的写入时机也非常简单，事务执行过程中，先把日志写到`binlog cache`，事务提交的时候，再把`binlog cache`写到`binlog`文件中。

因为一个事务的`binlog`不能被拆开，无论这个事务多大，也要确保一次性写入，所以系统会给每个线程分配一个块内存作为`binlog cache`。

我们可以通过`binlog_cache_size`参数控制单个线程 binlog cache 大小，如果存储内容超过了这个参数，就要暂存到磁盘（`Swap`）。

`binlog`日志刷盘流程如下

![image-20230413230606384](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230413230606384.png)

- **上图的 write，是指把日志写入到文件系统的 page cache，并没有把数据持久化到磁盘，所以速度比较快**
- **上图的 fsync，才是将数据持久化到磁盘的操作**

`write`和`fsync`的时机，可以由参数`sync_binlog`控制，默认是`0`。

为`0`的时候，表示每次提交事务都只`write`，由系统自行判断什么时候执行`fsync`。

虽然性能得到提升，但是机器宕机，`page cache`里面的 binlog 会丢失。

为了安全起见，可以设置为`1`，表示每次提交事务都会执行`fsync`，就如同 **redo log 日志刷盘流程** 一样。

最后还有一种折中方式，可以设置为`N(N>1)`，表示每次提交事务都`write`，但累积`N`个事务后才`fsync`。



### 41.请你说说undo log 日志？

我们知道如果想要保证事务的原子性，就需要在异常发生时，对已经执行的操作进行**回滚**，在 MySQL 中，恢复机制是通过 **回滚日志（undo log）** 实现的，所有事务进行的修改都会先记录到这个回滚日志中，然后再执行相关的操作。如果执行过程中遇到异常的话，我们直接利用 **回滚日志** 中的信息将数据回滚到修改之前的样子即可！并且，回滚日志会先于数据持久化到磁盘上。这样就保证了即使遇到数据库突然宕机等情况，当用户再次启动数据库的时候，数据库还能够通过查询回滚日志来回滚将之前未完成的事务。

另外，`MVCC` 的实现依赖于：**隐藏字段、Read View、undo log**。在内部实现中，`InnoDB` 通过数据行的 `DB_TRX_ID` 和 `Read View` 来判断数据的可见性，如不可见，则通过数据行的 `DB_ROLL_PTR` 找到 `undo log` 中的历史版本。每个事务读到的数据版本可能是不一样的，在同一个事务中，用户只能看到该事务创建 `Read View` 之前已经提交的修改和该事务本身做的修改



### 42.explain语句

`EXPLAIN` 关键字在 MySQL 中用于查看 SQL 查询语句的执行计划，返回的结果通常是一个表格，包含以下列：

1. `id`: 查询块的唯一标识符，通常为数字，表示查询中的每个子查询或表。
2. `select_type`: 查询类型，表示查询的类型，如 `SIMPLE`（简单查询）、`PRIMARY`（最外层查询）、`SUBQUERY`（子查询）、`DERIVED`（派生表查询）等。
3. `table`: 表名，表示查询操作涉及到的表。
4. `type`: 访问类型，**表示 MySQL 在执行查询时使用的访问方法**，如 `ALL`（全表扫描）、`index`（索引扫描）、`range`（范围扫描）等。**`const`表示查询使用了常量条件进行索引查找**。
5. `possible_keys`: 可能使用的索引，表示 MySQL 可能会使用的索引列。
6. `key`: **实际使用的索引**，表示 MySQL 实际使用的索引列。
7. `key_len`: 索引长度，表示 MySQL 使用的索引的长度。
8. `ref`: 关联条件，表示连接表之间的关联条件，如外键等。
9. `rows`: 扫描的行数，表示 MySQL 扫描的行数。
10. `Extra`: 额外信息，表示其他一些关于查询执行的附加信息，如是否使用了临时表、是否使用了文件排序等。

通过分析 `EXPLAIN` 的查询结果，可以判断查询语句是否高效地利用了索引，是否存在潜在的性能问题，并根据需要进行优化。











# 六、常用框架



### 1.spring包含哪些模块？

#### Core Container

Spring框架的核心模块，也可以说是基础模块，主要提供ioc依赖注入功能的支持。Spring其他所有的功能基本上都需要依赖这个模块。

* **spring-core:** Spring框架基本的核心工具类；
* **spring-bean:** 提供对bean的创建，配置和管理等功能；
* **spring-content:** 提供对国际化、事件传播、资源加载等功能的支持；
* **spring-expression:** 提供对表达式语言（Spring Expression Language） SpEL的支持，只依赖于core模块，不依赖于其他模块，可以单独使用。



#### AOP

* **spring-aspects:** 该模块为与AspectJ的继承提供支持；

* **spring-aop:** 提供了面向切面的编程实现；

* **spring-instrument：**提供了为 JVM 添加代理（agent）的功能。 具体来讲，它为 Tomcat 提供 了⼀个织⼊代理，能够为 Tomcat 传递类⽂件，就像这些⽂件是被类加载器加载的⼀样。没有 理解也没关系，这个模块的使⽤场景⾮常有限。

  

#### Data Access/Integration

* **spring-jdbc:** 提供了对数据库访问的抽象JDBC。不同的数据库都有自己独立开发的API用于操作数据库，而java程序员只需要与JDBC API 交互，这样就屏蔽了数据库的影响。

* **spring-tx:** 提供对事务的支持。

* **spring-orm:** 提供对JPA、iBatis、Hibernate等ORM框架的支持。

* **spring-oxm ：**提供⼀个抽象层⽀撑 OXM(Object-to-XML-Mapping)，例如：JAXB、Castor、 XMLBeans、JiBX 和 XStream 等。

* **spring-jms：**消息服务。⾃ Spring Framework 4.1 以后，它还提供了对 spring-messaging 模块 的继承。

  

#### Spring Web

* **spring-web**: 对Web功能的实现提供一些最基础的支持。
* **spring-webmvc:** 提供对Web MVC的支持。
* **spring-websocket:** 提供了对WebSocket的支持，WebSocket可以让客户端和服务器进行双向通信。
* **spring-webflux：** 提供对 WebFlux 的⽀持。WebFlux 是 Spring Framework 5.0 中引⼊的新的 响应式框架。与 Spring MVC 不同，它不需要 Servlet API，是完全异步。



### 2.谈谈你对Spring IoC的理解

**IoC（Inverse of Control:控制反转）** 是一种设计思想，而不是一种技术的具体体现。**IoC的思想就是将原本在程序中手动创建对象的控制权，交给框架来管理**。IoC在其他语言中也有应用。

将对象之间相互依赖的关系交给IoC容器来进行管理，并由IoC容器来进行注入，这可以很大程度上简化应用的开发。

在Spring中，IoC容器是Spring用来实现IoC的载体，**IoC实际上是一个Map(key,value)的结构，里面存放着对象。**



### 3.什么是Spring Bean?

**Bean实际上指的是那些被IoC管理的对象。**

我们需要告诉IoC容器我们要管理哪些对象，因此我们需要配置元数据。**配置元数据可以通过XML文件、注解或者java配置类来实现。**



### 4.将一个类声明为Bean的注解有哪些？

* `@Component` : 通用的注解，可以标注任一类为`Spring`的组件，如果不知道一个Bean属于哪一层，可以用`Conponent`注解来实现。
* `@Service`: 在服务层上的注解，主要涉及到一些复杂的逻辑。
* `@Controller`：在控制层上的注解，对应Spring MVC 的控制层，主要是接收用户的请求，然后调用Service层并将数据返回给前端界面。
* `@Repository`: 对应持久层，即DAO层，主要用于数据库相关操作。



### 5.@Component和@Bean的区别？

* `@Component`注解主要作用于类，而`@Bean`主要作用在方法上。
* `@Component` 通常是通过扫描类路径来自动检测以及自动装配到Spring容器中（我们可以使用`@ComponentScan`注解定义要扫描的路径从中找到需要装配的类并且自动装配到Spring容器中）。而`@Bean`是在标注该注解的方法上来产生这个bean,当我们需要的时候让它返还给我们。
* `@Bean`比`@Component` 自定义更强，而且很多地方我们都只能通过`@Bean`来注册bean。比如我们需要引用第三方库的类装配到spring 容器中时，就需要用到`@Bean` 来实现。

`@Bean` 使用示例：

```java
@Configuration
public class AppConfig {
	@Bean
	public TransferService transferService() {
		return new TransferServiceImpl();
 	}
}
```

上面的代码相当于下面的xml配置：

```xml
<beans>
	<bean id="transferService" class="com.acme.TransferServiceImpl"/>
</beans>
```



### 6.注入bean的注解有哪些？

`Spring`内置的`@Autowired` 和JDK自带的`@Resource`和`Inject`都可以注入bean。

![image-20230309153758691](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230309153758691.png)

当然,`@Autowired` 和 `@Resource` 使用得更多一点。



### 7.`@AutoWired ` 和`@Resource`   有什么区别？

`@Autowired`是spring内置的注解，它是通过`by Type`（即根据类型匹配）来实现注入的。也就是说会优先根据接口的类型去匹配并注入bean（接口的实现类）。

但是这样会造成一个问题，那就是如果接口有多个实现类的话，那么这个时候spring容器就不知道匹配哪一个了。

如果`@Autowired`通过`by Type`的方式匹配不成功，那么就会通过`by Name`（即通过名称匹配）来实现注入。这个名称通常是类名的首字母小写。

举个例⼦， `SmsService` 接⼝有两个实现类: `SmsServiceImpl1` 和 `SmsServiceImpl2` ，且它们都已经被 Spring 容器所管理。

```java
//注入失败，首先通过by Type来匹配，但是发现有两个实现类，所以匹配失败，
//然后通过by Name 来匹配，结果两个实现类的名字都不对应
//所以这句代码报错
@Autowired
private SmsService smsService;

//通过名称，注入成功(smsServiceImpl1就是实现类的类名并且是首字母小写)
@Autowired
private SmsService smsServiceImpl1;

//注入成功，通过另外一个注解@Qualifier来指定具体的实现类的名称
@Autowred
@Qualifier(value = "smsServiceImpl1")
private SmsService smsService;
```



`@Resource` 是JDK自带的注解，它默认是通过`by Name`是实现注入的。如果无法通过名称匹配到对应的bean的话，就会通过`by Type`的形式来注入。

```java
//注入失败 先通过by Name,但因为两个实现类的名称都不是smsService，所以失败
//然后通过 by Type，但是有两个实现类，所以不行
@Resource
private SmsService smsService;

//注入成功 因为名称是正确的
@Resource
private SmsService smsServiceImpl1;

//注入成功 通过name属性来指定具体的实现类
@Resource(name = "smsServiceImpl1")
private SmsService smsService;
```

总结一下就是：

* `@Autowired`是spring自带的注解，`@Resource` 是JDK提供的注解。
* `@Autowired`默认的注入方式是`by Type`（按照类型匹配）,`@Resource`默认的注入方式是`by Name`（按照名称匹配）。
* `Autowired`可以通过`@Qualifier`注解显示指定名称，`Resource`则可以通过`value`属性来显示指定名称。



### 8.Bean的作用域有哪些？

* **request（仅web应用可用）**: 每一次HTTP请求都会产生一个新的bean（请求bean），该bean仅在当前HTTP request内生效。
* **session（仅web应用可用）：**每一次来自新session的HTTP请求都会产生一个新的bean（会话bean），该bean仅在当前HTTP session内生效。
* **singleton:** Ioc容器中只有唯一的bean实例。**Spirng中的bean默认都是单例的，是Spring对单例模式的运用。**
* **prototype:** 每次获取都会创建一个新的bean。也就是说连续两次`getBean()`，获取到的都是不同的bean实例。
* **application/global-session（仅在web应用可用）：** 每个web程序在启动时创建一个bean（应用bean），该bean在应用程序启动时间内生效。
* **websocket（仅在web应用可用）：** 每一次websocket会话都会产生一个新的bean。

如何配置bean的作用域呢？

XML方式：

```xml
<bean id="..." class="..." scope="singleton"></bean>
```

注解方式：

```java
@Bean
@Scope(value = ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public Person personPrototype() {
	return new Person();
}
```



### 9.单例Bean的线程安全问题

对于单例bean来说，所有线程都共享一个单例bean实例，所以会存在资源竞争的问题，因此单例bean存在线程安全问题。

如果单例bean是一个无状态的bean，也就是线程中的操作不会对bean的成员执行除了==查询==以外的操作，那么单例bean从某种程度上来说是线程安全的。比如我们开发中经常说到的`Controller`、`Service`、`Dao`层等。这些bean都都是无状态的，只关注方法本身。

**为什么我们说`Controller`、`Service`、`Dao`这些bean都是无状态的呢？**

因为我们一般在开发中，在这些层里面我们通常不会去定义成员变量，**只是去调用实例的方法，而每个线程调用方法都会去生成一个个的栈帧，这些虚拟机栈是每个线程独有的，会在自己的工作内存中去工作，所以是安全的**。因此在这种情况下我们不用担心这些层的线程安全问题。

常见的有两种解决办法：

1.在bean中尽可能避免定义可变的变量。

2.在类中定义一个`ThreadLocal`成员变量，将需要的可变成员变量保存在`ThreadLocal`当中（推荐的一种方式）。

### 10.Bean的生命周期了解吗？

* Bean 容器找到配置⽂件中 Spring Bean 的定义。
* Bean 容器利⽤ Java Reflection API 创建⼀个 Bean 的实例。
* 如果涉及到⼀些属性值 利⽤ set() ⽅法设置⼀些属性值。
* 如果 Bean 实现了 BeanNameAware 接⼝，调⽤ setBeanName() ⽅法，传⼊ Bean 的名字。
* 如果 Bean 实现了 BeanClassLoaderAware 接⼝，调⽤ setBeanClassLoader() ⽅法，传⼊ ClassLoader 对象的实例。
* 如果 Bean 实现了 BeanFactoryAware 接⼝，调⽤ setBeanFactory() ⽅法，传⼊ BeanFactory 对 象的实例。
* 与上⾯的类似，**如果实现了其他 *.Aware 接⼝，就调⽤相应的⽅法。**
* 如果有和加载这个 Bean 的 Spring 容器相关的 BeanPostProcessor 对象，执⾏ postProcessBeforeInitialization() ⽅法。
* 如果 Bean 实现了 InitializingBean 接⼝，执⾏ afterPropertiesSet() ⽅法。
* 如果 Bean 在配置⽂件中的定义包含 init-method 属性，执⾏指定的⽅法。
* 如果有和加载这个 Bean 的 Spring 容器相关的 BeanPostProcessor 对象，执 ⾏ postProcessAfterInitialization() ⽅法。
* 当要销毁 Bean 的时候，如果 Bean 实现了 DisposableBean 接⼝，执⾏ destroy() ⽅法。
* 当要销毁 Bean 的时候，如果 Bean 在配置⽂件中的定义包含 destroy-method 属性，执⾏指定 的⽅法。

![image-20230309210708256](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230309210708256.png)

总结来说，分为以下几个步骤：

1. 实例化阶段：在该阶段，spring容器会使用反射机制创建bean实例，此时还没有进行任何依赖注入或者其他处理。
2. 设置对象属性：spring容器会将bean的属性值注入到bean的实例中，可以通过构造函数注入、setter方法注入、接口注入等方式进行属性赋值。
3. Aware接口回调阶段：spring容器会调用实现了Aware接口的bean的相关方法，比如BeanNameAware,BeanFactoryAware,ApplicationContentAware等，让bean获取spring容器相关的信息。
4. BeanPostProcessor前置处理阶段：spring容器会调用实现了BeanPostProcessor接口的类的postProcessBeforeInitialization方法，对bean进行预处理。
5. 初始化方法调用阶段：spring容器会调用bean的初始化方法，包括实现了InitializingBean接口的afterPropertiesSet方法以及通过注解方式配置的初始化方法。
6. BeanPostProcess后置处理阶段：spring容器会调用实现了BeanPostProcessor接口的类的postProcessAfterInitialization方法，对Bean进行后置处理。
7. 使用阶段：在该阶段，bean实例被应用程序使用。
8. 销毁阶段：该阶段，Spring容器会调用实现了DisposableBean接口的destroy方法以及通过注解方式配置的销毁方法，销毁Bean实例。



### 11.谈谈自己对AOP的理解

AOP（Aspect-Oriented Programming） 即面向切面编程。它能够将那些与业务无关，但是每个业务都需要用到的功能（事务处理，日志管理，权限控制）封装起来，从而减少系统代码的重复量，简化了开发，有利于以后的拓展。

切面，即`切点`跟`通知`的联系，下面是一些专业术语：

![image-20230309215630132](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230309215630132.png)

Spirng AOP 的实现是基于代理模式的运用，而且是动态代理，它由两种**动态代理**模式来实现：

* **JDK动态代理**：Spring默认使用JDK动态代理来实现AOP，如果要**代理的对象实现了某个接口，**那么Spring就会采用这种方式去实现。JDK动态代理是通过==反射==来完成代理的。
* **CGlib动态代理：**JDK动态代理是代理了实现了接口的类，但是如果不能实现的类，这个时候就需要用到CGlib动态代理了，它是通过**继承**的方式，直接操作字节码，生成要代理对象的子类，重写类的方法完成代理。



### 12.Spring AOP 和 AspectJ AOP有什么区别？

**Spring AOP 属于运行时增强，Aspect AOP属于编译时增强。**前者基于代理，后者基于字节码操作。

Spring AOP 已经集成了 AspectJ ，AspectJ 应该算的上是 Java ⽣态系统中最完整的 AOP 框架了。

AspectJ 相⽐于 Spring AOP 功能更加强⼤，但是 Spring AOP 相对来说更简单， 如果我们的切⾯比较少，那么两者性能差异不⼤。但是，当切⾯太多的话，最好选择 AspectJ ，它 ⽐ Spring AOP 快很多。



### 13.AspectJ 定义的通知类型有哪些？

* **Before（前置通知）：**目标对象的方法调用之前触发。
* **After（后置通知）：**目标对象的方法调用之后触发。
* **ArterReturning（返回通知）：**目标对象的方法调用完成，在返回结果值之后触发。
* **AfterThrowing（异常通知）：**目标对象在调用过程中抛出异常之后触发。
* **Around（环绕通知）：**在调用方法前后触发都可以。



### 14.多个切面的执行顺序如何控制？

* 第一种：通常使用`@Order`注解直接定义切面顺序：

  ```java
  @Order(3)
  @Component
  @Aspect
  public class LoggingAspect implements Ordered {
      
  }
  ```

* 第二种：实现`Ordered`接口重写`getOrder`方法：

  ```java
  @Component
  @Aspect
  public class LoggingAspect implements Ordered {
      // ....
      @Override
      public int getOrder() {
      	// 返回值越⼩优先级越⾼
      	return 1;
      }
  }
  ```

  

### 15.什么是Spring MVC?

**MVC是模型（Model）、视图（View）、控制器（Controller）的缩写，**其核心思想是通过将业务逻辑、数据、显示分离来组织代码。。Spring MVC 可以帮助我们进⾏更简洁的 Web 层的开发，并且它天⽣与 Spring 框架集成。Spring MVC 下我们⼀般把后端项⽬分为 Service 层（处理业务）、Dao 层（数据库操作）、Entity 层（实体类）、Controller 层(控制层，返回数据给前台页面)。



### 16.Spring MVC 的核心组件有哪些？

* `DispatcherServlet`：**核心的中央处理器**，处理接收请求、分发，并返回信息给客户端。

* `HandlerMapping`：**处理器映射器**，根据地址去匹配`Handler`，并将请求涉及到的拦截器和`Handler`一起封装。

* `HandlerAdapter`： **处理器适配器**，根据处理器映射器找到的处理器，适配具体的处理器，然后执行处理器。

* `Handler`：**请求处理器**，处理实际的请求。

* `ViewResovler`：**视图解析器**，根据处理器返回的视图渲染出真正的视图，然后通过`DispatcherServlet`传递给前端。

  

### 17.Spring MVC 的工作原理了解吗？

工作流程如下：

![image-20230309225602930](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230309225602930.png)

1. 客户端（浏览器）发送请求， **DispatcherServlet** 拦截请求。

2. **DispatcherServlet** 根据请求信息调⽤ **HandlerMapping** 。 **HandlerMapping** 根据 uri 去匹配查找 能处理的 **Handler** （也就是我们平常说的 **Controller** 控制器） ，并会将请求涉及到的拦截器和 Handler ⼀起封装。

3. **DispatcherServlet** 调⽤ **HandlerAdapter** 适配执⾏ **Handler** 。

4. **Handler** 完成对⽤户请求的处理后，会返回⼀个 **ModelAndView** 对象给 **DispatcherServlet** ， ModelAndView 顾名思义，包含了数据模型以及相应的视图的信 息。 Model 是返回的数据对象， View 是个逻辑上的 View 。

5. **ViewResolver** 会根据逻辑 **View** 查找实际的 **View** 、

6. **DispaterServlet** 把返回的 **Model** 传给 **View** （视图渲染）。

7. **View** 返回给请求者（浏览器）。



### 18.统一异常处理怎么做？

推荐使用注解的方式统一异常处理，具体会使用到`ControllerAdvice` + `@ExceptionHandler`这两个注解。

```java
@ControllerAdvice
public class AllExceptionHandler {

    @ExceptionHandler(Exception.class)
    @ResponseBody
    public ResultInfo doException(Exception exception) {
        exception.printStackTrace();
        return ResultInfo.fail(-999, "系统异常");
    }
}
```

在这种处理方法下，会给所有或指定的`Controller` 织入异常处理的逻辑（AOP），当`Controller`中的方法抛出异常的时候，由被`@ExceptionHandler`修饰的方法进行处理。



### 19.Spring框架中用到了哪些设计模式？

* **工厂模式：**Spring 使用工厂模式通过`BeanFactory` 、`ApplicationContext`创建bean对象。
* **代理模式：**Spring AOP功能的实现就用到了代理模式。
* **单例模式：**Spring中的bean默认是单例的。
* **模板方法模式：**Spirng 中的`jdbcTemplet`、`hibernateTemplate`等以**Template**结尾的对数据库操作的类，他们就是用到了模板模式。
* **观察者模式：**Spring 事件驱动模型就是观察者模式的一个经典应用。
* **包装器模式：**我们的项目需要连接多个数据库，而且不同的客户在每次访问中会根据需要去访问不同的数据库。这种模式让我们可以根据用户的需求能够动态地切换不同的数据源。
* **适配器模式：**Spring AOP 的增强或是通知（advice）使用到了适配器模式，Spring MVC中也用到了适配器模式去匹配`Controller`。



### 20.Spring管理事务的方式有几种？

* **编程式事务：**即在代码中硬编码（不推荐使用）,通过`TransactionTemplate` 或者 `TransactionManager`手动管理事务，在实际应用中很少用。
* **声明式事务：**在XML配置文件中配置或者直接基于注解（推荐使用），实际上是通过AOP实现（基于`Transactional`的全注解方式使用最多）。



### 21.@Transactional（rollbackFor = Exception.class）注解了解吗？

`Exception`分为`RuntimeException`和非运行时异常。事务管理对于企业应用来说是至关重要的，即使出现异常，它也可以保护数据的一致性。

当`@Transactional`注解作用于类上时，该类的所有public 方法都将具有该类型的事务属性，同时，我们也可以用在方法上来覆盖用在类上的定义。如果类或者方法用上了这个注解，那么在这个类的方法中出现异常的时候，就会回滚，数据库里面的数据也会回滚。

在`Transactional`注解中如果不配置`rollbackFor`属性，那么事务只有在遇到`RuntimeException`时候才会回滚，加上`rollbackFor = Exception.class`,可以让事务在遇到非运行时异常也可以回滚。



### 22.#{} 和${} 的区别是什么？

* `${}` 是Properties文件中的变量**占位符**，它可以使用与标签属性值和sql内部，**属于静态文本替换。**比如`${driver}`会被静态替换为 `com.mysql.jdbc. Driver` 。
* `#{}` 是sql的参数占位符，Mybatis会将`#{}`替换成 ? 号，在sql执行之前会使用`prepareStatement`的参数设置方法，按照顺序来设置参数值。

总结：**`#{}`是预编译处理，`${}`是文本替换。**预编译可以很好的防止SQL注入。



### 23.XML文件中，除了常见的select、update、delete、insert标签之外，还有哪些标签？

还有很多标签：

* `<resultMap>`、`<sql>`、`<include>`等， `<sql>`为sql片段标签，通过`<include>`标签引入sql片段，`<resultMap>`为表与实体的映射关系。
* sql的动态标签：if 、where 、foreach 、choose 、trim 、when 等。



### 24.Dao接口的工作原理是什么？

通常一个XML文件，都会对应一个Dao接口与之对应。Dao层接口就是我们常说的`Mapper`接口，接口的全限定名，就是XML文件中`nameSpace`的值，接口的方法，就对应MXL文件中的`id`值，接口方法的参数，就对应传给sql的参数。

接口是没有实现类的，当调用接口方法时，会将`接口全限定名`+`方法名`作为一个key，去到对应的XML文件中寻找到对应的语句（即对应的标签），比如说`<select>`、`<update>`、`<delete>`和`<insert>`标签。

Dao接口的工作原理是`JDK动态代理`**,Mybatis运行时会使用JDK动态代理来为Dao接口生成代理对象，代理对象会拦截接口方法，转而执行XML文件中对应的sql语句，并将执行结果返回。**



### 25.Dao接口中的方法可以重载吗？

网上众说纷纭，有的说可以重载，有的说不可以重载，并且都举出了例子。关于这道题，可以试着去跟面试官讲讲你自己的理解。



### 26.Mybatis是如何进行分页的？分页插件的原理是什么？

* Mybatis使用`RowBounds`对象分页，他是针对ResultSet结果集的逻辑分页（**就是先把数据全部查询出来，然后再在结果中检索分页的数据，缺点是消耗大量内存，有内存溢出的风险**）,并不是物理分页（**从数据库中查出具体条数的数据，弥补了一次性全部查出的所有数据的种种缺点**）。

* 可以在SQL语句中直接书写物理分页的参数来进行分页。

* 也可以使用分页插件来进行分页。

  

分页插件的原理是**使用Mybatis提供的插件接口，实现自定义插件，在插件的拦截方法内拦截待执行的sql，然后重写sql，根据`dialect`方言，添加对应的物理分页语句和分页参数。**



### 27.Mybatis是如何将sql执行结果封装成目标对象并返回的？都有哪些映射方式？



* 第一种：通过`<resultMap>` 标签，逐一定义表中的列名跟实体类中的属性名的映射关系。
* 第二种：通过sql的别名功能，将属性名当做列名的别名，从而完成映射。

**有了列名和属性名的映射关系后，Mybatis根据==反射==创建对象，同时通过反射给对象的属性一一赋值，然后将结果返回。那些找不到映射关系的属性名，是无法完成赋值的。**



### 28.Mybatis能执行一对一、一对多的关联查询吗？

可以。

对象关联查询，有两种实现方式：

* **分步查询**：先去将关联对象查出来，然后再赋给主对象。
* **单步查询：**意味着使用join查询，SQL只用写一句。

在 MyBatis 中，通过`<resultMap>`标签的子标签`<association>` 处理**一对一级联关系**。如下所示（分部查询）：

```xml
<mapper namespace="net.biancheng.mapper.StudentMapper">
    <!-- 一对一根据id查询学生信息：级联查询的第一种方法（嵌套查询，执行两个SQL语句） -->
    <resultMap type="net.biancheng.po.Student" id="cardAndStu1">
        <id property="id" column="id" />
        <result property="name" column="name" />
        <result property="sex" column="sex" />
        <!-- 一对一级联查询 -->
        <association property="studentCard" column="cardId"
            javaType="net.biancheng.po.StudentCard"
            select="net.biancheng.mapper.StudentCardMapper.selectStuCardById" />
    </resultMap>
    <select id="selectStuById1" parameterType="Integer"
        resultMap="cardAndStu1">
        select * from student where id=#{id}
    </select>
</mapper>
```

对应的实体类为：

```java
package net.biancheng.po;

public class Student {
    private int id;
    private String name;
    private int sex;

    private StudentCard studentCard;

    /*省略setter和getter方法*/

    @Override
    public String toString() {
        return "Student [id=" + id + ", name=" + name + ", sex=" + sex + ", studentCard=" + studentCard + "]";
    }
}
```

在 MyBatis 中，通过`<resultMap>`标签的子标签`<association>` 处理**一对多级联关系**。如下所示（分部查询）：

```xml
<!-- 一对多 根据id查询用户及其关联的订单信息：级联查询的第一种方法（分步查询） -->
<resultMap type="net.biancheng.po.User" id="userAndOrder1">
    <id property="id" column="id" />
    <result property="name" column="name" />
    <result property="pwd" column="pwd" />
    <!-- 一对多级联查询，ofType表示集合中的元素类型，将id传递给selectOrderById -->
    <collection property="orderList"
        ofType="net.biancheng.po.Order" column="id"
        select="net.biancheng.mapper.OrderMapper.selectOrderById" />
</resultMap>
<select id="selectUserOrderById1" parameterType="Integer"
    resultMap="userAndOrder1">
    select * from user where id=#{id}
</select>
```

对应的实体类为：

```java
package net.biancheng.po;

import java.util.List;

public class User {
    private int id;
    private String name;
    private String pwd;
    private List<Order> orderList;

    /*省略setter和getter方法*/

    @Override
    public String toString() {
        return "User [id=" + id + ", name=" + name + ", orderList=" + orderList + "]";
    }
}
```



关于这方面可以看看这里([MyBatis一对一关联查询 (biancheng.net)](http://c.biancheng.net/mybatis/one-to-one.html#:~:text=MyBatis一对一关联查询 1 示例 下面以学生和学号为例讲解一对一关联查询的处理过程。 1）创建数据表 创建 student（学生）和 studentcard（学号）数据表，SQL,  ))关联查询。



### 29.Mybatis是否支持延迟加载？如果支持，它的原理是什么？

在这里，有必要认识一下什么是延迟加载？举这样一个例子：

我们有一个用户，他有一百个账户，试想一下：

1. 在查询用户信息时，要不要把关联的账户信息查询出来？
2. 在查询账户信息时，要不要把关联的用户信息查询出来？

* 对于第一个问题，我们应该是什么时候需要查询账户信息，才查询。没必要每次查询用户信息都把账户信息也查询出来。因为如果每次都查询出账户信息，对我们的内存开销是很大的，而且每次查询也都不一定用到账户信息。
* 对于第二个问题，我们就可以在查询账户信息的时候查询出关联的用户信息，因为我们如果只是单纯的账户信息没有说明用户是谁，这对于我们来说是不友好的。也没什么意义，所以在每次查询账户信息的时候都要显示出关联的用户信息。

第一个问题实际上是**延迟加载**，第二个问题实际上是**立即加载**。

* **延迟加载**：在真正的使用数据时才发起查询，不用的时候不查。按需加载（懒加载）。
* **立即加载：**不管用不用，只要一调用方法，马上发起查询。



**Mybatis仅支持`association`管理对象和`collection`关联集合对象的延迟加载**。association指的就是⼀对⼀，collection指的就是⼀对多查询。在Mybatis配置文件中，可以配置是否启用延迟加载`lazyLoadingEnabled`属性，值可以是`true`和`false`。

延迟加载的原理是：使用`CGLIB` 创建目标代理对象，当调用目标方法时，进入拦截器方法，比如调用`a.getB().getName()` ，拦截器 `invoke()` 方法发现`a.getB()` 是 null 值，那么就会单独发送事先保存好的关联B对象的sql,把B查询上来，然后调用 `a.getB()` ，于是 a的对象 b属性就有了，接着完成`a.getB().getName()` 的调用。



### 30.为什么说Mybaits是半自动 ORM映射工具？它与全自动的区别在哪里？

Hibernate 属于全自动ORM映射工具，使用 Hibernate 查询关联对象或者关联集合对象时，可以根据对象模型关系直接获取，所以它是全自动的，但是Mybatis在查询关联对象或者关联集合对象时，需要手动编写sql来完成，所以它被称为半自动ORM映射工具。



### 31.依赖注入的方式有几种，各是什么？

* **构造器注入**：通过构造函数将被依赖对象传入依赖对象，并且在初始化对象的时候注入。

  优点：对象初始化完成后便可以获得可使用的对象。

  缺点：当需要注入的对象很多时，构造器参数列表会很长，不够灵活。

* **setter方法注入** ：通过调用成员变量提供的setter方法将被依赖对象注入依赖类。

  优点：可以选择性的注入需要的对象。

  缺点：依赖注入初始化完成后由于尚未注入被依赖对象，因此还不能使用。

* **接口注入** ：依赖类必须要实现指定的接口，然后实现该接口中的一个函数，该函数用于依赖注入。该函数的参数就是要注入的对象。

  优点：接口注入中，接口的名字、函数的名字都不重要，只要保证函数的参数是要要注入的对象的类型即可。

  缺点：侵入性太强，不推荐使用。（侵入性就是如果类A要使用别人提供的功能，需要在自己的类中增加额外的代码，这就是侵入性。）

  

### 32.Spring事务中有哪几种事务传播行为？

事务传播行为是为了解决业务层之间方法相互调用的事务问题。

当事务方法被另外一个事务方法调用时，必须指定事务该怎么传播。例如：方法可能继续在现有事务中运行，也有可能重新开启一个事务，并在自己的事务中运行。比如说A 方法调用 B方法，需要指定B方法中的事务传播规则。常见的有以下几种：

* **PROPAGATION_REQUIRED** ：使用的最多的一个事务传播行为，也是Spring 默认的事务传播级别。我们平常经常使用的`@Transactional` 注解默认的就是使用这个事务传播级别。它的意思是，如果当前存在事务，则加入当前事务，如果当前不存在事务，则创建一个新的事务。

* **PROPAGATION_REQUIRED_NEW** ：创建一个新的事务。如果当前存在事务，则把当前事务挂起。也就是说不管外部方法是否开启事务，被`PROPAGATION_REQUIRED_NEW` 修饰的内部方法都会新开启自己的事务，且开启的事务相互独立，互不干扰。

* **PROPAGATION_NESTED** ：如果当前存在事务，则创建一个事务作为当前事务的嵌套事务来运行，如果当前不存在事务，则开启一个新的事务，类似于`PROPAGATION_REQUIRED` 。

* **PROPAGATION_MANDATORY** ：如果当前存在事务，则加入当前事务。如果当前没有事务，则抛出异常。（mandatory：强制性）

  

上面的事务传播都会发生回滚，但是如果错误的配置了下面的三种，那么事务将不会发生回滚：

* **PROPAGATION_SUPPORTS** ：如果当前存在事务，则加入该事务，如果当前不存在事务，则以**非事务**的方式继续运行。
* **PROPAGATION_NOT_SUPPORTS** ：以非事务的方式运行，如果当前存在事务，则挂起当前事务。
* **PROPAGATION_NEVER** ：以非事务的方式运行，如果当前存在事务，则抛出异常。



### 33.JDK动态代理和CGLIB动态代理有什么区别？

1. JDK动态代理只能代理实现了接口的类，而CGLIB动态代理可以代理没有实现接口的类。

2. JDK动态代理是基于接口实现的，它通过接口中的方法来生成代理对象，因此它只能代理接口中已有的方法；而CGLIB动态代理是基于子类实现的，它通过继承被代理类来生成代理对象，因此它可以代理被代理类中所有非final的方法。

3. JDK动态代理生成的代理对象性能相对较低，因为它是通过反射来调用被代理方法的；而CGLIB动态代理生成的代理对象性能相对较高，因为它是通过继承被代理类并生成子类来实现代理的。

4. JDK动态代理只需要引入JDK包，而CGLIB动态代理需要引入第三方包，因此JDK动态代理更加轻量级。

   

综上所述，如果被代理类实现了接口，建议使用JDK动态代理；如果被代理类没有实现接口，或者需要代理类中的所有方法，建议使用CGLIB动态代理。



### 34.JDK动态代理的简单实现？

* 定义一个接口，里面定义方法：

  ```java
  public interface UserDao {
      void save();
  }
  ```

* 定义一个类，实现上面的接口，并且重写里面的方法：

  ```java
  public class UserDaoImpl implements UserDao{
      @Override
      public void save() {
          System.out.println("保存用户");
      }
  }
  ```

* 编写一个代理类，实现`InvocationHandler` 接口，重写里面的`invoke`方法：

  ```java
  public class UserDaoProxy implements InvocationHandler {
  
      private Object target;
  
      public UserDaoProxy(UserDao userDao) {
          this.target = userDao;
      }
  
      @Override
      public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
          System.out.println("事务执行前");
          method.invoke(target, args);
          System.out.println("事务执行后");
          return null;
      }
  }
  ```

  `invoke`方法中的三个参数分别为代理对象、目标方法对象以及方法的参数数组。

* 编写测试：

  ```java
  public class JDKTest {
      public static void main(String[] args) {
          UserDao userDao = new UserDaoImpl();
          UserDaoProxy userDaoProxy = new UserDaoProxy(userDao);
          UserDao proxyInstance = (UserDao)Proxy.newProxyInstance(userDao.getClass().getClassLoader(),
                  userDao.getClass().getInterfaces(), userDaoProxy);
          proxyInstance.save();
      }
  }
  ```

  使用`Proxy` 类的`newProxyInstance` 来创建代理实例，该方法中的三个参数分别为被代理类的ClassLoader，被代理类要实现的接口列表以及InvocationHandler对象。

  上面的代码输出为：

  ```java
  事务执行前
  保存用户
  事务执行后
  ```

  

### 35.BeanFactory跟ApplicationContenxt有什么区别？

BeanFactory和ApplicationContext是Spring框架中两个重要的接口，用于管理和获取Java对象（也称为Bean）的实例。它们之间的区别如下：

1. 初始化时机：BeanFactory是Spring IoC容器的基本接口，负责创建和管理Bean的生命周期，但它在初始化时并不会主动实例化Bean，而是在获取Bean时才进行实例化。而ApplicationContext是BeanFactory的子接口，它在容器初始化时就会主动实例化和管理所有的Bean，并且支持各种扩展特性，例如事件发布、国际化、资源加载等。
2. 功能和扩展特性：ApplicationContext相比于BeanFactory提供了更多的功能和扩展特性。例如，ApplicationContext支持AOP（面向切面编程）、事务管理、消息处理、缓存管理等。它也支持各种外部配置文件（如属性文件、XML文件、注解等）的加载和解析，从而支持更灵活的配置和管理方式。
3. 生命周期管理：ApplicationContext在管理Bean的生命周期上比BeanFactory更加方便。ApplicationContext支持多种方式的Bean生命周期管理，包括单例（Singleton）、多例（Prototype）、请求作用域（Request）、会话作用域（Session）等。而BeanFactory只支持单例和多例两种方式。
4. 自动装配（Autowiring）：ApplicationContext相比BeanFactory在自动装配方面更加强大。ApplicationContext支持五种自动装配方式：no（不自动装配）、byName（根据Bean的名称自动装配）、byType（根据Bean的类型自动装配）、constructor（根据构造函数自动装配）、autodetect（根据Bean的名称和类型自动装配）。而BeanFactory只支持byType和byName两种方式。
5. 性能和内存占用：由于ApplicationContext在容器初始化时会主动实例化和管理所有的Bean，因此相比BeanFactory在性能和内存占用上会稍有一些差异。BeanFactory在容器初始化时延迟实例化和管理Bean，因此在一些性能要求较高的场景下可能会更加适合。

总的来说，ApplicationContext是Spring框架的高级容器，提供了更多的功能和扩展特性，适合大多数的应用场景。而BeanFactory则是Spring框架的基础容器，适用于一些对性能要求较高、功能需求较简单的场景。



### 36.springboot自动装配的原理？

@SpringbootApplication注解里面有一个@EnableAutoConfiguration注解，该注解下面有个@Import注解，@Import注解导入了AutoConfigurationImportSelector。然后根据里面一些方法，找到jar包下面的 META-INF目录下面的 `spring.factories`文件，里面存储了各种键值对，这些键值对就是对应的类。然后加载这些类来实现一个自动装配的过程。



### 37.jar包和 war包有什么区别？

JAR（Java ARchive）和WAR（Web ARchive）都是Java中用于打包和部署应用程序的文件格式，但它们在用途和应用场景上有一些区别。

1. JAR包：JAR包是一种用于打包和发布Java应用程序的文件格式，通常包含Java类、资源文件、配置文件和库文件等。JAR包可以包含可执行的Java应用程序，也可以作为Java库（例如，Java类库、第三方库等）在其他Java应用程序中引用。JAR包通常用于Java SE（标准版）和Java EE（企业版）应用程序。
2. WAR包：WAR包是一种用于打包和发布Java Web应用程序的文件格式，通常包含Web应用程序的Servlet、JSP、HTML、CSS、JavaScript等文件，以及配置文件、资源文件和库文件等。WAR包用于将Java Web应用程序部署到支持Java Servlet规范的Web服务器（例如Tomcat、Jetty等）中。WAR包通常用于Java EE（企业版）应用程序。

主要区别如下：

- 用途：JAR包用于打包和部署Java应用程序，而WAR包用于打包和部署Java Web应用程序。
- 内容：JAR包通常包含Java类、资源文件、配置文件和库文件等，而WAR包通常包含Web应用程序的Servlet、JSP、HTML、CSS、JavaScript等文件，以及配置文件、资源文件和库文件等。
- 部署目标：JAR包可以直接运行，也可以作为Java库在其他Java应用程序中引用；而WAR包主要用于部署到支持Java Servlet规范的Web服务器中，用于运行Java Web应用程序。
- 扩展性：JAR包通常可以在不同的Java SE和Java EE环境中使用，而WAR包通常只能在支持Java Servlet规范的Web服务器中使用。
- 文件结构：JAR包通常是一个压缩文件，包含多个文件和目录；而WAR包也是一个压缩文件，但其内部文件结构按照Java Web应用程序的目录结构进行组织，例如WEB-INF目录下包含Web应用程序的配置文件和资源文件等。

需要注意的是，虽然JAR包和WAR包在用途和应用场景上有一些区别，但它们都是Java应用程序的一种打包和部署方式，可以根据具体需求选择使用哪种方式来组织和部署Java应用程序。



### 38.Springboot支持哪些日志框架？推荐和默认的日志框架是哪个？

Logback,log4j2, 还有 java util logging。

默认使用Logback作为日志框架。



### 39.@Slf4j有什么作用呢？

`@Slf4j` 是一种用于在 Java 类中引入日志记录功能的注解。它是由 Lombok 这个 Java 库提供的，可以通过在类上添加 `@Slf4j` 注解来自动生成常见日志记录框架（如 Logback、Log4j2、JDK Logging 等）的日志记录代码。

具体而言，`@Slf4j` 注解会自动在类中生成一个名为 `log` 的私有静态 final 字段，其类型根据所使用的日志记录框架而定，例如使用 Logback 则生成 `private static final org.slf4j.Logger log = org.slf4j.LoggerFactory.getLogger(ClassName.class);`。这样，类中就可以直接使用 `log` 字段进行日志记录，而无需手动创建和初始化 Logger 实例。

使用 `@Slf4j` 注解可以简化日志记录的代码编写，减少样板代码，提高开发效率。同时，它还可以通过 Lombok 的插件在编译时自动生成日志记录框架的相应依赖，避免了手动添加日志记录框架的繁琐配置步骤。

需要注意的是，在使用 `@Slf4j` 注解时，需要事先在项目中引入相应的日志记录框架的依赖，并进行相应的配置，以便日志记录正常工作。

如果你希望更换日志框架，可以按照以下步骤进行操作：

1. 添加新的日志框架依赖

2. 移除原有的日志框架依赖

3. 配置新的日志框架依赖

4. 重新构建和启动项目

   

### 40.springboot打成的jar包跟普通的jar包有什么区别？

![image-20230407005157016](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230407005157016.png)





### 41.运行springboot的方式有哪几种？

1. **打包用命令或者放到容器中去运行**

   使用内嵌的 Servlet 容器：Spring Boot 默认集成了内嵌的 Servlet 容器，如 Tomcat、Jetty 或 Undertow，可以将 Spring Boot 应用程序打包成一个可执行的 JAR 文件，并通过 `java -jar` 命令来运行。

   ```java
   java -jar my-spring-boot-app.jar
   ```

   

2. **用maven插件运行**

   Spring Boot 提供了 Maven 和 Gradle 插件，可以通过在项目的 pom.xml 或 build.gradle 文件中配置相应的插件，然后使用 Maven 或 Gradle 构建工具来运行 Spring Boot 应用程序。例如，在 Maven 中可以使用以下命令运行：

   ```java
   mvn spring-boot:run
   ```

3. **直接执行main方法**





### 42.mybatis 逻辑分页和物理分页的区别是什么？

* **逻辑分页** 

  逻辑分页是指在应用程序层面进行分页处理，也称为内存分页。在逻辑分页中，**查询结果从数据库中一次性获取全部数据，然后在应用程序层面进行分页处理，即在内存中对查询结果进行切片，只返回需要的分页数据**。逻辑分页的实现通常通过在 SQL 查询语句中使用 LIMIT、OFFSET、ROWNUM 等关键字来限制查询结果集的大小，从而实现分页效果。

* **物理分页**

  物理分页是指在数据库层面进行分页处理，也称为数据库分页。在物理分页中，**数据库仅返回需要的分页数据，而不是一次性获取全部数据**。物理分页通常通过数据库的特定功能，如 MySQL 的 LIMIT、Oracle 的 ROWNUM、SQL Server 的 ROW_NUMBER 等来实现。物理分页的优点是可以减少数据传输量和内存占用，对大数据集查询性能较好。

两者区别如下：

1. 数据库压力：逻辑分页会将查询结果一次性从数据库中加载到应用程序内存中，而物理分页只会加载需要的分页数据，减轻了数据库的查询压力。

2. 数据传输量：逻辑分页需要一次性将查询结果传输到应用程序中，而物理分页只传输需要的分页数据，减少了数据传输量。

3. 内存占用：逻辑分页需要将查询结果集加载到应用程序内存中，占用较大的内存空间，而物理分页只加载需要的分页数据，内存占用较小。

4. 性能表现：逻辑分页在应用程序层面进行分页处理，可能对大数据集查询性能较差，而物理分页在数据库层面进行分页处理，通常具有较好的性能表现。

   

### 43.mybatis的物理分页和逻辑分页的具体实现？

#### 物理分页

##### 采用limit分页（物理分页）

* 实体类：

  ```java
  @Data
  public class User {
      private Integer id;
      private String username;
      private Date birthday;
      private String sex;
      private String address;
  }
  ```

  

* SQL语句：

  ```xml
  <select id="listUser" resultMap="BaseResultMap">
      select * from user
      <if test="pageNum!=null and pageSize!=null">
          limit #{pageNum},#{pageSize}
      </if>
  </select>
  ```

* Mapper方法：

  ```java
  List<User> listUser(Integer pageNum,Integer pageSize);
  ```

  

##### 使用PageHelper分页插件（物理分页）

* pom文件中引入PageHelper依赖

```xml
<dependency>
    <groupId>com.github.pagehelper</groupId>
    <artifactId>pagehelper-spring-boot-starter</artifactId>
    <version>1.2.3</version>
</dependency>
```

* SQL语句：

  ```xml
  <!--pageHelper-->
  <select id="listUser2" resultMap="BaseResultMap">
      select * from user
  </select>
  ```

* Mapper方法：

  ```java
  List<User> listUser2();
  ```

* 测试：其中`PageHelper.startPage()`方法用于开启分页，通过拦截SQL的方式(**只要在该方法后面执行的SQL都会被拦截，在前面执行的SQL语句则不会被拦截**),把查询语句拦截下来加上limit。

  ```java
  @Test
  void test2() {
      //pageNum为前端传递过来的分页后的“当前处在第几页”，默认在第一页
      int pageNum=1;
      //pageSize，表示每页存放的记录数
      int pageSize=4;
      PageHelper.startPage(pageNum,pageSize);
      List<User> users = userDao.listUser2();
      //得到分页对象
      PageInfo<User> page = new PageInfo<>(users);
      for (User user : page.getList()) {
          System.out.println(user.toString());
      }
  }
  ```

  

##### 使用 mybatis plus分页

MyBatisPls分页是基于 MyBatis的**物理分页**，开发者无需关心具体操作，配置好插件之后，写分页等同于普通 List 查询。

- SpringBoot引入MyBatis-plus依赖

  ```xml
  <dependency>
      <groupId>com.baomidou</groupId>
      <artifactId>mybatis-plus-boot-starter</artifactId>
      <version>3.3.2</version>
  </dependency>
  ```

- 配置yml配置文件

  ```yaml
  spring:
    #配置数据源
    datasource:
      driver-class-name: com.mysql.cj.jdbc.Driver
      url: jdbc:mysql://localhost:3306/students?serverTimezone = Asia/Shanghai
      username: root
      password: root
  
  
  # Mybatis-plus配置
  mybatis-plus:
    mapper-locations: classpath*:/mapper/*Mapper.xml
    # 配置mybatis数据返回类型别名
    type-aliases-package: com.example.mp.pojo
    configuration:
      # 自动驼峰命名
      map-underscore-to-camel-case: false
  
  # 配置sql打印，指向mapper的包
  logging:
    level:
      com.example.mp.mapper: debug
  server:
    port: 8081
  ```

- 配置`PaginationInterceptor`分页拦截器组件

  ```java
  @Configuration
  public class MyBatisPlusConfig {
  
      @Bean
      public PaginationInterceptor paginationInterceptor(){
          return new PaginationInterceptor();
      }
  }
  ```

- 定义Mapper接口

  ```java
  public interface UserMapper extends BaseMapper<User> {
  }
  ```

- 测试：

  ```java
  @Test
  void test() {
      Page<User> page = new Page<>(1,4);
      Page<User> userPage = userMapper.selectPage(page,null);
      for(User user:userPage.getRecords){
          System.out.println(user.toString());
      }
  }
  ```

  

#### 逻辑分页

##### RowBounds（逻辑分页）

RowBounds分页属于逻辑分页，即实际上SQL查询的是所有的数据，然后在业务层对数据进行可截取(即对ResultSet结果集进行分页)，该方式比较占用内存，在大数据量的情况下不推荐使用！

* SQL语句

  ```xml
  <!--RowBounds-->
  <select id="listUser3" resultMap="BaseResultMap">
      select * from user
  </select>
  ```

* Mapper方法

  ```java
  List<User> listUser3(RowBounds rowbouns);
  ```

* 测试：取第一页的4行数据

  ```java
  @Test
  void test3() {
      RowBounds rowBounds = new RowBounds(0, 4);
      List<User> users = userDao.listUser3(rowBounds);
      for (User user : users) {
          System.out.println(user.toString());
      }
  }
  ```

  

### 44.为什么PageHelper.startPage() 方法之前的查询语句不会被拦截，而只拦截PageHelper.startPage()后面的查询语句呢？

PageHelper.startPage() 方法之前的查询语句不会被拦截是因为 PageHelper 插件是基于 MyBatis 的拦截器（Interceptor）机制实现的。MyBatis 的拦截器是通过动态代理（Dynamic Proxy）来实现的，当执行查询语句时，MyBatis 会将查询语句封装成一个 Statement 对象，然后通过拦截器的方式对 Statement 对象进行增强处理。

PageHelper 插件的拦截器会在执行查询语句时拦截对应的 Statement 对象，判断是否需要进行分页处理，如果需要分页，则会生成对应的分页 SQL，并替换原始的查询语句。但在调用 PageHelper.startPage() 方法之前的查询语句还没有生成对应的 Statement 对象，因此不会被拦截。

PageHelper.startPage() 方法的作用是设置分页参数，包括页码和每页显示的记录数等信息，以便 PageHelper 插件在后续的查询语句中生成对应的分页 SQL。只有在调用 PageHelper.startPage() 方法之后的查询语句才会生成对应的 Statement 对象，并经过插件的拦截器进行分页处理。因此，PageHelper.startPage() 方法之前的查询语句不会被拦截，仍然会按照原始的 SQL 进行查询。

一般情况下，PageHelper.startPage() 方法之后的**第一个查询语句会被拦截**，生成分页 SQL。**之后的查询语句也会被拦截**，生成相应的分页 SQL，以确保分页效果能够在连续的多次查询中得以保持一致。当然，如果在 PageHelper.startPage() 方法之后没有执行查询语句，那么就不会有查询语句被拦截和生成分页 SQL。





















# 七、计算机网络



### 1.OSI七层模型是什么？

OSI七层模型是一个网络分层模型，按照自底向上的分层，可分为以下：

* **物理层**：传输比特流
* **数据链路层**：帧编码和误差纠错
* **网络层：**路由和寻址
* **传输层：**数据传输
* **会话层：**管理应用程序之间的会话
* **表现层：** 数据处理（编码，压缩）
* **应用层：** 为用户提供服务



### 2.TCP/IP四层模型是什么?

OSI七层模型偏向于理论，TCP/IP四层模型是真正应用的模型，按照自底向上可分为：

* **网络接口层**
* **网络层**
* **传输层**
* **应用层**



### 3.我们一般学习网络，将其分为几层？

五层。

自底向上分别为：

* **物理层**
* **数据链路层**
* **网络层**
* **传输层**
* **应用层**

分为这些层是为了方便我们学习。



### 4.物理层是什么？知道信道（单工、半双工、全双工）吗？

物理层定义了**接口标准、传输速率、传输方式**等。

信道：数据传输的通道，一条传输介质上可以有多条信道。

#### 单工

* 信号只能往一个方向传输，任何时候都不能改变方向
* 常见的有**无线电广播**、**有线电视广播**

#### 半双工

* 信号可以**双向传输**,但是必须交替进行，同一时间只能往一个方向传输
* 常见的比如**对讲机**

#### 全双工

* 信号可以双向传输，且可以同时传输
* 比如说**手机**，打电话可以同时进行听和说

### 5.数据链路层有哪些协议？要解决的基本问题是什么？

* 广播信道：**CSMA/CD协议**（比如同轴电缆、集线器等组成的网络）
* 点对点信道：**PPP协议**（比如两个**路由器**之间的通信）



数据链路层要解决的三个基本问题如下：

* **透明传输**
* **差错检测**
* **封装成帧**



### 7.网络层有哪些协议？都有什么作用？

* **IP协议：**是TCP/IP协议中最重要的协议之一，也是网络层的重要协议。主要分为两种：IPv4和IPv6。目前后者已经取代前者。互联网上的每一个主机都有一个IP地址。

* **ARP协议：**也称全地址解析协议。他的作用是将**IP地址转换成MAC地址。**

* **ICMP协议：** 互联网控制消息协议，通常用于返回错误信息。

* **NAT协议：** 网络地址转换协议，应用在内部网到外网的地址转换过程中，具体的来说，就是**在同一个局域网下的所有私有IP计算机想要访问公网资源，那么就需要一个具有公网IP和NAT功能的设备来访问公网资源** ，这就需要NAT协议的帮助。

  

### 8.传输层有哪些协议？都有什么用？

传输层主要使用以下两种协议：

* **传输控制协议TCP（Transmisson Control Protocol）:** 提供面向**连接的**、可靠的数据传输服务。
* **用户数据协议DCP（User Datagram Protocol）:** 提供**无连接的**、尽最大努力的数据传输服务。（不保证可靠传输）

### 9.应用层具有哪些协议？都有什么作用？

应用层具有很多种协议：

* **超文本传输协议HTTP（HyperText Transfer Protocol）:** 主要是为了web浏览器和web服务器之间的通信进行设计的。HTTP是基于TCP协议的，目前所使用的HTTP协议大都在1.1。
* **文件传输协议FTP**： 主要提供文件传输的功能，基于TCP实现的可靠传输。
* **简单邮件传输（发送）协议SMTP（Simple Mail Transfer Protocol）** : 负责发送电子邮件，基于TCP。
* **邮件传输协议（POP3/IMAP）:** **接收**电子邮件的协议。
* **远程登录协议Telent** ： 专为远程登录会话和其他服务器提供安全性的协议。基于TCP。
* **安全的网络传输协议SSH** : 目前较为可靠，专为远程登录会话和其他服务器提供安全性的协议，基于TCP。**Telent和SSH最主要的区别在于SSH协议会对传输的数据进行加密，确保数据安全性。**
* **域名系统DNS协议** ：由于IP地址不方便记忆，并且不能表达组织的名称和性质，所以人们设计出了域名系统。DNS协议可以让我们通过域名寻找到对应的IP地址。**基于UDP协议。**
* **动态主机配置DHCP协议** ：从DHCP服务器自动获取IP地址。使用场景为：移动设备，无线设备等。**基于UDP协议。**



### 10.TCP和UDP的区别？

![image-20230312022717511](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230312022717511.png)

解释一些不明白的地方：

* TCP是有状态的，这个有状态说的是TCP会去记录自己发送消息的状态，会维持复杂的连接状态表。但是UDP是无状态服务，发出去就不管其他事情了。
* TCP只至此点对点通信，UDP支持一对一，一对多，多对一，多对多。

### 11.TCP三次握手是什么？

示意图如下：

![image-20230312150016264](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230312150016264.png)

建立一个TCP连接需要”三次握手“，缺一不可。

一些名词解释：

* **SYN** : 同步序列编号（Synchronize Sequence Numbers）是TCP/IP建立连接时的握手信号。当`SYN=1,ACK=0`时，表示这是一个建立连接的请求，如果对方同意建立连接，那么就回复`SYN=1,ACK=1`。第二次握手时传回SYN的目的是：为了告诉客户端：”我确实收到你传给我的信息了“。
* **seq** :序号（Sequence Number），代表**这一次传给对方的TCP数据部分的第一个字节的编号。**
* **ack** :确认编号（Acknowlledgment Number），代表**希望下一次对方传过来的TCP数据部分的第一个字节的编号。**
* **ACK** : 确认位（Acknowledgment）,一般作大写（当然也不一定，没有明确的规范），当`ACK=1`时，**确认编号字段**才有效。

### 12.为什么要三次握手？

总的来说，三次握手的目的是为了确保双方的接收和发送能力都是正常的。

1. 当第一次握手时，客户端什么都不能确认，服务端确认了：自己接收正常，对方发送正常。
2. 当第二次握手时，客户端确认了：自己接收、发送正常，对方发送、接收正常。服务端确认了：自己接收正常，对方发送正常。
3. 当第三次握手时，客户端确认了：自己接收、发送正常，对方接收、发送正常。服务端确认了：自己接收、发送正常，对方接收、发送正常。

三次握手就能够确认双方收发功能都正常，缺一不可。



### 13.什么是四次挥手？

**断开连接**需要“四次挥手”。示意图如下：

![image-20230312160243324](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230312160243324.png)

* **FIN** : finish，当`FIN=1` 时，表名数据已经发送完毕，请求断开连接。

TCP在设计上，允许任意一方先请求断开连接，这里演示的是客户端先发起断开连接的请求。

### 14.为什么要四次挥手？

**TCP是全双工通信**，任何一方都可以在数据传输完成之后发起断开连接的通知，等待对方确认后进入半关闭状态。当另一方也没有数据要发送时，则发出释放连接的通知，对方确认之后就完全关闭了TCP连接。

**第一次挥手：**当主机1发出FIN报文时，表明主机1已经没有什么东西要发送了，但是主机1还可以接收来自主机2的数据。

**第二次挥手：** 当主机2返回ACK报文时，表明主机2知道主机1没有数据发送了，但是主机2还是可以发送数据到主机1。

**第三次挥手：** 当主机2发出FIN报文时，表明主机2没有什么数据发给主机1了。

**第四次挥手：** 当主机1返回ACK报文时，表明主机1知道主机2没有什么数据要发送了，随后就开始正式断开TCP连接。



### 15.为什么第四次挥手客户端需要等待2*MSL（报文段最长寿命）时间后才进入CLOSED状态？

第四次挥手时，客户端发送给服务端的ACK报文可能丢失，造成服务端接收不到返回信号，这个时候服务端会重新发起FIN报文段，如果在这2*MSL时间内，客户端接收到了FIN报文，那么会重新发送ACK报文段并继续等待2 * MSL，防止服务端没有收到ACK而不断重发FIN，因此必须有一个时间来限制，不然一收不到信号就重发那就不行了。 

* **MSL（maximum Segement LifeTime）:** 一个片段在网络上的最大存活时间，2MSL就是一段发送和一段回复的时间。



### 16.HTTP和HTTPS的区别？

* **端口**：HTTP端口默认是80端口，HTTPS默认端口是443。
* **URL前缀：** HTTP前缀是`http://`，HTTPS的前缀是`https://`。
* **安全性：** HTTP传输的东西都是明文，不安全；HTTPS运用加密算法，安全程度更高。
* **开销：** 和HTTP相比，HTTPS通信会因为加解密从而消耗更多的CPU资源。同时HTTPS通常都需要证书或者向专业机构购买。



### 17.说一下HTTP的长连接和短连接？

#### 短连接

**在HTTP/1.0中默认的就是使用短连接**。即客户端与服务器每进行一次HTTP操作，就进行一次HTTP连接，任务结束之后立马断开连接。比如说我们要访问某个服务器上面的`HTML`资源，这个时候就进行一次连接，访问完之后就断开连接。

#### 长连接

**在HTTP/1.1中默认的就是使用长连接。** 跟短连接相反，当客户端与服务端完成任务后，HTTP并不会断开连接，如果后面客户端需要继续访问服务器的资源，则会继续利用该HTTP。当然，长连接是有时间限制的，`Keep-Alive`属性可以开启长连接。 



### 18.HTTP状态码有哪些？

![image-20230312235150720](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230312235150720.png)

#### 1xx (信息状态码)

平时大概率不会遇到，所以这里略过。

#### 2xx（成功状态码）

* **200 OK** : 请求被处理成功。
* **201 Created** ：请求被成功处理并且在服务端创建了资源。比如说我们通过POST请求创建一个新的用户。
* **202 Accepted** : 请求被接收，但是还没有处理。

#### 3xx （重定向状态码）

* **301**  ： **资源被永久重定向了**。比如说你要访问的网站换了网址。
* **302** ： **资源被临时重定向了。** 比如说你要访问的网站的某些资源被暂时转移到另外一个网站上。

#### 4xx（客户端错误状态码）

* **400 Bad Request** : 发送的请求存在错误。比如说请求方法不对，或者说参数错误。
* **401 Unauthorized** : 未认证却想要访问需要认证的资源。
* **403 Forbidden** : 直接拒接请求，一般用于处理非法请求。
* **404 Not Found** : 请求的资源在服务端未找到。
* **409 Conflit**  : 请求的资源跟服务器的状态存在冲突。

#### 5xx（服务端错误状态码）

* **500 Internal Server Error** : 服务器出现问题了（通常是服务器端的代码出现bug）。比如说服务器接收请求的时候出现异常，但是异常并没有被正确地处理。

* **502 Bad Gateway** : 我们的网关将请求转发到服务器上，但是服务器给的是一个错误的响应。

  

### 19.TCP如何保证传输的可靠性？

1. **序列号和确认号机制** ： TCP发送端发送数据的时候会给一个序列号seq，接收端接到后会检查数据的完整性，如果检测通过会发送确认号ack表示收到了数据包。
2. **超时重传机制** ：TCP发送端在发送数据的同时会启动一个定时器，如果到了一定时间，还没有收到接收端的确认信号，那么就会重新传送该数据包。
3. **排序和去重机制** ：数据包在发送过程中会乱序，TCP层会负责排好序。同时可能会出现包重复，TCP还会负责去重的工作。
4. **流量控制** ： TCP发送端和接收端都有一个固定大小的缓冲空间，为了防止发送端发送数据太快导致接收端缓冲区溢出，发送端只能发送接收端能容纳的数据，为了达到这种控制效果，TCP用了流量控制协议（**可变大小的滑动窗口协议**）来实现。
5. **拥塞控制** ： 当网络发生拥堵时，减少数据包的发送。



### 20.HTTP/1.0和HTTP/1.1有什么区别？

* **连接方式** ：HTTP/1.0是短连接，HTTP/1.1是长连接。
* **状态响应码** ： HTTP/1.1加入了很多状态响应码。
* **缓存策略** ：HTTP/1.1中引入了更多可供选择的缓存头来控制缓存策略。
* **Host头处理** ：HTTP/1.1在请求头中加入了`Host`字段。（虚拟主机技术）。



### 21.什么时候选择TCP，什么时候选择UDP？

* TCP用于**对传输准确性要求特别高**的场景，比如说文件传输，发送和接收邮件，远程登录等。

* UDP一般用于**即时通讯**，比如语音、视频、直播等，这些场景对传输数据的准确性要求不高，比如你看视频即使少一两帧，给人的感觉区别不大。

  

### 22.从输入URL到页面展示到底发生了什么？

* 浏览器查找域名的IP地址（按顺序通过浏览器缓存、路由器缓存、DNS缓存查找）。
* 建立TCP连接（三次握手）
* 发送HTTP请求
* 服务器处理请求并返回HTTP报文
* 浏览器解析并渲染页面
* 连接结束



### 23.Forward跟Redirect的区别？

**浏览器地址栏的变化**：

* `Forward`是**服务器内部的重定向**，**URL地址栏是不会发生改变的**；
* `Redirect`是客户端请求服务器，然后服务器给客户端返回了一个302状态码（**资源被临时重定向**）和新的location，然后客户端重新向新的location发送HTTP请求，此时**URL地址栏发生了变化**。

**数据的共享：**

* `forward`是在服务器内部的重定向，`request`在整个重定向过程中是不变的，所以request的信息在servlet间是共享的。
* `Redirect`发起两次HTTP请求分别使用不同的request。

**请求的次数** ：

* `Forward`请求只有一次，`Redirect`请求两次。



### 24.GET和POST请求有什么区别？

**用途** ：

* get请求是用来向服务器获取资源。
* post请求是用来向服务器提交数据。

**表单的提交方式** ：

*  get请求直接将表单的数据以`name1=value1&name2=value2`拼接到URL上面，参数之间用`&`隔开，且用`?`拼接到`action`后面。如：`http://www.baidu.com/action?name1=value1&name2=value2` 。
* post请求将表单的数据放在请求头或者请求体中。

**传输数据的大小限制** ：

* get请求传输数据的大小受URL长度的限制，而URL的长度取决于浏览器。
* post请求传输数据在理论上来说是无限制的。

**参数的编码** ：

* get请求的参数会在地址栏上展示，且用的是URL的编码格式。（URL编码一般是UTF-8编码）
* post请求使用二进制数据多重编码传递参数。

### 25.知道HTTP的报文格式吗？

![img](https://img-blog.csdnimg.cn/20210119001837544.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MzczNDA5NQ==,size_16,color_FFFFFF,t_70)

一个请求和响应的报文如下：

![image-20230313175131480](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230313175131480.png)

### 26.HTTP的头部字段了解哪些？

**请求头字段：** 

![image-20230313180304270](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230313180304270.png)

![image-20230313180358768](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230313180358768.png)

![image-20230313180430337](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230313180430337.png)



**响应头字段** ：

![image-20230313181539888](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230313181539888.png)

![image-20230313181608225](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230313181608225.png)

![image-20230313181722142](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230313181722142.png)



### 27.了解同源策略吗？

浏览器有个`同源策略`，默认情况下，AJAX只能访问同源的URL，就是说**不允许当前的源中的资源与其他源中的资源进行交互**。

同源是指三个同：**协议、域名（IP）、端口** 都相同

![image-20230313182414636](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230313182414636.png)



### 28.如何实现跨域？

#### JSONP方式

script、img、iframe、link、video、audio等带有src属性的标签可以跨域请求和执行资源。可以利用这一点实现跨域。

```html
<script>
 var scriptTag = document.createElement('script');
 scriptTag.type = "text/javascript";
 scriptTag.src = "http://10.10.0.101:8899/jsonp?callback=f";
 document.head.appendChild(scriptTag);
</script>
```

```js
$.ajax({
 // 请求域名
 url:'http://10.10.0.101:8899/login',
// 标明本次请求来自哪个源（协议+域名+端口）
Origin: http://127.0.0.1:8080
// IP
Host: 127.0.0.1:8080
// 长连接
Connection: keep-alive
Content-Type: text/plain
如果 Origin 标明的域名在服务器许可范围内，那么服务器就会给出响应：
 // 请求方式
 type:'GET',
 // 数据类型选择 jsonp
 dataType:'jsonp',
 // 回调方法名
 jsonpCallback:'callback',
});
// 回调方法
function callback(response) {
 console.log(response);
}
```

这种方式只支持`GET`请求。而且在服务端收到命令后，还会设置响应头，**添加`Access-Control-Allow-Origin`属性，属性值为`*`，表示允许所有域名访问，**这样浏览器才会正常解析。

```java
response.setHeader("Access-Control-Allow-Origin",*);
```



#### CORS方式

CORS（cross-Origin Resource Sharing） ，即跨域资源共享，需要服务器和浏览器同时支持。简单来说就是客户端在发送请求时，请求头会携带`Origin`属性，服务端响应的时候在响应头中添加`Access-Control-Allow-Origin`属性。然后浏览器判断根据返回的`Access-Control-Allow-Origin`属性判断是否允许当前地址访问，如果匹配不成功，那么浏览器报错。



#### 代理方式

跨域限制是由于**浏览器**的**同源策略**造成的，那么我们不用浏览器去访问就行了。

因此我们可以用nginx当做服务器访问别的服务器的HTTP接口，这样就不会收到浏览器的同源策略限制了。

可以利用Nginx创建一个代理服务器，这个代理服务器的域名要跟浏览器访问的域名一致，然后通过这个代理服务器修改cookie中的域名为要访问的HTTP接口的域名，通过反向代理实现跨域。

假设我们有两个域名：`www.example.com` 和 `api.example.com`，我们希望在 `www.example.com` 域名下的前端应用中请求 `api.example.com` 域名下的接口，但是因为跨域问题，请求会被浏览器拦截。

为了解决这个问题，我们可以使用 nginx 来做一个反向代理。

首先，在 `api.example.com` 域名下启动一个 Node.js 服务器，用于提供接口服务。这里为了简单起见，我们只提供一个 `/hello` 接口，返回一个字符串。

```js
// app.js
const http = require('http');

const server = http.createServer((req, res) => {
  if (req.url === '/hello') {
    res.setHeader('Content-Type', 'text/plain');
    res.end('Hello from api.example.com');
  } else {
    res.statusCode = 404;
    res.end();
  }
});

server.listen(3000, () => {
  console.log('Server running on http://localhost:3000');
});

```

然后，在 `www.example.com` 域名下的前端应用中，我们可以使用 axios 库发送请求。

```js
// index.js
import axios from 'axios';

axios.get('http://api.example.com/hello')
  .then(response => {
    console.log(response.data);
  })
  .catch(error => {
    console.error(error);
  });

```

这时候，我们会遇到跨域问题。为了解决这个问题，我们可以使用 nginx 做一个反向代理。

首先，在服务器上安装 nginx，然后在 nginx 的配置文件中添加如下配置：

```nginx
http {
  server {
    listen 80;   #表示监听在 80 端口上，等待来自客户端的请求
    server_name www.example.com; 
        #表示该 server 区块处理的请求域名为 example.com，也就是当客户端访问 example.com 时，会交给该 server 区块处理。
    
    location /api {
      proxy_pass http://api.example.com;
      add_header 'Access-Control-Allow-Origin' '*';
    }
    
    location / {
      root /path/to/www.example.com;
      index index.html;
    }
  }
}

```

这个配置的含义是：

- 当请求 `www.example.com/api` 路径时，反向代理到 `api.example.com` 域名下，并在响应头中添加 `Access-Control-Allow-Origin: *`，允许跨域请求。
- 当请求 `www.example.com` 路径时，返回 `/path/to/www.example.com` 目录下的 `index.html` 文件。

这样，在前端应用中，我们只需要修改请求的地址为 `http://www.example.com/api/hello`，就可以访问 `api.example.com` 域名下的 `/hello` 接口了。nginx 会将请求转发到 `api.example.com` 域名下，并在响应头中添加 `Access-Control-Allow-Origin: *`，允许跨域请求。（**是nginx添加，不是真正存放资源的服务器添加**）









### 29.反向代理和正向代理的区别？

* **正向代理代理的对象是客户端，** 比如说我们经常用代理软件去访问外国网站，俗称“翻墙”,这就是正向代理。正向代理的作用有：隐藏客户端IP，绕过防火墙限制等。

* **反向代理代理的对象是服务器，** 比如说某网站访问量太大，可以使用代理服务器来承担一部分流量。反向代理的作用有：隐藏服务器IP，负载均衡，安全防护等。

  

### 30.说一下TCP粘包是怎么产生的，如何解决粘包问题？

**TCP传输基于字节流**，从应用层到传输层的多个数据包是一串字节流是没有边界的，而且TCP首部并没有记录数据包的长度，所以TCP传输的时候容易出现粘包和拆包的问题。

而UDP是基于数据报传输数据的，而且UDP首部也记录了数据报的长度，可以轻易分出不同数据报的长度。

**发生粘包的原因：**

* 要发送的数据报小于TCP缓冲空间，然后TCP将多个数据包写满缓冲区一次性传出去。
* 接收端没有及时读取TCP缓冲区中的数据包，将会发生粘包。

**发生拆包的原因：** 

* TCP发送缓冲区剩余空间不足以发送一个完整的包，所以会发生拆包。
* 要发送的数据包超过了最大报文长度的限制，将会发生拆包。

**解决办法：** 

* 给数据包添加首部，首部中添加数据包的长度属性。
* 发送端给不同的数据包添加间隔符确定边界。



### 31.URI跟URL的区别是什么？

* URI：统一资源标志符，可以唯一标识一个资源。
* URL：统一资源定位符，可以提供该资源的路径。它是一种具体的URI，可以用来标识一个资源，而且还指明了如何找到这个资源。







# 八、Redis

### 1.Redis除了做缓存，还能做什么？

* **分布式锁** ：通过Redis来做分布式锁是一种比较常见的方式。通常情况下，我们都基于**Redisson**来实现分布式锁。
* **限流** ：一般通过**Redis+Lua脚本**的方式来实现限流。
* **消息队列** ：Redis自带的 `list` 数据结构可以作为一个简单的队列使用。Redis5.0中增加的Stream类型的数据结构更加适合用来做消息队列。
* **复杂业务场景** ：通过Redis 以及Redis扩展（比如Redisson）提供的数据结构，我们可以很方便的完成很多复杂的业务场景，比如通过`bitmap` 统计活跃用户、通过`sorted set` 维护排行榜。



### 2.Redis常用的数据结构有哪些？

我们知道Redis是一个 key-value型的数据库，里面存的所有数据都是 k-v 结构，**对于key来说，都是统一的 string类型**，值却有以下类型：

* **5种基础数据结构** ：String（字符串）、List（列表）、Set（集合）、Hash（散列）、Zset（有序集合）

* **3种特殊结构** ：HyperLogLogs（基数统计）、BitMap（位存储）、Geospatial（地理位置）

  

### 3.什么是缓存穿透？有哪些解决办法？

缓存穿透说简单一点就是**大量请求的key是不合理的，根本不存在于缓存中，也不存在于数据库中。** 这就导致那么多的请求直接到了数据库，根本没有经过缓存这一层，对数据库造成了巨大的压力。

解决办法：

* **参数校验** ：这是最简单的方法，一些不合法不合理的参数请求直接抛出异常或返回错误信息给客户端。比如说主键id不能小于0，电子邮箱格式传入错误等。

* **缓存无效的key** : 如果Redis和数据库中都没有某个key的数据，那么我们就写一个key到Redis中去并设置过期时间。这种方式可以解决请求的key变化不频繁的情况，如果黑客大量攻击，每次构建不同的key，会导致Redis中缓存大量的无效key。很明显，这种方法治标不治本，如果非要用这种方法的话，那么可以将key的过期时间设置得短一点。

* **使用布隆过滤器来快速判断数据是否存在** 。即一个请求查询过来时，先通过布隆过滤器判断值是否存在，存在才继续往下查找。

  ![image-20230407213740504](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230407213740504.png)

  布隆过滤器存在一定的误判，因为可能会存在哈希冲突。**解决办法是增加hash函数。**

  

### 4.什么是缓存击穿？有哪些解决办法？

缓存击穿简单的说就是**请求的key是热点数据，存在于数据库中，但是不存在缓存中（通常是因为缓存中的数据已经过期）** ，这可能会导致大量的请求直接打到数据库上，给数据库带来很大的压力。

解决办法：

* 设置热点数据永不过期或者过期时间比较长。
* **针对热点数据进行预热，将其存入缓存中并设置合理的过期时间**，比如说秒杀场景下的数据在秒杀结束之前永不过期。
* 请求数据库写数据到缓存之前，先获取互斥锁，保证只有一个请求会落到数据库上，减少数据库的压力。

### 5.什么是缓存雪崩？有哪些解决办法？

缓存雪崩就是**缓存在同一时间内大面积的失效，后面的请求都直接打到数据库上**，造成数据库压力骤增，可能会导致宕机。

解决办法：

**针对redis服务不可用的情况** ：

* 采用Redis集群，避免单机出现问题整个缓存服务器都没办法采用。
* 限流，避免同时处理大量的请求。比如说使用hystrix来进行限流。

**针对热点缓存失效的情况** ：

* 设置不同的失效时间，比如随机设置缓存的失效时间。
* 缓存永不失效（不太推荐，实用性太差）。
* 设置二级缓存。



### 6.Redis为什么那么快？

* Redis基于内存，内存的访问速度是硬盘的上千倍。
* Redis的单线程事件循环和IO多路复用。
* Redis内置了多种经过优化的数据结构，性能非常高。



### 7.String的应用场景有哪些？

* **常规数据（比如session，token, 序列化后的对象）的缓存**。相关命令有`SET`、`GET` 。
* **计数**，比如用户单位时间的请求数（简单限流可以用到）、页面单位时间的访问数。`SET` ,`GET` ,`INCR` ,`DECR` 。



### 8.List的应用场景有哪些？

**Redis中的`List` 其实是链表数据结构的实现，不过Redis中的链表是个双向链表**。具体应用场景如下：

* **信息流展示** ：最新文章、最新动态。相关命令有`LPUSH` ,`LRANGE` 。
* **消息队列** ：可以用来做消息队列，功能简单而且存在很多缺陷。



### 9.Hash（哈希）的应用场景有哪些？

Redis中的哈希是一个 String 类型的 field-value（键值对） 的映射表，特别适合用于存储对象。主要应用场景如下：

* **对象数据存储场景** ：用户信息、商品信息、文章信息、购物车信息。相关命令：`HSET` （设置单个字段的值）、`HGET` （获取单个字段的值）、`HMGET` （获取多个字段的值）

### 10.Set的应用场景有哪些？

Redis中的 Set 类型是一种无序集合，集合中的元素没有先后顺序但是都是唯一的。主要应用场景如下：

* **需要存放的数据不能重复的场景** ：网站UV统计（独立访客，即一天内访问某站点的用户数）、文章点赞、动态点赞等场景。相关命令：`SCARD` （获取集合数量）
* **需要获取多个数据源交集、并集和差集的情况** ：共同好友（交集）、好友推荐（差集）、音乐推荐（差集） ，订阅号推荐（交集+差集）。相关命令有：`SINTER` （交集）、`SINTERSTORE` （交集），`SUNION` （并集）、`SUNIONSTORE` （交集）、`SDIFF` （差集），`SDIFFSTORE` （差集）。
* **需要随机获取数据源中的元素的场景** ：抽奖系统，随机。相关命令：`SPOP` （随机获取集合中的元素并移除，适合不允许重复中奖的场景）、`SRANDMEMBER` （随机获取集合中的元素，适合允许重复中奖的场景）。

### 11.Sorted Zet （有序集合）的引用场景有哪些？

类似于`Set` ,但是增加了一个权重参数`score` ，使得集合中的元素能够按`score` 进行有序排列。

* **需要随机获取数据源中的元素按照某个权重进行排序的场景** ：比如各种排行榜。相关命令：`ZRANGE` （从小到大排序），`ZREVRANGER` （从大到小排列）、`ZREVRANK` （指定元素排名） 。
* **需要存储的数据有优先级** ：优先级任务队列。相关命令：`ZRANGE` （从小到大排序），`ZREVRANGER` （从大到小排列）、`ZREVRANK` （指定元素排名） 。



### 12.bitmap如何实现签到功能？

Redis中的bitmap可以用于实现签到功能，通过设置每个用户的签到状态，可以方便地判断用户当日是否已经签到。

1. 首先在Redis中创建一个bitmap，用于记录每个用户的签到状态。例如，我们可以使用用户id作为bitmap的key，将签到状态存储在一个64位的bitmap中。

   ```java
   public class RedisUtils {
       
       private final RedisTemplate<String, Object> redisTemplate;
       
       public RedisUtils(RedisTemplate<String, Object> redisTemplate) {
           this.redisTemplate = redisTemplate;
       }
       
       /**
        * 设置用户签到状态
        * @param userId 用户ID
        * @param date 日期，格式为"yyyyMMdd"
        * @return 是否设置成功
        */
       public boolean setUserSignState(String userId, String date) {
           String key = "sign:" + date;
           Long offset = Long.parseLong(userId);
           return (Boolean) redisTemplate.execute((RedisCallback<Boolean>) connection -> {
               byte[] value = connection.get(key.getBytes());
               if (value == null) {
                   // 如果该日期的bitmap不存在，则先创建一个全0的bitmap
                   byte[] initValue = new byte[8];
                   connection.set(key.getBytes(), initValue);
                   value = initValue;
               }
               // 将对应位的值设为1
               value = connection.getSetBit(key.getBytes(), offset) ? value : connection.get(key.getBytes());
               return value[offset.intValue() / 8] >> (offset.intValue() % 8) & 1 == 1;
           });
       }
       
       /**
        * 判断用户当日是否已经签到
        * @param userId 用户ID
        * @param date 日期，格式为"yyyyMMdd"
        * @return 是否已经签到
        */
       public boolean getUserSignState(String userId, String date) {
           String key = "sign:" + date;
           Long offset = Long.parseLong(userId);
           return (Boolean) redisTemplate.execute((RedisCallback<Boolean>) connection -> {
               byte[] value = connection.get(key.getBytes());
               return value == null ? false : value[offset.intValue() / 8] >> (offset.intValue() % 8) & 1 == 1;
           });
       }
   }
   
   ```

2. 然后，在Spring Boot项目中创建一个签到接口，当用户请求该接口时，调用上述Redis工具类中的方法来更新用户的签到状态。

   ```java
   @RestController
   public class SignController {
   
       @Autowired
       private RedisUtils redisUtils;
   
       @PostMapping("/sign")
       public String sign(@RequestParam("userId") String userId) {
           // 获取当前日期
           String date = LocalDate.now().format(DateTimeFormatter.BASIC_ISO_DATE);
           boolean result = redisUtils.setUserSignState(userId, date);
           if (result) {
               return "今日已签到";
           } else {
               return "签到成功";
           }
       }
   
       @GetMapping("/sign")
       public String getSignState(@RequestParam("userId") String userId) {
           // 获取当前日期
           String date = LocalDate.now().format(DateTimeFormatter.BASIC_ISO_DATE);
           boolean result = redisUtils.getUserSignState(userId, date);
           if (result) {
               return "已签到";
           } else {
               return "未签到";
           }
       }
   }
   
   ```

   通过以上的实现，用户每次请求签到接口时，都会更新对应的bitmap中的相应位置，表示用户已经签到。而在查询签到状态时，只需要查询对应日期的bitmap中相应用户的位置即可判断用户是否已经签到。

   在我们写程序时，在进行签到功能之前，应该去判断当前的用户是否已经签到，如果没有签到，我们就去进行签到，否则就返回“已签到”的响应信息。



### 13.说说你对redis事务的理解？

#### 什么是Redis事务？原理是什么？

Redis中的事务是一组命令的集合，是Redis的最小执行单元。它可以保证一次执行多个命令，每个事务是一个单独的隔离操作，事务中的所有命令都会序列化、按顺序执行。

它的原理是先将属于一个事务的命令发给Redis，然后依次执行这些命令。

#### 如何使用Redis事务？

可以使用 `MULIT`、`EXEC`等来实现事务功能。

`mulit` 后面可以跟多个命令，Redis不会立刻执行这些命令，而是会将这些命令放到队列中，当调用了`EXEC`命令之后，再执行所有的命令。

也可以通过`DISCARD`命令取消一个事务，它会清空队列中的所有命令。

可以通过`WATCH` 命令监听指定的key，当调用 `EXEC`命令时，如果这个key被其他客户端修改的话，那么整个事务都不会执行。不过，如果 **WATCH** 与 **事务** 在同一个 Session 里，并且被 **WATCH** 监视的 Key 被修改的操作发生在事务内部，这个事务是可以被执行成功的。

#### Redis事务的注意点有哪些？

* Redis事务是不支持回滚的，不想MySQL事务一样，要么都执行要么都不执行。 
* Redis服务端在执行事务的过程中，不会被其他客户端发送来的命令请求打断。直到事务命令全部执行完毕才会执行其他客户端的命令。

#### Redis事务为什么不支持回滚？

Redis的事务不支持回滚，如果执行的命令有语法错误，Redis会执行失败，这些问题可以从程序层面捕获并解决。但是如果出现了其他问题，则依然会继续执行剩余的命令。这样做的原因是因为回滚需要增加很多工作，而不支持回滚则可以保持简单、快速地特性。



### 14.Redis的持久化方式？

Redis支持持久化的方式有两种，一种是**快照（RDB）** ,另一种方式是**只追加文件（AOF）** 。

#### 什么是RDB持久化？

通过创建快照来获得存储在内存中的数据在某个时间点上的副本。Redis创建快照后，可以对快照进行备份，可以将快照复制到其他服务器上，还可以留在原地以便重启服务器的时候使用。

快照持久化是Redis默认采用的持久化方式，在`redis.conf` 配置文件中默认有下面的配置：

```conf
save 900 1           #在900秒(15分钟)之后，如果至少有1个key发生变化，Redis就会自动触发bgsave命令创建快照。

save 300 10          #在300秒(5分钟)之后，如果至少有10个key发生变化，Redis就会自动触发bgsave命令创建快照。

save 60 10000        #在60秒(1分钟)之后，如果至少有10000个key发生变化，Redis就会自动触发bgsave命令创建快照。
```



#### RDB创建快照时会阻塞主线程吗？

Redis提供了两个命令来生成RDB快照文件：

* **save** ：同步保存操作，会阻塞Redis主线程。
* **bagsave** ：fork出一个子进程，子进程执行，不会阻塞Redis主进程，默认选项。



#### 什么是AOF持久化？

与快照持久化相比，AOF持久化的实时性更好，因此已成为主流的持久化方案。默认情况下Redis没有开启AOF持久化。

开启持久化后每执行一条会更改Redis数据中的命令，Redis就会将这个命令写入到`server.aof.buf` ，然后再根据`appendfsync` 配置来决定何时将其同步到硬盘中的AOF文件。

AOF 文件的保存位置和 RDB 文件的位置相同，都是通过 dir 参数设置的，默认的文件名是 `appendonly.aof` 。

在Redis的配置化文件中存在三种不同的AOF持久化方式，他们分别是：

```aof
appendfsync always    #每次有数据修改发生时都会写入AOF文件,这样会严重降低Redis的速度
appendfsync everysec  #每秒钟同步一次，显式地将多个写命令同步到硬盘
appendfsync no        #让操作系统决定何时进行同步
```

为了兼顾数据和写入性能，可以考虑`appendfsync everysec` 选项，让Redis每秒同步一次AOF文件，Redis性能几乎不会收到任何影响。这样即使出现系统崩溃，用户最多只会丢失一秒之内产生的数据。

#### AOF日志是如何实现的

关系型数据库（如MySQL）通常都是先记录日志在执行命令的（方便故障恢复），而RedisAOF持久化机制是在执行完命令之后再记录日志。

![image-20230328152127529](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230328152127529.png)

**为什么先执行命令后面在记录日志呢？** 

* 避免额外的开销，AOF记录日志不会对命令进行检查。
* 命令执行完再记录，不会阻塞当前命令的执行。

这样也带来了风险：

* 如果刚执行完Redis命令就马上宕机会导致相应的修改丢失。
* 可能会阻塞其他命令的执行（**因为AOF记录日志是在Redis主进程中执行的**）。





### 15.Redis主从复制、哨兵模式、集群搭建？

#### 主从复制

是指将一台Redis服务器的数据，复制到其他的Redis服务器。前者称为主节点(Master)，后者称为从节点(Slave)，数据的复制是单向的，只能由主节点到从节点。Master以写为主，Slave 以读为主。

![image-20230405172106065](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230405172106065.png)

这样的好处肯定是显而易见的：

- 实现了读写分离，提高了性能。
- 在写少读多的场景下，我们甚至可以安排很多个从节点，这样就能够大幅度的分担压力，并且就算挂掉一个，其他的也能使用。

当有多个从节点时，有下面的模式：

![image-20230405172710505](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230405172710505.png)

采用这种方式，优点肯定是显而易见的，但是缺点也很明显，整个传播链路一旦中途出现问题，那么就会导致后面的从节点无法及时同步。



#### 哨兵模式

我们发现，实际上最关键的还是主节点，因为一旦主节点出现问题，那么整个主从系统将无法写入，因此，我们得想一个办法，处理一下主节点故障的情况。实际上我们可以参考之前的服务治理模式，比如Nacos和Eureka，所有的服务都会被实时监控，那么只要出现问题，肯定是可以及时发现的，并且能够采取响应的补救措施，这就是我们即将介绍的哨兵：

![image-20230405173231201](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230405173231201.png)

哨兵会对所有的节点进行监控，如果发现主节点出现问题，那么会立即让从节点进行投票，选举一个新的主节点出来，这样就不会由于主节点的故障导致整个系统不可写（注意要实现这样的功能最小的系统必须是一主一从，再小的话就没有意义了）。

![image-20230405173330783](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230405173330783.png)

那么，这个选举规则是怎样的呢？是在所有的从节点中随机选取还是遵循某种规则呢？

1. 首先会根据优先级进行选择，可以在配置文件中进行配置，添加`replica-priority`配置项（默认是100），越小表示优先级越高。

2. 如果优先级一样，那就选择偏移量最大的

3. 要是还选不出来，那就选择runid（启动时随机生成的）最小的。

   

要是哨兵也挂了咋办？没事，咱们可以多安排几个哨兵，只需要把哨兵的配置复制一下，然后修改端口，这样就可以同时启动多个哨兵了。



#### 集群搭建

如果我们服务器的内存不够用了，但是现在我们的Redis又需要继续存储内容，那么这个时候就可以利用集群来实现扩容。

因为单机的内存容量最大就那么多，已经没办法再继续扩展了，但是现在又需要存储更多的内容，这时我们就可以让N台机器上的Redis来分别存储各个部分的数据（每个Redis可以存储1/N的数据量），这样就实现了容量的横向扩展。同时每台Redis还可以配一个从节点，这样就可以更好地保证数据的安全性。

![image-20230405173937164](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230405173937164.png)



那么问题来，现在用户来了一个写入的请求，数据该写到哪个节点上呢？我们来研究一下集群的机制：

首先，一个Redis集群包含16384个插槽，集群中的每个Redis 实例负责维护一部分插槽以及插槽所映射的键值数据，那么这个插槽是什么意思呢？

实际上，插槽就是键的Hash计算后的一个结果，注意这里出现了`计算机网络`中的CRC循环冗余校验，这里采用CRC16，能得到16个bit位的数据，也就是说算出来之后结果是0-65535之间，再进行取模，得到最终结果：

**Redis key的路由计算公式：slot = CRC16（key） % 16384**

果的值是多少，就应该存放到对应维护的Redis下，比如Redis节点1负责0-25565的插槽，而这时客户端插入了一个新的数据`a=10`，a在Hash计算后结果为666，那么a就应该存放到1号Redis节点中。简而言之，本质上就是通过哈希算法将插入的数据分摊到各个节点的。



### 16.redis 6.0之前为什么不用多线程？

* 使用Redis，CPU不是瓶颈，内存、网络才是限制速度的原因。
* 单线程，内部维护比较低
* 如果是多线程，会涉及到线程切换，并发读和写的时候要加锁跟解锁，导致死锁问题。



### 17.Redis 6.0之后为什么要引入多线程？

* 针对大的公司，需要更大的QPS，而且多线程是对于IO来说，内部执行命令还是单线程。
* 为了让Redis抗住更大的并发。



### 18.为什么要用Redis?

* 高性能
* 高并发



### 19.Redis跟Memcached的区别？

* 整体类型：都支持内存，但是Redis有更多的数据结构，而memcache只支持key-value的形式
* 数据类型：Redis有String,list,set.hash.zset,而memcache只支持文本型和二进制类型。
* 操作类型：Redis支持单个操作，批量添加，支持事务。memcache只支持curd和少量的命令。
* 附加功能：Redis支持发布/订阅模式，类似于跟消息队列一样，还支持主从高可用，序列化支持，支持Lua脚本。而memcache支持多线程服务。
* 网络IO模型：Redis网络操作是多线程。memcache网络操作属于非阻塞的IO模式。
* 持久化：Redis支持RDB和AOF持久化，memcache不支持持久化。



### 20.Redis给缓存数据设置过期时间有什么用？

因为内存是有限的，如果缓存中的所有数据都是一直保存的话，分分钟直接 Out of memory。

注意：**Redis 中除了字符串类型有自己独有设置过期时间的命令 `setex` 外，其他方法都需要依靠 `expire` 命令来设置过期时间 。另外， `persist` 命令可以移除一个键的过期时间。**

**过期时间除了有助于缓解内存的消耗，还有什么其他用么？**

很多时候，我们的业务场景就是需要某个数据只在某一时间段内存在，比如我们的短信验证码可能只在 1 分钟内有效，用户登录的 token 可能只在 1 天内有效。



### 21.Redis是如何判断数据是否过期的呢？

Redis 通过一个叫做过期字典（可以看作是 hash 表）来保存数据过期的时间。过期字典的键指向 Redis 数据库中的某个 key(键)，过期字典的值是一个 long long 类型的整数，这个整数保存了 key 所指向的数据库键的过期时间（毫秒精度的 UNIX 时间戳）。



### 22.过期的数据的删除策略了解么？

如果假设你设置了一批 key 只能存活 1 分钟，那么 1 分钟后，Redis 是怎么对这批 key 进行删除的呢？

常用的过期数据的删除策略就两个（重要！自己造缓存轮子的时候需要格外考虑的东西）：

1. **惰性删除** ：只会在取出 key 的时候才对数据进行过期检查，如果过期了立即删除，不会给你返回任何东西。这样对 CPU 最友好，但是可能会造成太多过期 key 没有被删除。
2. **定期删除** ： 每隔一段时间抽取一批 key 执行删除过期 key 操作。并且，Redis 底层会通过限制删除操作执行的时长和频率来减少删除操作对 CPU 时间的影响。

定期删除对内存更加友好，惰性删除对 CPU 更加友好。两者各有千秋，所以 Redis 采用的是 **定期删除+惰性/懒汉式删除** 。



### 23.Redis内存淘汰机制？

仅仅通过给 key 设置过期时间还是有问题的。因为还是可能存在定期删除和惰性删除漏掉了很多过期 key 的情况。这样就导致大量过期 key 堆积在内存里，然后就 Out of memory 了。

怎么解决这个问题呢？答案就是：**Redis 内存淘汰机制**。

Redis 提供 6 种数据淘汰策略：

1. **volatile-lru（least recently used）**：从已设置过期时间的数据集（server.db[i].expires）中挑选最近最少使用的数据淘汰
2. **volatile-ttl**：从已设置过期时间的数据集（server.db[i].expires）中挑选将要过期的数据淘汰
3. **volatile-random**：从已设置过期时间的数据集（server.db[i].expires）中任意选择数据淘汰
4. **allkeys-lru（least recently used）**：当内存不足以容纳新写入数据时，在键空间中，移除最近最少使用的 key（这个是最常用的）
5. **allkeys-random**：从数据集（server.db[i].dict）中任意选择数据淘汰
6. **no-eviction**：禁止驱逐数据，也就是说当内存不足以容纳新写入数据时，新写入操作会报错。这个应该没人使用吧。



### 24.Redis如何实现分布式锁？

对于单机多线程来说，我们通常使用`ReentranLock` ,`Sychornized` 等来控制多个进程对共享资源的访问，这是一种本地锁。但是到了分布式的环境下，多台机器操控同一份共享资源的话，那么本地锁就没有用了，因为本地锁基于JVM，而分布式是基于多个JVM，所以我们需要用到分布式锁。

以下是实现分布式锁的步骤：

* **客户端请求加锁** ：客户端使用 `SETNX` 命令，如果返回值为1，表示获取锁成功，如果返回值为0，则表示获取锁失败。
* **设置过期时间** ：为了避免因客户端崩溃等原因导致锁不能释放（死锁问题），需要为锁设置过期时间。可以使用 `EXPIRE` 命令设置过期时间。
* **客户端请求解锁** ：完成业务之后，需要解锁，让别的线程进来竞争共享资源。客户端使用 `DEL` 命令释放锁，但是需要确保只有持有锁的客户端才能释放锁。可以使用 Lua脚本实现解锁操作，通过比较锁的值和客户端提供的值来确定是否释放锁。



**如果操作共享资源的时间大于过期时间，那么就会出现锁提前过期的问题，进而分布式锁失效，但是如果设置时间过长，又会影响性能，该怎么办呢？**

使用 Redisson。

Redisson中的分布式锁自带自动续期机制。其提供了一个专门用来监控和续期锁的 Watch Dog （看门狗）实际上就是一个守护线程。如果操作共享资源的线程还未执行完成的话，**看门狗会不断的延长锁的过期时间，进而保证锁不会因为超时而被释放**。



### 25.Redis如何实现简单消息队列？

基于List的 lpush 和 rpop。但是会有很多缺点，比如说要处理空闲连接的问题，如果线程一直在阻塞，Redis客户端的连接就成了闲置连接。那么服务器一般会断开连接，这个时候如果在使用lush 和 rpop就会出现异常。同时还有消费端确认ACK麻烦，不能保证消费者消费后成功处理的问题。



### 26.什么是bigkey？

bigkey指的是key对应的value所占的空间比较大。比如说string类型的value超过10kb。复合类型的value包含的元素超过5000个。

bigkey的危害主要体现在三个方面：

1. 内存空间分布不均。
2. 超时阻塞。由于Redis是单线程，操作bigkey比较耗时，所以可能会造成阻塞。
3. 网络拥塞。每次获取bigkey的网络耗时很大。



### 27.怎么提高缓存命中率？

* 提前加载
* 加大Redis的容量。比如说原来2g，扩大到20g。
* 提升缓存的更新频率



### 28.如何保证缓存和数据库双写时的一致性？

#### 新增数据类

如果是新增数据，数据会直接写到数据库中，不用对缓存做任何操作，此时，缓存中本身就没有新增数据，而数据库库中是最新值，此时，缓存和数据库的数据是一致的。

#### 更新缓存类（非常不推荐）

* 先更新缓存，再更新数据库：

  一般不考虑。因为更新缓存成功，更新数据库出现问题了，就会导致不一致，而且很难发现。

* 先更新数据库，再更新缓存：

  一般不考虑。因为更新数据库成功，更新缓存出现问题了，就会导致不一致。

#### 删除缓存类

* **先删除缓存，再更新数据库**

    2 个线程要并发「读写」数据，可能会发生以下场景：

  1. 线程 A 要更新 X = 2（原值 X = 1）
  2. 线程 A 先删除缓存
  3. 线程 B 读缓存，发现不存在，从数据库中读取到旧值（X = 1）
  4. 线程 A 将新值写入数据库（X = 2）
  5. 线程 B 将旧值写入缓存（X = 1）

​		最终 X 的值在缓存中是 1（旧值），在数据库中是 2（新值），发生不一致。

如何解决：**延迟双删** 。在线程 A 删除缓存、更新完数据库之后，先「休眠一会」，再「删除」一次缓存。这样一来，下次就可以从数据库读取到最新值，写入缓存。休眠时间可以根据业务来估计。

* **先更新数据库，后删除缓存** 

  这种方式被称为cache aside pattern，读的时候，先读缓存，没有的话，就读数据库，然后取出数据后放入缓存。

  更新的时候，先更新数据库，然后再删除缓存。

  如果更新数据库成功，而删除缓存这一步失败的情况的话，简单说两个解决方案：

  1. **缓存失效时间变短（不推荐，治标不治本）** ：我们让缓存数据的过期时间变短，这样的话缓存就会从数据库中加载数据。另外，这种解决办法对于先操作缓存后操作数据库的场景不适用。
  2. **增加 cache 更新重试机制（常用）**： 如果 cache 服务当前不可用导致缓存删除失败的话，我们就隔一段时间进行重试，重试次数可以自己定。如果多次重试还是失败的话，我们可以把当前更新失败的 key 存入队列中，等缓存服务可用之后，再将缓存中对应的 key 删除即可。




==在极端环境下，要保证缓存和数据库的强一致性，最好的办法是分布式锁，但是这样做并发性能会大大地降低。==

### 29.什么情况下可能会导致Redis阻塞？

* 客户端阻塞 ，比如说一些命令： key *  ，Hgetall smembers 。
* bigkey删除 
* 清空库 flushdb   flushall
* AOF 日志同步写,记录AOF日志，大量的写操作。（**AOF写日志是在主进程中进行的，会阻塞其他命令**）
* 从库加载 RDB文件



### 30.

























# 九、SpringCloud

### Eureka注册中心

#### 服务间的调用

在spring项目中，进行服务远程调用我们需要用到`RestTemplete` 。

`RestTemplate` 是Spring 框架中的一个用于进行 RESTful 风格的HTTP请求类的模板，它封装了HTTP请求的实现细节，使得开发者可以更加方便的发送HTTP请求。

在Spring Boot 项目中，我们通过在项目中引入`spring-boot-starter-web` 依赖来使用它。

`RestTemplate` 可以用于服务间的调用。在spirngcloud中，我们可以用它来实现服务间的调用。

```java
@Service
public class BorrowServiceImpl implements BorrowService{

    @Resource
    BorrowMapper mapper;

    @Override
    public UserBorrowDetail getUserBorrowDetailByUid(int uid) {
        List<Borrow> borrow = mapper.getBorrowsByUid(uid);
        //RestTemplate支持多种方式的远程调用
        RestTemplate template = new RestTemplate();
        //这里通过调用getForObject来请求其他服务，并将结果自动进行封装
        //获取User信息
        User user = template.getForObject("http://localhost:8082/user/"+uid, User.class);
        //获取每一本书的详细信息
        List<Book> bookList = borrow
                .stream()
                .map(b -> template.getForObject("http://localhost:8080/book/"+b.getBid(), Book.class))
                .collect(Collectors.toList());
        return new UserBorrowDetail(user, bookList);
    }
}
```



#### 服务注册与发现

Eureka能够自动注册并发现微服务，然后对服务的状态、信息进行集中管理，这样我们需要获取其他服务的信息时，只需要向Eureka进行查询就可以了。

有了Eurake之后，我们可以直接向其进行查询，得到对应的微服务地址。这里省略了注册过程。

```java
@Service
public class BorrowServiceImpl implements BorrowService {

    @Resource
    BorrowMapper mapper;

    @Resource
    RestTemplate template;

    @Override
    public UserBorrowDetail getUserBorrowDetailByUid(int uid) {
        List<Borrow> borrow = mapper.getBorrowsByUid(uid);

        //这里不用再写IP，直接写服务名称userservice
        User user = template.getForObject("http://userservice/user/"+uid, User.class);
        //这里不用再写IP，直接写服务名称bookservice
        List<Book> bookList = borrow
                .stream()
                .map(b -> template.getForObject("http://bookservice/book/"+b.getBid(), Book.class))
                .collect(Collectors.toList());
        return new UserBorrowDetail(user, bookList);
    }
}

```

接着我们手动将RestTemplate声明为一个Bean，然后添加`@LoadBalanced`注解，这样Eureka就会对服务的调用进行自动发现，并提供负载均衡：

```java
@Configuration
public class BeanConfig {
    @Bean
    @LoadBalanced
    RestTemplate template(){
        return new RestTemplate();
    }
}
```



**当我们的服务启动之后，会每隔一段时间跟Eurake发送一次心跳包，这样Eurake就能告知到我们的服务是否处于运行的状态。** 



#### 注册中心高可用

Eurake可以实现服务注册和发现，但是如果 Eurake服务器崩了怎么办？

为了避免这个问题，我们可以搭建 Euraka集群，存在多个 Eurake服务器，这样就算崩掉一个，那其他的Eurake服务器也可以正常运行。

![image-20230323154114497](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230323154114497.png)



### LoadBalancer负载均衡

#### OpenFeign实现负载均衡

Feign和RestTemplate一样，也是HTTP客户端请求工具，但是它的使用方式更加便捷。首先是依赖：

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```

接着在启动类添加`@EnableFeignClients`注解：

```java
@SpringBootApplication
@EnableFeignClients
public class BorrowApplication {
    public static void main(String[] args) {
        SpringApplication.run(BorrowApplication.class, args);
    }
}
```

那么现在我们需要调用其他微服务提供的接口，该怎么做呢？我们直接创建一个对应服务的接口类即可：

```java
@FeignClient("userservice")
public interface UserClient {

      //路径保证和其他微服务提供的一致即可
    @RequestMapping("/user/{uid}")
    User getUserById(@PathVariable("uid") int uid);  //参数和返回值也保持一致
}
```

其他也是一样的，最后我们的service代码就成了：

```java
@Service
public class BorrowServiceImpl implements BorrowService {

    @Resource
    BorrowMapper mapper;

    @Resource
    UserClient userClient;
    
    @Resource
    BookClient bookClient;

    @Override
    public UserBorrowDetail getUserBorrowDetailByUid(int uid) {
        List<Borrow> borrow = mapper.getBorrowsByUid(uid);

        User user = userClient.getUserById(uid);
        List<Book> bookList = borrow
                .stream()
                .map(b -> bookClient.getBookById(b.getBid()))
                .collect(Collectors.toList());
        return new UserBorrowDetail(user, bookList);
    }
}
```



### Hystrix 服务熔断

微服务之间是可以进行调用的，如果出现了下面的情况怎么办呢？

![image-20230323155623359](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230323155623359.png)



由于位于最底端的服务提供者E发生故障，那么就会导致服务器ABCK全崩溃。就像雪崩一样。

这种问题无法避免，由于多种因素，比如网络卡顿，系统故障，硬件故障。

为了解决分布式系统的雪崩问题，SpringCloud提供了 Hystrix 熔断器组件。



#### 服务降级

服务降级并不会直接返回错误，而是提供一个补救措施，正常响应给请求者。这样相当于服务依然可以用，但是服务能力肯定是下降了的。

虽然请求没有办法正常响应，但是我们可以提供一个备选方案，也就是说当服务出现异常时，返回我们的备选方案。

服务降级是一种比较温柔的解决方案，虽然服务本身不可用，但是能够保证正常的响应信息。

使用服务降级需要导入Hystrix的依赖。



#### 服务熔断

是应对雪崩效应的一种微服务链路保护机制。当检测到链路的某个微服务不可用或者响应时间太长时，会先进行服务的降级，进而熔断该微服务的调用，快速返回“错误”的信息。**当检测到该节点微服务响应正常后恢复调用链路**。 

实际上，熔断就是在降级的基础上进一步升级的。也就是说，在一段时间内多次调用失败，那么就直接升级为熔断。



#### OpenFeign实现降级

Hystrix也可以配合Feign进行降级，我们可以对应接口中定义的远程调用单独进行降级操作。



### Gateway路由网关

一般情况下，并不是所有的微服务都需要直接暴露给外部使用，这是我们就可以**使用路由机制，添加一层防护，让所有的请求全部通过路由来转发到各个微服务，并且转发给多个相同微服务实例也可以实现负载均衡。**

![image-20230323172041995](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230323172041995.png)



#### 部署网关

第一个依赖就是网关的依赖，而第二个则跟其他微服务一样，需要注册到Eureka才能生效，注意别添加Web依赖，使用的是WebFlux框架。



#### 路由过滤器

路由过滤器支持以某种方式修改传入的HTTP请求或传出的HTTP响应，**路由过滤器的范围是某一个路由**。比如说我们现在希望请求到达时，在请求头中添加一些信息再转发给我们的服务，那么这个时候就可以使用路由过滤器来完成。

除了针对某一个路由编写过滤器之外，我们也可以自定义全局过滤器。

**过滤器是可以存在多个的，我们可以手动指定过滤器之间的顺序。** 





### Config配置中心

如果我们的微服务需要部署多个实例，那么配置文件需要我们一个一个的改，如果实例很多的话，如果还是手动去改，那么无疑会很麻烦。

所以我们需要一种更加高级的集中化配置文件管理工具，集中地对配置文件进行配置。





### 微服务CAP原则

CAP原则又称CAP定理，指的是在一个分布式系统中，存在Consistency（一致性）、Availability（可用性）,Partition tolerance（分区容错性），三者不可同时保证，最多只能保证其中的两者。

一致性（C） ：在分布式系统中的所有数据备份，在同一时刻都是同样的值（所有的节点无论何时访问都能拿到最新的值）。

可用性（A）：系统中非故障节点收到的每个请求都必须得到响应。

分区容错性（P）：一个分布式系统中，节点之间组成的网络本来就是连通的，然后可能因为一些故障（比如说网络丢包，这是很难避免的），使得有些节点不连通了，整个网络分成了几块区域，数据就散步在这些不连通的区域中（这样就可能出现某些被分区节点存放的数据访问失败，我们需要容忍这些不可靠的情况）。



### Nacos 更加全能的注册中心

Nacos是一款阿里巴巴开源的服务注册与发现、配置管理的组件，**相当于Eureka跟Config的组合形态。**

#### 服务注册与发现

如果我们要实现基于Nacos的服务注册与发现，那么就需要导入SpringCloudAlibaba相关的依赖，我们将在父工程将依赖进行管理。

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.mybatis.spring.boot</groupId>
            <artifactId>mybatis-spring-boot-starter</artifactId>
            <version>2.2.0</version>
        </dependency>
      
          <!-- 这里引入最新的SpringCloud依赖 -->
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>2021.0.1</version>
              <type>pom</type>
            <scope>import</scope>
        </dependency>

           <!-- 这里引入最新的SpringCloudAlibaba依赖，2021.0.1.0版本支持SpringBoot2.6.X -->
        <dependency>
            <groupId>com.alibaba.cloud</groupId>
            <artifactId>spring-cloud-alibaba-dependencies</artifactId>
            <version>2021.0.1.0</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

nacos实例有临时和非临时之分：

* 临时实例：和Eureka一样，采用心跳机制向Nacos发送请求保持在线状态，一旦心跳停止，代表实例下线，不保留实例信息。
* 非临时实例：由Nacos主动进行联系，如果连接失败，那么不会移除实例信息，而是将健康状态设定为false，相当于会对某个实例状态持续地进行监控。



#### 集群分区

在一个分布式应用中，相同服务的实例可能会在不同的机器、位置上启动，比如我们的用户管理服务，可能在成都有一台服务器部署，重庆有一台服务器部署，而这时，我们在成都的服务器上启动了借阅服务，那么如果我们的借阅服务现在要调用用户服务，就应该优先选择同一个区域的用户服务进行调用，这样会使得响应速度加快。

![image-20230323214153764](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230323214153764.png)



因此，我们可以对部署在不同机房的服务进行分区。



#### 配置中心

前面我们学习了SpringCloud config，我们可以通过配置服务来加载远程配置，这样我们就可以在远端集中管理配置文件。

nacos也支持这样做。



#### 命名空间

我们可以将配置文件或是服务实例划分到不同的命名空间中，其实就是区分开发、生产环境或是引用归属之类的。

我们**在不同的命名空间下，实例和配置都是相互隔离**的，我们也可以在配置文件中指定当前的命名空间。



#### 实现高可用

像之前Eureka一样，搭建Nacos集群，实现高可用。它的实现方式如下：

![image-20230323215432068](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230323215432068.png)

它推荐我们在所有的nacos服务端之前建立一个负载均衡，我们通过访问负载均衡服务器来间接访问到各个Nacos服务器。实际上就，是比如有三个Nacos服务器做集群，但是每个服务不可能把每个Nacos都去访问一次进行注册，实际上只需要在任意一台Nacos服务器上注册即可，Nacos服务器之间会自动同步信息，但是如果我们随便指定一台Nacos服务器进行注册，如果这台Nacos服务器挂了，但是其他Nacos服务器没挂，这样就没办法完成注册了，但是实际上整个集群还是可用的状态。

所以这里就需要在所有Nacos服务器之前搭建一个SLB（服务器负载均衡），这样就可以避免上面的问题了。但是我们知道，如果要实现外界对服务访问的负载均衡，我们就得用比如之前说到的Gateway来实现，而这里实际上我们可以用一个更加方便的工具：**Nginx**。

关于SLB最上方还有一个DNS（我们在`计算机网络`这门课程中学习过），这个是因为SLB是裸IP，如果SLB服务器修改了地址，那么所有微服务注册的地址也得改，所以这里是通过加域名，通过域名来访问，让DNS去解析真实IP，这样就算改变IP，只需要修改域名解析记录即可，域名地址是不会变化的。





### Sentinel 流量防卫兵

随着微服务的流行，服务与服务之间的稳定性变得越来越重要。**Sentinel 以流量为切入点，从流量控制，熔断降级，系统负载保护等多个维度保护服务的稳定性。**

Sentinel具有以下特征：

* **丰富的应用场景** ：Sentinel承接了阿里巴巴近10年的双十一大促流量的核心场景，例如秒杀、消息削峰填谷、集群流量控制、实施熔断下游不可用应用等。
* **完备的实时监控** ：Sentinel同时提供实时的监控功能。
* **广泛的开源生态** ：Sentinel 提供开箱即用的与其它开源框架/库的整合模块，例如与Spring Cloud、Apache Dubbo、gRPC、Quarkus 的整合。您只需要引入相应的依赖并进行简单的配置即可快速地接入 Sentinel。同时 Sentinel 提供 Java/Go/C++ 等多语言的原生实现。
* **完善的SPI扩展机制** ：Sentinel提供简单易用、完善的SPI扩展接口。你可以通过实现扩展接口来快速地定制逻辑。例如定制规则管理、适配动态数据源等。

#### 流量控制

我们的机器不可能无限制的接受和处理客户端的请求，如果不加以限制，当发生高并发时，系统资源将很快被耗尽。为了避免这种情况，我们可以添加流量控制，当一段时间内的流量到达一定的阈值时，新的请求将不再进行处理，这样不仅可以合理地处理高并发请求，同时也能在一定程度上保护服务器不受外界的恶意攻击。



#### 限量和异常处理

限量状态下的返回结果是Sentinel默认的数据，我们可以对返回结果进行一些自定义操作。



#### 热点参数限流

我们还可以对某一个热点数据进行精准限流，比如在某一时刻，不同参数被携带访问的频率是不一样的：

- http://localhost:8301/test?a=10 访问100次
- http://localhost:8301/test?b=10 访问0次
- http://localhost:8301/test?c=10 访问3次

由于携带参数`a` 的请求比较多，我们就可以只对携带参数`a` 的请求进行限流。



#### 服务熔断和降级

如果在某一时刻，服务B出现故障（可能就卡在那里了），而这时服务A依然有大量的请求，在调用服务B，那么，由于服务A没办法再短时间内完成处理，新来的请求就会导致线程数不断地增加，这样，CPU的资源很快就会被耗尽。

为了要防止这种情况发生，我们可以进行隔离。



### Seate与分布式事务

Seata是一款开源的分布式事务解决方案，致力于提供高性能和简单易用的分布式事务服务。Seata为用户提供AT、TCC、SAGA和XA事务模式，为用户打造一站式的分布式解决方案。





### 1.分布式、SOA、微服务之间的区别？

* 分布式架构：将单体各个部分进行拆分，部署到不同的机器上，SOA和微服务基本上都是分布式架构的。
* SOA：系统所有的服务都注册在总线上，当调用服务时，从总线上获取。
* 微服务：将系统中各个功能抽成一个小的模块，每一个模块对应一个微服务。



### 2.spring cloud和 dubbo有什么区别？

spring cloud是大而全的框架，dubbo则侧重于服务调用（**一开始是一个rpc框架，核心是解决服务间的调用问题**），所以dubbo提供的没有cloud全面，但是性能比cloud高，两者可以结合起来使用。



### 3.高并发场景下如何实现系统限流？

 在高并发场景下，系统限流是一种常用的保护机制，用于控制系统的访问量，防止系统因过多的请求而过载或崩溃。下面是一些实现系统限流的常见方法：

1. **令牌桶算法(**Token Bucket Algorithm)：令牌桶算法是一种基于队列的限流算法，系统会以固定的速率往令牌桶中放入令牌，每当请求到来时，需要从令牌桶中取出一个令牌，如果令牌桶中没有足够的令牌，则请求被拒绝。这种方法可以平滑限制请求的流量，但可能导致请求在高峰期间排队等待。
2. **漏桶算法(**Leaky Bucket Algorithm)：漏桶算法是一种基于队列的限流算法，类似于令牌桶算法，但不同之处在于漏桶算法是以固定的速率从桶中漏出请求，如果请求到来时，桶已满，则请求被拒绝。这种方法可以控制请求的速率，但可能导致请求在高峰期间丢失。
3. **计数器算法**(Counter Algorithm)：计数器算法是一种简单的限流算法，通过统计单位时间内的请求数量，并与阈值进行比较来限制请求的数量。例如，可以设置每秒钟最多处理的请求数量，超过这个数量的请求将被拒绝。这种方法简单直观，但可能在短时间内出现突发请求，导致系统无法应对。
4. **动态调整限流策略**：在高并发场景下，系统负载可能会不断变化，因此可以考虑动态调整限流策略。例如，可以根据系统的实时负载情况，动态调整限流算法的参数，如令牌放入速率、漏桶漏出速率或请求阈值，以适应系统的实际情况。
5. **分布式限流**：在分布式系统中，可以将限流策略应用到不同的节点或服务上，以限制整个系统的访问量。例如，可以在网关层进行限流，或者在每个服务的入口处进行限流。需要注意的是，分布式限流需要考虑多节点之间的同步和一致性问题。



### 4.什么是服务降级？什么是服务熔断？两者有什么区别？

* 服务熔断：当服务A调用服务B时，发现B不可用，上游A为了保证自己不受影响，不再调用服务B，而是直接返回一个结果，减轻A和B的压力，知道B恢复。
* 服务降级：当系统压力过载时，可以通过关闭某个服务，或限流某个服务来减轻系统压力。

相同点：

1. 都是为了防止系统崩溃

2. 都让用会体验到某些功能不可用

   

不同点：熔断是下游服务故障触发的，降级是为了降低系统负载。



### 5.什么是高内聚，低耦合？

高内聚（High Cohesion）和低耦合（Low Coupling）是软件工程中的两个重要原则，用于描述组件或模块之间的关系。

1. 高内聚：高内聚表示一个模块或组件内部的元素（例如方法、属性、功能等）之间关联度紧密，彼此之间相互依赖性较高，模块内的功能相互关联，共同完成某一特定的任务。高内聚的模块通常在实现上聚焦于单一的功能，且模块内的元素之间相互合作，共同完成特定的目标。高内聚的设计能够提高模块的可维护性、可测试性和重用性，同时减少模块之间的相互影响。
2. 低耦合：低耦合表示模块或组件之间的相互依赖性较低，模块之间通过定义清晰的接口进行通信，彼此之间独立存在，互不干扰。低耦合的设计能够降低模块之间的相互依赖性，使得系统更加灵活、可扩展和可维护。当一个模块或组件的修改不会对其他模块或组件造成较大的影响时，就表示低耦合的设计得以实现。

高内聚和低耦合的设计原则可以帮助软件系统实现模块化、可维护、可扩展和可测试的特性。高内聚可以提高模块内部的功能完整性和一致性，减少模块内部的复杂性；低耦合可以降低模块之间的相互依赖性，减少模块之间的耦合关系，提高系统的灵活性和可维护性。



### 6.eurake跟nacos有什么区别？

* nacos比eurake多了配置中心的功能，提供的功能也更加丰富。
* 心跳机制：
  * 服务定时向eruake发送心跳包，这样euraka就知道服务是否还在运行。
  * 而对于nacos来说，又分为临时实例和非临时实例：
    1. 临时实例采用的是跟eurake一样的机制，由服务向nacos发送心跳包。
    2. 非临时实例则是由nacos主动联系，如果连接失败，那么不会移除实例信息，而是将实例的健康状态设为false。

* 连接机制：nacos使用的是netty和服务直接进行连接，属于长连接。eurake使用定时发送和服务连接，属于短连接。



### 7.说说服务网关？

根据业务，可以分为两类：流量网关和业务网关。

* 流量网关：跟业务完全无关的部分，比如说安全策略，流量控制等。
* 业务网关：针对具体的业务。



### 8. 负载均衡的常用算法？

常用的负载均衡算法包括以下几种：

1. 轮询（Round Robin）：将请求按照顺序依次分发到多个服务器上，每个请求依次选择下一个服务器，从而平均分配请求到不同的服务器。适用于服务器性能相对均衡的场景。
2. 最小连接数（Least Connections）：选择当前连接数最少的服务器进行请求分发，从而将请求集中到连接数较少的服务器上，避免过载。适用于连接数不均衡的场景，可以有效降低服务器的负载。
3. 源IP哈希（Source IP Hash）：根据请求的源IP地址进行哈希计算，将同一源IP地址的请求分发到同一台服务器上，从而保证同一客户端的请求都发送到同一台服务器上，适用于需要保持会话状态或需要维持请求顺序的场景。
4. 加权轮询（Weighted Round Robin）：为不同的服务器设置不同的权重值，按照权重比例进行轮询分发请求，从而可以根据服务器性能的不同分配不同比例的请求到各个服务器上。
5. 加权最小连接数（Weighted Least Connections）：为不同的服务器设置不同的权重值，根据服务器的连接数和权重值进行计算，选择连接数和权重比例最小的服务器进行请求分发，从而实现更加精细化的负载均衡。



















# 十、MQ消息队列

### 1.rabbit mq的设计架构？

下面是rabbit mq的设计架构：

![image-20230327020003549](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230327020003549.png)



* **生产者** ：消息的生产者，负责将消息发生到 rabbit mq 服务器。
* **消费者** ：消息的消费者，负责从Queue中接收消息，并处理他们。
* **Channel**：我们的客户端都会使用一个Channel，再通过Channel去访问到 Rabbit MQ服务器，注意通信协议不是http，而是amqp协议。
* **Exchange** ：消息交换机。会根据我们的请求，转发给相应的消息队列，每个队列可以绑定到Exchange上，这样Exchange就可以将数据转发给队列了，可以存在多个，不同的Exchange类型可以用于实现不同消息的模式。
* **Queue** ：消息队列本体，生产者所有的消息都存放在消息队列中，等待消费者取出。
* **Virtual Host** ：有点类似于环境隔离，不同环境都可以单独配置一个 virtual Host，每个 Virtual Host可以包含很多个Exchange和Queue，每个Virtual Host之间互不影响。



### 2.什么是死信队列？如何导致的？延迟队列又是什么？怎么实现？

消息队列中的数据，如果迟迟没有消费者来处理，那么就会一直占用消息队列的空间。这个时候我们可以采取一定的措施，将数据重新路由到另一个特定的队列中去，这个特定的队列就是死信队列。

**如何导致的？**

* 消息被拒绝并且 requeue = false。
* 消息TTL（time to live）过期：消息可能会设置过期时间，当消息过期后，队列会将其从队列中删除并路由到死信队列。
* 队列到达最大长度：当队列中的消息数量达到最大长度时，队列无法再添加新的信息，测试新的消息将会被路由到死信队列。

**那么如何构建这样的一种使用模式呢？**

实际上本质就是一个死信交换机+绑定的死信队列，当正常队列中的消息被判定为死信时，会被发送到对应的死信交换机，然后再通过交换机发送到死信队列中，死信队列也有对应的消费者去处理消息。



延迟队列指的就是消息被放到队列中去，不让消费者立刻拿出来消费，而是等待一定的时间后，消费者才能拿到这个消息进行消费。

**如何实现延迟队列？**

可以利用死信队列和TTL。当队列中的消息TTL过期时，转发到死信队列中去，然后让消费者进行消费。





### 3.RabbitMQ 有哪些工作模式？

* **简单模式** ：基于一个队列，**一个发送者**将消息发送到队列，**一个接收者**从队列中接收消息并处理。在这种模式下，一**个消息只能被一个消费者消费。**

  ![image-20230408232916901](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230408232916901.png)

  

* **工作队列模式** ：在这种模式下，**一个生产者**将消息发送到队列，**多个消费者**从队列中接收消息并进行处理。**队列中的每个消息只能被一个消费者消费（会进行轮询操作）。**

  ![image-20230408232954736](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230408232954736.png)

  

* **发布/订阅模式** ：也称广播模式，一个生产者将消息发送到一个交换机，交换机将消息路由到所有与之绑定的队列中。多个消费者可以同时监听一个队列，并接收交换机路由到该队列的消息。在这种模式下，**一个消息可以被多个消费者处理**。

  ![image-20230408233456570](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230408233456570.png)

  

* **路由模式** ：在发布订阅的基础上增加了路由的概念，消息在发送时可以指定路由键（**routing key**），交换机将之路由到与之匹配的队列中。在这种模式下，多个消费者可以同时监听一个队列，**一个消息可以被多个消费者消费**。

  ![image-20230408234046980](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230408234046980.png)

  

* **主题模式** ：也成通配符模式，路由模式的基础上增加了通配符的概念，消息可以在发送时指定主题（topic） ，交换机将消息路由到与之匹配的队列中。在这种模式下，**一个消息可以被多个消费者消费，消费者可以通过统配符来匹配多个主题**。

  ![image-20230408234314999](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230408234314999.png)

  

### 4.如何保证消息的可靠性呢？

生产者端：

* **消息确认机制** ：信息发送者发送消息后，等待消息队列返回确认信息，告知发送者消息已被正确接收。
  * channel设置为confirm模式，则每条消息会被分配唯一的id。
  * 消息如果投递成功，会发送ack给生产者。包含Iid，回调ConfirmCallback接口
  * 如果中间出现错误，会返回nack给生产者。回调ConfirmCallback接口。
  * ack和nack只要一个会被触发，且是异步触发。
* **事务模式** ：消息发送者发送消息后，开启事务，如果消息队列正确接收到消息，事务就会被提交，否则事务就会回滚。
* **重试机制** ：如果消息发送失败，可以通过重试机制来重新发送消息，直到消息被成功发送到Rabbit MQ 中。

Rabbit MQ自身：

* **消息持久化** ：可以将队列和消息设置为持久化，当Rabbit MQ宕机时可以通过磁盘来持久化来保证消息不会丢失。
* **集群部署** ：Rabbit MQ支持集群部署，可以通过主备机制，镜像队列等方式来提高Rabbit MQ的可靠性和容错性。

消费者端：

* **消息确认机制** ：可以通过**手动ACK**或者自动ACK机制来确认消息，**手动ACK可以保证消息被正确处理后再发送ACK**，自动ACK则可以将ACK机制交给框架来处理，但需要注意自动ACK可能会出现重复消费的问题。

  * 声明队列时，指定noack = false，即手动ack。
  * broker的ack没有超时机制，如果没有给broker返回ack，那么这条消息不会被删。broker只会判断链接是否断开，如果断开,消息会被重新发送。
  
  

### 5.如何保证消息的顺序性？

出现消费错乱的情况：

* 为了提高效率，一个 queue存在多个 consumer

  ![image-20230327155500287](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230327155500287.png)

* 一个queue只存在一个consumer，但是为了提高处理效率，consumer中使用了多线程进行处理

  ![image-20230327155639253](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230327155639253.png)

  

保证消息顺序性的方法：

* 将原来的queue拆分成多个queue，每个队列都有自己的一个consumer。

  ![image-20230327160444796](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230327160444796.png)

* 一个queue就一个consumer，在consumer中维护多个内存队列，根据业务数据关键字将消息加入到不同的内存队列中。

  ![image-20230327160641450](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230327160641450.png)

  



### 6.如何保证Rabbit MQ的高可用？

* **集群模式** ：在多个节点上运行 rabbit mq，这样即使某个节点发生故障，集群中的节点仍然可以提供服务，从而提高高可用性。在rabbit mq集群中，消息会自动在各个节点间进行同步复制，从而避免单点故障。

* **消息镜像** ：在集群中的每个节点都创建一个队列，并将这些队列设置为镜像队列。这样在每个节点上都会存储一份完整地消息，保证了消息的高可用性。

  

### 7.分布式常见的幂等性场景有哪些？分布式幂等性如何设计？

以下是一些常见的分布式幂等性场景的例子：

1. 支付系统：在处理支付请求时，需要保证同一笔支付请求只能被处理一次，避免重复扣款或多次支付。

2. 订单系统：在生成订单时，需要保证同一笔订单只能被创建一次，避免重复下单或重复生成订单。

3. 秒杀系统：在处理秒杀请求时，需要保证同一用户对同一商品的秒杀请求只能被处理一次，避免重复秒杀或多次减库存。

4. 优惠券系统：在领取优惠券时，需要保证同一用户对同一优惠券只能领取一次，避免重复领取或重复消费。

5. 积分系统：在处理积分增加或减少请求时，需要保证同一用户对同一积分操作只能执行一次，避免重复操作或积分不一致。

6. 活动系统：在参与活动或抽奖时，需要保证同一用户对同一活动或抽奖请求只能参与一次，避免重复参与或重复中奖。

   

在分布式系统中，幂等性是指对同一请求的多次执行所产生的结果是相同的，不会因为重复请求而导致业务数据的错误变化或产生不一致的状态。设计分布式幂等性是为了保证系统在面对网络分区、节点故障、消息重复等异常情况时，依然能够保持正确的业务逻辑和数据一致性。

下面是一些设计分布式幂等性的常用方法：

1. 请求唯一标识：在每个请求中使用唯一标识来标记请求的唯一性，可以使用全局唯一的请求ID、流水号、UUID等，将该唯一标识作为幂等性的依据。在每次处理请求时，先检查该唯一标识在系统中是否已存在，如果已存在，则说明该请求已经被处理过，直接返回处理结果，避免重复处理。
2. 幂等性校验：在每个请求的处理逻辑中，添加幂等性校验的步骤，判断请求是否已经处理过，如果已处理，则直接返回之前的处理结果，避免重复处理。可以通过在数据库、缓存、消息队列等地方记录已处理的请求信息，并使用请求唯一标识来索引和检查。
3. 乐观锁：在数据库中使用乐观锁机制来实现幂等性。通过在数据表中添加版本号（Version）字段，并在更新操作时对版本号进行比对和更新，如果版本号匹配，则说明请求已经被处理过，直接返回处理结果，避免重复处理。
4. 消息队列去重：在使用消息队列进行异步消息处理时，可以通过在生产者端进行去重操作，避免重复发送相同的消息。可以使用消息队列提供的幂等性特性，如RabbitMQ的deduplication header或Kafka的幂等性Producer。
5. 时间戳或过期时间：在处理请求时，可以使用时间戳或过期时间的方式来实现幂等性。例如，在处理请求时记录请求的处理时间戳或过期时间，如果当前时间小于过期时间，说明请求已经处理过，直接返回处理结果，避免重复处理。
6. 分布式锁：使用分布式锁来保证在分布式环境下的幂等性。例如，使用分布式锁工具如ZooKeeper、Redis等，在处理请求时先尝试获取分布式锁，如果获取成功，则执行请求处理逻辑，否则直接返回之前的处理结果，避免重复处理。

**如何判断是同一个请求呢？**

在分布式系统中，判断是否是同一个请求可以通过以下几种方式：

1. 请求唯一标识：为每个请求生成一个唯一的标识，例如一个全局唯一的请求ID或Token。可以通过在请求头、请求参数、请求体等地方添加该标识，并在服务端进行提取和校验，判断是否是同一个标识，从而确定是否是同一个请求。
2. 请求参数：请求参数中携带了足够的信息来唯一标识一个请求。例如，在提交订单的请求中，可以携带订单号作为请求参数，在服务端进行校验，判断是否是同一个订单号，从而判断是否是同一个请求。
3. 请求来源：请求来源的网络地址或者服务名也可以作为判断是否是同一个请求的依据。例如，在微服务架构中，可以使用服务名、IP地址、端口等信息来标识请求的来源，从而判断是否是同一个请求。
4. 请求时间戳：请求的时间戳可以作为判断是否是同一个请求的依据。例如，可以在请求中携带一个时间戳，并在服务端进行校验，判断请求的时间戳是否在合理的时间范围内，从而判断是否是同一个请求。



### 8.rabbitmq中的交换机类型有哪些？

* direct 类型的交换机：一个是`（AMQP default）`还有一个是`amq.direct`，它们都是直连模式的交换机。
  * AMQP default：是所有虚拟主机都会自带的一个默认交换机，并且此交换机不可删除，此交换机默认绑定到所有的消息队列，如果是通过默认交换机发送消息，那么会根据消息的`routingKey`（之后我们发消息都会指定）决定发送给哪个同名的消息队列，同时也不能显示地将消息队列绑定或解绑到此交换机。
  * amq.direct：一个普通的直连交换机。具有绑定关系，如果没有指定的消息队列绑定到此交换机上，那么这个交换机无法正常将信息存放到指定的消息队列中，也是根据`routingKey`寻找消息队列（但是可以自定义）。

* fanout（扇出）类型的交换机：一种广播类型，消息会被广播到所有与此交换机绑定的消息队列中。
* topic（主题）类型的交换机：将`routingKey`以模糊匹配的方式去进行转发，匹配到相应的队列中。
* header（头部）类型的交换机：根据头部信息来决定的，在我们发送的消息中是可以携带一些头部信息的（类似于HTTP），我们可以根据这些头部信息来决定路由到哪一个消息队列中。





# 十一、Linux

### 1.绝对路径用什么符号表示？当前目录、上层目录用什么表示？主目录用什么表示？切换目录用什么命令？

* 绝对路径：如 /etc/init.d

* 当前目录：./

* 上层目录：../

* （用户）主目录：~/

* 切换目录：cd 

  

### 2.查看文件有哪些命令？

* `vi/vim  文件名`：以编辑方式查看，可以修改，如果没有该文件就创建新的文件。
* `cat 文件名`：显示全部文件内容
* `more 文件名` ：分页显示文件内容
* `less 文件名` ：与more相似，更好的可以往前翻页
* `tail 文件名` ：仅查看尾部，还可以指定行数
* `head 文件名` ：仅查看头部，还可以指定行数



### 3.怎么查看当前进程？怎么执行退出？

查看当前进程：ps  

执行退出：exit

### 4.怎么查看当前路径？

pwd。

### 5.怎么清屏？怎么退出当前命令？怎么执行睡眠？查找指定帮助命令？

* 清屏：clear
* 退出当前命令：ctrl  + c
* 执行睡眠：ctrl + z 挂起当前进程
* 查找指定帮助命令：man



### 6.创建目录用什么命令？创建文件用什么命令？复制文件用什么命令？

* 创建目录：mkdir
* 创建文件：touch、vi、vim  后面跟文件名
* 复制文件：cp   



### 7.怎样向屏幕输出字符串？

echo +字符串， 如向屏幕输出hello world ：echo   "hello world" 。

### 8.移动文件用哪个命令？改名用哪个命令？

移动文件：

```shell
mv file.txt /home/user/documents
```

改名：

```shell
mv file.txt newfile.txt
```

### 9.复制文件用哪个命令？如果需要连同文件夹一块复制呢?

复制文件：

```shell
cp file.txt /home/user/documents
```

连同文件夹一块复制：

```shell
cp -r mydir /home/user/documents
```



### 10.删除文件用哪个命令？如果需要连目录及目录下文件一块删除呢？删除空文件夹用什么命令？

删除文件：

```shell
rm example.txt
```

连同文件夹一块删除：

```shell
rm -r my_directory
```

删除空文件夹：

```shell
rmdir
```



### 11.linux中有几种通配符？都代表什么含义？

"*" ，代表匹配任意字符，包括0个字符。

“?” ，匹配单个字符。

“[]”，匹配在中括号中的任意一个字符。



### 12.用什么命令对一个文件的内容进行统计（行号，单词数，字节数）？

```shell
wc -l -w -c example.txt
```

-l ,行数

-w ,单词数

-c ,字节数



### 13.grep 命令有什么用？

是一种强大的文本搜索工具，它能使用正则表达式搜索文本，并把匹配的行打印出来。



### 14.怎么使一个命令在后台运行？

一般都是使用 & 在命令结尾来让程序自动运行。

```shell
sleep 10 &
```



### 15.利用 ps怎么显示所有的进程？怎么利用ps查看指定进程的信息

显示所有进程：

```shell
ps -ef
```

查看指定进程的信息：

```shell
ps -ef | grep pid
```

**`ps -ef`/`ps -aux`：** 这两个命令都是查看当前系统正在运行进程，两者的区别是展示格式不同。如果想要查看特定的进程可以使用这样的格式：**`ps aux|grep redis`** （查看包括 redis 字符串的进程），也可使用 `pgrep redis -a`。

注意：如果直接用 ps（（Process Status））命令，会显示所有进程的状态，通常结合 grep 命令查看某进程的状态。



### 16.linux中的 “|”是什么？有什么作用？

“|” 作为管道符，将“|”前面命令的输出作为“|”后面的输入。

```shell
grep "example" file.txt | wc -l
```



### 17.把后台任务调到前台执行使用什么命令?把停下的后台任务在后台执行起来用什么命令?

把后台调到前台运行：

```shell
fg %1   ### 1 是 job id
```

把前台调到后台运行：

```shell
bg %1   ### 1 是 job id
```



### 18.终止进程用什么命令？两者之间有什么区别?

kill  pid:

```shell
kill  1234
```

kill -9  pid:

```shell
kill -9  1234
```

两者区别：

* 使用 kill 命令会向进程发送一个信号，默认是`SIGTERN` ，它允许进程在终止前执行任何清理的操作。
* 使用 kill -9 命令会向进程发送一个信号`SIGKILL` ,它不允许进程在终止之前执行任何清理操作。



### 19.如何查看内存使用情况？

**top**命令用于查看进程的CPU和内存使用情况。当然也会报告内存总量，以及内存使用情况，所以可用来监控物理内存的使用情况。



### 20.压缩文件的操作命令

**打包并压缩文件** 

Linux中的打包文件一般是以 .tar 结尾的，压缩文件一般是以.gz结尾的。而一般情况**下打包和压缩是一起进行的，打包并压缩后的文件的后缀名一般.tar.gz。**

命令：`tar -zcvf  打包压缩后的文件名  要打包压缩的文件`

比如：假如 test 目录下有三个文件分别是：aaa.txt bbb.txt ccc.txt，如果我们要打包 test 目录并指定压缩后的压缩包名称为 test.tar.gz 可以使用命令：`tar -zcvf test.tar.gz aaa.txt bbb.txt ccc.txt` 或 

`tar -zcvf test.tar.gz /test/`



**解压压缩包** 

命令：`tar [-xvf] 压缩文件`

- 将 /test 下的 test.tar.gz 解压到当前目录下可以使用命令：**`tar -xvf test.tar.gz`**

- 将 /test 下的 test.tar.gz 解压到根目录/usr 下:**`tar -xvf test.tar.gz -C /usr`**（- C 代表指定解压的位置）



### 21.讲讲Linux的权限命令？

通过 `ls -l` 命令我们可以查看某个目录下的文件或者目录的权限

![image-20230330003008479](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230330003008479.png)

第一列的信息解释如下：

![image-20230330003047125](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230330003047125.png)

文件的类型：

* -：代表文件。
* d：代表目录
* l：代表软连接（可以认为是windows中的快捷方式）



Linux中的权限分为以下几种：

* r：可读，用数字4来表示
* w：可写，用数字2表示
* x：可执行，用数字1表示



修改文件/目录的权限的命令：

示例：修改/test 下的 aaa.txt 的权限为文件所有者有全部权限，文件所有者所在的组有读写权限，其他用户只有读的权限。

命令：**`chmod u=rwx,g=rw,o=r aaa.txt`** 或者 **`chmod 764 aaa.txt`** 

（**这里为什么是764？** 第一个是给文件所有者赋予所有权限：可读是4，可写是2，可执行是1，三者加起来就是7，后面的6跟4也是一样的道理，6是针对文件所有者所在的组，4是针对其他用户的权限。）

![image-20230330004200476](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230330004200476.png)





### 22.说一说网络通信命令？

* 查看当前系统的网卡信息：ifconfig
* 查看与某台机器的连接情况：ping
* 查看当前系统的端口使用：netstat -an





# 十二、设计模式



### 1.单例模式

































# 十三、十大经典排序算法

### 简介

常见的内部排序算法有：**插入排序、希尔排序、选择排序、冒泡排序、归并排序、快速排序、堆排序、基数排序**等。 

![image-20230319011800739](C:\Users\rqt\AppData\Roaming\Typora\typora-user-images\image-20230319011800739.png)

图片名词解释：

* n : 数据规模
* k ：桶的个数
* In-place ：占用常数内存，不占用额外内存
* Out-place：占用额外内存

术语说明：

* **稳定** ：A=B,如果原本A在B的前面，排序之后A仍然在B的前面。
* **不稳定** ：A=B,如果原本A在B的前面，排序之后A在B的后面。
* **内排序** ：所有排序操作都在内存中完成。
* **外排序** ：由于数据太大，因此把数据放在磁盘中，而排序通过磁盘和内存的数据传输才能进行。
* **时间复杂度** ：定性描述一个算法执行所耗费的时间。
* **空间复杂度** ：定性描述一个算法执行所需内存的大小。









# 十四、Git的使用

### 1.初始化仓库（需要具备一些git知识）

1. 新建一个文件夹，代表git项目所在。文件夹就是代表本地库。比如说我建立一个笔记总结的文件项目，专门用来做笔记的。于是我可以在该项目下使用如下命令：

   ```shell
   rqt@DESKTOP-IKU305R MINGW64 ~/Desktop/笔记总结
   $ git init
   Initialized empty Git repository in C:/Users/rqt/Desktop/笔记总结/.git/
   ```

2. 当在文件夹中出现.git隐藏目录的时候，就说明该文件夹已经被git接管了。

3. 然后让本地库与github上面的远程库连接，使用如下命令。

   ```shell
   git remote add origin https://github.com/rqt2333/note
   ```

4. 使用如下命令查看git的一些配置，可以看到已经将本地库和远程库连接了。

   ```shell
   git config -l
   ```

   ```shell
   diff.astextplain.textconv=astextplain
   filter.lfs.clean=git-lfs clean -- %f
   filter.lfs.smudge=git-lfs smudge -- %f
   filter.lfs.process=git-lfs filter-process
   filter.lfs.required=true
   http.sslbackend=openssl
   http.sslcainfo=D:/program/Git/mingw64/ssl/certs/ca-bundle.crt
   core.autocrlf=true
   core.fscache=true
   core.symlinks=false
   pull.rebase=false
   credential.helper=manager-core
   credential.https://dev.azure.com.usehttppath=true
   init.defaultbranch=master
   credential.https://gitee.com.provider=generic
   user.name=rqt
   user.email=rqt2333@foxmial.com
   http.sslverify=false
   http.proxy=socks5://127.0.0.1:7890
   credential.https://git.kingdonsoft.com:9001.provider=generic
   https.proxy=socks5://127.0.0.1:7890
   core.repositoryformatversion=0
   core.filemode=false
   core.bare=false
   core.logallrefupdates=true
   core.symlinks=false
   core.ignorecase=true
   remote.origin.url=https://github.com/rqt2333/note
   remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
   ```

   remote.origin.url=https://github.com/rqt2333/note
   remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*

   这两行可以看出已经和远程库连接了。

5. 如果远程仓库什么都没有，可以不用pull。但是如果远程仓库存在一些文件，那个你在push之前应该要先pull。

   默认情况下，`git pull`和`git push`都将与当前分支关联的远程分支的代码进行合并或推送。例如，如果你当前在`master`分支上，并且与远程仓库的`origin/master`分支存在关联，则`git pull`将尝试将远程分支`origin/master`合并到本地`master`分支中，而`git push`将尝试将本地`master`分支中的更改推送到远程分支`origin/master`中。

   分支如何关联呢？使用如下命令

   ```shell
   git branch --set-upstream-to=<remote>/<branch> <local_branch>
   ```

   其中，`<remote>`表示远程仓库名，`<branch>`表示远程分支名，`<local_branch>`表示本地分支名。

   例如，假设你的远程仓库名为`origin`，你要将本地分支`dev`关联到远程分支`origin/dev`上，可以使用以下命令

   ```shell
   git branch --set-upstream-to=origin/dev dev
   ```

   如果你想查看本地分支关联的远程分支，可以使用以下命令：

   ```shell
   git branch -vv
   ```

   其中，`-vv`表示显示本地分支和远程分支的关联关系。

6. 

### 2.清屏快捷键

ctrl + L。在使用git 命令行时,可以使用ctrl + L快速清屏。

























