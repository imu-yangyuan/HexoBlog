---
title: Linux命令
date: 2018-10-30 20:00:00
tags: linux
---
## sort
### 常用参数
-  -n ： 依照数值的大小排序。(不加-n参数，默认按照字符ASSII码的排序 会出现如（1,11,2,3..）这样的排序)
-  -k 指定按某一列排序 从1开始。
-  -r: 以相反的顺序来排序。(默认是从小到大，加上-r即从大到小)
---
- -t 设定分隔符,使用指定的分隔符代替非空格到空格的转换
- -b   忽略每行前面开始出的空格字符。
- -c   检查文件是否已经按照顺序排序。
- -d   排序时，处理英文字母、数字及空格字符外，忽略其他的字符。
- -f   排序时，将小写字母视为大写字母。
- -i   排序时，除了040至176之间的ASCII字符外，忽略其他的字符。
- -m   将几个排序好的文件进行合并。
- -M   将前面3个字母依照月份的缩写进行排序。
- -o<输出文件>   将排序后的结果存入指定的文件。
- +<起始栏位>-<结束栏位>   以指定的栏位来排序，范围由起始栏位到结束栏位的前一栏位。
sort -n -k 2 -t'-' test.txt
```
//原来的内容
[root@h2 ~]# cat test.txt
2018-12-01
2013-01-08
2015-10-24
2016-04-25

[root@h2 ~]# sort -nk2 -t'-' test.txt
2013-01-08
2016-04-25
2015-10-24
2018-12-01

```

## head
head用于显示文件的开头的内容。在默认情况下，head命令显示文件的头10行内容。
- -n<数字> --lines=[-]K	 ：指定显示头部内容的行数；如果附加"-"参数，则除了每个文件的最后K 行外显示
                     			剩余全部内容
- -v：总是显示文件名的头信息；
- -q：不显示文件名的头信息。
- -c,  --bytes=[-]K    显示每个文件的前K 字节内容

## uniq
只过滤相邻的重复行。
- -c, --count		在每行前加上表示相应行目出现次数的前缀编号

## find
- find base_path 列出当前目录和子目录下的所有文件和文件夹
- find path -name '*txt' 根据文件名或者正则表达式匹配搜索
- find path -iname '*txt' 同上，忽略大小写
- find path ! -name '*txt' 对上面的搜索结果取反
- find path -type d 根据文件类型搜索，d文件夹，f普通文件，etc
- find path -type f -size +2k 根据文件大小搜索，+2k大于2k的文件，-2k小于2k的文件，2k等你2k的文件
- find path -type f -name '*txt' -delete 删除匹配到的文件
- find path -mtime -2 查找文件更新日时在距现在时刻二天以内的文件
- find path -mtime +2 查找文件更新日时在距现在时刻二天以上的文件
- find path -mtime 2 查找文件更新日时在距现在时刻一天以上二天以内的文件
- find path -mmin -2 查找文件更新日时在距现在时刻二分以内的文件
- find path -mmin +2 查找文件更新日时在距现在时刻二分以上的文件
- find path -mmin 2 查找文件更新日时在距现在时刻一分以上二分以内的文件
- find path -perm 664 查找权限为664的文件或目录(需完全符合)
- find path -empty 查找空文件或空目录
- find path -empty -type f -print -delete查找空文件并删除
- find path -size -10c 查找文件size小于10个字节的文件或目录
- find path -size 10c 查找文件size等于10个字节的文件或目录
- find path -size +10c 查找文件size大于10个字节的文件或目录
- find path -size -10k 查找文件size小于10k的文件或目录
- find path -size -10M 查找文件size小于10M的文件或目录
- find path -size -10G 查找文件size小于10G的文件或目录