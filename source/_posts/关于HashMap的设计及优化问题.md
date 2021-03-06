---
title: 关于HashMap的设计及优化问题
date: 2020-05-27 20:39:04
tags: HashMap
cover: static/bgpic/luis-paico-NNTGEoohoE4-unsplash.jpg
---

-    - ##### JDK1.8中对hash算法和寻址算法的优化
         - 优化一 hash算法： 
     ``` hash值的位运算+异或运算（^）保证低位二进制数据包含高低位数据的特征，一定程度上避免后续运算hash碰撞而计算出相同的数组下标 ```
         - 优化二 寻址算法：
         ```  寻址时对hash值取模性能较低，改用位与运算提高性能。hash &(n-1)（优化后所得哈希值和n-1做与运算--n数组长度为2的n次幂）```
          
         ##### HashMap如何解决hash碰撞问题
         - ###### 问题原因：
             map.get()、map.set()都是算出key的hash值，到数组中寻址，放入或者取出key-value对，在寻址时，根据键算出的hash值与（n-1）^keyHash（相当于取模，位运算提高性能）寻址确定。该动作可能会产生hash冲突，不同键值对运算后可能得到相同的数组地址。
         - ###### 解决方式
             存放数据时，在寻址后具有相同位置的地方挂一个链表存放元素；取数据定位到数组时若存在链表则遍历链表，查找对应的key取值。
          -- 链表长度过长时，遍历时间复杂度为O(n)；链表达到一定长度后，会将链表转换为红黑树，红黑树遍历查找一个元素的时间复杂度为O（logn）,性能通链表。
         ##### HashMap的扩容
            - ###### rehash双倍扩容     
         ##### ConcurrentHashMap实现线程安全的底层原理
             - ###### 
        
       - 
       
         ![1591270893261](C:\Users\JP\AppData\Roaming\Typora\typora-user-images\1591270893261.png)