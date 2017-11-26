---
layout: post
title: java集合框架详解
categories: java知识
---
## 1 java集合的基本概念 ##

### 1.1 数组ＶＳ集合 ###

使用数组的前提是我们事先已经明确知道我们将要保存的对象的数量。一旦在数组初始化时指定了这个数组长度，这个数组长度就是不可变的。

如果我们需要保存一个可以动态增长的数据(在编译时无法确定具体的数量)，java的集合类就是一个很好的设计方案了。

集合类主要负责保存、盛装其他数据，因此集合类也被称为`容器类`。所以的集合类都位于java.util包下，后来为了处理多线程环境下的并发安全问题，java5还在java.util.concurrent包下提供了一些多线程支持的集合类。

### 1.2 Java集合框架常用两种类型 ###
Java集合框架主要包括两种类型的容器，一种是集合（Collection），存储一个元素集合，另一种是图（Map），存储键/值对映射。

区别：

Collection(接口)

一组"对立"的元素，`每个位置只能保存一个元素(对象)`，通常这些元素都服从某种规则，例如：
1. List必须保持元素特定的顺序
2. Set不能有重复元素
3. Queue保持一个队列(先进先出)的顺序
4. ..等等

Map(接口)

一组成对的"键值对"对象，`保存的是"键值对"，就像一个小型数据库。我们可以通过"键"找到该键对应的"值"`

