## **集合概述**

***

### **Java集合概述**

Java 集合， 也叫作容器，主要是由两大接口派生而来：一个是 `Collection`接口，主要用于存放单一元素；另一个是 `Map` 接口，主要用于存放键值对。对于`Collection` 接口，下面又有三个主要的子接口：`List`、`Set` 和 `Queue`。

![Java 集合框架概览](https://oss.javaguide.cn/github/javaguide/java/collection/java-collection-hierarchy.png)

![image.png](https://camo.githubusercontent.com/eb7c526190e720a854a2b02ce84fceeecdaf2dbc5cf79ef5e46bf6853c9dcf16/68747470733a2f2f63646e2e6e6c61726b2e636f6d2f79757175652f302f323032332f706e672f32383535313031302f313637393632363637353838372d65383261303032392d663363312d343537382d613263322d3861666138326633653566392e706e6723617665726167654875653d25323366376637663726636c69656e7449643d7534653664656534382d303138612d342666726f6d3d7061737465266865696768743d3638342669643d753238666334343132266e616d653d696d6167652e706e67266f726967696e4865696768743d363834266f726967696e57696474683d393435266f726967696e616c547970653d62696e61727926726174696f3d3126726f746174696f6e3d302673686f775469746c653d66616c73652673697a653d3439333537267374617475733d646f6e65267374796c653d6e6f6e65267461736b49643d7534643233643164642d633864652d346465312d613630342d6232383035373066346662267469746c653d2677696474683d393435)

**`HashSet`：**底层数据结构是hash表，基于`HashMap`实现。 

**`HashMap`：** JDK1.8 之前：`HashMap` 由数组+链表组成的，数组是 `HashMap` 的主体，链表则是主要为了解决哈希冲突而存在的（“拉链法”解决冲突）。 JDK1.8 以后：在解决哈希冲突时有了较大的变化，**当链表长度大于阈值（默认为 8）**（将链表转换成红黑树前会判断，**如果当前数组的长度小于 64，那么会选择先进行数组扩容**，而不是转换为红黑树)时，将链表转化为红黑树，以减少搜索时间。

**`LinkedHashMap`：**`LinkedHashMap` 继承自 `HashMap`，所以它的底层仍然是基于拉链式散列结构即由数组和链表或红黑树组成。另外，`LinkedHashMap` 在上面结构的基础上，增加了一条双向链表，使得上面的结构可以保持键值对的插入顺序。同时通过对链表进行相应的操作，实现了访问顺序相关逻辑。

**`Hashtable`：**数组+链表组成的，数组是 `Hashtable` 的主体，链表则是主要为了解决哈希冲突而存在的

**`priorityQueue`：** `Object[]` 数组来实现二叉堆

**`ArrayQueue`：** `Object[]` 数组 + 双指针

### **说说 List，Set， Queue， Map 四者的区别？**

- `List`（对付顺序的好帮手）：存储的元素是有序的、可重复的。
- `Set`（注重独一无二的性质)： 存储的元素是无序的、不可重复的。
- `Queue`(实现排队功能的叫号机)：按特定的排队规则来确定先后顺序，存储的元素是有序的、可重复的。
- `Map`(用 key 来搜索的专家)： 使用键值对（key-value）存储，key 是无序的、不可重复的，value 是无序的、可重复的，每个键最多映射到一个值。

### **为什么要使用集合？**

当我们需要存储一组类型相同的数据时，数组是最常用且最基本的容器之一。但是，使用数组存储对象存在一些不足之处，因为在实际开发中，存储的数据类型多种多样且数量不确定。这时，Java 集合就派上用场了。与数组相比，Java 集合提供了更灵活、更有效的方法来存储多个数据对象。Java 集合框架中的各种集合类和接口可以存储不同类型和数量的对象，同时还具有多样化的操作方式。相较于数组，Java 集合的优势在于它们的**大小可变**、**支持泛型**、**具有内建算法**等。总的来说，Java 集合提高了数据的存储和处理灵活性，可以更好地适应现代软件开发中多样化的数据需求，并支持高质量的代码编写。

## **List**

***

### **ArrayList 和 Array（数组）的区别？**

