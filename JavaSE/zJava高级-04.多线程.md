#### 1.进程与线程

> 进程：正在运行的程序，负责了这个程序的内存空间分配，代表了内存中的执行区域;
>
> 线程：就是在一个进程中负责一个执行路径;线程被称作轻量级进程 ;
>
> 多线程：就是在一个进程中多个执行路径同时执行;
>
> 并发性:在同一时刻,只用一个处理器,所有最多只有一个指令在执行,由于现在处理器性能很高,使得多个指令快速轮播执行,宏观上看上去是多个指令同时执行;
>
> 并行性:在同一时刻,多个指令在多个处理器上同时执行;
>
> 多线程的好处:
>
> ~~~
> (1).解决了一个进程里面可以同时运行多个任务（执行路径）;
> (2).提供资源的利用率，而不是提供效率;
> ~~~
>
> 多线程的弊端:
>
> ~~~
> (1).降低了一个进程里面的线程的执行频率。
> (2).对线程进行管理要求额外的 CPU开销。线程的使用会给系统带来上下文切换的额外负担。
> (3).公有变量的同时读或写。当多个线程需要对公有变量进行写操作时,后一个线程往往会修改掉前一个线程存放的数据，发生线程安全问题。
> (4).线程的死锁。即较长时间的等待或资源竞争以及死锁等多线程症状。
> ~~~

#### 2.线程的生命周期



