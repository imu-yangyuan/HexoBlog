---
title: Linux常用命令
date: 2018-10-31 21:00:00
tags:
---
- **<font color=#000 face="微软雅黑">查看使用内存最多的10个进程</font>**

- ps -aux | sort -k4nr | head -n 10
- top （然后按下M，注意大写）

- **<font color=#000 face="微软雅黑">查看使用CPU最多的10个进程</font>**

- ps -aux | sort -k3nr | head -n 10
- top （<font color=#FF0000 face="微软雅黑">然后按下P，注意大写</font>)
 ---
 ps命令参数解释
 ```
 -a ： 显示现行终端机下的所有进程，包括其他用户的进程；
 -u ： 以用户为主的进程状态 ；
 x ： 通常与 a 这个参数一起使用，可列出较完整信息。
```
 ## 查看网卡流量
 - watch more /proc/net/dev  可以查看每2秒的字节和数据包的变化
