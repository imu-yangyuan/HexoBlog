---
title: 【Java并发】Java多线程Future的使用
date: 2018-10-17 17:07:10
tags: java并发
---
## Future模式简述
- 在传统单线程环境下，调用函数是同步的，必须等待程序返回结果后，才可进行其他处理。
- Future模式下，调用方式改为异步。
- Future模式的核心在于：充分利用主函数中的等待时间，利用等待时间处理其他任务，充分利用计算资源
示例代码：

```java
import java.util.concurrent.Callable;

public class ManipulationDataTask implements Callable<String> {
    private String data;

    public ManipulationDataTask(String data) {
        this.data = data;
    }

    @Override
    public String call() throws Exception {
        String data1 = data.toUpperCase();
        System.out.println(Thread.currentThread().getName() + "业务处理线程处理中...");
        Thread.sleep(1000);
        System.out.println(Thread.currentThread().getName() + "业务处理线程处理完成,处理好的数据为" + data1);
        return data1;
    }
}
```

```java
import java.util.concurrent.ExecutionException;
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;
import java.util.concurrent.Future;
import java.util.concurrent.FutureTask;

public class MainTest {
    public static void main(String[] args) throws InterruptedException, ExecutionException {

        FutureTask<String> future1 = new FutureTask<String>(new ManipulationDataTask("abc"));
        FutureTask<String> future2 = new FutureTask<String>(new ManipulationDataTask("def"));
        FutureTask<String> future3 = new FutureTask<String>(new ManipulationDataTask("ghi"));
        ManipulationDataTask manipulationDataTask = new ManipulationDataTask("jkl");
        ExecutorService executor = Executors.newFixedThreadPool(3);
        executor.submit(future1);
        executor.submit(future2);
        executor.submit(future3);
        Future<String> future4 =executor.submit(manipulationDataTask);
        System.out.println("请求完毕！");
        try {
            System.out.println("主线程先去做点别的事");
            Thread.sleep(5000);
            System.out.println("主线程的事情做完了");
        } catch (InterruptedException e) {

        }
        System.out.println("主线程开始获取子任务处理完的结果");
        System.out.println("数据处理完成：" + future1.get());
        System.out.println("数据处理完成：" + future2.get());
        System.out.println("数据处理完成：" + future3.get());
        System.out.println("数据处理完成：" + future4.get());
        executor.shutdown();
    }
}


```

#### 程序运行结果：
```
请求完毕！
主线程先去做点别的事
pool-1-thread-1业务处理线程处理中...
pool-1-thread-2业务处理线程处理中...
pool-1-thread-3业务处理线程处理中...
pool-1-thread-1业务处理线程处理完成,处理好的数据为ABC
pool-1-thread-1业务处理线程处理中...
pool-1-thread-2业务处理线程处理完成,处理好的数据为DEF
pool-1-thread-3业务处理线程处理完成,处理好的数据为GHI
pool-1-thread-1业务处理线程处理完成,处理好的数据为JKL
主线程的事情做完了
主线程开始获取子任务处理完的结果
数据处理完成：ABC
数据处理完成：DEF
数据处理完成：GHI
数据处理完成：JKL
```