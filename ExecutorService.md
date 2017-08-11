#### 
```
此接口更确切的说法应该是线程池服务,真正意义的线程池应该是:ThreadPoolExecutor
ThreadPoolExecutor实现了ExecutorService接口，但是由于构造方法过于复杂，所以提供了Executors这个工厂类
```
#### Executors提供的五种功能的线程池
* newFixedThreadPool() -----> LinkedBlockingQueue
* newCachedThreadPool() -------> SynchronousQueue（无界线程池,可以自动回收线程）
* newSingleThreadExecutor() ------> LinkedBlockingQueue
* newScheduledThreadPool()  -------> DelayedWorkQueue
* newSingleThreadScheduledExecutor() -------> DelayedWorkQueue

#### 队列类型
* LinkedBlockingQueue：无界的队列
* SynchronousQueue：直接提交的队列
* DelayedWorkQueue：等待队列
* PriorityBlockingQueue 优先级队列
* ArrayBlockingQueue有界的队列

#### 自定义线程池ThreadPoolExecutor步骤
1. 根据任务类型选择你要用的队列,例如需要优先级的任务，那么选择PriorityBlockingQueue
```
ExecutorService priorityThreadPool = 
new ThreadPoolExecutor(3,3,0L,TimeUnit.SECONDS,new PriorityBlockingQueue());
```
2. 然后创建Runnable接口的类，并向外提供一个抽象方法供我们实现自定义功能，
并实现Comparable接口，实现这个接口主要就是进行优先级的比较，代码如下:
```
public abstract class PriorityRunnable implements Runnable, Comparable {
    private int priority;

    public PriorityRunnable(int priority) {
        if (priority 0)
            throw new IllegalArgumentException();
        this.priority = priority;
    }

    @Override
    public int compareTo(PriorityRunnable another) {
        int my = this.getPriority();
        int other = another.getPriority();
        return my 1 : my > other ? -1 : 0;
    }

    @Override
    public void run() {
        doSth();
    }

    public abstract void doSth();

    public int getPriority() {
        return priority;
    }
}
```
3. 使用如下:
```
ExecutorService priorityThreadPool 
= new ThreadPoolExecutor(3, 3, 0L, TimeUnit.SECONDS, new PriorityBlockingQueue());
        for (int i = 1; i 10; i++) {
            final int priority = i;
            priorityThreadPool.execute(new PriorityRunnable(priority) {
                @Override
                public void doSth() {
                    String threadName = Thread.currentThread().getName();
                    try {
                        Thread.sleep(2000);
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    }
                }
            });
        }
```
#### 优化线程池 通常核心线程数可以设为CPU数量+1，而最大线程数可以设为CPU的数量\2+1*
```
Runtime.getRuntime().availableProcessors();
```


