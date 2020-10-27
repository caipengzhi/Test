## 创建线程的方式不同会导致使用synchronized产生的结果不同
  MyThread t = new MyThread();
 * Thread t1 = new Thread(t);
 * Thread t2 = new Thread(t);
 * Thread t3 = new Thread(t);
 * new Thread()中调用同一个实现Runnable实例对象时，不同线程共享同一个资源
 * 在线程可以被阻塞时可能发生重复读和超读
 * 在方法上加synchronized，非静态有效
 * 在代码块上加synchronized(object、this、MyThread.class),非静态有效
 *
 * Thread t1 = new Thread(new MyThread());
 * Thread t2 = new Thread(new MyThread());
 * Thread t3 = new Thread(new MyThread());
 * 创建线程时使用了新的Runnable实例，不同线程的资源是独立的。Runnable中的资源是静态时，多个线程共享资源。
 * 在线程可以被阻塞时可能发生重复读和超读
 * 在方法上加synchronized，非静态与静态均无效
 * 在代码块上加synchronized(object、this)，静态与非静态无效
 * 使用synchronized(MyThread.class)，静态有效，非静态无效
