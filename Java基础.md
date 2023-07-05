# **JAVA基础**

## **面向对象和面向过程的区别**

* **面向过程：面向过程的性能比面向对象要高。**因为类调⽤时需要实例化，开销⽐较⼤，⽐较消耗资源，所以当性能是最重要的考量因素的时候，⽐如单⽚机嵌⼊式开发、Linux/Unix 等⼀般采⽤⾯向过程开发。
* **面向对象：面向对象以维护、易复用、易扩展。**因为⾯向对象有封装、继承、多态性的特性，所以可以设计出低耦合的系统，使系统更加灵活、更加易于维护。

**面向过程性能比面向对象高？**

Java 性能差的主要原因是 Java 是半编译语⾔，最终的执⾏代码并不是可以直接被 CPU 执⾏的⼆进制机械码。⽽⾯向过程语⾔⼤多都是直接编译成机械码在电脑上执⾏，并且其它⼀些⾯向过程的脚本语
⾔性能也并不⼀定⽐ Java 好。

## **Java语言有哪些特点？**

1. 面向对象（封装、继承、多态）；
2. 平台无关性（Java虚拟机实现平台无关性）；
3. 安全可靠；
4. 支持多线程（C++没有内置多线程机制，需要调用操作系统的多次线程功能）；
5. 支持网络编程且方便；（网络编程就就是编写程序使联网的多个设备之间进行数据传输。Java语言对网络编程提供了良好的支持，通过其提供的接口我们可以很方便地进行网络编程。）
6. 编译与解释并存。（编译（Compile）的过程是把整个源程序代码翻译成另外一种代码，翻译后的代码等待被执行或者被优化等等，发生在运行之前，产物是**另一份代码**。解释（Interpret）的过程是把源程序代码一行一行的读懂，然后一行一行的执行，发生在运行时，产物是**运行结果**。）

## **JVM vs JDK vs JRE**

**JVM：**Java虚拟机时运行Java字节码的虚拟机。JVM 有针对不同系统的特定实现（Windows，Linux，macOS），⽬的是使⽤相同的字节码，它们都会给出相同的结果。

![image-20230630105731049](E:\八股图\Java基础\java程序编译解释过程.png)

**JDK：**Java Development Kit，是功能齐全的Java SDK（软件开发工具）。它拥有JRE所拥有的一切，还有编译器（javac）和工具（javadoc、jdb）。它能够创建和编译程序。

**JRE：**java运行时环境。它是**运⾏已编译 Java 程序所需的所有内容的集合**，包括 Java 虚拟机（JVM），Java 类库，java 命令和其他的⼀些基础构件。但是，它不能⽤于创建新程序。

## **Java和C++的区别？**

- 都是面向对对象的语言，都支持封装、继承和多态；
- Java不提供指针来直接访问内存，程序内存更加安全
- Java 的类是单继承的，C++ ⽀持多重继承；虽然 Java 的类不可以多继承，但是接⼝可以多继承。
- Java 有⾃动内存管理机制，不需要程序员⼿动释放⽆⽤内存
- 在 C 语⾔中，字符串或字符数组最后都会有⼀个额外的字符‘\0’来表示结束。但是，Java 语⾔中没有结束符这⼀概念。

## **字符型常量和字符串常量的区别？**

1. 形式上：字符常量是**单引号**引起的⼀个字符；字符串常量是**双引号**引起的若⼲个字符；
2. 含义上：字符常量相当于⼀个**整型值( ASCII 值),可以参加表达式运算**; 字符串常量代表⼀个**地址值(**该字符串在内存中存放位置)；
3. 占内存⼤⼩：字符常量只占 2 个字节；字符串常量占若⼲个字节 (**注意： char 在 Java 中占两个字节)**

![image-20230630110916013](E:\八股图\Java基础\java基本类型大小.png)

## **构造器Constructor是否可被override？**

Constructor 不能被 override（重写），但是可以 overload（重载），所以你可以看到⼀个类中有多个构造函数的情况。

**重载：**发⽣在同⼀个类中，⽅法名必须相同，参数类型不同、个数不同、顺序不同，⽅法返回值和访问修饰符可以不同。重载就是同⼀个类中多个同名⽅法根据不同的传参来执⾏不同的逻辑处理。

**重写：**重写发⽣在运⾏期，是⼦类对⽗类的允许访问的⽅法的实现过程进⾏重新编写。

1. 返回值类型、⽅法名、参数列表必须相同，抛出的异常范围⼩于等于⽗类，访问修饰符范围⼤于等于⽗类。
2. 如果⽗类⽅法访问修饰符为 private/final/static 则⼦类就不能重写该⽅法，但是被 static 修饰的⽅法能够被再次声明。
3. 构造⽅法⽆法被重写。

综上：重写就是⼦类对⽗类⽅法的重新改造，外部样⼦不能改变，内部逻辑可以改变。

![image-20230630112226584](E:\八股图\Java基础\重写和重载.png)

## **Java面向对象编程三大特性：封装、继承、多态**

**封装：**封装把⼀个对象的属性私有化，同时提供⼀些可以被外界访问的属性的⽅法，如果属性不想被外界访问，我们⼤可不必提供⽅法给外界访问。

**继承：**继承是使⽤已存在的类的定义作为基础建⽴新类的技术，新类的定义可以增加新的数据或新的功能，也可以⽤⽗类的功能，但不能选择性地继承⽗类。通过使⽤继承我们能够⾮常⽅便地复⽤以前的代码。

1. ⼦类拥有⽗类对象所有的属性和⽅法（包括私有属性和私有⽅法），但是⽗类中的私有属性和⽅法⼦类是⽆法访问，只是拥有。
2. ⼦类可以拥有⾃⼰属性和⽅法，即⼦类可以对⽗类进⾏扩展。
3. ⼦类可以⽤⾃⼰的⽅式实现⽗类的⽅法。（以后介绍）。

**多态：**程序中定义的引⽤变量所指向的具体类型和通过该引⽤变量发出的⽅法调⽤在编程时并不确定，⽽是在程序运⾏期间才确定，即⼀个引⽤变量到底会指向哪个类的实例对象，该引⽤变量发出的⽅法调⽤到底是哪个类中实现的⽅法，必须在由程序运⾏期间才能决定。

在 Java 中有两种形式可以实现多态：继承（多个⼦类对同⼀⽅法的重写）和接⼝（实现接⼝并覆盖接⼝中同⼀⽅法）。

