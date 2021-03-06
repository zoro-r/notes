# 异步I/O

### 什么是I/O？
I指的是Input（输入）O指的是Output (输出)；

操作系统对计算机进行了抽象，将所有输入输出设备抽象为文件。内核在进行文件IO操作室，通过文件描述符进行管理，而文件描述符类似于应用程序于系统之间的凭证，应用程序如果需要进行IO调用，需要先打开文件描述符，然后根据文件描述符去实现文件的数据读写，此处非阻塞IO和阻塞IO的区别在于阻塞IO完成整个获取数据的过程，而非阻塞IO则不带数据之间返回,要获取数据，还需要通过文件描述符再次读取
其实异步的体现更多的是对硬件CPU的使用，能够更高效的去利用CPU的计算能力，不让某些时刻一直处于等待的状态从而导致性能浪费；

## 摘要
1、在众多高级编程语言或运行平台中，将异步作为主要编程方式和设计理念的，Node是首个

2、单线程和事件驱动 构成Node的基调

3、与Node的事件驱动、异步I/O设计理念比较相近的一个知名产品为Nginx

前端典型的异步操作就是 Ajax

## 重要性
在游览器端，如果页面的渲染等待脚本执行后再进行，如果脚本执行比较晚，那么页面就会卡顿，
如果同时加载两个资源A、B 如果同步情况下 等待时间为A+B，异步情况下则是MAX(A，B)，况且现在的应用肯定是很多的文件，显而易见的异步的方式要胜出；这就是异步I/O在Node中如此盛行，甚至
将其作为主要理念进行设计的原因，---**I/O是昂贵的，分布式I/O是更昂贵的。** 只有后端能够快速的响应资源，才能让前端的体验变好。
  
单线程同步编程模型会因阻塞I/O导致硬件资源得不到更优的使用，多线程编程模型也因为编程中的死锁，状态同步等问题让开发头疼；
Node在两者之间给出了它的方案：利用单线程，远离多线程死锁，状态同步等问题；利用异步I/O，让单线程远离阻塞，以更好的利用CPU

那么怎么高效的利用Cpu呢？
为了单线程无法利用多核CPU的缺点，NODE提供了类似前端游览器中 **Web Workers的子进程**，

## 如何实现异步IO呢
操作系统内核对于IO只有两种方式：阻塞和非阻塞
阻塞IO为获取数据后等待数据一起返回，而非阻塞IO只会返回文件描述符，那么就需要不停的进行**轮询**或者其他的操作去实现数据的获取

轮询的技术主要有以下几种

1、read
2、select 数组的方式
3、poll selct的改进方案 才用链表的方式
4、epoll
5、kqueue 仅在FreeBSD系统下存在

轮询的技术对于应用程序而言，它仍然只能算是一种同步，因为应用程序仍然需要等待返回，那么理想的I/O应该是在数据读取完成之后，直接返回数据执行回调就好了，在Linux下就存在这样的一种方式，它原生提供的一种异步IO（AIO）就是通过信号或回调来传递数据的；
那么其他的系统怎么办呢？那就是启动多线程的方式，通过让部分线程进行阻塞IO或者非阻塞IO加轮询技术来完成数据获取；让一个线程进行计算处理，通过线程之间的通信将IO得到的数据进行传递来模拟异步IO


## NODE的异步IO
1、事件循环 NODE异步IO的核心是事件循环，也正是它让回调函数十分普遍，

2、观察者

3、请求对象

4、I/O 线程池


## 异步API
setTImeout、setInterval

setImmediate、process.nextTick


## 总结

Node正是依靠构建了一套完善的高性能异步IO框架，打破了JavaScript在服务器端止步不前的局面
