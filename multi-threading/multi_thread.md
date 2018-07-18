iOS多线程

## 目的

本文主要是分享iOS多线程的相关内容，为了更系统的讲解，将分为以下7个方面来展开描述。

1 多线程的基本概念
2 线程的状态与生命周期
3 多线程的四种解决方案：pthread，NSThread，GCD，NSOperation
4 线程安全问题
5 NSThread的使用
6 GCD的理解与使用
7 NSOperation的理解与使用


## 一、多线程的基本概念

* 进程：可以理解成一个运行中的应用程序，是系统进行资源分配和调度的基本单位，是操作系统结构的基础，主要管理资源。
* 线程：是进程的基本执行单元，一个进程对应多个线程。
* 主线程：处理UI，所有更新UI的操作都必须在主线程上执行。不要把耗时操作放在主线程，会卡界面。
* 多线程：在同一时刻，一个CPU只能处理1条线程，但CPU可以在多条线程之间快速的切换，只要切换的足够快，就造成了多线程一同执行的假象。
* 线程就像火车的一节车厢，进程则是火车。车厢（线程）离开火车（进程）是无法跑动的，而火车（进程）至少有一节车厢（主线程）。多线程可以看做多个车厢，它的出现是为了提高效率。
* 多线程是通过提高资源使用率来提高系统总体的效率。
* 我们运用多线程的目的是：将耗时的操作放在后台执行！
## 二、线程的状态与生命周期

下图是线程状态示意图，从图中可以看出线程的生命周期是：新建 - 就绪 - 运行 - 阻塞 - 死亡