## **String、StringBuffer、StringBuilder的区别是什么？**

**可变性**

**String为什么是不可变的？**

String 类中使⽤ final 关键字修饰**字符数组**来保存字符串， **private final char value[]** ，所以 **String 对象是不可变**的。

⽽ StringBuilder 与 StringBuffer 都继承⾃ AbstractStringBuilder 类，在 AbstractStringBuilder 中也是使⽤字符数组保存字符串 char[]value 但是没有⽤ final 关键字修饰，所以**这两种对象都是可变**的。

**线程安全性**

String 中的对象是不可变的，也就可以理解为常量，线程安全。AbstractStringBuilder 是 StringBuilder 与 StringBuffer 的公共⽗类，定义了⼀些字符串的基本操作，如 expandCapacity、append、insert、indexOf 等公共⽅法。StringBuffer 对⽅法加了同步锁或者对调⽤的⽅法加了同步锁，所以是线程安全的。StringBuilder 并没有对⽅法进⾏加同步锁，所以是⾮线程安全的。

**性能**

每次对 String 类型进⾏改变的时候，都会⽣成⼀个新的 String 对象，然后将指针指向新的 String 对象。

StringBuffer 每次都会对 StringBuffer 对象本身进⾏操作，⽽不是⽣成新的对象并改变对象引⽤。

相同情况下使⽤ StringBuilder 相⽐使⽤ StringBuffer 仅能获得 10%~15% 左右的性能提升，但却要冒多线程不安全的⻛险。

**对于三者使用的总结：**

1. 操作少量的数据：适用String
2. 单线程操作字符串缓冲区下操作大量数据：适用StringBuilder
3. 多线程操作字符串缓冲区下操作大量数据：适用StringBuffer

## **⾃动装箱与拆箱**

