---
layout: post
title: java并发编程详解之核心理论
categories: java知识
---
<u>【原文链接】(http://www.cnblogs.com/paddix/p/5374810.html)</u>

并发编程是Java程序员最重要的技能之一，也是最难掌握的一种技能。它要求编程者对计算机最底层的运作原理有深刻的理解，同时要求编程者逻辑清晰、思维缜密，这样才能写出高效、安全、可靠的多线程并发程序。

## 1 共享性 ##

`数据共享性是线程安全的主要原因之一`。如果所有的数据只是在线程内有效，那就不存在线程安全性问题，这也是我们在编程的时候经常不需要考虑线程安全的主要原因之一。但是，在多线程编程中，数据共享是不可避免的。最典型的场景是数据库中的数据，为了保证数据的一致性，我们通常需要共享同一个数据库中数据，即使是在主从的情况下，访问的也同一份数据，主从只是为了访问的效率和数据安全，而对同一份数据做的副本。我们现在，通过一个简单的示例来演示多线程下共享数据导致的问题：

```java
public class TestJava {
    //被多个线程共享的资源
    public static int count = 0;

    public static void main(String[] args) {
        final TestJava data = new TestJava();
        for (int i = 0; i < 10; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    try {
                        //进入的时候暂停1毫秒，增加并发问题出现的几率
                        Thread.sleep(1);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    for (int j = 0; j < 100; j++) {
                        data.addCount();
                    }
                    System.out.print(count + " ");
                }
            }).start();
        }
        try {
            //主程序暂停3秒，以保证上面的程序执行完成
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("count=" + count);
    }

    public void addCount() {
        count++;
    }
}
```

上述代码的目的是对count进行加一操作，执行1000次，不过这里是通过10个线程来实现的，每个线程执行100次，正常情况下，应该输出1000。不过，如果你运行上面的程序，你会发现结果却不是这样。下面是某次的执行结果（每次运行的结果不一定相同，有时候也可能获取到正确的结果）：
![](https://raw.githubusercontent.com/ADeveloperH/ADeveloperH.github.io/master/assets/20171201/01.png)

可以看出，对共享变量操作，在多线程环境下很容易出现各种意想不到的的结果。

## 2 互斥性 ##

`资源互斥是指同时只允许一个访问者对其进行访问，具有唯一性和排它性`。我们`通常允许多个线程同时对数据进行读操作，但同一时间内只允许一个线程对数据进行写操作`。所以我们通常将锁分为共享锁和排它锁，也叫做读锁和写锁。如果资源不具有互斥性，即使是共享资源，我们也不需要担心线程安全。例如，对于不可变的数据共享，所有线程都只能对其进行读操作，所以不用考虑线程安全问题。但是对共享数据的写操作，一般就需要保证互斥性，上述例子中就是因为没有保证互斥性才导致数据的修改产生问题。Java 中提供多种机制来保证互斥性，最简单的方式是使用Synchronized。现在我们在上面程序中加上Synchronized再执行：
```java
public class TestJava {

    public static int count = 0;

    public static void main(String[] args) {
        final TestJava data = new TestJava();
        for (int i = 0; i < 10; i++) {
            new Thread(new Runnable() {
                @Override
                public void run() {
                    try {
                        //进入的时候暂停1毫秒，增加并发问题出现的几率
                        Thread.sleep(1);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                    for (int j = 0; j < 100; j++) {
                        data.addCount();
                    }
                    System.out.print(count + " ");
                }
            }).start();
        }
        try {
            //主程序暂停3秒，以保证上面的程序执行完成
            Thread.sleep(3000);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("count=" + count);
    }

    public synchronized void addCount() {
        count++;
    }
}
```

现在再执行上述代码，会发现无论执行多少次，返回的最终结果都是1000。
![](https://raw.githubusercontent.com/ADeveloperH/ADeveloperH.github.io/master/assets/20171201/02.png)

## 3 原子性 ##

原子性就是指对数据的操作是一个独立的、不可分割的整体。换句话说，就是一次操作，`是一个连续不可中断的过程，数据不会执行的一半的时候被其他线程所修改`。保证原子性的最简单方式是操作系统指令，就是说如果一次操作对应一条操作系统指令，这样肯定可以能保证原子性。但是很多操作不能通过一条指令就完成。例如，对long类型的运算，很多系统就需要分成多条指令分别对高位和低位进行操作才能完成。还比如，我们经常使用的整数 i++ 的操作，其实需要分成三个步骤：（1）读取整数 i 的值；（2）对 i 进行加一操作；（3）将结果写回内存。这个过程在多线程下就可能出现如下现象：

![](https://raw.githubusercontent.com/ADeveloperH/ADeveloperH.github.io/master/assets/20171201/03.png)

这也是代码段一执行的结果为什么不正确的原因。对于这种组合操作，要保证原子性，最常见的方式是加锁，如Java中的Synchronized或Lock都可以实现，代码段二就是通过Synchronized实现的。除了锁以外，还有一种方式就是CAS（Compare And Swap），即修改数据之前先比较与之前读取到的值是否一致，如果一致，则进行修改，如果不一致则重新执行，这也是乐观锁的实现原理。不过CAS在某些场景下不一定有效，比如另一线程先修改了某个值，然后再改回原来值，这种情况下，CAS是无法判断的。

## 4 可见性 ##

要理解可见性，需要先对JVM的内存模型有一定的了解，JVM的内存模型与操作系统类似，如图所示：

![](https://raw.githubusercontent.com/ADeveloperH/ADeveloperH.github.io/master/assets/20171201/04.png)

从这个图中我们可以看出，`每个线程都有一个自己的工作内存`（相当于CPU高级缓冲区，这么做的目的还是在于进一步缩小存储系统与CPU之间速度的差异，提高性能），对于共享变量，线程每次读取的是工作内存中共享变量的副本，写入的时候也直接修改工作内存中副本的值，然后在某个时间点上再将工作内存与主内存中的值进行同步。这样导致的问题是，如果线程1对某个变量进行了修改，线程2却有可能看不到线程1对共享变量所做的修改。通过下面这段程序我们可以演示一下不可见的问题：

```java
public class TestJava {
    private static boolean ready;
    private static int number;

    private static class WriterThread extends Thread {
        public void run() {
            try {
                Thread.sleep(10);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            number = 100;
            ready = true;
        }
    }

    private static class ReaderThread extends Thread {
        public void run() {
            try {
                Thread.sleep(10);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            if (!ready) {
                System.out.println(ready);
            }
            System.out.println(number);
        }
    }

    public static void main(String[] args) {
        new WriterThread().start();
        new ReaderThread().start();
    }
}
```

从直观上理解，这段程序应该只会输出100，ready的值是不会打印出来的。实际上，如果多次执行上面代码的话，可能会出现多种不同的结果，下面是我运行出来的某两次的结果：
