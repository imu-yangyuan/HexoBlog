---
title: Java创建Listener
date: 2019-02-18 19:05:47
tags:
    - Java
---

```
import java.util.concurrent.Executors;
import java.util.concurrent.ScheduledExecutorService;
import java.util.concurrent.TimeUnit;

public class Listener implements Runnable{
    private ScheduledExecutorService scheduledExecutorService;
    private static final int DEFAULT_INTERVAL = 100000;

    public Listener() {
        int interval = DEFAULT_INTERVAL;
        this.scheduledExecutorService = Executors.newSingleThreadScheduledExecutor();
        scheduledExecutorService.scheduleWithFixedDelay(this, 0, interval, TimeUnit.MILLISECONDS);
    }

    @Override
    public void run() {
        Thread.currentThread().setName("XXXListener");
        System.out.println("exec check data.");
    }
    public void close() {
        if (scheduledExecutorService != null) {
            scheduledExecutorService.shutdown();
            try {
                if (!scheduledExecutorService.awaitTermination(10, TimeUnit.SECONDS)) {
                    scheduledExecutorService.shutdownNow();
                }
            } catch (InterruptedException e) {
                scheduledExecutorService.shutdownNow();
            }
            scheduledExecutorService = null;
        }
    }
}

```