（[详情]（[深入剖析Java中的装箱和拆箱 - Matrix海子 - 博客园 (cnblogs.com)](https://www.cnblogs.com/dolphin0520/p/3780005.html)））

- **装箱：**将基本类型用它们对应的引用类型（包装器类型）包装起来；
- **拆箱：**将包装类型转换为基本数据类型；

```java
public` `class` `Main {
  ``public` `static` `void` `main(String[] args) {
    ``Integer i = ``10``;	//装箱
    ``int` `n = i;	//拆箱
  ``}
}
```

装箱过程是通过调用包装器的valueOf方法实现的，而拆箱过程是通过调用包装器的 xxxValue方法实现的。（xxx代表对应的基本数据类型）。

**下面这段代码的输出结果是什么？**

```java
public` `class` `Main {
  ``public` `static` `void` `main(String[] args) {
    ``Integer i1 = ``100``;
    ``Integer i2 = ``100``;
    ``Integer i3 = ``200``;
    ``Integer i4 = ``200``;
    ``System.out.println(i1==i2);
    ``System.out.println(i3==i4);
  ``}
}
```

输出：true false。

原因：在通过valueOf方法创建Integer对象的时候，如果数值在[-128,127]之间，便返回指向IntegerCache.cache中已经存在的对象的引用；否则创建一个新的Integer对象。

**谈谈`Integer i = new Integer(xxx);`和`Integer i =xxx;`这两种方式的区别。**

1. 第一种方式不会触发自动装箱的过程；而第二种方式会触发；
2. 在执行效率和资源占用上的区别。第二种方式的执行效率和资源占用在一般性情况下要优于第一种情况（注意这并不是绝对的）。

需要注意的是：当 "=="运算符的两个操作数都是包装器类型的引用，则是比较指向的是否是同一个对象，而如果其中有一个操作数是表达式（即包含算术运算）则比较的是数值（即会触发自动拆箱的过程）。另外，对于包装器类型，equals方法并不会进行类型转换。

> `c.equals(a+b)`会先触发自动拆箱过程，再触发自动装箱过程，也就是说`a+b`，会先各自调用`intValue`方法，得到了加法运算后的数值之后，便调用`Integer.valueOf`方法，再进行`equals`比较。

## **在一个静态方法内调用一个非静态成员为什么是非法的？**

由于静态方法可以不通过对象进行调用，因此在静态方法内，不能调用其他非静态变量，也不可以访问非静态变量的成员。

## **在 Java 中定义⼀个不做事且没有参数的构造⽅法的作⽤**

Java 程序在执⾏⼦类的构造⽅法之前，如果没有⽤ super() 来调⽤⽗类特定的构造⽅法，则会调⽤⽗类中“没有参数的构造⽅法”。因此，如果⽗类中只定义了有参数的构造⽅法，⽽在⼦类的构造⽅法中⼜没有⽤ super() 来调⽤⽗类中特定的构造⽅法，则编译时将发⽣错误，因为 Java 程序在⽗类中找不到没有参数的构造⽅法可供执⾏。解决办法是在⽗类⾥加上⼀个不做事且没有参数的构造⽅法。

子类是不继承父类的构造器（构造方法或者构造函数）的，它只是调用（隐式或显式）。**如果父类的构造器带有参数，则必须在子类的构造器中显式地通过 super 关键字调用父类的构造器并配以适当的参数列表。**如果父类构造器没有参数，则在子类的构造器中不需要使用 **super** 关键字调用父类构造器，**系统会自动调用父类的无参构造器**。**在调⽤⼦类构造⽅法之前会先调⽤⽗类没有参数的构造⽅法。**

```java
class SuperClass {  
    private int n;  
    SuperClass(){    					      	      			 System.out.println("SuperClass()";  
    }  
      SuperClass(int n) {    
          System.out.println("SuperClass(int n)");    
          this.n = n;  } 
      }                                                              // SubClass 类继承 
      class SubClass extends SuperClass{  
          private int n;    
          SubClass(){ // 自动调用父类的无参数构造器
              System.out.println("SubClass");  
          }      
          public SubClass(int n){     
              super(300);  // 调用父类中带有参数的构造器    
              System.out.println("SubClass(int n):"+n);    
              this.n = n;  } 
      } 
      // SubClass2 类继承 
      class SubClass2 extends SuperClass{  
          private int n;    
          SubClass2(){    
              super(300);   // 调用父类中带有参数的构造器   
              System.out.println("SubClass2");  
          }      
          public SubClass2(int n){    // 自动调用父类的无参数构造器 
              System.out.println("SubClass2(int n):"+n);    
              this.n = n;  } 
      } 
      public class TestSuperSub{                                       public static void main (String args[]){    
          System.out.println("------SubClass 类继承------");    
          SubClass sc1 = new SubClass();    
          SubClass sc2 = new SubClass(100);     
          System.out.println("------SubClass2 类继承------");    
          SubClass2 sc3 = new SubClass2();    
          SubClass2 sc4 = new SubClass2(200);   
      } 
}
```

输出结果为：

```java
------SubClass 类继承------
SuperClass()
SubClass
SuperClass(int n)
SubClass(int n):100
------SubClass2 类继承------
SuperClass(int n)
SubClass2
SuperClass()
SubClass2(int n):200
```

## **接口和抽象类的区别是什么？ **

**抽象类：**在Java中被abstract关键字修饰的类称为抽象类，被abstract关键字修饰的方法称为抽象方法，抽象方法只有方法的声明，没有方法体。

1. 抽象类不能被实例化只能被继承；
2. 包含抽象方法的一定是抽象类，但是抽象类不一定含有抽象方法；
3. 抽象类中的抽象方法的修饰符只能为public或者protected，默认为public；
4. 一个子类继承一个抽象类，则子类必须实现父类抽象方法，否则子类也必须定义为抽象类；
5. 抽象类可以包含属性、方法、构造方法，但是构造方法不能用于实例化，主要用途是被子类调用。

**接口：**Java中接口使用interface关键字修饰，特点为：

1. 接口可以包含变量、方法；变量被隐式指定为`public static final`，方法被隐士指定为`public abstract`（JDK1.8之前）；
2. 接口支持多继承，即一个接口可以extends多个接口，间接的解决了Java中类的单继承问题；

**相同点：**

1. 都不能实例化；
2. 都包含抽象方法，其子类都必须对这些方法进行重写；
3. 都可以有默认实现的方法。

**不同点：**

1. 接口只有定义，不能有方法的实现，java 1.8中可以定义`default`方法体，而抽象类可以有定义与实现，方法可在抽象类中实现。
2. 一个类可以实现多个接口，但一个类只能继承一个抽象类。所以，使用接口可以间接地实现多重继承。
3. 接口强调特定功能的实现，而抽象类强调所属关系。
4. 从设计层⾯来说，抽象是对类的抽象，是⼀种模板设计，⽽接⼝是对⾏为的抽象，是⼀种⾏为的规范。继承是一个 "是不是"的关系，而接口实现则是 "有没有"、具不具备的关系。
5. 接口成员变量默认为`public static final`，必须赋初值，不能被修改；抽象类中成员变量默认`default`，可在子类中被重新定义，也可被重新赋值；
6.  接⼝⽅法默认修饰符是 `public` ，抽象⽅法可以有 `public` 、 `protected` 和 `default` 这些修饰符（抽象⽅法就是为了被重写所以不能使⽤ `private` 关键字修饰！）。

## **成员变量与局部变量的区别有哪些？**

1. 从语法形式上看：成员变量是属于类的，⽽局部变量是在⽅法中定义的变量或是⽅法的参数；成员变量可以被 `public` ，`private`，`static` 等修饰符所修饰，⽽局部变量不能被访问控制修饰符及 `static` 所修饰；但是，成员变量和局部变量都能被 `final` 所修饰。
2. 从变量在内存中的存储⽅式来看：如果成员变量是使⽤ `static` 修饰的，那么这个成员变量是属于类的，如果没有使⽤ `static` 修饰，这个成员变量是属于实例的。**对象存于堆内存**，如果局部变量类型为基本数据类型，那么存储在栈内存，如果为引⽤数据类型，那存放的是指向堆
   内存对象的引⽤或者是指向常量池中的地址。
3. 从变量在内存中的⽣存时间上看：成员变量是对象的⼀部分，它随着对象的创建⽽存在，⽽局部变量随着⽅法的调⽤⽽⾃动消失。
4. 成员变量如果没有被赋初值：则会⾃动以类型的默认值⽽赋值（⼀种情况例外：被 final 修饰的成员变量也必须显式地赋值），⽽局部变量则不会⾃动赋值。

## **创建⼀个对象⽤什么运算符？对象实体与对象引⽤有何不同？**

new运算符，new创建对象实例（对象实例在堆内存中），对象引⽤指向对象实例（对象引⽤存放在栈内存中）。⼀个对象引⽤可以指向 0 个或 1 个对象（⼀根绳⼦可以不系⽓球，也可以系⼀个⽓球）；⼀个对象可以有 n 个引⽤指向它（可以⽤ n 条绳⼦系住⼀个⽓球）。

## **构造⽅法有哪些特性？**

1. 名字与类名相同。
2. 没有返回值，但不能用void声明构造函数。
3. 生成类的对象时自动执行，无需调用。

## **静态方法和实例方法有何不同？**

1. 在外部调用静态方法时，可以使用"类名.方法名"的方式，也可以使用"对象名.方法名"的方式。而实例方法只有后面这种方式。也就是说，调用静态方法可以无需创建对象。
2. 静态⽅法在访问本类的成员时，只允许访问静态成员（即静态成员变量和静态⽅法），⽽不允许访问实例成员变量和实例⽅法；实例⽅法则⽆此限制。

## **== 与 equals**

**== :** 它的作⽤是判断两个**对象的地址**是不是相等。即，判断两个对象是不是同⼀个对象(基本数据类型==⽐较的是值，引⽤数据类型==⽐较的是内存地址)。

**equals() :** 它的作⽤也是判断两个对象是否相等。但它⼀般有两种使⽤情况：

- 情况 1：类没有覆盖 equals() ⽅法。则通过 equals() ⽐较该类的两个对象时，等价于通过
  “==”⽐较这两个对象。
- 情况 2：类覆盖了 equals() ⽅法。⼀般，我们都覆盖 equals() ⽅法来⽐较两个对象的内容是
  否相等；若它们的内容相等，则返回 true (即，认为这两个对象相等)。

```java
public class test1 {
    public static void main(String[] args) {
        String a = new String(&quot;ab&quot;); // a 为⼀个引⽤
        String b = new String(&quot;ab&quot;); // b为另⼀个引⽤,对象的内容⼀样
        String aa = &quot;ab&quot;; // 放在常量池中
        String bb = &quot;ab&quot;; // 从常量池中查找
        if (aa == bb) // true
            System.out.println(&quot;aa==bb&quot;);
        if (a == b) // false，⾮同⼀对象
            System.out.println(&quot;a==b&quot;);
        if (a.equals(b)) // true
            System.out.println(&quot;aEQb&quot;);
        if (42 == 42.0) { // true
            System.out.println(&quot;true&quot;);
        }
    }
}
```

说明：

- String 中的 equals ⽅法是被重写过的，因为 object 的 equals ⽅法是⽐较的对象的内存地址，⽽ String 的 `equals` ⽅法⽐较的是对象的值。
- 当创建 String 类型的对象时，虚拟机会在常量池中查找有没有已经存在的值和要创建的值相同的对象，如果有就把它赋给当前引⽤。如果没有就在常量池中重新创建⼀个 String 对象。
- `equals` 方法会依次比较**引用地址、对象类型、值的内容**是否相同，都相同才会返回true。所以`equals`方法比`==`比较的范围更大、内容更多。 用`==`判断为true的两个值，用`equals`判断不一定为true。

## **hashCode 与 equals **

1) **hashCode()介绍：**  

   `hashCode()` 的作⽤是获取哈希码，也称为散列码；它实际上是返回⼀个 int 整数。这个哈希码的作⽤是确定该对象在哈希表中的索引位置。 `hashCode()` 定义在 JDK 的 Object 类中，这就意味着 Java 中的任何类都包含有 `hashCode()` 函数。另外需要注意的是： Object 的 hashcode ⽅法是本地⽅法，也就是⽤ c 语⾔或 c++ 实现的，该⽅法通常⽤来将对象的 内存地址 转换为整数之后返回。

