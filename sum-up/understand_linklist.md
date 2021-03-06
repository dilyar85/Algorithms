# 掌握链表

在熟悉链表后，发现链表是一个很有趣的数据结构，对链表的操作里可以体现出不同的编程思想，如dfs，递归，排序等。本篇主要记录一些典型的关于链表类的题目。

##链表定义

链表是一种常见的数据结构，一般分为单向链表和双向链表。双向链表是在单向链表的基础上多了一个prev节点，用来指向之前元素。与数组类似，搜索链表需要O(n)的时间复杂度，但是链表不能通过常数时间来读取第k个数据。链表的优势能在于以较高的效率在任意位置插入或者
删除一个节点。

## 常用技巧

### dummy node
dummyNode是一个处理链表问题的常用方法，通常将链表的head元素赋给另外的一个值cur后，处理cur的值就相当于处理head，但是对cur我们又能改变其指向，让其指向另外的元素但是head却不受影响。
比如说，对于一个head`1->2->3->4`，如果我们进行如下操作：
```js
let cur = head;
cur.val = 100;
cur = cur.next;
```
我们会发现head最后会变成`100->2>3>4`,cur会是`2->3->4`,通过这种改变cur对象指向的办法我们可以对链表进行层层遍历。


### fast & slow
对于寻找链表的特定位置的题目，我们可以用两个指针变量，如fast和slow，或者right和left来用不同的速度遍历链表，比如我要找到距离表尾k个元素的位置，那我们可以让right前进k个节点，然后再让left和right同时前进，只要right到头了，此时left指向的位置也就是离终点k个位置的节点。除了了这种以外，我们还能用不同速度去访问链表，这样的情况在处理环形链表尤其常见。

### 典型的例题总结

下面有做过的题的一些总结：

>##### 给定一个链表，返回链表中间点

用一倍速度和两倍速度来进行链表遍历，之后再进行第二次遍历即可找到中间点。


> ##### 给定一个可能包含一个环的链表，找到环开始的节点

用一倍速度和两倍速度进行链表遍历，如果有环，两点一定能在某点相遇，相遇后再让某一指针回到顶部，两者再以相同速度前进。可以证明，第二次相遇的位置就是环的节点。

> ##### 给定一个链表，交换两个相邻的位置

对于交换节点的问题，可以采取的策略是
- 先交换两个前驱节点的next指针的值
- 再交换这两个节点的next指针的值
无论两个节点的相对位置和绝对位置如何，以上方式总成立。

> ##### 合并两个sort链表

先处理常规情况，就是`while(l1&&l2)`,再处理特殊情况，比如一个链表已经为空，另一个链表还存在的时候。

> ##### 相加两个链表，分别从正序或者倒序

对于正序来说，即
（1-> 7 -> 6) 和 （2->5->6) 等于（3->2->3->1) 我们顺序遍历，用常规方法即可
对于倒序来说，可以栈的思想去处理。

> ##### 重组链表，从` L: L0→L1→…→Ln-1→Ln,`修改为`L0→Ln→L1→Ln-1→L2→Ln-2→…`

- 先用不同倍速遍历链表找到链表中间值middle，
- 截取middle之后的链表部分并翻转
- 合并两个链表。
