---
title: Java 线程池关闭
date: 2019-02-19 20:10:03
tags:
---
```
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
```