2) **为什么要有hashCode？**

   我们以`HashSet` 如何检查重复为例⼦来说明为什么要有 hashCode？

   当你把对象加⼊ HashSet 时， HashSet 会先计算对象的 hashcode 值来判断对象加⼊的位置，同时也会与其他已经加⼊的对象的 hashcode 值作⽐较，如果没有相符的 hashcode， HashSet 会假设对象没有重复出现。但是如果发现有相同 hashcode 值的对象，这时会调⽤ equals() ⽅法来检查 hashcode 相等的对象是否真的相同。如果两者相同， HashSet 就不会让其加⼊操作成功。如果不同的话，就会重新散列到其他位置。这样我们就⼤⼤减少了 equals 的次数，相应就⼤⼤提⾼了执⾏速度。

3) **为什么重写 equals 时必须重写 hashCode ⽅法？**

   如果两个对象相等，则 hashcode ⼀定也是相同的。两个对象相等，对两个对象分别调⽤ equals ⽅法都返回 true。但是，两个对象有相同的 hashcode 值，它们也不⼀定是相等的 。因此，equals ⽅法被覆盖过，则 hashCode ⽅法也必须被覆盖。**重写 hashcode() 方法的原因，简单的说就是：为了保证是同一个对象，在 equals 比较相同的情况下 hashcode值必定相同。**

   > hashCode() 的默认⾏为是对堆上的对象产⽣独特值。如果没有重写 hashCode() ，则该 class 的两个对象⽆论如何都不会相等（即使这两个对象指向相同的数据）。

## **为什么Java中只有值传递？**

**按值调⽤(call by value)**表示⽅法接收的是调⽤者提供的值，⽽**按引⽤调⽤（call by reference)**表示⽅法接收的是调⽤者提供的变量地址。⼀个⽅法可以修改传递引⽤所对应的变量值，⽽不能修改传递值调⽤所对应的变量值。 它⽤来描述各种程序设计语⾔（不只是 Java)中⽅法参数传递⽅式。

Java 程序设计语⾔总是采⽤按值调⽤。也就是说，⽅法得到的是所有参数值的⼀个拷⻉，也就是说，⽅法不能修改传递给它的任何参数变量的内容。

```java
public class Demo {
    public static void main(String[] args) {
        int a = 1;
        printValue(a);
        System.out.println("a:" + a);
    }

    public static void printValue(int b){
        b = 2;
        System.out.println("b:" + b);
    }
}
```

输出结果：b : 2   a : 1。通过上⾯例⼦，我们已经知道**⼀个⽅法不能修改⼀个基本数据类型的参数，⽽对象引⽤作为参**
**数就不⼀样。**

```java
public static void main(String[] args) {
    int[] arr = { 1, 2, 3, 4, 5 };
    System.out.println(arr[0]);
    change(arr);
    System.out.println(arr[0]);
  }
public static void change(int[] array) {
    // 将数组的第⼀个元素变为0
    array[0] = 0;
  }

```

输出结果为：1    0。array 被初始化 arr 的拷⻉也就是⼀个对象的引⽤，也就是说 array 和 arr 指向的是同⼀个数组对象。 因此，外部对引⽤对象的改变会反映到所对应的对象上。通过 example2 我们已经看到，实现⼀个改变对象参数状态的⽅法并不是⼀件难事。理由很简单，⽅法得到的是对象引⽤的拷⻉，对象引⽤及其他的拷⻉同时引⽤同⼀个对象。

下⾯再总结⼀下 Java 中⽅法参数的使⽤情况：

- **⼀个⽅法不能修改⼀个基本数据类型的参数（即数值型或布尔型）。**
- **一个方法可以改变一个对象参数的状态。**
- **一个方法不能让对象参数引用一个新的对象。（方法中传入两个对象引用的拷贝，交换这两个拷贝不会改变原引用）**

## **关键字**

**static**

**static作用：**方便在没有创建对象时，调用方法和变量、优化程序性能。

**static变量：**用 static 修饰的变量被称为**静态变量**，也被称为类变量，可以直接通过类名来访问它。 静态变量被所有的对象共享，在内存中只有一个副本，**仅当在类初次加载时会被初始化**，而非静态变量在创建对象的时候被初始化，并且存在多个副本，各个对象拥有的副本互不影响。

**static方法：**static 方法不依赖于任何对象就可以进行访问，**在 static 方法中不能访问类的非静态成员变量和非静态成员方法**，因为非静态成员方法/变量都是必须依赖具体的对象才能够被调用，但是在非静态成员方法中是可以访问静态成员方法/变量的。

**static代码块：**静态代码块的主要用途是可以用来**优化程序的性能**，因为它只会在类加载时加载一次，很多时候会将一些**只需要进行一次的初始化操作都放在 static 代码 块中进行**。 如果程序中有多个 static 块，在类初次被加载的时候，**会按照 static 块的顺序来执行每个 static 块。**

