#### HashTable vs HashMap
* 继承不同 HashTable继承自Dictionary, HashMap继承自 AbstractMap
* HashTable线程安全,HashMap非线程安全
* 对null处理 HashTable 不允许null(key和value均不可以) HashMap 允许 null(key和value都可以)
* 增长率不同 HashTable中hash数组默认大小是11，增加的方式是 old*2+1。HashMap中hash数组的默认大小是16，而且一定是2的指数
* HashTable使用Enumeration，HashMap使用Iterator
* hashCode 不同 HashTable直接使用对象的hashCode
