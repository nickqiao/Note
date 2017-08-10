#### ArrayMap vs HashMap
ArrayMap用两个数组模拟Map,第一个数组存放item的hash值,第二个数组把key,value连续存放在数组里
通过先算hash在第一个数组里找到它的hash index(二分查找)，根据这个index在去第二个数组里找到这个key-value
* 优点 这个数据结构的设计就做到了，有多个item我就分配多少内存，做到了memory的节约。
  并且因为数据结构是通过数组组织的，所以遍历的时候可以用index直接遍历也是很方便的有没有！。
* 缺点 查找达不到HashMap O(1)的查找时间