**初始化顺序：**静态变量和静态语句块**优先于**实例变量和普通语句块，静态变量和静态语句块的初始化顺序**取决于它们在代码中的顺序**。 如果存在继承关系的话，初始化顺序为：

1. **父类**中的**静态**变量和**静态**代码块
2. **子类**中的**静态**变量和**静态**代码块
3. **父类**中的**实例**变量和**普通**代码块
4. 父类的构造函数
5. **子类**中的**实例**变量和**普通**代码块
6. 子类的构造函数

**总结：静态优于普通，父类优于子类**

**final**

final 关键字主要⽤在三个地⽅：变量、⽅法、类。

1. 对于⼀个 final 变量，如果是基本数据类型的变量，则其数值⼀旦在初始化之后便**不能更改**；如果是引⽤类型的变量，则在对其初始化之后便**不能再让其指向另⼀个对象**。
2. 当⽤ final 修饰⼀个类时，表明这个类**不能被继承**。final 类中的所有成员⽅法都会被隐式地指定为 final ⽅法。
3. 使⽤ final ⽅法的原因有两个。第⼀个原因是把**⽅法锁定**，以防任何继承类修改它的含义；第⼆个原因是效率。在早期的 Java 实现版本中，会将 final ⽅法转为内嵌调⽤。但是如果⽅法过于庞⼤，可能看不到内嵌调⽤带来的任何性能提升（现在的 Java 版本已经不需要使⽤ final ⽅法进⾏这些优化了）。类中所有的 private ⽅法都隐式地指定为 final。

## **Java中的异常处理**

![image-20230702173318421](E:\八股图\Java基础\异常.png)

在 Java 中，所有的异常都有一个共同的祖先 `java.lang` 包中的 `Throwable` 类。`Throwable` 类有两个重要的子类：`Exception`（异常）和 `Error`（错误）。 `Exception` 能被程序本身处理( `try-catch` )， `Error` 是⽆法处理的(只能尽量避免)。

`Exception` 和 `Error` ⼆者都是 Java 异常处理的重要⼦类，各⾃都包含⼤量⼦类。

- **`Exception`** ：程序本身可以处理的异常，可以通过 `catch` 来进⾏捕获。 `Exception` ⼜可以分为受检查异常`Check Exceptions`(必须处理) 和 不受检查异常`Uncheck Exceptions`(可以不处理)。
- **`Error`** ： `Error` 属于程序⽆法处理的错误 ，我们没办法通过 catch 来进⾏捕获 。例如，Java 虚拟机运⾏错误（`Virtual MachineError`）、虚拟机内存不够错误(`OutOfMemoryError`)、类定义错误（`NoClassDefFoundError`）等。这些异常发⽣时，Java 虚拟机（JVM）⼀般会选择线程终⽌。

**受检查异常**

Java 代码在编译过程中，如果受检查异常没有被 `catch` / `throw` 处理的话，就没办法通过编译。除`RuntimeException` 及其⼦类以外，其他的 `Exception` 类及其⼦类都属于检查异常 。常⻅的受检查异常有： IO 相关的异常、`ClassNotFoundException` 、 `SQLException` ...。

**不受检查异常**

Java 代码在编译过程中 ，我们即使不处理不受检查异常也可以正常通过编译。`RuntimeException` 及其⼦类都统称为⾮受检查异常，例如： `NullPointExecrption` 、 `NumberFormatException` （字符串转换为数字）、 `ArrayIndexOutOfBoundsException`（数组越界）、 `ClassCastException` （类型转换错误）、 `ArithmeticException` （算术错误）等。

## **序列化和反序列化**

### **什么是序列化？什么是反序列化？**

如果我们需要持久化 Java 对象比如将 Java 对象保存在文件中，或者在网络传输 Java 对象，这些场景都需要用到序列化。

- **序列化**：将数据结构或对象转换成二进制字节流的过程
- **反序列化**：将在序列化过程中所生成的二进制字节流转换成数据结构或者对象的过程

常用场景：

- 对象在进行网络传输（比如远程方法调用 RPC 的时候）之前需要先被序列化，接收到序列化的对象之后需要再进行反序列化；
- 将对象存储到文件之前需要进行序列化，将对象从文件中读取出来需要进行反序列化；
- 将对象存储到数据库（如 Redis）之前需要用到序列化，将对象从缓存数据库中读取出来需要反序列化；
- 将对象存储到内存之前需要进行序列化，从内存中读取出来之后需要进行反序列化。

综上：**序列化的主要目的是通过网络传输对象或者说是将对象存储到文件系统、数据库、内存中。**

###  如果有些字段不想进行序列化怎么办？

对于不想进行序列化的变量，使用 `transient` 关键字修饰。

`transient` 关键字的作用是：阻止实例中那些用此关键字修饰的的变量序列化；当对象被反序列化时，被 `transient` 修饰的变量值不会被持久化和恢复。

关于 `transient` 有几点需注意：

- `transient` 只能修饰变量，不能修饰类和方法。
- `transient` 修饰的变量，在反序列化后变量值将会被置成类型的默认值。例如，如果是修饰 `int` 类型，那么反序列后结果就是 `0`。
- `static` 变量因为不属于任何对象(Object)，所以无论有没有 `transient` 关键字修饰，均不会被序列化。

## **IO流**

### **IO流分类**

- 按照流的流向分，可以分为**输⼊流**和**输出流**；
- 按照操作单元划分，可以划分为**字节流**和**字符流**；
- 按照流的⻆⾊划分为**节点流**和**处理流**。

Java IO 流共涉及 40 多个类，这些类看上去很杂乱，但实际上很有规则，⽽且彼此之间存在⾮常
紧密的联系， Java I0 流的 40 多个类都是从如下 4 个抽象类基类中派⽣出来的。

- **InputStream/Reader：** 所有的输⼊流的基类，前者是字节输⼊流，后者是字符输⼊流。
- **OutputStream/Writer：** 所有输出流的基类，前者是字节输出流，后者是字符输出流。

### **既然有了字节流，为什么还要有字符流？**

字符流是由 Java 虚拟机将字节转换得到的，问题就出在这个过程还算是⾮常耗时，并且，如果我们不知道编码类型就很容易出现乱码问题。所以， I/O 流就⼲脆提供了⼀个直接操作字符的接⼝，⽅便我们平时对字符进⾏流操作。

