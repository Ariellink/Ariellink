# Oct 9 Summary

### Coroutine in C++ are stackless :

stackful 和 stackless的不同在于协程切换的方式。

协程挂起时return给call, 并将协程状态保存在堆上。由人来通过函数返回，来决定何时切换上下文挂起协程，以及保存协程的状态。

与之相对的stackful coroutine （golang）, 是调用一些方法，由语言层面runtime来决定协程进行切换和阻塞，保存协程上下文。

### coroutine 和 thread ：

线程切换：用户态和内核态切换。一个线程栈是4M，因此拷贝一个thread需要4M。

协程切换：只发生用户态切换，没有内核态的介入，切换效率更高。内存消耗上，一个协程只占用4KB寄存器大小。因此，一个线程的内存在MB级别，而协程只需要KB级别。切换成本低。

### 协程的应用场景：

当其在进行I/O操作时候，CPU实际上是空闲的。当一个协程需要io阻塞，等disk 或 网络io的情况下， 协程A挂起，让出cpu，切换到协程B上去执行。 由DMA加载，处理完了，call 协程A回来继续执行。