`ArrayList` 内部基于动态数组实现，比 `Array`（静态数组） 使用起来更加灵活：

- `ArrayList`会根据实际存储的元素**动态地扩容或缩容**，而 `Array` 被创建之后就不能改变它的长度了。
- `ArrayList` 允许你**使用泛型**来确保类型安全，`Array` 则不可以。
- `ArrayList` 中**只能存储对象**。对于基本类型数据，需要使用其对应的包装类（如 Integer、Double 等）。`Array` 可以直接存储基本类型数据，也可以存储对象。
- `ArrayList` 支持插入、删除、遍历等常见操作，并且提供了丰富的 **API 操作方法**，比如 `add()`、`remove()`等。`Array` 只是一个固定长度的数组，只能按照下标访问其中的元素，不具备动态添加、删除元素的能力。
- `ArrayList`创建时不需要指定大小，而`Array`创建时必须指定大小。

### **ArrayList 和 Vector 的区别?（了解即可）**

`ArrayList` 是 `List` 的主要实现类，底层使用 `Object[]`存储，**适用于频繁的查找工作，线程不安全** 。

`Vector` 是 `List` 的古老实现类，底层使用`Object[]` 存储，**线程安全**。

### **Vector 和 Stack 的区别?（了解即可）**

- `Vector` 和 `Stack` 两者都是**线程安全**的，都是**使用 `synchronized` 关键字进行同步处理**。
- `Stack` 继承自 `Vector`，是一个后进先出的栈，而 `Vector` 是一个列表。

随着 Java 并发编程的发展，`Vector` 和 `Stack` 已经被淘汰，推荐使用并发集合类（例如 `ConcurrentHashMap`、`CopyOnWriteArrayList` 等）或者手动实现线程安全的方法来提供安全的多线程操作支持

### **ArrayList插入和删除元素的时间复杂度？**

对于插入：

- **头部插入：**由于需要将所有元素都依次向后移动一个位置，因此**时间复杂度是 O(n)**。
- **尾部插入：**当 `ArrayList` 的**容量未达到极限时，往列表末尾插入元素的时间复杂度是 O(1)**，因为它只需要在数组末尾添加一个元素即可；当容量已达到极限并且**需要扩容时，则需要执行一次 O(n) 的操作将原数组复制到新的更大的数组中，然后再执行 O(1) 的操作添加元素。**
- **指定位置插入：**需要将目标位置之后的所有元素都向后移动一个位置，然后再把新元素放入指定位置。这个过程需要移动平均 n/2 个元素，因此**时间复杂度为 O(n)**。

对于删除：

- **头部删除：**由于需要将所有元素依次向前移动一个位置，因此**时间复杂度是 O(n)**。
- **尾部删除：**当删除的元素位于列表末尾时，**时间复杂度为 O(1)**。
- **指定位置删除：**需要将目标元素之后的所有元素向前移动一个位置以填补被删除的空白位置，因此需要移动平均 n/2 个元素，**时间复杂度为 O(n)**。

### **LinkedList 插入和删除元素的时间复杂度？**