![img](https://images0.cnblogs.com/i/426802/201406/232002051747387.jpg)

> 线程与状态相关的方法:

~~~java
（1）start();//线程处于就绪状态,等待抢占CPU时间片，抢到了就能执行run方法
（2）run()://线程的核心工作任务，说明该线程处于运行状态，若单独调用run,thread.run(),就不存在多线程，是单线程顺序执行，run方法成为普通方法
（3）sleep(ms);//线程休眠，进入阻塞状态，该线程放弃占有的资源
（4）join();//等待某一个线程全部执行结束  join(ms) : 等待某一个线程执行一段时间
（5）yield();//当前线程退出CPU执行,进入就绪状态; 让优先级>= 本线程的其他线程（包括本线程）一起继续抢占CPU时间片
（6）wait();//当前线程处于等待状态
（7）notify();//唤醒在等待队列的线程，进入锁池状态
~~~



#### 3.五种基本状态

- 新建状态(New):

  > 当线程对象对创建后，即进入了新建状态，如：Thread t = new MyThread();

- 就绪状态(Runnable):

  > 当调用线程对象的start()方法（t.start();），线程即进入就绪状态。处于就绪状态的线程，只是说明此线程已经做好了准备，随时等待CPU调度执行，并不是说执行了t.start()此线程立即就会执行； 

- 运行状态(Running):

  > 当CPU开始调度处于就绪状态的线程时，此时线程才得以真正执行，即进入到运行状态。注：就绪状态是进入到运行状态的唯一入口，也就是说，线程要想进入运行状态执行，首先必须处于就绪状态中； 

- 阻塞状态(Blocked):

  > 处于运行状态中的线程由于某种原因，暂时放弃对CPU的使用权，停止执行，此时进入阻塞状态，直到其进入到就绪状态，才有机会再次被CPU调用以进入到运行状态。根据阻塞产生的原因不同，阻塞状态又可以分为三种：
  >
  > (1).等待阻塞：运行状态中的线程执行wait()方法，使本线程进入到等待阻塞状态；
  >
  > (2).同步阻塞 -- 线程在获取synchronized同步锁失败(因为锁被其它线程所占用)，它会进入同步阻塞状态；
  >
  > (3).其他阻塞 -- 通过调用线程的sleep()或join()或发出了I/O请求时，线程会进入到阻塞状态。当sleep()状态超时、join()等待线程终止或者超时、或者I/O处理完毕时，线程重新转入就绪状态。 

- 死亡状态(Dead):

  > 线程执行完了或者因异常退出了run()方法，该线程结束生命周期。 





#### 4.线程的创建方式及启动

- (1).**继承Thread类**，重写该类的run()方法,调用start()方法启动线程

~~~java
class MyThread extends Thread{
    @Override
    public void run(){
        for(int i=0;i<100;i++){
            //Thread.currentThread().getName()是获取当前运行线程的名字
            System.out.println(Thread.currentThread().getName()+" "+i);
        }
    }
}
~~~

```java
public class ThreadTest{
    public static void main(String[] args){
        for(int i=0;i<100;i++){
            System.out.println(Thread.currentThread().getName()+" "+i);
            if(i==30){
               //创建一个新的线程t1,此线程进入新建状态
                Thread t1=new MyThread();
                //创建一个新的线程t2,此线程进入新建状态
                Thread t2=new MyThread();
                //调用start()方法使得t1线程进入就绪状态
                t1.start();
                //调用start()方法使得t2线程进入就绪状态
                t2.start();
            }
        }
    }
}
```
> 如上所示，继承Thread类，通过重写run()方法定义了一个新的线程类MyThread，其中run()方法的方法体代表了线程需要完成的任务，称之为线程执行体。当创建此线程类对象时一个新的线程得以创建，并进入到线程新建状态。通过调用线程对象引用的start()方法，使得该线程进入到就绪状态，此时此线程并不一定会马上得以执行，这取决于CPU调度时机。 



- (2).**实现Runnable接口**，并重写该接口的run()方法，该run()方法同样是线程执行体，创建Runnable实现类的实例，并以此实例作为Thread类的target来创建Thread对象，该Thread对象才是真正的线程对象。new Thread(Runnable r);

~~~java
class MyRunnable implements Runnable{
    @Override
    public void run(){
        for(int i=0;i<100;i++){
            System.out.println(Thread.currentThread().getName()+" "+i);
        }
    }
}
~~~

~~~java
public class ThreadTest{
    public static void main(String[] args){
        for(int i=0;i<100;i++){
            System.out.println(Thread.currentThread().getName()+" "+i);
            if(i==30){
                // 创建一个Runnable实现类的对象
                Runnable r1=new MyRunnable();
                // 将myRunnable作为Thread target创建新的线程
                Thread t1=new Thread(r1);
                Thread t2=new Thread(r2);
                // 调用start()方法使得线程进入就绪状态
                t1.start();
                t2.start();
            }
        }
    }
}
~~~

> Thread和Runnable之间的关系?

~~~java
public class ThreadTest{
    public static void main(String[] args){
        for(int i=0;i<100;i++){
            System.out.println(Thread.currentThread().getName()+" "+i);
            if(i==30){
                Runnable myRunnable=new MyRunnable();
                Thread thread=new MyThread(myRunnable);
                thread.start();
            }
        }
    }
}

class MyRunnble implements Runnable{  
    @Override
    public void run(){
        System.out.println("In MyRunnble run");
        for(int i=0;i<100;i++){
            System.out.println(Thread.currentThread().getName()+" "+i);
        }
    }
}

class MyThread exetends Thread{
    public MyThread(Runnable runnable){
        super(runnable);
    }
    @Override
    public void run(){
        System.out.println("In MyThread run");
        for(int i=0;i<100;i++){
            System.out.println(Thread.currentThread().getName()+" "+i);
        }
    }
}
~~~

> 同样的，与实现Runnable接口创建线程方式相似，不同的地方在于 

~~~java
 Thread thread = new MyThread(myRunnable);
~~~

> 那么这种方式可以顺利创建出一个新的线程么？答案是肯定的。至于此时的线程执行体到底是MyRunnable接口中的run()方法还是MyThread类中的run()方法呢？通过输出我们知道线程执行体是MyThread类中的run()方法。其实原因很简单，因为Thread类本身也是实现了Runnable接口，而run()方法最先是在Runnable接口中定义的方法。

~~~java
public interface Runnable{
    public abstract void run();
}
~~~

>  我们看一下Thread类中对Runnable接口中run()方法的实现： 

~~~~java
@Override
public void run() {
    if (target != null){
        target.run();
    }
}
~~~~

> 也就是说，当执行到Thread类中的run()方法时，会首先判断target是否存在，存在则执行target中的run()方法，也就是实现了Runnable接口并重写了run()方法的类中的run()方法。但是上述给到的列子中，由于多态的存在，根本就没有执行到Thread类中的run()方法，而是直接先执行了运行时类型即MyThread类中的run()方法。 

- (3). **实现Callable和Future接口创建线程。**具体是创建Callable接口的实现类，并实现clall()方法。并使用FutureTask类来包装Callable实现类的对象，且以此FutureTask对象作为Thread对象的target来创建线程** 

~~~

~~~

> 上述主要讲解了三种常见的线程创建方式，对于线程的启动而言，都是调用线程对象的start()方法，需要特别注意的是：**不能对同一线程对象两次调用start()方法。** 

线程的使用细节

(1).如果线程对象直接调用run()，那么JVN不会当作线程来运行，会认为是普通的方法调用。
(2).线程的启动只能由一次，否则抛出异常
(3).可以直接创建Thread类的对象并启动该线程，但是如果没有重写run()，什么也不执行。
(4).匿名内部类的线程实现方式





#### 5.常见线程的方法

~~~java
 Thread(String name);//初始化线程的名字
 getName();//返回线程的名字
 setName(String name);//设置线程对象名
 getPriority();//返回当前线程对象的优先级,默认线程的优先级是5
 setPriority(int newPriority);//设置线程的优先级虽然设置了线程的优先级，但是具体的实现取决于底层的操作系统的实现（最大的优先级是10 ，最小的1 ， 默认是5）。
 currentThread();//返回CPU正在执行的线程的对象
~~~





#### 6.Java多线程的就绪、运行和死亡状态 

> 就绪状态转换为运行状态：当此线程得到处理器资源；
>
> 运行状态转换为就绪状态：当此线程主动调用yield()方法或在运行过程中失去处理器资源。
>
> 运行状态转换为死亡状态：当此线程线程执行体执行完毕或发生了异常。
>
> 此处需要特别注意的是：当调用线程的yield()方法时，线程从运行状态转换为就绪状态，但接下来CPU调度就绪状态中的哪个线程具有一定的随机性，因此，可能会出现A线程调用了yield()方法后，接下来CPU仍然调度了A线程的情况
>
> 由于实际的业务需要，常常会遇到需要在特定时机终止某一线程的运行，使其进入到死亡状态。目前最通用的做法是设置一boolean型的变量，当条件满足时，使线程执行体快速执行完毕。如： 

~~~java
public class ThreadTest {
    public static void main(String[] args) {
        MyRunnable myRunnable = new MyRunnable();
        Thread thread = new Thread(myRunnable);
        for (int i = 0; i < 100; i++) {
            System.out.println(Thread.currentThread().getName() + " " + i);
            if (i == 30) {
                thread.start();
            }
            if(i == 40){
                myRunnable.stopThread();
            }
        }
     }
 }

class MyRunnable implements Runnable {
    private boolean stop;
    @Override
    public void run() {
        for (int i = 0; i < 100 && !stop; i++) {
            System.out.println(Thread.currentThread().getName() + " " + i);
        }
    }
    public void stopThread() {
        this.stop = true;
    }
}
~~~
#### 7.线程同步锁(synchronized)

| 单线程(非线程安全) | 多线程(线程安全) |
| :----------------: | :--------------: |
|   StringBuilder    |   StringBuffer   |
|     ArrayList      |      Vector      |
|      HashMap       |    Hashtable     |

#### 8.死锁:经典的“哲学家就餐问题”;

(1).5个哲学家吃中餐，坐在圆卓子旁。每人有5根筷子（不是5双），每两个人中间放一根，哲学家时而思考，时而进餐;
(2).每个人都需要一双筷子才能吃到东西，吃完后将筷子放回原处继续思考，如果每个人都立刻抓住自己左边的筷子;
(3).然后等待右边的筷子空出来，同时又不放下已经拿到的筷子，这样每个人都无法得到1双筷子，无法吃饭都会饿死;
(4).*这种情况就会产生死锁：每个人都拥有其他人需要的资源，同时又等待其他人拥有的资源,并且每个人在获得所有需要的资源之前都不会放弃已经拥有的资源;

- 1：两个任务以相反的顺序申请两个锁，死锁就可能出现

- 2：线程T1获得锁L1，线程T2获得锁L2，然后T1申请获得锁L2，同时T2申请获得锁L1，此时两个线程将要永久阻塞，死锁出现  

  如果一个类可能发生死锁，那么并不意味着每次都会发生死锁，只是表示有可能。要避免程序中出现死锁。
  例如，某个程序需要访问两个文件，当进程中的两个线程分别各锁住了一个文件，那它们都在等待对方解锁另一个文件，而这永远不会发生。

- 3：要避免死锁

~~~java
public class DeadLock {
	public static void main(String[] args) {
		new Thread(new Runnable() { // 创建线程, 代表中国人
					public void run() {
						synchronized ("刀叉") { // 中国人拿到了刀叉
System.out.println(Thread.currentThread().getName()
									+ ": 你不给我筷子, 我就不给你刀叉");
							try {
								Thread.sleep(10);
							} catch (InterruptedException e) {
								e.printStackTrace();
							}
							synchronized ("筷子") {
								System.out.println(Thread.currentThread()
										.getName() + ": 给你刀叉");
							}
						}
					}
				}, "中国人").start();
		new Thread(new Runnable() { // 美国人
					public void run() {
						synchronized ("筷子") { // 美国人拿到了筷子
							System.out.println(Thread.currentThread().getName()

									+ ": 你先给我刀叉, 我再给你筷子");
							try {
								Thread.sleep(10);
							} catch (InterruptedException e) {
								e.printStackTrace();
							}
							synchronized ("刀叉") {
								System.out.println(Thread.currentThread()
										.getName() + ": 好吧, 把筷子给你.");
							}
						}
					}
				}, "美国人").start();
	}
}
~~~

#### 9.线程的通讯:

线程间通信其实就是多个线程在操作同一个资源，但操作动作不同

#### 10.后台线程

**后台线程**：就是隐藏起来一直在默默运行的线程，直到进程结束。

**实现：**  
      setDaemon(boolean on)  
 **特点：**  
	当所有的非后台线程结束时，程序也就终止了同时还会杀死进程中的所有后台线程，也就是说，只要有非后台线程还在运行，程序就不会终止，执行main方法的主线程就是一个非后台线程。
	必须在启动线程之前（调用start方法之前）调用setDaemon（true）方法，才可以把该线程设置为后台线程。
	一旦main（）执行完毕，那么程序就会终止，JVM也就退出了。
	可以使用isDaemon() 测试该线程是否为后台线程（守护线程）。
	该案例：开启了一个qq检测升级的后台线程，通过while真循环进行不停检测，当计数器变为100的时候，表示检测完毕，提示是否更新，线程同时结束。
	为了验证，当非后台线程结束时，后台线程是否终止，故意让该后台线程睡眠一会。发现只要main线程执行完毕，后台线程也就随之消亡了。

~~~java
class QQUpdate implements Runnable {
	int i = 0;

	@Override
	public void run() {
		while (true) {

			System.out.println(Thread.currentThread().getName() + " 检测是否有可用更新");
			i++;
			try {
				Thread.sleep(10);
			} catch (InterruptedException e) {

				e.printStackTrace();
			}
			if (i == 100) {
				System.out.println("有可用更新，是否升级？");
				break;
			}
		}
	}
}
public class Demo9 {
	public static void main(String[] args) {
		QQUpdate qq = new QQUpdate();
		Thread th = new Thread(qq, "qqupdate");
		th.setDaemon(true);
		th.start();
		System.out.println(th.isDaemon());
		System.out.println("hello world");
	}
}
~~~



#### 11.实例分析

 (1).假设有1000个终端同时给一个账户存100，取100元;

~~~java
//银行账户类
public class Account {
    private String name;
    private double balance;
    public Account(String name, double balance) {
        this.name = name;
        this.balance = balance;
    }
    public double getBalance() {
        return balance;
    }
	 //存款
    public   Account  depoist(double money){
        double temp =this.balance;
        temp+= money;
        try {
            Thread.sleep(2);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        this.balance = temp;
        System.out.println("-----" + Thread.currentThread().getName() + "： 存款后的余额：" + this.balance);
        return this;
    }
    //取款
    public  Account  withdraw(double money){
        double temp =this.balance;
        temp-= money;
        try {
            Thread.sleep(2);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        this.balance = temp;
        System.out.println(Thread.currentThread().getName() + "： 取款后的余额：" + this.balance);
        return this;
    }

}

//模拟终端线程类
public class AccountThread extends Thread {
    private Account account;
    public AccountThread(Account account) {
         this.account= account;
    }
    @Override
    public void run(){
        account.depoist(100);
        account.withdraw(100);
    }
}

//测试
public  static void main(String [] args){
     //共享资源
     Account account = new Account("Tom",2000);
	//1000个终端
     for(int i =1;i<=1000;i++){
         AccountThread thread = new AccountThread(account);
         thread.start();
     }
     try {
		//让1000个终端有足够的时间运行结束，主线程再统计操作后的金额
         Thread.sleep(10000);
     } catch (InterruptedException e) {
         e.printStackTrace();
     }
     //获得账户的余额
     System.out.println("-----" + account.getBalance()+"-------------");
}
~~~

> 运行结果：账户余额多次运行是小于 正确金额  

> 分析问题：

~~~
		time1						time2						  time3
t1线程： 调用存款2000 +100(时间片到) 									balance =2100
t2线程： 							调用存款balance =2000 +100 =2100  

其他线程类似，就会产生数据错误。
~~~

> **解决：**为了保证数据的准确性，可以要求在同一时刻只有一个线程在访问存款/取款方法。使用关键字**synchronized**。

> **同步锁**:当它用来修饰一个方法或者一个代码块的时候，能够保证在同一时刻最多只有一个线程执行该段代码.
>
>  (1).当两个并发线程访问同一个对象object中的这个synchronized(this)同步代码块时，一个时间内只能有一个线程得到执行。另一个线程必须等待当前线程执行完这个代码块以后才能执行该代码块。
>  (2).然而，当一个线程访问object的一个synchronized(this)同步代码块时，另一个线程仍然可以访问该object中的非synchronized(this)同步代码块。
>  (3).尤其关键的是，当一个线程访问object的一个synchronized(this)同步代码块时，其他线程对object中所有其它synchronized(this)同步代码块的访问将被阻塞。
>  (4).当一个线程访问object的一个synchronized(this)同步代码块时，它就获得了这个object的对象锁。结果，其它线程对该object对象所有同步代码部分的访问都被暂时阻塞。
>  (5).以上规则对其它对象锁同样适用.

> **银行账户存取款重构：**

~~~java
    public  synchronized Account  depoist(double money){
        double temp =this.balance;
        temp+= money;
        try {
            Thread.sleep(2);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        this.balance = temp;
        System.out.println("-----" + Thread.currentThread().getName() + "： 存款后的余额：" + this.balance);
        return this;
    }

    //取款
    public  synchronized   Account  withdraw(double money){
        double temp =this.balance;
        temp-= money;
        try {
            Thread.sleep(2);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        this.balance = temp;
        System.out.println(Thread.currentThread().getName() + "： 取款后的余额：" + this.balance);
        return this;
    }
~~~



(2).生产者消费者(设计模式)

	我们需要生产者生产一次，消费者就消费一次,然后这样有序交替的循环执行;这就需要使用线程间的通信了;Java通过Object类的wait，notify，notifyAll这几个方法实现线程间的通信。

~~~java
    //共享资源，模拟表示生产与消费的资源
    public class PublicResource {
    	private int number = 0;	
    	//资源生产
    	public synchronized void produce(){
    //		System.out.println("<><><><><><><>生产者线程抢到CPU<><><><><><><><><> number = " + number);
    		if(number ==1){
    			try {//不生产，生产者线程进入等待队列，等待消费者消费
    				wait();
    			} catch (InterruptedException e) {
    				e.printStackTrace();
    			}
    		}else{
    			//执行生产，叫消费者来消费
    		   number++;
    		   System.out.println("生产者生产了一个面包，number = " + number);
    		   notify();//唤醒在等待队列的消费者线程来消费
    		}
        }
    	//资源消费
    	public synchronized void consume(){
    //		System.out.println("**********************消费者线程抢到CPU..................... number = " + number);
    		if(number ==0){
    			try {//不能消费，消费者线程进入等待队列，等待生产者生产
    				wait();
    			} catch (InterruptedException e) {
    				e.printStackTrace();
    			}		
    		}else{
    			//执行消费，叫生产者来生产
    			number--; 
    			System.out.println("【消费者】消费了一个面包，number = " + number);
    			notify();//唤醒在等待状态的生产者来生产
    		}	
    	}
    }

    /**
	 * 生产者线程
	 * @author chixing
	 *
	 */
	public class Producer implements Runnable{
        private PublicResource resource;
        public Producer(PublicResource resource){
    		this.resource = resource;
    	}
    	/**
    	 * 生产一个面包
    	 */
    	public void run() {
    		 while(true){
    			 resource.produce();
    		 }
    	}
    } 
    
    /**
     * 消费者线程
     * @author chixing
     *
     */
    public class Consumer  implements Runnable{
    	private PublicResource resource;
    	public Consumer(PublicResource resource){
    		this.resource = resource;
    	}
    	/**
    	 * 消费一个面包
    	 */
    	public void run() {
    		while(true){
    			resource.consume();
    		}
    	}
    }
    
    //测试
    public static void main(String[] args) {	
    	PublicResource resource = new PublicResource();
    	new Thread(new Producer(resource)).start();
    	new Thread(new Consumer(resource)).start();
    	 
    }
~~~

> 生产者消费者需求修改：
>
> 篮子中最多能放10个面包，若不满10个面包，生产者可以生产；篮子中只要有面包，消费者可以消费面包,然后这样无限生产与消费执行

~~~java
   /**
	 * 生产者线程
	 * @author 驰星 
	 */
public class Producer implements Runnable{
    private PublicResource resource;
	public Producer(PublicResource resource){
    this.resource = resource
}
	/**
	 * 生产面包
	 */
	public void run() {
		 while(true){
			for(int i =0;i<10;i++) {
			 resource.produce();
			 try {
					Thread.sleep(5);
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			}
		 }
		
	}
} 


/**
 * 消费者线程
 * @author 驰星 
 */
public class Consumer  implements Runnable{
	private PublicResource resource;
	public Consumer(PublicResource resource){
		this.resource = resource;
	}
	/**
	 * 消费面包
	 */
	public void run() {
		while(true){
			for(int i =0;i<10;i++) {					
				resource.consume();
				try {
					Thread.sleep(15);//5-15随机数
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			}
		}
	}

}


//共享资源，模拟表示生产与消费的资源
public class PublicResource {
	private int number = 0;	
	
	//资源生产
	public synchronized void produce(){
		if(number ==10){
			try {//不生产，生产者线程进入等待队列，等待消费者消费
				wait();
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}else{
			//执行生产，叫消费者来消费
		   number++;
		   System.out.println("生产者生产了一个面包，number = " + number);
		   notify();//唤醒在等待队列的消费者线程来消费
		}
	}
	
	//资源消费
	public synchronized void consume(){
		if(number ==0){
			try {//不能消费，消费者线程进入等待队列，等待生产者生产
				wait();
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
         }else{
			//执行消费，叫生产者来生产
			number--; 
			System.out.println("【消费者】消费了一个面包，number = " + number);
			notify();//唤醒在等待状态的生产者来生产
		}
    }
}

//测试：
public static void main(String[] args) {
	PublicResource resource = new PublicResource();
	new Thread(new Producer(resource)).start();
	new Thread(new Consumer(resource)).start();
}
~~~

**等待唤醒机制**

- wait：告诉当前线程放弃执行权，并放弃监视器（锁）并进入阻塞状态，直到其他线程持有获得执行权，并持有了相同的监视器（锁）并调用notify为止。
- notify：唤醒持有同一个监视器（锁）中调用wait的第一个线程，例如，餐馆有空位置后，等候就餐最久的顾客最先入座。注意：被唤醒的线程是进入了可运行状态。等待cpu执行权。
- notifyAll：唤醒持有同一监视器中调用wait的所有的线程。

线程间通信其实就是多个线程在操作同一个资源，但操作动作不同，wait，notify（），notifyAll()都使用在同步中，因为要对持有监视器（锁）的线程操作，所以要使用在同步中，因为只有同步才具有锁。

**为什么这些方法定义在Object类中?**
	因为这些方法在操作线程时，都必须要标识他们所操作线程持有的锁，只有同一个锁上的被等待线程，可以被统一锁上notify唤醒，
	不可以对不同锁中的线程进行唤醒，就是等待和唤醒必须是同一个锁。而锁由于可以使任意对象，所以可以被任意对象调用的方法定义在Object类中;

**wait() 和 sleep()有什么区别？**  

- wait():释放资源，释放锁。是Object的方法
- sleep():释放资源，不释放锁。是Thread的方法
- 定义了notify为什么还要定义notifyAll，因为只用notify容易出现只唤醒本方线程情况，导致程序中的所有线程都在等待。 



**Thread的join方法**  
当A线程执行到了B线程Join方法时A就会等待，等B线程都执行完A才会执行，Join可以用来临时加入线程执行

~~~java
public class JoinDemo {
    public static void main(String[] args){
        B b = new B("B线程");
        A a = new A("A线程",b);

        a.start();
        b.start();
    }
}

 class A extends  Thread{
     private String name;
     private B b;
     public A(){}
     public A(String name,B b) {
       super(name);
         this.b = b;
     }
     @Override
     public void run() {
        //1-100 当i = 50 时候， b.join()
         for(int i=1;i<=100;i++){
             if(i == 50 ){
                 try {
                     b.join(); //等待b线程执行结束后，a线程再执行 
                 } catch (InterruptedException e) {
                     e.printStackTrace();
                 }
             }

             System.out.println(Thread.currentThread().getName() + ":" + i);
             try {
                 Thread.sleep(2);
             } catch (InterruptedException e) {
                 e.printStackTrace();
             }
         }
     }
 }

 class B extends  Thread{
     private String name;
     public B(){}
     public B(String name) {
         super(name);
     }
     @Override
     public void run() {
         for(int i=1;i<=100;i++){
             System.out.println(Thread.currentThread().getName() + ":" + i);
             try {
                 Thread.sleep(2);
             } catch (InterruptedException e) {
                 e.printStackTrace();
             }
         }
     }
 }
~~~

**API中其他常用的线程安全类**

- 字符串  
  String:字符串常量，适用于字符串内容不经常发生改变的时候
  StringBuiler:字符串序列可变，适用于字符串内容经常发生改变的时候，线程不安全，适用于单线程
  StringBuffer: 是StringBuilder的等价类，线程安全，适用于多线程（StringBuffer中的数据被多个线程同时修改数据）
- ArrayList、Vector
  ArrayList：可动态增长的数组，线程不安全，适用于单线程
  Vector:可动态增长的数组，线程安全，适用于多线程 （Vector集合中的数据被多个线程同时修改数据）
- HashMap、Hashtable
  HashMap: 是key-value形式存储数据，线程不安全，适用于单线程
  Hashtable: 是key-value形式存储数据，线程安全，适用于多线程（Hashtable映射中的数据被多个线程同时修改数据）