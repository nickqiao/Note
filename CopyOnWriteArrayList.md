#### 读多写少 
####  CopyOnWriteArrayList的另一个使用案例是观察者设计模式。
  如果事件监听器由多个不同的线程添加和移除，那么使用CopyOnWriteArrayList将会使得正确性和简单性得以保证