### **BIO，NIO，AIO 有什么区别？**

- **BIO (Blocking I/O)：**同步阻塞 I/O 模式，数据的**读取写⼊必须阻塞在⼀个线程内等待其完成**。在活动连接数不是特别⾼（⼩于单机 1000）的情况下，这种模型是⽐较不错的。线程池本身就是⼀个天然的漏⽃，可以缓冲⼀些系统处理不了的连接或请求。但是，当⾯对⼗万甚⾄百万级连接的时候，传统的 BIO 模型是⽆能为⼒的。因此，我们需要⼀种更⾼效的 I/O 处理模型来应对更⾼的并发量。
- **NIO (Non-blocking/New I/O)：** NIO 是⼀种同步⾮阻塞的 I/O 模型，在 Java 1.4 中引⼊了 NIO 框架，对应`java.nio` 包，**提供了 `Channel` , `Selector`，`Buffer` 等抽象**。它⽀持⾯向缓冲的，基于通道的 I/O 操作⽅法。 NIO 提供了与传统 BIO 模型中的 `Socket` 和 `ServerSocket` 相对应的 `SocketChannel` 和 `ServerSocketChannel` 两种不同的套接字通道实现，**两种通道都⽀持阻塞和⾮阻塞两种模式**。阻塞模式使⽤就像传统中的⽀持⼀样，⽐较简单，但是性能和可靠性都不好；⾮阻塞模式正好与之相反。在**同步非阻塞 IO** 模型中，应用程序会**一直发起 read()调用**，等待数据从内核空间拷贝到用户空间的这段时间里，线程依然是阻塞的，直到在内核把数据拷贝到用户空间。 相比于**同步阻塞 IO 模型**，同步非阻塞 IO 模型确实有了很大改进。通过轮询操作，避免了一直阻塞。但是，这种 IO 模型同样存在问题：应用程序不断进行 I/O 系统调用轮询数据是否已经准备好的过程是**十分消耗 CPU 资源的**。**对于低负载、低并发的应⽤程序，可以使⽤同步阻塞 I/O 来提升开发速率和更好的维护性；对于⾼负载、⾼并发的（⽹络）应⽤，应使⽤ NIO 的⾮阻塞模式来开发。**
- **AIO (Asynchronous I/O)：** AIO 也就是 NIO 2。在 Java 7 中引⼊了 NIO 的改进版 NIO 2，它是异步⾮阻塞的 IO 模型。**异步 IO 是基于事件和回调机制实现**的，也就是应⽤操作之后会直接返回，不会堵塞在那⾥，当后台处理完成，操作系统会通知相应的线程进⾏后续的操作。AIO 是异步 IO 的缩写，虽然 NIO 在⽹络操作中，提供了⾮阻塞的⽅法，但是 NIO 的 IO ⾏为还是同步的。对于 NIO 来说，我们的业务线程是在 IO 操作准备好时，得到通知，接着就由这个线程⾃⾏进⾏ IO 操作，IO 操作本身是同步的。

区别：

举个生活中简单的例子，你妈妈让你烧水， **同步阻塞BIO**： 小时候你比较笨啊，在那里傻等着水开（**傻傻等待数据的到达**） **优点：实现简单； 缺点：线程阻塞，并发能力差** **同步非阻塞NIO： **等你稍微大一点，你知道烧水的空隙可以去玩，只需时不时来看看水开了没有（**轮询**） **优点：线程不需要阻塞； 缺点：每个线程都需要多次轮询** **异步非阻塞AIO** ： 后来你家用上水开会发声的壶，你只需听到响声就知水开了，期间可以随便玩（**通知**） **优点：非阻塞，不需要轮询**

## **深拷贝和浅拷贝**

- **浅拷贝**：浅拷贝会在堆上**创建一个新的对象**（区别于引用拷贝的一点），不过，如果原对象内部的属性是引用类型的话，浅拷贝会直接复制内部对象的引用地址，也就是说**拷贝对象和原对象共用同一个内部对象**。（对基本数据类型进行值传递，对引用数据类型，复制一个引用指向原始引用的对象，就是让复制的引用和原始引用指向同一个对象。）
- **深拷贝：**深拷贝会**完全复制**整个对象，包括这个对象所包含的内部对象。（ 对基本数据类型进行值传递，对引用数据类型，**创建一个新的对象**， 并**复制**其内容，两个引用指向两个对象，但对象内容相同。）

**浅拷贝**

浅拷贝的示例代码如下，这里实现了 `Cloneable` 接口，并重写了 `clone()` 方法。`clone()` 方法的实现很简单，直接调用的是父类 `Object` 的 `clone()` 方法。

```java
public class Address implements Cloneable{
    private String name;
    // 省略构造函数、Getter&Setter方法
    @Override
    public Address clone() {
        try {
            return (Address) super.clone();
        } catch (CloneNotSupportedException e) {
            throw new AssertionError();
        }
    }
}

public class Person implements Cloneable {
    private Address address;	//address为引用类型
    // 省略构造函数、Getter&Setter方法
    @Override
    public Person clone() {
        try {
            Person person = (Person) super.clone();
            return person;
        } catch (CloneNotSupportedException e) {
            throw new AssertionError();
        }
    }
}
```

测试结果：

```java
Person person1 = new Person(new Address("武汉"));
Person person1Copy = person1.clone();
// true
System.out.println(person1.getAddress() == person1Copy.getAddress());
```

从输出结构就可以看出， `person1` 的克隆对象和 `person1` 使用的仍然是同一个 `Address` 对象。

**深拷贝**

这里我们简单对 `Person` 类的 `clone()` 方法进行修改，连带着要把 `Person` 对象内部的 `Address` 对象一起复制。

```java
@Override
public Person clone() {
    try {
        Person person = (Person) super.clone();
        //address为引用类型，重新赋值
        person.setAddress(person.getAddress().clone());
        return person;
    } catch (CloneNotSupportedException e) {
        throw new AssertionError();
    }
}
```

输出结果为：

```java
Person person1 = new Person(new Address("武汉"));
Person person1Copy = person1.clone();
// false
System.out.println(person1.getAddress() == person1Copy.getAddress());
```

从输出结构就可以看出，显然 `person1` 的克隆对象和 `person1` 包含的 `Address` 对象已经是不同的了。

![image-20230703103931651](E:\八股图\Java基础\拷贝.png)

## **Object类的常见方法**

