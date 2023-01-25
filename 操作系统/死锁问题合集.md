# Q 1.1：Conditions for deadlock to happen

**What is a deadlock**  

A phenomenon where no process is able to finish execution. The system keeps spinning forever.



Deadlock could arise if and only if all four conditions below are met

- **Mutual Exclusion**: data sharing is not allowed. A resource is either held by one process, or free.

- **Hold and wait**: a process can hold a resource while waiting for another 
- **Non-preemption**: only the process holding the resource can release the resource

- **Circular Wait**: each process is currently waiting for a resource held by another 



# Q 1.2：Resolve a deadlock

There are four main approaches:

- Ostrich algorithm
- Detect deadlock then resolve it
- Prevent deadlock
- Avoid deadlock



# Ostrich algorithm

To stick one's head in the sand and pretend there is no problem. This is used when

- It's more cost-effective to leave the deadlock be than to resolve it

- It is rare for deadlock to happen
- It is harmful to the users

Most operating systems, including Unix, Linux and Windows, somehow implements ostrich algorithm



# Detect deadlock then resolve it

Do not try to avoid a deadlock, instead, resolve a deadlock when it already happened



## 1. Detection of deadlock (single resources)

The picture is no longer available at the time when the translator forked from main branch



## 2. Detection of deadlock (multi resources)

The picture is no longer available at the time when the translator forked from main branch



## 3. Resolve a deadlock

- Preempt the resource (e.g. a process of higher priority forces another process to release the resource)
- Force a process to restart: rollback to its previous state (hence release the resources)
- Kill the process (hence release the resources)



# Q 1.3：Code that causes deadlock
```java
package deadlock;

public class Deadlock {
	public static String str1 = "str1";
    public static String str2 = "str2";

    public static void main(String[] args){
        Thread a = new Thread(() -> {
            try {
                while (true) {
                    synchronized(deadlock1.str1) {
                        System.out.println(Thread.currentThread().getName()+"锁住 str1");
                        Thread.sleep(1000);
                        synchronized(deadlock1.str2) {
                            System.out.println(Thread.currentThread().getName()+"锁住 str2");
                        }
                    }
                }
            }catch (Exception e) {
                e.printStackTrace();
            }
        });

        Thread b = new Thread(() -> {
            try{
                while(true){
                    synchronized(deadlock1.str2){
                        System.out.println(Thread.currentThread().getName()+" locks str2");
                        Thread.sleep(1000);
                        synchronized(deadlock1.str1){
                            System.out.println(Thread.currentThread().getName()+" locks str1");
                        }
                    }
                }
            }catch(Exception e){
                e.printStackTrace();
            }
        });

        a.start();
        b.start();
    }
}
```

Output:

```
Thread-1 locks str2  
Thread-0 locks str1
```



There are two threads in the programme. Thread 1 locks str1, then sleep for 1 second; in the meantime Thread 2 locks str2, and enters sleep() as well

Thread 1, after the sleep, then tries to grab str2; thread 2, after the sleep, tries to grab str1. Both would fail and unable to proceed. A deadlock therefore occurred.



# Q 1.4：说明在数据库管理系统或者JAVA中如何解决死锁

## A.死锁预防  

在程序运行之前预防死锁。

**1.破坏互斥条件**
产生死锁需要四个条件，那么，只要这四个条件中至少有一个条件得不到满足，就不可能发生死锁了。由于互斥条件是非共享资源所必须的，不仅不能改变，还应加以保证，所以，主要是破坏产生死锁的其他三个条件。

**2.破坏占有和等待条件**
- 方法一：所有的进程在开始运行之前，必须一次性地申请其在整个运行过程中的全部资源。  
优点：简单易实施且安全；  
缺点：因为某项资源不满足而导致进程无法启动，而其他已经满足了的资源也不会得到利用，严重降低了资源的利用率，造成资源浪费，使进程经常出现饥饿现象。

- 方法二：是对方法一的改进，允许进程只获得运行初期需要的资源，便开始运行，在运行过程中逐步释放掉分配到的已经使用完毕的资源，然后再去请求新的资源。这样的话，资源的利用率会得到提高，也会减少进程的饥饿情况。

**3.破坏不可抢占条件**
当一个已经持有了一些资源的进程在提出新的资源请求没有得到满足时，它必须释放已经保持的所有资源，待以后需要使用的时候再重新申请。这就意味着进程已占有的资源会被短暂地释放或者说是被抢占了。  
该种方法实现起来比较复杂，且代价也比较大。释放已经保持的资源很有可能会导致进程之前的工作实效等，反复的申请和释放资源会导致进程的执行被无限的推迟，这不仅会延长进程的周转周期，还会影响系统的吞吐量。

**4.破坏环路等待**
给资源统一编号，进程只能按编号顺序来请求资源。当一个进程占有编号为i的资源时，那么它下一次申请资源只能申请编号大于i的资源。如下图所示
<div align="center"> <img src="https://img-blog.csdn.net/2018051322430635"/> </div><br>