![线程状态](http://cc.cocimg.com/api/uploads/20170707/1499394752139363.png)

下面分别阐述线程生命周期中的每一步

* 新建：实例化线程对象
* 就绪：向线程对象发送start消息，线程对象被加入可调度线程池等待CPU调度。
* 运行：CPU 负责调度可调度线程池中线程的执行。线程执行完成之前，状态可能会在就绪和运行之间来回切换。就绪和运行之间的状态变化由CPU负责，程序员不能干预。
* 阻塞：当满足某个预定条件时，可以使用休眠或锁，阻塞线程执行。sleepForTimeInterval（休眠指定时长），sleepUntilDate（休眠到指定日期），@synchronized(self)：（互斥锁）。
* 死亡：正常死亡，线程执行完毕。非正常死亡，当满足某个条件后，在线程内部中止执行/在主线程中止线程对象
还有线程的exit和cancel
* [NSThread exit]：一旦强行终止线程，后续的所有代码都不会被执行。
* [thread cancel]取消：并不会直接取消线程，只是给线程对象添加 isCancelled 标记。

## 三、多线程的四种解决方案

多线程的四种解决方案分别是：pthread，NSThread，GCD， NSOperation。

下图是对这四种方案进行了解读和对比。

![对比](http://cc.cocimg.com/api/uploads/20170707/1499394732413995.png)

## 四、线程安全问题

当多个线程访问同一块资源时，很容易引发数据错乱和数据安全问题。就好比几个人在同一时修改同一个表格，造成数据的错乱。

解决多线程安全问题的方法

* 方法一：互斥锁（同步锁）

```
@synchronized(锁对象) {
    // 需要锁定的代码
}
```

判断的时候锁对象要存在，如果代码中只有一个地方需要加锁，大多都使用self作为锁对象，这样可以避免单独再创建一个锁对象。

加了互斥做的代码，当新线程访问时，如果发现其他线程正在执行锁定的代码，新线程就会进入休眠。


* 方法二：自旋锁
加了自旋锁，当新线程访问代码时，如果发现有其他线程正在锁定代码，新线程会用死循环的方式，一直等待锁定的代码执行完成。相当于不停尝试执行代码，比较消耗性能。

属性修饰atomic本身就有一把自旋锁。

下面说一下属性修饰nonatomic 和 atomic

```
nonatomic 非原子属性,同一时间可以有很多线程读和写
atomic 原子属性(线程安全)，保证同一时间只有一个线程能够写入(但是同一个时间多个线程都可以取值)，atomic 本身就有一把锁(自旋锁)
atomic：线程安全，需要消耗大量的资源
nonatomic：非线程安全，不过效率更高，一般使用nonatomic
```

## 五、NSThread的使用

### No.1：NSThread创建线程

NSThread有三种创建方式：

* init方式
* detachNewThreadSelector创建好之后自动启动
* performSelectorInBackground创建好之后也是直接启动

```
/** 方法一，需要start */
NSThread *thread1 = [[NSThread alloc] initWithTarget:self selector:@selector(doSomething1:) object:@"NSThread1"];
// 线程加入线程池等待CPU调度，时间很快，几乎是立刻执行
[thread1 start];
 
/** 方法二，创建好之后自动启动 */
[NSThread detachNewThreadSelector:@selector(doSomething2:) toTarget:self withObject:@"NSThread2"];
 
/** 方法三，隐式创建，直接启动 */
[self performSelectorInBackground:@selector(doSomething3:) withObject:@"NSThread3"];
 
- (void)doSomething1:(NSObject *)object {
    // 传递过来的参数
    NSLog(@"%@",object);
    NSLog(@"doSomething1：%@",[NSThread currentThread]);
}
 
- (void)doSomething2:(NSObject *)object {
    NSLog(@"%@",object);
    NSLog(@"doSomething2：%@",[NSThread currentThread]);
}
 
- (void)doSomething3:(NSObject *)object {
    NSLog(@"%@",object);
    NSLog(@"doSomething3：%@",[NSThread currentThread]);
}
```

### No.2：NSThread的类方法

* 返回当前线程

```
// 当前线程
[NSThread currentThread];
NSLog(@"%@",[NSThread currentThread]);
 
// 如果number=1，则表示在主线程，否则是子线程
打印结果：{number = 1, name = main}
```

* 阻塞休眠

```
//休眠多久
[NSThread sleepForTimeInterval:2];
//休眠到指定时间
[NSThread sleepUntilDate:[NSDate date]];
```

* 类方法补充

```
//退出线程
[NSThread exit];
//判断当前线程是否为主线程
[NSThread isMainThread];
//判断当前线程是否是多线程
[NSThread isMultiThreaded];
//主线程的对象
NSThread *mainThread = [NSThread mainThread];
```

### No.3：NSThread的一些属性

```
//线程是否在执行
thread.isExecuting;
//线程是否被取消
thread.isCancelled;
//线程是否完成
thread.isFinished;
//是否是主线程
thread.isMainThread;
//线程的优先级，取值范围0.0到1.0，默认优先级0.5，1.0表示最高优先级，优先级高，CPU调度的频率高
 thread.threadPriority;
```


## 六、GCD的理解与使用

### No.1：GCD的特点

* GCD会自动利用更多的CPU内核
* GCD自动管理线程的生命周期（创建线程，调度任务，销毁线程等）
* 程序员只需要告诉 GCD 想要如何执行什么任务，不需要编写任何线程管理代码

### No.2：GCD的基本概念

* 任务（block）：任务就是将要在线程中执行的代码，将这段代码用block封装好，然后将这个任务添加到指定的执行方式（同步执行和异步执行），等待CPU从队列中取出任务放到对应的线程中执行。
* 同步（sync）：一个接着一个，前一个没有执行完，后面不能执行，不开线程。
* 异步（async）：开启多个新线程，任务同一时间可以一起执行。异步是多线程的代名词
* 队列：装载线程任务的队形结构。(系统以先进先出的方式调度队列中的任务执行)。在GCD中有两种队列：串行队列和并发队列。
* 并发队列：线程可以同时一起进行执行。实际上是CPU在多条线程之间快速的切换。（并发功能只有在异步（dispatch_async）函数下才有效）
* 串行队列：线程只能依次有序的执行。
* GCD总结：将任务(要在线程中执行的操作block)添加到队列(自己创建或使用全局并发队列)，并且指定执行任务的方式(异步dispatch_async，同步dispatch_sync)

### No.3：队列的创建方法

* 使用dispatch_queue_create来创建队列对象，传入两个参数，第一个参数表示队列的唯一标识符，可为空。第二个参数用来表示串行队列（DISPATCH_QUEUE_SERIAL）或并发队列（DISPATCH_QUEUE_CONCURRENT）。

```
/ 串行队列
dispatch_queue_t queue = dispatch_queue_create("test", DISPATCH_QUEUE_SERIAL);
// 并发队列
dispatch_queue_t queue1 = dispatch_queue_create("test", DISPATCH_QUEUE_CONCURRENT);
```

* GCD的队列还有另外两种

主队列：主队列负责在主线程上调度任务，如果在主线程上已经有任务正在执行，主队列会等到主线程空闲后再调度任务。通常是返回主线程更新UI的时候使用。dispatch_get_main_queue()

```
dispatch_async(dispatch_get_global_queue(0, 0), ^{
      // 耗时操作放在这里
      
      dispatch_async(dispatch_get_main_queue(), ^{
          // 回到主线程进行UI操作

      });
  });
```
全局并发队列：全局并发队列是就是一个并发队列，是为了让我们更方便的使用多线程。
dispatch_get_global_queue(0, 0)

```
//全局并发队列
dispatch_queue_t queue = dispatch_get_global_queue(DISPATCH_QUEUE_PRIORITY_DEFAULT, 0);
//全局并发队列的优先级
#define DISPATCH_QUEUE_PRIORITY_HIGH 2 // 高优先级
#define DISPATCH_QUEUE_PRIORITY_DEFAULT 0 // 默认（中）优先级
#define DISPATCH_QUEUE_PRIORITY_LOW (-2) // 低优先级
#define DISPATCH_QUEUE_PRIORITY_BACKGROUND INT16_MIN // 后台优先级
//iOS8开始使用服务质量，现在获取全局并发队列时，可以直接传0
dispatch_get_global_queue(0, 0);
```

### No.4：同步/异步/任务、创建方式

同步（sync）使用dispatch_sync来表示。

异步（async）使用dispatch_async。

任务就是将要在线程中执行的代码，将这段代码用block封装好。

代码如下：

```
// 同步执行任务
    dispatch_sync(dispatch_get_global_queue(0, 0), ^{
        // 任务放在这个block里
        NSLog(@"我是同步执行的任务");
 
    });
    // 异步执行任务
    dispatch_async(dispatch_get_global_queue(0, 0), ^{
        // 任务放在这个block里
        NSLog(@"我是异步执行的任务");
 
    });
```