Object 类是一个特殊的类，是所有类的父类。它主要提供了以下 11 个方法：

```java
//native 方法，用于返回当前运行时对象的 Class 对象，使用了 final 关键字修饰，故不允许子类重写。
 public final native Class<?> getClass()

//native 方法，用于返回对象的哈希码，主要使用在哈希表中，比如 JDK 中的HashMap。
public native int hashCode()

//用于比较 2 个对象的内存地址是否相等，String 类对该方法进行了重写以用于比较字符串的值是否相等。
public boolean equals(Object obj)

//native 方法，用于创建并返回当前对象的一份拷贝。
protected native Object clone() throws CloneNotSupportedException

//返回类的名字实例的哈希码的 16 进制的字符串。建议 Object 所有的子类都重写这个方法。
public String toString()

//native 方法，并且不能重写。唤醒一个在此对象监视器上等待的线程(监视器相当于就是锁的概念)。如果有多个线程在等待只会任意唤醒一个。
public final native void notify()

//native 方法，并且不能重写。跟notify一样，唯一的区别就是会唤醒在此对象监视器上等待的所有线程，而不是一个线程。
public final native void notifyAll()

//native方法，并且不能重写。暂停线程的执行。注意：sleep 方法没有释放锁，而 wait 方法释放了锁 ，timeout 是等待时间。
public final native void wait(long timeout) throws InterruptedException

//多了 nanos 参数，这个参数表示额外时间（以毫微秒为单位，范围是 0-999999）。 所以超时的时间还需要加上 nanos 毫秒。。
public final void wait(long timeout, int nanos) throws InterruptedException

//跟之前的2个wait方法一样，只不过该方法一直等待，没有超时时间这个概念
public final void wait() throws InterruptedException

//实例被垃圾回收器回收的时候触发的操作
protected void finalize() throws Throwable { }
```

## **泛型**

### **什么是泛型？有什么作用？**

**Java 泛型（Generics）** 是 JDK 5 中引入的一个新特性。使用泛型参数，可以增强代码的可读性以及稳定性。编译器可以对泛型参数进行检测，并且通过泛型参数可以指定传入的对象类型。比如 `ArrayList<Person> persons = new ArrayList<Person>()` 这行代码就指明了该 `ArrayList` 对象只能传入 `Person` 对象，如果传入其他类型的对象就会报错。

### 泛型的使用方式有哪几种？

泛型一般有三种使用方式：**泛型类**、**泛型接口**、**泛型方法**。

1. **泛型类**

   ```java
   //此处T可以随便写为任意标识，常见的如T、E、K、V等形式的参数常用于表示泛型
   //在实例化泛型类时，必须指定T的具体类型
   public class Generic<T>{
       private T key;
       public Generic(T key) {
           this.key = key;
       }
       public T getKey(){
           return key;
       }
   }
   //实例化泛型类
   Generic<Integer> genericInteger = new Generic<Integer>(123456);
   ```

2. **泛型接口**

   ```java
   public interface Generator<T> {
       public T method();
   }
   
   //实现泛型接口，指定类型（也可以不指定）：
   class GeneratorImpl<T> implements Generator<String>{
       @Override
       public String method() {
           return "hello";
       }
   }
   ```

3. **泛型方法**

   ```java
   public static < E > void printArray( E[] inputArray )
   {
         for ( E element : inputArray ){
           System.out.printf( "%s ", element );
        }
        System.out.println();
   }
   
   //使用
   // 创建不同类型数组：Integer, Double 和 Character
   Integer[] intArray = { 1, 2, 3 };
   String[] stringArray = { "Hello", "World" };
   printArray(intArray);
   printArray(stringArray);
   ```

> 注意: `public static < E > void printArray( E[] inputArray )` 一般被称为静态泛型方法；**在 java 中泛型只是一个占位符**，必须在传递类型后才能使用。类在实例化时才能真正的传递类型参数，由于**静态方法的加载先于类的实例化**，也就是说类中的泛型还没有传递真正的类型参数，静态的方法的加载就已经完成了，所以**静态泛型方法是没有办法使用类上声明的泛型的。只能使用自己声明的** `<E>`

## **反射**

### **反射机制是什么**

1. Java反射机制的核心是在程序**运行时动态加载类并获取类的详细信息**，从而操作类或对象的属性和方法。本质是JVM得到class对象之后，**再通过class对象进行反编译，从而获取对象的各种信息**
2. Java属于先编译再运行的语言，程序中对象的类型在编译期就确定下来了，而当程序在运行时可能需要动态加载某些类，这些类因为之前用不到，所以没有被加载到JVM。通过反射，可以在运行时动态地创建对象并调用其属性，**不需要提前在编译期知道运行的对象是谁。**

### **获取Class对象的四种方式**

1. 知道具体类的情况下使用：

   ```java
   Class alunbarClass = TargetObject.class;
   ```

   但是我们一般是不知道具体类的，基本都是通过遍历包下面的类来获取 Class 对象，通过此方式获取 Class 对象不会进行初始化

2. **通过 `Class.forName()`传入类的全路径获取**：

   ```java
   Class alunbarClass1 = Class.forName("cn.javaguide.TargetObject");
   ```

3. **通过对象实例`instance.getClass()`获取：**

   ```java
   TargetObject o = new TargetObject();
   Class alunbarClass2 = o.getClass();
   ```

4. **通过类加载器`xxxClassLoader.loadClass()`传入类路径获取：**

   ```java
   ClassLoader.getSystemClassLoader().loadClass("cn.javaguide.TargetObject");
   ```

   通过类加载器获取 Class 对象不会进行初始化，意味着不进行包括初始化等一系列步骤，静态代码块和静态对象不会得到执行

### **使用反射创建对象的两种方式**

1. **通过Class的`newInstance()`方法**

   - 该方法要求该Class对象的对应类有无参构造方法
   - 执行`newInstance()`实际上就是执行无参构造方法来创建该类的实例

   ```java
   String className = "com.bjsxt.why.Dog";
   //2.根据完整路径字符串获取Class对象信息
   Class clazz = Class.forName(className);
   //3.直接使用Class的方法创建对象
   Object obj = clazz.newInstance();
   ```

