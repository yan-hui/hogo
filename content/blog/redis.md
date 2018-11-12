---
title: "Redis"
date: 2018-10-17T15:47:34+08:00
draft: false
---

>**特点**

>>1. redis支持数据的持久化，可将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用

>>2. 支持key-value类型的数据，还提供list、set、zset、hash等数据结构的存储

>>3. 支持数据的备份，即master-slave模式的数据备份

>**优势**

>>1. 性能极高，读的次数能达110000次/s，写的数据达81000次/s
>>2. 丰富的数据类型。Redis支持二进制案例的Strings,Lists，Hashes,Sets以及Ordered Sets数据类型操作
>>3. 原子性。操作要么完全执行要么完全不执行，通过MULTI和EXEC指令包起来
>>4. 丰富的特性。Redis还支持publish/subscribe,通知key过期等特征

>**运行**

>>1. 命令行切换到redis目录下，执行</br>
```redis-server.exe redis.windows.conf```
>>2. 重新新开一个命令行，在redis目录下执行</br>
```redis-cli.exe -h 127.0.0.1 -p 6379```
>>3. 设置键值对: ```set myKey asd```
>>4. 取出键值对：```get myKey```
