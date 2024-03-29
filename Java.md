# Java

![img](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8xMTc5Mzg5LTc1MTcyZGZmNDZiZWNmYWMucG5n)

## Basic Lang

### 类对象的创建过程

> 参考地址：[JVM类生命周期概述：加载时机与加载过程](https://blog.csdn.net/justloveyou_/article/details/72466105)
>
> 加载->验证->准备->解析->初始化->使用->卸载

类对象的变量的初始化是在准备和初始化阶段。准备阶段即为分配地址空间并对属性设置默认值。初始化即执行收集了所有的静态变量和类变量按照源码顺序合并的类构造器\<clinit>

### 对象的创建过程

> 父类的类构造器\<clinit>() -> 子类的类构造器\<clinit>() -> 父类的成员变量和实例代码块 -> 父类的构造函数 -> 子类的成员变量和实例代码块 -> 子类的构造函数。

Java对象创建过程中，先是地址分配，实例对象的变量初始化，实例代码块的初始化，以及构造函数的初始化。其中实例对象的变量初始化和实例代码块的初始化是会被编译器放在构造函数代码中，并且先为执行。实例的变量和代码块的执行顺序是依照于编程顺序

Java对象在实例化完成前，必须完成其超类对象的实例化，且为构造函数的第一行。可靠编译器自动生成

实例对象的属性可最多被初始化四次

类的初始化过程与类的实例化过程的异同？类的初始化是指类加载过程中的初始化阶段对类变量按照程序猿的意图进行赋值的过程；而类的实例化是指在类完全加载到内存中后创建对象的过程。

### 内部类

> 参考地址：https://www.cnblogs.com/GrimMjx/p/10105626.html#_label2_1

​	非静态内部类：其实例不可单独存在，不可含有静态方法。通过外部类的所持有其构造方法进行创建。<br>该方法是否有该名字的成员变量 - 直接用该变量名，<br>内部类中是否有该名字的成员变量 - 使用this.变量名。<br>外部类中是否有该名字的成员变量 - 使用外部类的类名.this.变量名<br>	静态内部类不会持有外部类的对象，只是借壳，变量访问规则参考静态变量。

### Switch

Switch基本用法。略。可接受对象会有很多，

switch 对于不同case，会有break用法。没有break会一直匹配下去。

不要忘记default:

### 代理

1. 静态代理实现较简单，只要代理对象对目标对象进行包装，即可实现增强功能，但静态代理只能为一个目标对象服务，如果目标对象过多，则会产生很多代理类。
2. JDK动态代理需要目标对象实现业务接口，代理类只需实现InvocationHandler接口。
3. 动态代理生成的类为 lass com.sun.proxy.\$Proxy4，cglib代理生成的类为class com.cglib.UserDao\$\$EnhancerByCGLIB\$\$552188b6。
4. 静态代理在编译时产生class字节码文件，可以直接使用，效率高。
5. 动态代理必须实现InvocationHandler接口，通过反射代理方法，比较消耗系统性能，但可以减少代理类的数量，使用更灵活。
6. cglib代理无需实现接口，通过生成类字节码实现代理，比反射稍快，不存在性能问题，但cglib会继承目标对象，需要重写方法，所以目标对象不能为final类。

### 泛型

​	泛型是用来适合多种数据类型来执行相同的代码。在开发过程中对于某类或者很多类型来说，操作是相同的，故设计了泛型通过类型擦除来使用相同的代码。实现了代码量的降低。

​	对于泛型匹配符？来说，其是不可get，也不可set。对于存在上下限的，可选一。如果皆需要，则必须要显式指定类型。

​	使用上来说，可在类上显式指定，接口，方法。然后即可往下作用。

### 注解

​	注解有点意思，自JDK1.5版本之后引入，对代码进行说明。主要作用为生成文档，编译器检查，编译器动态处理，运行期动态处理四大功能

​	通过Java自身标准注解，元注解（@Retention，@Target，@Inherited，@Document及自定义注解实现

### 异常

​	Java中的异常由顶级设计Throwable，下分Error和Exception。Exception下分RuntimeException和非运行时异常。另外异常又可分为受检查异常和不受检查异常。

| Type                | Example                                                      |
| ------------------- | ------------------------------------------------------------ |
| Error               | IOError/ThreadDeath/OOM                                      |
| RuntimeException    | IndexOutOfBoundsException/NullPointException/ClassCastException |
| 非运行时异常        | ClassNotFoundException                                       |
|                     |                                                              |
| Unchecked Exception | RuntimeException和Error                                      |
| Checked Exception   | Exception下的非运行时异常                                    |

### 反射

在运行时能动态的获取到类的属性和方法，并且能调用它的任一方法和属性。这种动态获取信息和动态调用对象的功能的方式称之为反射。

在使用这里，主要是类的获取，Constructor，field，Method。

| Type        | Useage                                                       | Description                                               |
| ----------- | ------------------------------------------------------------ | --------------------------------------------------------- |
| TypeGet     | 1. Class.forName("ClassName")  class.getName<br />2. ClassName.class  class.getSimpleName<br />3. new ClassNme().getClass()  class.newInstance() | 1. 通过全限定类名<br />2. 通过类名<br />3. 通过实例类对象 |
| Constructor |                                                              |                                                           |
| Field       |                                                              |                                                           |
| Method      |                                                              |                                                           |

### SPI

> spi即service provider interface

通过自定义规范（接口），主程序只需要按照规范进行API调用，Java支持按照依赖文件中的META-INF/services进行加载实现类。然后实现类完成API功能。

META-INF/services目录下文件的写法：文件名需为接口的全限定名称，文件内容行需为实现类的全限定名称。在程序开发中通过使用ServiceLoader.load(Interface.class)，API完成服务加载。

### Collection

> 回答某某类型时，回答套路：基于XX实现，支持XX，不支持XX，时间复杂度为XX。可用于什么场景

Collection：List，Queue，Set

- List：

  - ArrayList：动态数组实现，支持顺序查找和随机查找
  - LinkedList：双向链表实现，支持快速插入和删除，可用作栈和队列

  - Vector

- Queue

  - LinkedQueue：双向链表实现，可用作双向队列
  - PriorityQueue：堆结构实现，可用作优先队列

- Set

  - HashSet：红黑树实现，支持有序操作
  - TreeSet：Hash表实现，支持快速查找，不支持有序操作
  - LinkedHashSet：：Hash表实现，双向链表维护

Map：HashMap，HashTable（ConcurrentHashMap），LinkedHashMap，TreeMap

### Map

参考文章地址：https://www.nowcoder.com/discuss/820700

### Stream 

> 参考地址：https://blog.csdn.net/m0_56223907/article/details/125790208
>
> Stream的创建，筛选，映射，结果选择，归约与收集

创建
```java
collect.stream;
Arrays.stream;
Stream.of;
Stream.iterate/Stream.generate;
```

筛选

```java
stream.filter;
stream.distinct;
stream.skip;
stream.limit;
```

映射(参数都为函数)

```java
stream.map;
stream.flatMap;
```

结果筛选，收集与归约

```java
stream.allMatch/anyMatch;
stream.findFirst/findAny;
stream.count/max/min;

stream.reduce;
stream.collect;
```





***数据结构***

JDK1.7之前是数组加链表<br>JDK1.8之后是数组+链表+红黑树

***put/get的过程***

put<br>1. 判断数组是否为空，为空则创建数组。<br>2. 计算key值（key.hashCode()&(length-1)），定位到数组位置，<br>3. 判断该位置是否为null，为null，则设置该值，不为null，则通过hashcode和equals进行比较，相同更新，不同则判断该点是否为红黑树节点，是则直接插入，不是则链表插入，<br>4. 链表插入完成之后，当前链表长度大于8且数组长度大于64则转为红黑树。链表长度大于8且数组长度小于64则进行数组扩容。<br>5. 最后当插入操作完成后，进行数组整体容量和负载因子判断，是否需要进行扩容。

get：<br>1. 对于给定key的hashcode值定位数组位置，如果为null，返回null<br>2. 不为null，判断是否为红黑树节点，是则按照红黑树查找，不是则按照链表查找

***HashMap的扩容机制***

1. 初始16，容量是2的n次方，负载因子默认为0.75。解释以上三者原因<br>时间和空间上需要权衡，太小会频繁扩容，太大浪费空件，而且16是2的幂次方<br>计算位置时是通过hashcode&(n-1)，n为2的幂次方可以确保n-1值的全为1，避免不必要的hash冲突的发生<br>当为1的时候，不会扩容。为0.5的时候，虽然可能减少hash冲突，但是会频繁扩容，而且空间利用率低

2. HashMap扩容过程

   > 伯努利试验（同样的条件下重复地、相互独立地进行的一种随机试验），试验次数是否很大，p是否很小即可
   >
   > 二项分布趋于泊松分布，用泊松分布的概率值作二项分布概率值的近似

3. HashMap为什么线程不安全

   > 更新丢失会有俩种，撤销回滚更新丢失，覆盖更新丢失

   1. 1.7中采用头插法会造成死锁和数据丢失
   2. 1.8采用尾插法，避免死锁，数据更新丢失在多线程仍无法避免

4. HashMap如何解决Hash冲突

   拉链法（链地址法），采用单向链表，链表长度大于等于8可能转为红黑树，链表长度所见缩减小于6，会转为链表

5. HashMap为什么使用[红黑树](https://www.nowcoder.com/jump/super-jump/word?word=红黑树)而不是B树或[平衡二叉树](https://www.nowcoder.com/jump/super-jump/word?word=平衡二叉树)AVL或二叉查找树

   1.不使用二叉查找树

   二叉[排序树在极端情况下会出现线性结构。例如：二叉排序树左子树所有节点的值均小于根节点，如果我们添加的元素都比根节点小，会导致左子树线性增长，这样就失去了用树型结构替换链表的初衷，导致查询时间增长。所以这是不用二叉查找树的原因。 

   2.不使用平衡二叉树 

   平衡二叉树是严格的平衡树，红黑树是不严格平衡的树，平衡二叉树在插入或删除后维持平衡的开销要大于红黑树。 

   红黑树的虽然查询性能略低于平衡二叉树但在插入和删除上性能要优于平衡二叉树。 

   选择红黑树是从功能、性能和开销上综合选择的结果。 

   3.不使用B树/B+树

   HashMap本来是数组+链表的形式，链表由于其查找慢的特点，所以需要被查找效率更高的树结构来替换。 

   如果用B/B+树的话，在数据量不是很多的情况下，数据都会“挤在”一个结点里面，这个时候遍历效率就退化成了链表。

   ```java
   /**
        * Implements Map.put and related methods.
        *
        * @param hash hash for key
        * @param key the key
        * @param value the value to put
        * @param onlyIfAbsent if true, don't change existing value
        * @param evict if false, the table is in creation mode.
        * @return previous value, or null if none
        */
       final V putVal(int hash, K key, V value, boolean onlyIfAbsent,boolean evict) {
           Node<K,V>[] tab; Node<K,V> p; int n, i;
         // 如果数组为空，创建数组
           if ((tab = table) == null || (n = tab.length) == 0)
               n = (tab = resize()).length;
         // 如果数组映射位置为空，直接等于替换
           if ((p = tab[i = (n - 1) & hash]) == null)
               tab[i] = newNode(hash, key, value, null);
           else {
               Node<K,V> e; K k;
             // 如果hash相同并且（key相同或者equal），直接替换
               if (p.hash == hash &&
                   ((k = p.key) == key || (key != null && key.equals(k))))
                   e = p;
               else if (p instanceof TreeNode)
                   e = ((TreeNode<K,V>)p).putTreeVal(this, tab, hash, key, value);
               else {
                   for (int binCount = 0; ; ++binCount) {
                       if ((e = p.next) == null) {
                           p.next = newNode(hash, key, value, null);
                           if (binCount >= TREEIFY_THRESHOLD - 1) // -1 for 1st
                               treeifyBin(tab, hash);
                           break;
                       }
                       if (e.hash == hash &&
                           ((k = e.key) == key || (key != null && key.equals(k))))
                           break;
                       p = e;
                   }
               }
               if (e != null) { // existing mapping for key
                   V oldValue = e.value;
                   if (!onlyIfAbsent || oldValue == null)
                       e.value = value;
                   afterNodeAccess(e);
                   return oldValue;
               }
           }
           ++modCount;
           if (++size > threshold)
               resize();
           afterNodeInsertion(evict);
           return null;
       }
   ```

**HashMap动态缩容**： 目前暂无自动缩容，可以手动remove掉。没有动态缩容的原因有：1. 首先节约空间有限还需要rehash重新计算。2. 大部分应用于局部变量，方法调用后一般很快都会被GC掉。另外可能Java设计习惯就是空间换时间。

**JDK1.7头插法出现死循环**：死循环的原因是 HashMap 在 JDK 1.7 使用的是头插法，头插法 + 链表 + 多线程并发 + HashMap 扩容，这几个点加在一起就形成了 HashMap 的死循环，解决死锁可以采用线程安全容器 ConcurrentHashMap 替代。

### 日期

### SimpleDateFormate 线程不安全

多个线程之间共享变量calendar，并修改calendar。因此在多线程环境下，当多个线程同时使用相同的SimpleDateFormat对象（如static修饰）的话，如调用format方法时，多个线程会同时调用calender.setTime方法，导致time被别的线程修改，因此线程是不安全的。此外，parse方法也是线程不安全的，parse方法实际调用的是CalenderBuilder的establish来进行解析，其方法中主要步骤不是原子操作。

解决方案：1、将SimpleDateFormat定义成局部变量。2、 加一把线程同步锁：synchronized(lock)。3、使用ThreadLocal，每个线程都拥有自己的SimpleDateFormat对象副本。4、使用DateTimeFormatter代替SimpleDateFormat。 5、使用JDK8全新的日期和时间API

JDK 8 中的日期LocalDateTime, LocalDate, LocalTime.

> [LocalDateTime, LocalDate, LocalTime 关系](https://cloud.tencent.com/developer/article/1598040)

Export:<br>	LocalDateTime -> LocalDate/LocalTime. toLocalTime/toLocalDate.<br>	LocalDate/LocalTime -> LocalDateTime. of/at.

Reset:<br>	plus/plusXXXX:增加<br>	minus/minusXXXX:减少<br>	with/withXXXX:直接设置 

格式化:<br>	DateTimeFormatter:<br>		固定枚举:DateTimeFormatter.ISO_LOCAL_DATE<br>		自定义格式类型:DateTimeFormatter.ofPattern();<br>	Format: LocalDateTime.format(DateTimeFormatter);<br>	Parse:LocalDateTime.parse("",DateTimeFormatter);

### 枚举

> 枚举也是类，所以可以有属性及方法，所以对应枚举类的属性和方法的初始化

```java 
package com.lushixiang.TestSimple;

public enum Operator {
    // 实现抽象方法
    ADD(1,3){
        @Override
        public int apply(int a, int b){
            return a+b;
        }
    };

    // 定义枚举属性
    public final int a ;
    public final int b;
    // 定义抽象方法
    public abstract int apply(int a, int b);
    // 定义初始化方法
    private Operator(int x1, int x2){
        a = x1;
        b = x2;
        System.out.println("Operator is init...");
    }
}
```

### BigDecimal

> 解决高精度计算准确的问题，double（7），float（16）

#### 使用注意点

> [参考博客](https://blog.csdn.net/jianghao233/article/details/125970370)

1. 创建BigDecimal时，不能使用BigDecimal(Double value)->小数字面量默认是double，中间一层自动转换，需要注意；
2. BigDecimal对象不变性，对象创建后加减乘除都是不变的
3. 保留小数位是注意精度及默认舍入模式为不舍入；

```txt
BigDecimal.ROUND_CEILING      //向正无穷方向舍入
BigDecimal.ROUND_DOWN         //向零方向舍入
BigDecimal.ROUND_FLOOR        //向负无穷方向舍入
BigDecimal.ROUND_HALF_DOWN    //向（距离）最近的一边舍入，除非两边（的距离）是相等,如果是这样，向下舍入,例如1.55 保留一位小数结果为1.5
BigDecimal.ROUND_HALF_EVEN    //向（距离）最近的一边舍入，除非两边（的距离）是相等,如果是这样，如果保留位数是奇数，使用BigDecimal.ROUND_HALF_UP，如果是偶数，使用ROUND_HALF_DOWN
BigDecimal.ROUND_HALF_UP      //向（距离）最近的一边舍入，除非两边（的距离）是相等,如果是这样，向上舍入, 1.55保留一位小数结果为1.6
BigDecimal.ROUND_UNNECESSARY  //计算结果是精确的，不需要舍入模式
BigDecimal.ROUND_UP           //向远离0的方向舍入
```

4. BigDecimal转String，默认toString可能会使用科学计数法。建议使用toPlainString；
5. BigDecimal等值比较，equal会比较精度和数值，compareTo则只比较数值；
6. BigDecimal计算时参数不可为null，除数不可以为0；
7. 使用divide的时候设置舍入模式
8. BigDecimal的执行顺序不能交换，要先乘后除，减小差异

## Feature

> what's the feature, what I think that is pretty fun, so that's 

### ThreadLocal

> 参考博客地址：https://blog.csdn.net/qq_35246620/article/details/106437183
>
> ThreadLocal，线程隔离通过副本保证本线程访问资源的安全性，即在多线程中为每一个线程单独创建变量副本，避免了在多线程环境中由于竞争导致数据不一致情况

用法：

```java 
ThreadLocal<Type> myThreadLocal = new ThreadLocal<XX>();
// get set remove都会移除ThreadLocalMap中entry的key为null的value；
myThreadLocal.set(type);
myThreadLocal.get();
myThreadLocal.remove();
```

原理：

<img src="https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/2020053018053863.png" alt="thread-local" style="zoom:50%;" />

每一个线程都会有一个类型为ThreadLocalMap的threadLocals本地变量，该变量默认16，实际上是一个table里面每一个都是Entry`class Entry extends WeakReference<ThreadLocal<?>>` 。访问都是代码层自定义寻址方法（hash映射后从entry中取值）。

调用set方法时传递为threadLocals的set，该对象保留了自定义了hashcode映射值与斐波那契散列乘数`0x61c88647`可以较好的散列；

内存泄漏原因：Entry中的Key是一个弱应用，若threadLocal不存在，则其会被GC，但是Value是一个强引用，其对象会在伴随着回收之后无法释放，其生命周期为线程的生命周期，尤其是当使用线程池时问题格外严重；及时remove即可

# IO 

> 背景就是应用程序向操作系统发起不同调用请求。操作系统作出不同响应，进而实现将内核中数据拷贝到应用程序中
>
> IO的理解方式，可以在数据的传输方式和操作方式俩个维度。Java具体实现中是通过装饰者模式

关于IO的基础定义

> 阻塞与非阻塞、同步与非同步、Linux的IO模型

## 网络IO的五种模型

>  BIO、NIO、AIO、IO多路复用、信号驱动IO

> 作者：云飞扬°
> 链接：https://www.nowcoder.com/discuss/820703
> 来源：牛客网

***BIO（Blocking IO）***<br>	阻塞型IO，用户线程发起IO请求后，必须等待内核线程准备好数据，并且将数据拷贝到用户线程存储空间，才会返回。期间用户线程处于阻塞状态，释放CPU资源。

![img](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/1639358986184-e10c4719-aa95-4093-92cc-b868160df3d7.png)

***NIO（nonblocking IO）***<br>	非阻塞型IO，发出IO操作后，不进入阻塞状态，不放弃CPU资源，开始轮询内核数据准备情况。内核准备好且收到系统调用，就将输出拷贝到用户线程。并返回

![img](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/1639359034221-3ddfaad7-1378-4de1-8aa4-6f75a16f6364-20220904150804563.png)

***AIO (异步IO Asynchronous IO)***

​	异步IO，发出IO请求之后，就会继续做其他的事情，内核收到后准备数据并将数据拷贝到用户线程存储空间中，然后通知用户线程。用户线程直接使用

![img](https://raw.githubusercontent.com/xiaoluxiang/picCollect/main/workDesign/img/1639359071332-7ebcbc03-c25a-4ab6-876a-35aa0b1343be.png)

***IO多路复用 和 信号驱动IO***

1. IO多路复用<br>	在多路复用IO模型中，会有一个线程不断去轮询多个socket的状态，只有当socket真正有读写事件时，才真正调用实际的IO读写操作。<br>	select：轮询所有的socket <br>	poll：轮询所有的socket，但是和select相比，没有最大连接数的限制，原因是它是基于链表]()存储的 <br>	epoll：只会轮询发生了IO请求的socket。虽然连接数有上限，但是很大，1G内存的机器上可以打开10W左右的连接；
2. I/O 多路复用模型是利用select、poll、epoll可以同时监察多个流的 I/O 事件的能力，在空闲的时候，会把当前线程阻塞掉，当有一个或多个流有I/O事件时，就从阻塞态中唤醒，于是程序就会轮询一遍所有的流（epoll是只轮询那些真正发出了事件的流），依次顺序的处理就绪的流，这种做法就避免了大量的无用操作。这里“多路”指的是多个网络连接，“复用”指的是复用同一个线程。

***信号驱动IO***（signal driven IO） 

1. 在信号驱动IO模型中，当用户线程发起一个IO请求操作，会给对应的socket注册一个**信号函数**，然后用户线程会继续执行，当内核数据]()就绪时会发送一个信号给用户线程，用户线程接收到信号之后，便在**信号函数**中调用IO读写操作来进行实际的IO请求操作。 

2.  应用进程使用 sigaction 系统调用，内核立即返回，应用进程可以继续执行，也就是说等待数据阶段应用进程是非阻塞的。 

3. 内核在数据到达时向应用进程发送 SIGIO 信号，应用进程收到之后在信号处理程序中调用 recvfrom 将数据从内核复制到应用进程中。信号驱动 I/O 的 CPU 利用率很高。 

***异步 IO 与信号驱动 IO***

 异步 I/O 与信号驱动 I/O 的区别在于，异步 I/O 的信号是通知应用进程 I/O 完成，而信号驱动 I/O 的信号是通知应用进程可以开始 I/O。

## Java Reator 模型

No

## 零拷贝

> 系统调用次数*2=上下文切换次数
>
> 文件读取分为DMA读取和CPU读取

传统提供文件传输IO过程，是俩次（read、write）调用，四次上下文切换，四次拷贝（DMA2，CPU2）

mmap+write传输文件过程，是俩次（mmap、write）调用，四次上下文切换，三次拷贝（DMA2，CPU1）

sendfile传输文件过程，是一次（sendfile）调用，俩次上下文切换，三次拷贝（DMA2，CPU1）

sendfile+网卡支持 SG-DMA，是一次（sendfile）调用，俩次上下文切换，俩次拷贝（DMA）

## NIO

sockets是面向流的而非包导向的。它们可以保证发送的字节会按照顺序到达但无法承诺维持字节分组



# Design Principle

里氏替换原则

接口隔离原则

依赖倒置原则

单一职责原则

迪米特法则

​	最小知道法则，直接尽量只与自己的朋友通讯。朋友包括this，成员对象，方法参数，自己创建的对象。狭义上是尽量只调用自己朋友的公共方法和属性。目的是为了降低类之间的耦合性。广义上是指对信息流的隐藏，这种隐藏可以实现子系统之间的脱耦。

组合/聚合原则

开闭原则

记忆图：

```mermaid
graph TB
interface --接口隔离/依赖倒置--> child

subgraph extend
parent --里氏替换--> child
child[child: 单一职责/迪米特/组合聚合] --开闭原则--> grandson
end
subgraph implement
interface
end
```



# Design Model

## 设计原则

> 生成类：单例->原型->工厂->生成器（builder）
>
> 结构类：适配->组合->桥接->门面->装饰->代理->享元
>
> 行为类：责任链->旁观->访问->策略->模版->命令->状态...

单例模式

Get方法

静态属性->synchorized静态方法->双检锁静态方法->静态内部类->枚举

## Facade模式，适配器模式，桥接模式

> 参考文章[桥接模式和适配器模式的区别](https://blog.csdn.net/xiefangjin/article/details/51056411)

### 一. 目的：

1. Facade 模式使用在给一个复杂的系统提供统一的门面\(接口),目的是简化客户端的操作,但并没有改变接口
2. Adapter 模式使用在两个部分有不同的接口的情况,目的是改变接口,使两个部分协同工作
3. 桥接模式 是为了分离抽象和实现

### 二. 使用场合

1. Facade
出现较多是这样的情况,你有一个复杂的系统,对应了各种情况,
客户看了说功能不错,但是使用太麻烦.你说没问题,我给你提供一个统一的门面.
所以Facade使用的场合多是对系统的"优化".
2. Adapter
出现是这样的情况,你有一个类提供接口A,但是你的客户需要一个实现接口B的类,
这个时候你可以写一个Adapter让把A接口变成B接口,所以Adapter使用的场合是
指鹿为马.就是你受夹板气的时候,一边告诉你我只能提供给你A(鹿),一边告诉你说
我只要B\(马),他长了四条腿,你没办法了,把鹿牵过去说,这是马,你看他有四条腿.
(当然实现指鹿为马也有两种方法,一个方法是你只露出鹿的四条腿,说你看这是马,这种方式就是
封装方式的Adapter实现,另一种方式是你把鹿牵过去,但是首先介绍给他说这是马,因为他长了四条腿
这种是继承的方式.)
3. Bridge
在一般的开发中出现的情况并不多,AWT是一个,SWT也算部分是,
如果你的客户要求你开发一个系统,这个系统在Windows下运行界面的样子是Windows的样子.
在Linux下运行是Linux下的样子.在Macintosh下运行要是Mac Os的样子.
怎么办? 定义一系列的控件Button,Text,radio,checkBox等等.供上层开发者
使用,他们使用这些控件的方法,利用这些控件构造一个系统的GUI,然后你为这些控件
写好Linux的实现,让它在Linux上调用Linux本地的对应控件,
在Windows上调用Windows本地的对应控件,在Macintosh上调用Macintosh本地的对应控件
ok,你的任务完成了.

### 三. 需求程度

1. Facade的需求程度是  "中等"  ,因为你不提供Facade程序照样能工作,只是不够好.
2. Adapter的需求程度是  "必须"  ,因为你不这么做就不能工作,除非你自己从头实现一个.
3. Bridge的需求程度是  "一般"  ,适合精益求精的人,因为你可以写三个程序给客户.

### 四. 出现时期

1. Facade出现在项目中期,再优化
2. Adapter出现在项目后期,大部分都有了,差的仅仅是接口不同
3. Bridge出现在项目前期,你想让你的系统更灵活,更cool

### 五. 在写文章的时候想到的

1. Facade很多时候是1:m的关系
2. Adapter很多是候是1:1的关系
3. Bridge很多时候是m:n的关系





# UML

> 参考文章: [30分钟学会UML类图](https://zhuanlan.zhihu.com/p/109655171)

UML中的关系有继承，实现，关联，依赖

**依赖**一般是指方法参数，临时变量，或者对静态方法的调用。强调的仅仅是使用上的需要。依赖关系用一个带虚线的箭头表示，由使用方指向被使用方，表示使用方对象持有被使用方对象的引用

**关联**分为has-a聚合，contain-a组合。关联关系有单向关联和双向关联。如果两个对象都知道（即可以调用）对方的公共属性和操作，那么二者就是双向关联。如果只有一个对象知道（即可以调用）另一个对象的公共属性和操作，那么就是单向关联。大多数关联都是单向关联，单向关联关系更容易建立和维护，有助于寻找可重用的类。在UML图中，双向关联关系用带双箭头的实线或者无箭头的实线双线表示。单向关联用一个带箭头的实线表示，箭头指向被关联的对象

**聚合**人以类聚，物以群分，各自独立，完整的生命周期。聚合关系用空心菱形加实线箭头表示，空心菱形在整体一方，箭头指向部分一方

**组合**不可分割的组成部分，部分不能脱离整体，组合关系用实心菱形加实线箭头表示，实心菱形在整体一方，箭头指向部分一方

仅从类代码本身是区分不了聚合和组合的。如果一定要区分，那么如果在删除整体对象的时候，必须删掉部分对象，那么就是组合关系，否则可能就是聚合关系。从业务角度上来看，如果作为整体的对象必须要部分对象的参与，才能完成自己的职责，那么二者之间就是组合关系，否则就是聚合关系。汽车与轮胎，汽车作为整体，轮胎作为部分。如果用在二手车销售业务环境下，二者之间就是聚合关系。因为轮胎作为汽车的一个组成部分，它和汽车可以分别生产以后装配起来使用，但汽车可以换新轮胎，轮胎也可以卸下来给其它汽车使用。如果用在驾驶系统业务环境上，汽车如果没有轮胎，就无法完成行驶任务，二者之间就是一个组合关系。再比如网上书店业务中的订单和订单项之间的关系，如果订单没有订单项，也就无法完成订单的业务，所以二者之间是组合关系。而购物车和商品之间的关系，因为商品的生命周期并不被购物车控制，商品可以被多个购物车共享，因此，二者之间是聚合关系。