2. **通过Constructor的`newInstance()`方法**

   - 先使用Class对象获取指定的Constructor对象
   - 再调用Constructor对象的`newInstance()`创建Class对象对应类的对象
   - **通过 Constructor 对象创建类对象可以选择特定构造方法，而通过 Class 对象则只能使用默认的无参数构造方法**

   ```java
   //2.根据完整路径字符串获取Class对象信息
   Class clazz = Class.forName(className);
   //3.获取无参数构造方法
   Constructor con = clazz.getConstructor();
   //4.使用无参数构造方法来创建对象
   Object obj = con.newInstance("构造方法参数");
   ```

**Class类的常用方法**

**`getFields()`——** 获得类的public类型的属性。    **`getDeclaredFields()`——** 获得类的所有属性    **`getField(String name)`——** 获得类的指定属性    **`getMethods()`——** 获得类的public类型的方法    **`getMethod (String name,Class [] args)`——** 获得类的指定方法    **`getConstrutors()`——** 获得类的public类型的构造方法    **`getConstrutor(Class[] args)`——** 获得类的特定构造方法    **`newInstance()`——** 通过类的无参构造方法创建对象

### **反射机制的优缺点**

**优点**：可以让咱们的代码更加灵活、为各种框架提供开箱即用的功能提供了便利

**缺点**：让我们在运行时有了分析操作类的能力，这同样也增加了安全问题。比如可以无视泛型参数的安全检查（泛型参数的安全检查发生在编译时）。另外，反射的性能也要稍差点，不过，对于框架来说实际是影响不大的。

### **为什么反射的性能会差？**

1. 反射需要**动态解析类的信息**，包括访问修饰符、字段、方法、参数、注解等，因此**需要进行大量的运行时检查和解析**，会比直接调用代码的执行速度慢。
2. 反射机制在执行时会**涉及到许多动态分配对象的操作**，这些操作会**占用大量的内存**，并且**需要进行垃圾回收**，导致额外的性能损耗。
3. 反射方法**的调用通常比直接调用方法慢很多**，因为它需要进行许多额外的操作，如方法解析、参数类型检查、安全检查等。
4. 反射方法的调用通常**不能进行编译时优化**，因此会导致运行时性能低下

## **内部类**

内部类包含：**成员内部类**、**局部内部类**、**匿名内部类**和**静态内部类**

### **局部内部类**

局部内部类是定义在外部类的局部位置，比如**方法中**，并且有类名。

**局部内部类的使用**

1. 局部内部类可以直接访问**外部类的所有成员，包含私有的**，访问方式——直接访问。
2. 不能添加**访问修饰符**，因为它的地位就是一个局部变量，局部变量是不能使用修饰符的。但是可以使用**final修饰**，因为局部变量也可以使用final。
3. 作用域仅仅在定义它的方法或代码块中
4. **外部类**访问局部内部类，访问方式：**创建对象，再访问**(注意：必须在作用域内)
5. **外部其他类**不能直接访问局部内部类(因为局部内部类是一个局部变量) 
6. 如果外部类和局部内部类的成员重名时，默认遵循就近访问原则，如果想要打破原则访问外部类成员，则可以使用(外部类名.this.成员)去访问。

```java
public class TestDemo {
    public static void main(String[] args) {
        Person person = new Person();
        person.method2();
    }
}
class Person{//外部类
    private String name = "张三";
    private int age = 20;
    private void method1(){
        System.out.println("外部类中的method1方法");
    }
 
    public void method2(){
        final class Student{//局部内部类可以加fianl关键字
            private String name = "王五";
            public void method3(){
                method1();//可以访问外部类中的成员
            }
        }

        //外部类访问局部内部类的方式：创建对象再访问
        Student student = new Student();
        student.method3();
    }
}
```

### **成员内部类**

定义：成员内部类是定义在外部类的成员位置上，并且没有static修饰

**成员内部类的使用**

1. 可以直接访问外部类的所有成员，包括私有的。外部类访问成员内部类访问方式：创建对象，再访问；
2. 可以添加任意访问修饰符，因为它的地位就是一个成员；
3. 作用域和外部类的其他成员一样，为整个类体；
4. 如果外部类和内部类的成员重名时，内部类访问的话，遵循就近原则，如果想访问外部类的成员，则可以使用(外部类名.this.成员)去访问。
5. 外部其他类访问成员内部类有三种方式：第一种实例化外部类，然后访问；第二种将内部类作为外部类的成员实例化然后访问；第三种在外部类里面编写一个方法，可以返回内部类对象。

```java
public class TestDemo02 {
    public static void main(String[] args) {
        People people = new People();
        people.method();//访问的第一种方式实例化外部类，通过外部类里面的方法访问
        //People.Student student = people.new Student();//访问的第二种方式，将内部类作为外部类的成员实例化然后访问
        /**
         * 访问的第三种方式
         * People.Student getStudent = people.getStudent();
         * getStudent.say();
         */
    }
}
class People{//外部类
    private String name = "张三";
    private int age = 20;
 
    private void hi(){
        System.out.println("打招呼");
    }
 
    public class Student{//内部类
        private String name = "李四";
        private int age = 21;
        public void say(){
            System.out.println("name="+name+" age="+People.this.age);
        }
    }
 
    //返回Student类
    public Student getStudent(){
        return new Student();
    }
 
    public void method(){//外部类访问内部类
        Student student = new Student();
        student.say();
    }
}
```



### **匿名内部类**

定义：没有名字的内部类，在日常开发中使用较多。 **注意：使用匿名内部类的前提条件是必须继承一个父类或者实现一个接口。**一般来说，匿名内部类用于继承其他类或是实现接口，并不需要增加额外的方法，**只是对继承方法的实现或是重写**。

```java
interface Person{
    public void fun();
}

public class Demo {
    public static void main(String[] args) {
        new Person(){	//匿名内部类
            @Override
            public void fun(){
                System.out.println("hello");
            }
        }.fun();
    }
}
```

### **静态内部类**

定义：静态内部类是定义在外部类的成员位置上，并且有static修饰。

**静态内部类的使用**

1. 可以直接访问外部内的所有静态成员，包含私有的，**但不能直接访问非静态的成员** ；
2. 可以添加任意访问修饰符，因为它的地位就是一个成员；
3. 作用域和外部类的其他成员一样，为整个类体；
4. 如果外部类和内部类的成员重名时，内部类访问的话，遵循就近原则，如果想访问外部类的成员，则可以使用(外部类名.this.成员)去访问。

## **Java常量池**

JVM常量池主要分为**Class文件常量池、运行时常量池，全局字符串常量池，以及基本类型包装类对象常量池**。