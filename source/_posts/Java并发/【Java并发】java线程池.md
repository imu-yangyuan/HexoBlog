---
title: 【Java并发】java线程池
date: 2019-02-19 17:20:56
tags:
---
## 1. Executor
- Executor是线程池的顶级接口，只有一个方法execute()
- ExecutorService是Executor的子接口，提供了线程池生命周期管理的方法，一个可跟踪一个或多个异步任务执行情况返回Future的方法。

|方法|功能描述|
|-----|---|
|execute()|执行任务|
|shutdown()|调用后不再接收新任务，如果里面有任务，就执行完|
|shutdownNow()|调用后不再接收新任务，取消等待中的任务，返回等待执行的任务的list；有正在执行的任务，会尝试停止|
|isShutdown()|判断线程池是否完全停止|
|isTerminated()|判断线程池有任务在执行|
|submit()|提交带返回值的任务，返回值封装到Future中，通过Future.get()可以获取返回值|
|invokeAll()|执行一组任务|

## 2. ThreadPoolExecutor
### 2.1 构造方法
```
public ThreadPoolExecutor(
    int corePoolSize, //核心线程数
    int maximumPoolSize, //最大线程数
    long keepAliveTime, //保持存活时间
    TimeUnit unit, //时间单位
    BlockingQueue<Runnable> workQueue, //阻塞队列
    ThreadFactory threadFactory, //线程工厂
    RejectedExecutionHandler handler //异常捕获器
)
```
### 2.2 TimeUnit unit

参数keepAliveTime的时间单位，有7种取值
- TimeUnit.DAYS //天
- TimeUnit.HOURS //小时
- TimeUnit.MINUTES //分钟
- TimeUnit.SECONDS //秒
- TimeUnit.MILLISECONDS //毫秒
- TimeUnit.MICROSECONDS //微妙
- TimeUnit.NANOSECONDS //纳秒
### 2.3 keepAliveTime
当线程空闲时，所允许保存的最大时间，超过这个时间，线程将被释放销毁，但只针对于非核心线程。
## 3. 阻塞队列
### 3.1 BlockingQueue
|阻塞队列	          | 功能描述 |
|---|---|
|BlockingQueue	      | 阻塞队列的顶级接口，主要用于实现生产者消费者队列  |
|BlockingDeque	      | 双端队列  |
|SynchronousQueue	  | 同步队列，无界队列，直接提交策略，交替队列，在某次添加元素后必须等待其他线程取走后才能继续添加  |
|LinkedBlockingQueue   | 无界队列，基于链表的阻塞队列，可以并发运行，FIFO    |
|ArrayBlockingQueue	  | 基于数组的有界(固定大小的数组)阻塞队列，只有put方法和take方法才具有阻塞功能，公平性 fairness  |
|PriorityBlockingQueue |  基于优先级的阻塞队列，依据对象的自然排序顺序或者是构造函数所带的Comparator决定的顺序           |
|DelayQueue	          |  延时队列|
## 4. 线程池工具类Executors
|方法	|功能描述|
|---|---|
|newCachedThreadPool()	|创建一个可缓存的线程池|
|newFixedThreadPool()	|创建一个定长线程池，可控制线程最大并发数，超出的线程会在队列中等待|
|newScheduledThreadPool()|	创建一个定长线程池，支持定时及周期性任务执行。|
|newSingleThreadExecutor()|	创建单线程化线程池，始终保证线程池中会有一个线程在。当某线程死去，会找继任者|
|defaultThreadFactory()	|创建一个默认线程池工厂|