这样虽然避免了循环等待，但是这种方法是比较低效的，资源的执行速度回变慢，并且可能在没有必要的情况下拒绝资源的访问，比如说，进程c想要申请资源1，如果资源1并没有被其他进程占有，此时将它分配个进程c是没有问题的，但是为了避免产生循环等待，该申请会被拒绝，这样就降低了资源的利用率

## B.死锁避免
在使用前进行判断，只允许不会产生死锁的进程申请资源  
死锁避免是利用额外的检验信息，在分配资源时判断是否会出现死锁，只在不会出现死锁的情况下才分配资源。  
两种避免办法：  
- 如果一个进程的请求会导致死锁，则不会启动该进程；  
- 如果一个进程的增加资源会导致死锁，那么拒绝该申请。



**Banker's Algorithm**
一个小城镇的银行家，他向一群客户分别承诺了一定的贷款额度，算法要做的是判断对请求的满足是否会进入不安全状态，如果是，就拒绝请求；否则予以分配。

<div align="center"> <img src="https://gitee.com/CyC2018/CS-Notes/raw/master/docs/pics/d160ec2e-cfe2-4640-bda7-62f53e58b8c0.png"/> </div><br>

上图 c 为不安全状态，因此算法会拒绝之前的请求，从而避免进入图 c 中的状态。

**多个资源的银行家算法**

<div align="center"> <img src="https://gitee.com/CyC2018/CS-Notes/raw/master/docs/pics/62e0dd4f-44c3-43ee-bb6e-fedb9e068519.png"/> </div><br>

上图中有五个进程，四个资源。左边的图表示已经分配的资源，右边的图表示还需要分配的资源。最右边的 E、P 以及 A 分别表示：总资源、已分配资源以及可用资源，注意这三个为向量，而不是具体数值，例如 A=(1020)，表示 4 个资源分别还剩下 1/0/2/0。

检查一个状态是否安全的算法如下：

- 查找右边的矩阵是否存在一行小于等于向量 A。如果不存在这样的行，那么系统将会发生死锁，状态是不安全的。
- 假若找到这样一行，将该进程标记为终止，并将其已分配资源加到 A 中。
- 重复以上两步，直到所有进程都标记为终止，则状态时安全的。

如果一个状态不是安全的，需要拒绝进入这个状态。




# 附录：死锁检测与恢复
不试图阻止死锁，而是当检测到死锁发生时，采取措施进行恢复。

## 1. 每种类型一个资源的死锁检测

<div align="center"> <img src="https://gitee.com/CyC2018/CS-Notes/raw/master/docs/pics/b1fa0453-a4b0-4eae-a352-48acca8fff74.png"/> </div><br>

上图为资源分配图，其中方框表示资源，圆圈表示进程。资源指向进程表示该资源已经分配给该进程，进程指向资源表示进程请求获取该资源。

图 a 可以抽取出环，如图 b，它满足了环路等待条件，因此会发生死锁。

每种类型一个资源的死锁检测算法是通过检测有向图是否存在环来实现，从一个节点出发进行深度优先搜索，对访问过的节点进行标记，如果访问了已经标记的节点，就表示有向图存在环，也就是检测到死锁的发生。

## 2. 每种类型多个资源的死锁检测

<div align="center"> <img src="https://gitee.com/CyC2018/CS-Notes/raw/master/docs/pics/e1eda3d5-5ec8-4708-8e25-1a04c5e11f48.png"/> </div><br>

上图中，有三个进程四个资源，每个数据代表的含义如下：

- E 向量：资源总量
- A 向量：资源剩余量
- C 矩阵：每个进程所拥有的资源数量，每一行都代表一个进程拥有资源的数量
- R 矩阵：每个进程请求的资源数量

进程 P<sub>1</sub> 和 P<sub>2</sub> 所请求的资源都得不到满足，只有进程 P<sub>3</sub> 可以，让 P<sub>3</sub> 执行，之后释放 P<sub>3</sub> 拥有的资源，此时 A = (2 2 2 0)。P<sub>2</sub> 可以执行，执行后释放 P<sub>2</sub> 拥有的资源，A = (4 2 2 1) 。P<sub>1</sub> 也可以执行。所有进程都可以顺利执行，没有死锁。

算法总结如下：

每个进程最开始时都不被标记，执行过程有可能被标记。当算法结束时，任何没有被标记的进程都是死锁进程。

1. 寻找一个没有标记的进程 P<sub>i</sub>，它所请求的资源小于等于 A。
2. 如果找到了这样一个进程，那么将 C 矩阵的第 i 行向量加到 A 中，标记该进程，并转回 1。
3. 如果没有这样一个进程，算法终止。

## 3. 死锁恢复

- 利用抢占恢复
- 利用回滚恢复
- 通过杀死进程恢复

