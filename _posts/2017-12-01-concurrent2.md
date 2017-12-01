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