### 1.3 集合框架类图 ###
类关系图如下：
![java集合框架类图](https://raw.githubusercontent.com/ADeveloperH/ADeveloperH.github.io/master/assets/20171126/2243690-9cd9c896e0d512ed.png "java集合框架类图")

## 2 Collection 接口详解 ##

Collection是最基本的集合接口，一个Collection代表一组Object的集合，这些Object被称作Collection的元素。

所有实现Collection接口的类都必须提供两个标准的构造函数：无参数的构造函数用于创建一个空的Collection，有一个Collection参数的构造函数用于创建一个新的Collection，这 个新的Collection与传入的Collection有相同的元素。后一个构造函数允许用户复制一个Collection。

如何遍历Collection中的每一个元素？不论Collection的实际类型如何，它都支持一个iterator()的方法，该方法返回一个迭代子，使用该迭代子即可逐一访问Collection中每一个元素。典型的用法如下：
```java
Iterator it = collection.iterator(); // 获得一个迭代子 
while(it.hasNext()) { 
　　Object obj = it.next(); // 得到下一个元素 
}
```

Collection 接口提供的主要方法：
```
boolean add(Object o) 添加对象到集合；
boolean remove(Object o) 删除指定的对象；
int size() 返回当前集合中元素的数量；
boolean contains(Object o) 查找集合中是否有指定的对象；
boolean isEmpty() 判断集合是否为空；
Iterator iterator() 返回一个迭代器；
boolean containsAll(Collection c) 查找集合中是否有集合 C 中的元素；
boolean addAll(Collection c) 将集合 C 中所有的元素添加给该集合；
void clear() 删除集合中所有元素；
void removeAll(Collection c) 从集合中删除 C 集合中也有的元素；
void retainAll(Collection c) 从集合中删除集合 C 中不包含的元素。
```

根据用途的不同，Collection又划分为List(接口继承自Collection接口)与Set(接口继承自Collection接口)，Queue接口也扩展字Collection接口。

### 2.1 List接口(继承自Collection接口) ###
List继承自Collection接口。List是`有序的Collection`，使用此接口能够精确的控制每个元素插入的位置。用户能够使用索引（元素在List中的位置，类似于数组下标）来访问List中的元素，这类似于Java的数组。

跟Set集合不同的是，`List允许有重复元素`。对于满足e1.equals(e2)条件的e1与e2对象元素，可以同时存在于List集合中。当然，`也有List的实现类不允许重复元素的存在`。

除了具有Collection接口必备的iterator()方法外，List还提供一个listIterator()方法，返回一个 ListIterator接口，和标准的Iterator接口相比，ListIterator多了一些add()之类的方法，允许添加，删除，设定元素， 还能向前或向后遍历。

List 接口提供的主要方法：
```
void add(int index,Object element) 在指定位置上添加一个对象；
boolean addAll(int index,Collection c) 将集合 C 的元素添加到指定的位置；
Object get(int index) 返回 List 中指定位置的元素；
int indexOf(Object o) 返回第一个出现元素 O 的位置；
Object removeint(int index) 删除指定位置的元素；
Object set(int index,Object element) 用元素 element 取代位置 index 上的元素, 返回被取代的元素。
```

实现List接口的常用类有ArrayList，LinkedList，Vector和Stack。

#### 2.1.1 ArrayList类 ####
ArrayList实现了`可变大小的数组`。它允许所有元素，`包括null`。`ArrayList非同步的（unsynchronized）`。
size，isEmpty，get，set方法运行时间为常数。但是add方法开销为分摊的常数，添加n个元素需要O(n)的时间。其他的方法运行时间为线性。

ArrayList是用`数组`存储元素的，这个数组可以动态创建，如果元素个数超过了数组的容量，那么就创建一个更大的新数组，并将当前数组中的所有元素都复制到新数组中

每个ArrayList实例都有一个容量（Capacity），即用于存储元素的数组的大小。这个容量可随着不断添加新元素而自动增加，但是增长算法并没有定义。当需要插入大量元素时，在插入前可以调用ensureCapacity方法来增加ArrayList的容量以提高插入效率。

ArrayList 提供的主要方法：

```
Boolean add(Object o) 将指定元素添加到列表的末尾；
Boolean add(int index,Object element) 在列表中指定位置加入指定元素；
Boolean addAll(Collection c) 将指定集合添加到列表末尾；
Boolean addAll(int index,Collection c) 在列表中指定位置加入指定集合；
Boolean clear() 删除列表中所有元素；
Boolean clone() 返回该列表实例的一个拷贝；
Boolean contains(Object o) 判断列表中是否包含元素；
Boolean ensureCapacity(int m) 增加列表的容量，如果必须，该列表能够容纳 m 个元素；
Object get(int index) 返回列表中指定位置的元素；
Int indexOf(Object elem) 在列表中查找指定元素的下标；
Int size() 返回当前列表的元素个数。
```
假设第一次是集合没有任何元素，下面以插入一个元素为例看看源码的实现。
```
1、方法add(E e)向集合中添加指定元素。

   public boolean add(E e) {
        ensureCapacityInternal(size + 1);  // Increments modCount!!
        elementData[size++] = e;
        return true;
    }

2、此方法主要是确定将要创建的数组大小。

  private void ensureCapacityInternal(int minCapacity) {
        if (elementData == DEFAULTCAPACITY_EMPTY_ELEMENTDATA) {
            minCapacity = Math.max(DEFAULT_CAPACITY, minCapacity);
        }

        ensureExplicitCapacity(minCapacity);
    }

    private void ensureExplicitCapacity(int minCapacity) {
        modCount++;
        if (minCapacity - elementData.length > 0)
            grow(minCapacity);
    }

3、最后是创建数组，可以明显的看到先是确定了添加元素后的大小之后将元素复制到新数组中。

    private void grow(int minCapacity) {
        // overflow-conscious code
        int oldCapacity = elementData.length;
        int newCapacity = oldCapacity + (oldCapacity >> 1);
        if (newCapacity - minCapacity < 0)
            newCapacity = minCapacity;
        if (newCapacity - MAX_ARRAY_SIZE > 0)
            newCapacity = hugeCapacity(minCapacity);
        // minCapacity is usually close to size, so this is a win:
        elementData = Arrays.copyOf(elementData, newCapacity);
    }
```
#### 2.1.2 LinkedList 类 ####

LinkedList实现了List接口，`允许null元素`。此外LinkedList提供额外的get，remove，insert方法在 LinkedList的首部或尾部。这些操作使LinkedList可被用作堆栈（stack），队列（queue）或双向队列（deque）。

注意LinkedList没有同步方法。如果多个线程同时访问一个List，则必须自己实现访问同步。一种解决方法是在创建List时构造一个同步的List：
```List list = Collections.synchronizedList(new LinkedList(...));```

LinkedList是在一个链表中存储元素，我们知道链表和数组的最大区别在于它们对元素的存储方式的不同导致它们在对数据进行不同操作时的效率不同，同样，ArrayList与LinkedList也是如此，实际使用中我们需要根据特定的需求选用合适的类，`如果除了在末尾外不能在其他位置插入或者删除元素，那么ArrayList效率更高，如果需要经常插入或者删除元素，就选择LinkedList`。

#### 2.1.3 Vector 类 ####

Vector非常`类似ArrayList`，但是`Vector是同步的`。由Vector创建的Iterator，虽然和ArrayList创建的 Iterator是同一接口，但是，因为Vector是同步的，当一个Iterator被创建而且正在被使用，另一个线程改变了Vector的状态（例如，添加或删除了一些元素），这时调用Iterator的方法时将抛出

ConcurrentModificationException，因此必须捕获该异常。

#### 2.1.4 Stack  类 ####

Stack继承自Vector，实现一个`后进先出的堆栈`。Stack提供5个额外的方法使得Vector得以被当作堆栈使用。基本的push和pop方 法，还有peek方法得到栈顶的元素，empty方法测试堆栈是否为空，search方法检测一个元素在堆栈中的位置。Stack刚创建后是空栈。

### 2.2 Set接口(继承自Collection接口) ###

Set继承自Collection接口。Set是一种`不能包含有重复元素的集合`，即对于满足e1.equals(e2)条件的e1与e2对象元素，不能同时存在于同一个Set集合里，换句话说，Set集合里任意两个元素e1和e2都满足e1.equals(e2)==false条件，`Set最多有一个null元素`。

>因为Set的这个制约，在使用Set集合的时候，应该注意：
为Set集合里的元素的实现类实现一个有效的equals(Object)方法。
对Set的构造函数，传入的Collection参数不能包含重复的元素。
请注意：必须小心操作可变对象（Mutable Object）。如果一个Set中的可变元素改变了自身状态导致Object.equals(Object)=true将导致一些问题。

实现Set接口的常用类散列集HashSet、链式散列集LinkedHashSet和树形集TreeSet。

#### 2.2.1 HashSet 类 ####

此类实现 Set 接口，由哈希表（实际上是一个 HashMap 实例）支持。它`不保证集合的迭代顺序；特别是它不保证该顺序恒久不变`。此类`允许使用 null 元素`。

散列集HashSet可以使用它的无参构造方法来创建空的散列集，也可以由一个现有的集合创建散列集。在散列集中，有两个名词需要关注，初始容量和客座率。客座率是确定在增加规则集之前，该规则集的饱满程度，当元素个数超过了容量与客座率的乘积时，容量就会自动翻倍。

HashSet`不是同步的`，需要用以下语句来进行S同步转换：
```	
Set s = Collections.synchronizedSet(new HashSet(...));
```
#### 2.2.2 LinkedHashSet 类 ####

LinkedHashSet是用一个`链表实现来扩展HashSet类，它支持对规则集内的元素排序`。HashSet中的元素是没有被排序的，而LinkedHashSet中的元素可以按照它们插入规则集的顺序提取。

#### 2.2.3 TreeSet 类 ####

TreeSet扩展自AbstractSet，并实现了NavigableSet，AbstractSet扩展自AbstractCollection，树形集是一个有序的Set，其底层是一颗树，这样就能从Set里面提取一个有序序列了。在实例化TreeSet时，我们可以给TreeSet指定一个比较器Comparator来指定树形集中的元素顺序。树形集中提供了很多便捷的方法。

### 2.3 Queue 接口 ###

队列是一种先进先出的数据结构，元素在队列末尾添加，在队列头部删除。Queue接口扩展自Collection，并提供插入、提取、检验等操作。

接口Deque，是一个扩展自Queue的双端队列，它支持在两端插入和删除元素，因为`LinkedList类实现了Deque接口，所以通常我们可以使用LinkedList来创建一个队列`。PriorityQueue类实现了一个优先队列，优先队列中元素被赋予优先级，拥有高优先级的先被删除。

## 3 Map 接口 ##

Map没有继承Collection接口。也就是说Map和Collection是2种不同的集合。Collection可以看作是（value）的集合，而Map可以看作是（key，value）的集合。

Map接口由Map的内容提供3种类型的集合视图，一组key集合，一组value集合，或者一组key-value映射关系的集合。

在Map中键可以是任意类型的对象，但不能有重复的键，每个键都对应一个值，真正存储在图中的是键值构成的条目。

Map接口常用的实现类有：HashMap、Hashtable、LinkedHashMap、TreeMap、WeakHashMap。
### 3.1 Hashtable 类 ###

Hashtable继承Map接口，实现一个key-value映射的哈希表。任何`非空（non-null）的对象都可作为key或者value`。

添加数据使用put(key, value)，取出数据使用get(key)，这两个基本操作的时间开销为常数。

Hashtable 通过initial capacity和load factor两个参数调整性能。通常缺省的load factor 0.75较好地实现了时间和空间的均衡。增大load factor可以节省空间但相应的查找时间将增大，这会影响像get和put这样的操作。

由于作为key的对象将通过计算其散列函数来确定与之对应的value的位置，因此任何作为key的对象都必须实现hashCode和equals方 法。hashCode和equals方法继承自根类Object，如果你用自定义的类当作key的话，要相当小心，按照散列函数的定义，如果两个对象相 同，即obj1.equals(obj2)=true，则它们的hashCode必须相同，但如果两个对象不同，则它们的hashCode不一定不同，如 果两个不同对象的hashCode相同，这种现象称为冲突，冲突会导致操作哈希表的时间开销增大，所以尽量定义好的hashCode()方法，能加快哈希 表的操作。

如果相同的对象有不同的hashCode，对哈希表的操作会出现意想不到的结果（期待的get方法返回null），要避免这种问题，只需要牢记一条：要同时复写equals方法和hashCode方法，而不要只写其中一个。

`Hashtable是同步的。`

### 3.2 HashMap 类 ###

HashMap和Hashtable类似，不同之处在于`HashMap是非同步的，并且允许null，即null value和null key`。，但是将HashMap视为Collection时（values()方法可返回Collection），其迭代子操作时间开销和HashMap 的容量成比例。因此，如果迭代操作的性能相当重要的话，不要将HashMap的初始化容量设得过高，或者load factor过低。

HashMap是基于哈希表的Map接口的`非同步实现`，继承自AbstractMap，AbstractMap是部分实现Map接口的抽象类。在平时的开发中，HashMap的使用还是比较多的。我们知道`ArrayList主要是用数组`来存储元素的，`LinkedList是用链表`来存储的，在之前的版本中，`HashMap采用数组+链表实现`，即使用链表处理冲突，同一hash值的链表都存储在一个链表里。但是当链表中的元素较多，即hash值相等的元素较多时，通过key值依次查找的效率较低。而JDK1.8中，`HashMap采用数组+链表+红黑树实现`，当链表长度超过阈值（8）时，将链表转换为红黑树，这样大大减少了查找时间。

>在HashMap中要找到某个元素，需要根据key的hash值来求得对应数组中的位置。对于任意给定的对象，只要它的hashCode()返回值相同，那么程序调用hash(int h)方法所计算得到的hash码值总是相同的。我们首先想到的就是把hash值对数组长度取模运算，这样一来，元素的分布相对来说是比较均匀的。但是，“模”运算的消耗还是比较大的，在HashMap中，(n - 1) & hash用于计算对象应该保存在table数组的哪个索引处。HashMap底层数组的长度总是2的n次方，当数组长度为2的n次幂的时候，(n - 1) & hash 算得的index相同的几率较小，数据在数组上分布就比较均匀，也就是说碰撞的几率小，相对的，查询的时候就不用遍历某个位置上的链表，这样查询效率也就较高了。

#### 3.2.1 LinkedHashMap 类 ####

LinkedHashMap继承自HashMap，它主要是`用链表实现来扩展HashMap类`，HashMap中条目是没有顺序的，但是在`LinkedHashMap中元素既可以按照它们插入图的顺序排序，也可以按它们最后一次被访问的顺序排序。`

### 3.3 TreeMap 类 ###

`TreeMap基于红黑树数据结构的实现`，键值可以使用Comparable或Comparator接口来排序。TreeMap继承自AbstractMap，同时实现了接口NavigableMap，而接口NavigableMap则继承自SortedMap。SortedMap是Map的子接口，使用它可以确保图中的条目是排好序的。

在实际使用中，`如果更新图时不需要保持图中元素的顺序，就使用HashMap，如果需要保持图中元素的插入顺序或者访问顺序，就使用LinkedHashMap，如果需要使图按照键值排序，就使用TreeMap`。

### 3.4 WeakHashMap 类 ###

WeakHashMap 是一种改进的 HashMap，它对 Key 实行“弱引用”，如果一个 Key 不再被外部所引用，那么该 Key 可以被 GC 回收。

## 4 总结对比 ##

### 4.1 总结 ###
1. Java集合框架主要包括Collection和Map两种类型。其中Collection又有3种子类型，分别是List、Set、Queue。Map中存储的主要是键值对映射。
2. 规则集Set中存储的是不重复的元素，线性表中存储可以包括重复的元素，Queue队列描述的是先进先出的数据结构，可以用LinkedList来实现队列。效率上，规则集比线性表更高效。
3. ArrayList主要是用数组来存储元素，LinkedList主要是用链表来存储元素，HashMap的底层实现主要是借助数组+链表+红黑树来实现。
4. Vector、HashTable等集合类效率比较低但都是线程安全的。包java.util.concurrent下包含了大量线程安全的集合类，效率上有较大提升。
1. List,Set都是继承自Collection接口，Map则不是;
2. List特点：元素有放入顺序，元素可重复;
Set特点：元素无放入顺序，元素不可重复，重复元素会覆盖掉，（注意：元素虽然无放入顺序，但是元素在set中的位置是有该元素的HashCode决定的，其位置其实是固定的，加入Set 的Object必须定义equals()方法;
另外list支持for循环，也就是通过下标来遍历，也可以用迭代器，但是set只能用迭代，因为他无序，无法用下标来取得想要的值）。
3. Set和List对比：
Set：检索元素效率低下，删除和插入效率高，插入和删除不会引起元素位置改变。
List：和数组类似，List可以动态增长，查找元素效率高，插入删除元素效率低，因为会引起其他元素位置改变。
4. Map适合储存键值对的数据。
5. 线程安全集合类与非线程安全集合类
6. LinkedList、ArrayList、HashSet是非线程安全的，Vector是线程安全的;
HashMap是非线程安全的，HashTable是线程安全的;
StringBuilder是非线程安全的，StringBuffer是线程安全的。
7. Collection没有get()方法来取得某个元素。只能通过iterator()遍历元素。Set和Collection拥有一模一样的接口。List，可以通过get()方法来一次取出一个元素。使用数字来选择一堆对象中的一个，get(0)…。(add/get)
8. 一般使用ArrayList。用LinkedList构造堆栈stack、队列queue。
9. Map用 put(k,v) / get(k)，还可以使用containsKey()/containsValue()来检查其中是否含有某个key/value。
HashMap会利用对象的hashCode来快速找到key。
Map中元素，可以将key序列、value序列单独抽取出来。
使用keySet()抽取key序列，将map中的所有keys生成一个Set。
使用values()抽取value序列，将map中的所有values生成一个Collection。
为什么一个生成Set，一个生成Collection？那是因为，key总是独一无二的，value允许重复。

### 4.2 区别和使用场景 ###

#### 4.2.1 ArrayList与LinkedList的区别和适用场景 ####

Arraylist：

优点：ArrayList是实现了基于动态数组的数据结构,因为地址连续，一旦数据存储好了，查询操作效率会比较高（在内存里是连着放的）。
缺点：因为地址连续， ArrayList要移动数据,所以插入和删除操作效率比较低。

LinkedList：

优点：LinkedList基于链表的数据结构,地址是任意的，所以在开辟内存空间的时候不需要等一个连续的地址，对于新增和删除操作add和remove，LinedList比较占优势。LinkedList 适用于要头尾操作或插入指定位置的场景。
缺点：因为LinkedList要移动指针,所以查询操作性能比较低。

适用场景分析：

当需要对数据进行对此访问的情况下选用ArrayList，当需要对数据进行多次增加删除修改时采用LinkedList。

ArrayList与Vector的区别和适用场景

ArrayList有三个构造方法：
```
public ArrayList(int initialCapacity)//构造一个具有指定初始容量的空列表。    
public ArrayList()//构造一个初始容量为10的空列表。    
public ArrayList(Collection<? extends E> c)//构造一个包含指定 collection 的元素的列表   
```
Vector有四个构造方法：
```
public Vector() // 使用指定的初始容量和等于零的容量增量构造一个空向量。    
public Vector(int initialCapacity) // 构造一个空向量，使其内部数据数组的大小，其标准容量增量为零。    
public Vector(Collection<? extends E> c)// 构造一个包含指定 collection 中的元素的向量    
public Vector(int initialCapacity,int capacityIncrement)//使用指定的初始容量和容量增量构造一个空的向量
```
#### 4.2.2 ArrayList和Vector的区别和适用场景 ####
ArrayList和Vector都是用数组实现的，主要有这么三个区别：

1. Vector是多线程安全的，线程安全就是说多线程访问同一代码，不会产生不确定的结果。而ArrayList不是，这个可以从源码中看出，Vector类中的方法很多有synchronized进行修饰，这样就导致了Vector在效率上无法与ArrayList相比；
2. 两个都是采用的线性连续空间存储元素，但是当空间不足的时候，两个类的增加方式是不同。
3. Vector可以设置增长因子，而ArrayList不可以。
4. Vector是一种老的动态数组，是线程同步的，效率很低，一般不赞成使用。

适用场景：

1. Vector是线程同步的，所以它也是线程安全的，而ArrayList是线程异步的，是不安全的。如果不考虑到线程的安全因素，一般用ArrayList效率比较高。
2. 如果集合中的元素的数目大于目前集合数组的长度时，在集合中使用数据量比较大的数据，用Vector有一定的优势。

#### 4.2.3 HashSet与Treeset的适用场景 ####

1. TreeSet 是二叉树（红黑树的树据结构）实现的,Treeset中的数据是自动排好序的，不允许放入null值。
2. HashSet 是哈希表实现的,HashSet中的数据是无序的，可以放入null，但只能放入一个null，两者中的值都不能重复，就如数据库中唯一约束。
3. HashSet要求放入的对象必须实现HashCode()方法，放入的对象，是以hashcode码作为标识的，而具有相同内容的String对象，hashcode是一样，所以放入的内容不能重复。但是同一个类的对象可以放入不同的实例。

适用场景分析:

HashSet是基于Hash算法实现的，其性能通常都优于TreeSet。为快速查找而设计的Set，我们通常都应该使用HashSet，在我们需要排序的功能时，我们才使用TreeSet。

#### 4.2.4 HashMap与TreeMap、HashTable的区别及适用场景 ####

HashMap 非线程安全  
HashMap：基于哈希表(散列表)实现。使用HashMap要求添加的键类明确定义了hashCode()和equals()[可以重写hashCode()和equals()]，为了优化HashMap空间的使用，您可以调优初始容量和负载因子。其中散列表的冲突处理主要分两种，一种是开放定址法，另一种是链表法。HashMap的实现中采用的是链表法。
TreeMap：非线程安全基于红黑树实现。TreeMap没有调优选项，因为该树总处于平衡状态。

适用场景分析：

HashMap和HashTable:HashMap去掉了HashTable的contains方法，但是加上了containsValue()和containsKey()方法。HashTable同步的，而HashMap是非同步的，效率上比HashTable要高。HashMap允许空键值，而HashTable不允许。

HashMap：适用于Map中插入、删除和定位元素。
Treemap：适用于按自然顺序或自定义顺序遍历键(key)。