[[LinkedList 源码分析 | JavaGuide(Java面试 + 学习指南)](https://javaguide.cn/java/collection/linkedlist-source-code.html)]

- **头部插入/删除：**只需要修改头结点的指针即可完成插入/删除操作，因此**时间复杂度为 O(1)**。

- **尾部插入/删除：**只需要修改尾结点的指针即可完成插入/删除操作，因此**时间复杂度为 O(1)**。

- **指定位置插入/删除：**需要先移动到指定位置，再修改指定节点的指针完成插入/删除，因此需要移动平均 n/2 个元素，时间**复杂度为 O(n)**。

### **LinkedList 为什么不能实现 RandomAccess 接口？**

`RandomAccess` 是**一个标记接口**，用来表明实现该接口的类支持随机访问（即可以通过索引快速访问元素）。由于 **`LinkedList` 底层数据结构是链表，内存地址不连续，只能通过指针来定位，不支持随机快速访问，所以不能实现 `RandomAccess` 接口。**

> 查看源码我们发现实际上 `RandomAccess` 接口中什么都没有定义。所以，在我看来 `RandomAccess` 接口不过是一个标识罢了。标识什么？ 标识实现这个接口的类具有随机访问功能。在 `binarySearch（)` 方法中，它要判断传入的 list 是否 `RandomAccess` 的实例，如果是，调用`indexedBinarySearch()`方法，如果不是，那么调用`iteratorBinarySearch()`方法。

### **ArrayList 与 LinkedList 区别**

- **是否保证线程安全：** `ArrayList` 和 `LinkedList` 都是不同步的，也就是**不保证线程安全**；
- **底层数据结构：** `ArrayList` 底层使用的是**`Object`数组**；`LinkedList` 底层使用的是 **双向链表** 数据结构（JDK1.6 之前为循环链表，JDK1.7 取消了循环。注意双向链表和双向循环链表的区别，下面有介绍到！）
- **插入和删除是否受元素位置的影响：**

  - `ArrayList` 采用数组存储，所以插入和删除元素的时间复杂度受元素位置的影响。 比如：执行`add(E e)`方法的时候， `ArrayList` 会默认在将指定的元素追加到此列表的末尾，这种情况时间复杂度就是 O(1)。但是如果要在指定位置 i 插入和删除元素的话（`add(int index, E element)`），时间复杂度就为 O(n)。因为在进行上述操作的时候集合中第 i 和第 i 个元素之后的(n-i)个元素都要执行向后位/向前移一位的操作。

  - `LinkedList` 采用链表存储，所以在头尾插入或者删除元素不受元素位置的影响（`add(E e)`、`addFirst(E e)`、`addLast(E e)`、`removeFirst()`、 `removeLast()`），时间复杂度为 O(1)，如果是要在指定位置 `i` 插入和删除元素的话（`add(int index, E element)`，`remove(Object o)`,`remove(int index)`）， 时间复杂度为 O(n) ，因为需要先移动到指定位置再插入和删除。
- **是否支持快速随机访问：** `LinkedList` 不支持高效的随机元素访问，而 `ArrayList`（实现了 `RandomAccess` 接口） 支持。快速随机访问就是通过元素的序号快速获取元素对象(对应于`get(int index)`方法)。
- **内存空间占用：** `ArrayList` 的空间浪费主要体现在在 list 列表的结尾会预留一定的容量空间，而 LinkedList 的空间花费则体现在它的每一个元素都需要消耗比 ArrayList 更多的空间（因为要存放直接后继和直接前驱以及数据）。

### **ArrayList扩容机制分析**

![ArrayList扩容机制.png](https://github.com/NFSPRINGG/JavaWork/blob/main/pictures/ArrayList%E6%89%A9%E5%AE%B9%E6%9C%BA%E5%88%B6.png?raw=true)

`ArrayList`的底层采用`Object`数组来存储数据，在往 `ArrayList` 里面添加元素时，才会涉及到扩容机制。由于采用的是数组存储，所以会给数组设置默认长度10。 当数组中没有元素时，是不会设置为默认长度10 的，数组是一个空数组。只有要添加元素时，会进入 `ensureCapacityInternal()`进行判断，如果数据数组为空数组，在添加第一个元素时才将数组长度扩容为默认值10，如果数组不为空数组 ， 就在 `ensureCapacityInternal()`里 面 调 用 `ensureExplicitCapacity()`来判断是否需要扩容。

如果需要扩容，才调用 `grow()`方法进行扩容。在`grow()`方法里面，会通过右移位运算将数组长度的新长度扩容为**原来的 1.5倍左右（oldCapacity 为偶数就是 1.5 倍，否则是 1.5 倍左右)**。

扩容后如果新容量不能满足所需容量，就将新容量扩大为所需容量。也即新容量大于 `MAX_ARRAY_SIZE`，就调用`hugeCapacity()`方法来比较 `minCapacity` 和 `MAX_ARRAY_SIZE` 的大小，如果 `minCapacity` 大于最大容量，则新容量则为 `Integer.MAX_VALUE`，否则，新容量大小则为 `MAX_ARRAY_SIZE`，即为 `Integer.MAX_VALUE - 8`。

最后将原数组中的元素拷贝到扩容后的新数组， 并将原数组的引用设置为拷贝后的数组。

## **Set**

***

### **Comparable 和 Comparator 的区别**

`Comparable` 接口和 `Comparator` 接口都是 Java 中用于排序的接口，它们在实现类对象之间比较大小、排序等方面发挥了重要作用：

- `Comparable` 接口实际上是出自`java.lang`包它有一个 `compareTo(Object obj)`方法用来排序
- `Comparator`接口实际上是出自 `java.util`包它有一个`compare(Object obj1, Object obj2)`方法用来排序

### **Comparable接口**

Comparable是排序接口。若一个类实现了Comparable接口，就意味着该类支持排序。实现了Comparable接口的类的对象的列表或数组可以通过`Collections.sort`或`Arrays.sort`进行自动排序。实现此接口的对象可以用作有序映射中的键或有序集合中的集合，无需指定比较器

```java
public class Student implements Comparable<Student>{
    private int age;
    private String name;
    private int weight;
  ...  
  /**
     * 实现Comparable接口 重写compareTo方法即可
     * return表示的是   1【正序】 -1【倒叙】
     * 优点：灵活
     * 缺点：每次指定规则
     */ 
  @Override
    public int compareTo(Student o) {
        if (this.age == o.age){
            return ((this.weight < o.weight) ? -1 : ((this.weight == o.weight) ? 0 : 1));
        }else{
            return (this.age < o.age) ? -1 : 1;
        }
    }
}
```

**Comparator接口（比较器）**

若一个类要实现Comparator接口：它一定要实现compare(T o1, T o2) 函数

```java
// 定制排序的用法
Collections.sort(arrayList, new Comparator<Integer>() {
    @Override
    public int compare(Integer o1, Integer o2) {
        return o2.compareTo(o1);
    }
```

总结：

1. Comparable是排序接口，若一个类实现了Comparable接口，就意味着“该类支持排序”。
2. Comparator是比较器，我们若需要控制某个类的次序，可以建立一个“该类的比较器”来进行排序。
3. Comparable相当于“内部比较器”，而Comparator相当于“外部比较器”。
4. 用Comparable 简单， 只要实现Comparable 接口的对象直接就成为一个可以比较的对象，但是需要修改源代码。
5. 用Comparator 的好处是不需要修改源代码， 而是另外实现一个比较器， 当某个自定义的对象需要作比较的时候，把比较器和对象一起传递过去就可以比大小了， 并且在Comparator 里面用户可以自己实现复杂的可以通用的逻辑，使其可以匹配一些比较简单的对象，那样就可以节省很多重复劳动了。

### **HashSet 如何检查重复?**

当你把对象加入`HashSet`时，`HashSet` 会先计算对象的`hashcode`值来判断对象加入的位置，同时也会与其他加入的对象的 `hashcode` 值作比较，如果没有相符的 `hashcode`，`HashSet` 会假设对象没有重复出现。但是如果发现有相同 `hashcode` 值的对象，这时会调用`equals()`方法来检查 `hashcode` 相等的对象是否真的相同。如果两者相同，`HashSet` 就不会让加入操作成功。

## **Queue**

***

### **Queue与Deque的区别**

- `Queue` 是单端队列，只能从一端插入元素，另一端删除元素，实现上一般遵循 **先进先出（FIFO）** 规则。
- `Deque` 是双端队列，在队列的两端均可以插入或删除元素。

| `Queue` 接口 | 抛出异常  | 返回特殊值 |
| ------------ | --------- | ---------- |
| 插入队尾     | add(E e)  | offer(E e) |
| 删除队首     | remove()  | poll()     |
| 查询队首元素 | element() | peek()     |

`Deque` 扩展了 `Queue` 的接口，增加了在队首和队尾进行插入和删除的方法，同样根据失败后处理方式的不同分为两类：

| `Deque` 接口 | 抛出异常      | 返回特殊值      |
| :----------- | ------------- | --------------- |
| 插入队首     | addFirst(E e) | offerFirst(E e) |
| 插入队尾     | addLast(E e)  | offerLast(E e)  |
| 删除队首     | removeFirst() | pollFirst()     |
| 删除队尾     | removeLast()  | pollLast()      |
| 查询队首元素 | getFirst()    | peekFirst()     |
| 查询队尾元素 | getLast()     | peekLast()      |

### **ArrayDeque 与 LinkedList 的区别**

`ArrayDeque` 和 `LinkedList` 都实现了 `Deque` 接口，两者都具有队列的功能，但两者有什么区别呢？

- `ArrayDeque` 是基于可变长的数组和双指针来实现，而 `LinkedList` 则通过链表来实现。
- `ArrayDeque` 不支持存储 `NULL` 数据，但 `LinkedList` 支持。
- `ArrayDeque` 是在 JDK1.6 才被引入的，而`LinkedList` 早在 JDK1.2 时就已经存在。
- `ArrayDeque` 插入时可能存在扩容过程，不过均摊后的插入操作依然为 O(1)。虽然 `LinkedList` 不需要扩容，但是每次插入数据时均需要申请新的堆空间，均摊性能相比更慢。

从性能的角度上，选用 `ArrayDeque` 来实现队列要比 `LinkedList` 更好。此外，`ArrayDeque` 也可以用于实现栈。



## **Map（重要）**

***

### **HashMap 和 Hashtable 的区别**

- **线程是否安全：** `HashMap` 是非线程安全的，`Hashtable` 是线程安全的，因为 `Hashtable` 内部的方法基本都经过`synchronized` 修饰。（如果你要保证线程安全的话就使用 `ConcurrentHashMap` 吧！）；

- **效率：** 因为线程安全的问题，`HashMap` 要比 `Hashtable` 效率高一点。另外，`Hashtable` 基本被淘汰，不要在代码中使用它；

- **对 Null key 和 Null value 的支持：** `HashMap` 可以存储 null 的 key 和 value，但 null 作为键只能有一个，null 作为值可以有多个；Hashtable 不允许有 null 键和 null 值，否则会抛出 `NullPointerException`。

- **初始容量大小和每次扩充容量大小的不同：** ① 创建时如果不指定容量初始值，`Hashtable` 默认的初始大小为 11，之后每次扩充，容量变为原来的 2n+1。**`HashMap` 默认的初始化大小为 16**。之后每次扩充，容量变为原来的 2 倍。② 创建时如果给定了容量初始值，那么 `Hashtable` 会直接使用你给定的大小，而 `HashMap` 会将其扩充为 2 的幂次方大小（`HashMap` 中的`tableSizeFor()`方法保证，下面给出了源代码）。也就是说 `HashMap` 总是使用 2 的幂作为哈希表的大小，后面会介绍到为什么是 2 的幂次方。

- **底层数据结构：** JDK1.8 以后的 `HashMap` 在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）时，将链表转化为红黑树（将链表转换成红黑树前会判断，如果当前数组的长度小于 64，那么会选择先进行数组扩容，而不是转换为红黑树），以减少搜索时间（后文中我会结合源码对这一过程进行分析）。`Hashtable` 没有这样的机制。

### **HashMap 的底层实现**

#### JDK1.8之前

![jdk1.8 之前的内部结构-HashMap](https://oss.javaguide.cn/github/javaguide/java/collection/jdk1.7_hashmap.png)

JDK1.8 之前 `HashMap` 底层是 **数组和链表** 结合在一起使用也就是 **链表散列**。HashMap 通过它的hash()方法获取key对应的hashCode值（经过扰动函数处理过后得到 hash 值），然后通过 `(n - 1) & hash` 判断当前元素存放的位置（这里的 n 指的是数组的长度），如果当前位置存在元素的话，就判断该元素与要存入的元素的 hash 值以及 key 是否相同，如果相同的话，直接覆盖，不相同就通过**拉链法解决冲突**。

> 所谓**扰动函数**指的就是 HashMap 的 `hash` 方法。使用 `hash` 方法也就是扰动函数是为了防止一些实现比较差的 `hashCode()` 方法 换句话说使用扰动函数之后可以减少碰撞。
>
> 所谓 **“拉链法”** 就是：将链表和数组相结合。也就是说创建一个链表数组，数组中每一格就是一个链表。若遇到哈希冲突，则将冲突的值加到链表中即可。

#### JDK1.8 之后

相比于之前的版本， JDK1.8 之后在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）（将链表转换成红黑树前会判断，如果当前数组的长度小于 64，那么会选择先进行数组扩容，而不是转换为红黑树）时，将链表转化为红黑树，以减少搜索时间。

### **HashMap 的长度为什么是 2的幂次方**

**为了能让 HashMap 存取高效，尽量较少碰撞，也就是要尽量把数据分配均匀。**当我们往 HashMap 里面 put 元素的时候，会通过 hashMap 的 hash 方法，获取 key 对应的 hashCode 值，然后拿这个值去判断该元素要存放在那个地方，这里采用的是`(n-1) & hash`,也即右移16位，其中 n 为 HashMap 的长度，这个操作只有当 n 是 2 的幂次方时，`(n-1) & hash` 才和 hash%n 表示的是一个意思，这样才能找到这个 key 在数组中对应的位置。 如果不是 2 的幂次方， `(n-1) & hash` 是不等于 `hash%n` 的，之所以采用位运算的好处是：相较于%操作，它的**效率更高，保证散列均匀分布**。

**这个算法应该如何设计呢？**

我们首先可能会想到采用%取余的操作来实现。但是，重点来了：**“取余(%)操作中如果除数是 2 的幂次则等价于与其除数减一的与(&)操作（也就是说 hash%length==hash&(length-1)的前提是 length 是 2 的 n 次方；）。”** 并且 **采用二进制位操作 &，相对于%能够提高运算效率，这就解释了 HashMap 的长度为什么是 2 的幂次方。**

### **HashMap 多线程操作导致死循环问题**

JDK1.7 及之前版本的 `HashMap` 在多线程环境下扩容操作可能存在死循环问题，这是由于当一个桶位中有多个元素需要进行扩容时，多个线程同时对链表进行操作，**头插法可能会导致链表中的节点指向错误的位置，从而形成一个环形链表**，进而使得查询元素的操作陷入死循环无法结束。

为了解决这个问题，**JDK1.8 版本的 HashMap 采用了尾插法**而不是头插法来避免链表倒置，使得插入的节点永远都是放在链表的末尾，避免了链表中的环形结构。但是还是不建议在多线程下使用 `HashMap`，因为多线程下使用 `HashMap` 还是会存在数据覆盖的问题。并发环境下，推荐使用 `ConcurrentHashMap`。

### **HashMap 为什么线程不安全？**

JDK1.7 及之前版本，在多线程环境下，`HashMap` 扩容时会造成死循环和数据丢失的问题。数据丢失这个在 JDK1.7 和 JDK 1.8 中都存在，这里以 JDK 1.8 为例进行介绍。多个线程对 `HashMap` 的 `put` 操作会导致线程不安全，具体来说会有数据覆盖的风险。

举个例子：

- 两个线程 1，2 同时进行 put 操作，并且发生了哈希冲突（hash 函数计算出的插入下标是相同的）。
- 不同的线程可能在不同的时间片获得 CPU 执行的机会，当前线程 1 执行完哈希冲突判断后，由于时间片耗尽挂起。线程 2 先完成了插入操作。
- 随后，线程 1 获得时间片，由于之前已经进行过 hash 碰撞的判断，所有此时会直接进行插入，这就导致线程 2 插入的数据被线程 1 覆盖了。

还有一种情况是这两个线程同时 `put` 操作导致 `size` 的值不正确，进而导致数据覆盖的问题：

1. 线程 1 执行 `if(++size > threshold)` 判断时，假设获得 `size` 的值为 10，由于时间片耗尽挂起。
2. 线程 2 也执行 `if(++size > threshold)` 判断，获得 `size` 的值也为 10，并将元素插入到该桶位中，并将 `size` 的值更新为 11。
3. 随后，线程 1 获得时间片，它也将元素放入桶位中，并将 size 的值更新为 11。
4. 线程 1、2 都执行了一次 `put` 操作，但是 `size` 的值只增加了 1，也就导致实际上只有一个元素被添加到了 `HashMap` 中。

### **HashMap常见的遍历方式？**

#### **遍历方式**

1. 迭代器（Iterator）方式遍历（entrySet和keySet遍历）

   ```java
   // entrySet遍历
   Iterator<Map.Entry<Integer, String>> iterator = map.entrySet().iterator();
   while (iterator.hasNext()) {
       Map.Entry<Integer, String> entry = iterator.next();
       System.out.println(entry.getKey());
       System.out.println(entry.getValue());
   }
   
   // keySet遍历
   Iterator<Integer> iterator = map.keySet().iterator();
   while (iterator.hasNext()) {
       Integer key = iterator.next();
       System.out.println(key);
       System.out.println(map.get(key));
   }
   ```

2. For Each方式遍历

   ```java
   // entrySet遍历
   for (Map.Entry<Integer, String> entry : map.entrySet()) {
       System.out.println(entry.getKey());
       System.out.println(entry.getValue());
   }
   
   // keySet遍历
   for (Integer key : map.keySet()) {
       System.out.println(key);
       System.out.println(map.get(key));
   }
   ```

3. Lambda表达式遍历

   ```java
   // lambda表达式遍历
   map.forEach((key, value) -> {
       System.out.println(key);
       System.out.println(value);
   });
   ```

4. Streams API遍历

   ```java
   // 单线程遍历
   map.entrySet().stream().forEach((entry) -> {
       System.out.println(entry.getKey());
       System.out.println(entry.getValue());
   });
   // 多线程遍历
   map.entrySet().parallelStream().forEach((entry) -> {
       System.out.println(entry.getKey());
       System.out.println(entry.getValue());
   });
   ```

#### **性能分析**

`entrySet`的性能比`keySet`的性能好，尽量使用`entrySet`来遍历Map集合。`KeySet` 在循环时使用了 `map.get(key)`，而 map.get(key) 相当于又遍历了一遍 Map 集合去查询 key 所对应的值。为什么要用“又”这个词？那是因为**在使用迭代器或者 for 循环时，其实已经遍历了一遍 Map 集合了，因此再使用 map.get(key) 查询时，相当于遍历了两遍**。 而 `EntrySet `只遍历了一遍 Map 集合，之后通过代码“`Entry<Integer, String> entry = iterator.next()`”把对象的 key 和 value 值都放入到了 Entry 对象中，因此再获取 key 和 value 值时就无需再遍历 Map 集合，只需要从 Entry 对象中取值就可以了。 所以，**EntrySet 的性能比 KeySet 的性能高出了一倍，因为 KeySet 相当于循环了两遍 Map 集合，而 EntrySet 只循环了一遍**。

#### **安全性能**

我们不能在遍历中使用集合 map.remove() 来删除数据，这是非安全的操作方式，但我们可以使用迭代器的 iterator.remove() 的方法来删除数据，这是安全的删除集合的方式。同样的我们也可以使用 Lambda 中的 removeIf 来提前删除数据，或者是使用 Stream 中的 filter 过滤掉要删除的数据进行循环，这样都是安全的，当然我们也可以在 for 循环前删除数据在遍历也是线程安全的。 所以，**尽量使用迭代器（Iterator）来遍历EntrySet的遍历方式操作Map集合**

### **ConcurrentHashMap 和 Hashtable 的区别**

`ConcurrentHashMap` 和 `Hashtable` 的区别主要体现在实现线程安全的方式上不同。

- **底层数据结构：** JDK1.7 的 `ConcurrentHashMap` 底层采用 **分段的数组+链表** 实现，JDK1.8 采用的数据结构跟 `HashMap1.8` 的结构一样，数组+链表/红黑二叉树。`Hashtable` 和 JDK1.8 之前的 `HashMap` 的底层数据结构类似都是采用 **数组+链表** 的形式，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突而存在；

- **实现线程安全的方式（重要）：**

  - 在 JDK1.7 的时候，`ConcurrentHashMap` 对整个桶数组进行了**分割分段**(`Segment`，分段锁)，每一把锁只锁容器其中一部分数据（下面有示意图），多线程访问容器里不同数据段的数据，就**不会存在锁竞争，提高并发访问率**。

    ![Java7 ConcurrentHashMap 存储结构](https://oss.javaguide.cn/github/javaguide/java/collection/java7_concurrenthashmap.png)

  - 到了 JDK1.8 的时候，`ConcurrentHashMap` 已经摒弃了 `Segment` 的概念，而是直接用 `Node`数组+链表+红黑树的数据结构来实现，**并发控制使用 `synchronized` 和 CAS 来操作**。（JDK1.6 以后 `synchronized` 锁做了很多优化） 整个看起来就像是优化过且线程安全的 `HashMap`，虽然在 JDK1.8 中还能看到 `Segment` 的数据结构，但是已经简化了属性，只是为了兼容旧版本；

    ![Java8 ConcurrentHashMap 存储结构](https://oss.javaguide.cn/github/javaguide/java/collection/java8_concurrenthashmap.png)

  - **`Hashtable`(同一把锁)** ：使用 `synchronized` 来保证线程安全，效率非常低下。当一个线程访问同步方法时，其他线程也访问同步方法，可能会进入阻塞或轮询状态，如使用 put 添加元素，另一个线程不能使用 put 添加元素，也不能使用 get，竞争会越来越激烈效率越低。

    ![Hashtable 的内部结构](https://oss.javaguide.cn/github/javaguide/java/collection/jdk1.7_hashmap.png)

### **ConcurrentHashMap 线程安全的具体实现方式/底层具体实现**

####  JDK1.8 之前

首先将数据分为一段一段（这个“段”就是 `Segment`）的存储，然后给每一段数据配一把锁，当一个线程占用锁访问其中一个段数据时，其他段的数据也能被其他线程访问。**`ConcurrentHashMap` 是由 `Segment` 数组结构和 `HashEntry` 数组结构组成**。`Segment` 继承了 `ReentrantLock`，所以 `Segment` 是一种可重入锁，扮演锁的角色。`HashEntry` 用于存储键值对数据。

```java
static class Segment<K,V> extends ReentrantLock implements Serializable {
}
```

一个 `ConcurrentHashMap` 里包含一个 `Segment` 数组，`Segment` 的个数一旦**初始化就不能改变**。 `Segment` 数组的大小默认是 16，也就是说默认可以同时支持 16 个线程并发写。

`Segment` 的结构和 `HashMap` 类似，是一种数组和链表结构，一个 `Segment` 包含一个 `HashEntry` 数组，每个 `HashEntry` 是一个链表结构的元素，每个 `Segment` 守护着一个 `HashEntry` 数组里的元素，当对 `HashEntry` 数组的数据进行修改时，必须首先获得对应的 `Segment` 的锁。也就是说，**对同一 `Segment` 的并发写入会被阻塞，不同 `Segment` 的写入是可以并发执行的。**

#### JDK1.8 之后

`ConcurrentHashMap` 取消了 `Segment` 分段锁，采用 `Node + CAS + synchronized` 来保证并发安全。数据结构跟 `HashMap` 1.8 的结构类似，数组+链表/红黑二叉树。Java 8 在链表长度超过一定阈值（8）时将链表（寻址时间复杂度为 O(N)）转换为红黑树（寻址时间复杂度为 O(log(N))）。Java 8 中，**锁粒度更细，`synchronized` 只锁定当前链表或红黑二叉树的首节点，这样只要 hash 不冲突，就不会产生并发，就不会影响其他 Node 的读写，效率大幅提升。**

### **JDK 1.7 和 JDK 1.8 的 ConcurrentHashMap 实现有什么不同？**

- **线程安全实现方式**：JDK 1.7 采用 `Segment` 分段锁来保证安全， `Segment` 是继承自 `ReentrantLock`。JDK1.8 放弃了 `Segment` 分段锁的设计，采用 `Node + CAS + synchronized` 保证线程安全，锁粒度更细，`synchronized` 只锁定当前链表或红黑二叉树的首节点。

- **Hash 碰撞解决方法** : JDK 1.7 采用拉链法，JDK1.8 采用拉链法结合红黑树（链表长度超过一定阈值时，将链表转换为红黑树）。

- **并发度**：JDK 1.7 最大并发度是 Segment 的个数，默认是 16。JDK 1.8 最大并发度是 Node 数组的大小，并发度更大。
