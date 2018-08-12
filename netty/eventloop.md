# EventLoop

* 1 EventLoopGroup has N EventLoop
* 1 EventLoop mapped 1 Thread, 1 Channel registered 1 EventLoop
  * channel executed in the same thread
* 1 EventLoop in charge of N Channel
  * without thread switching, only 1 Thread can handle multi-channel
* 스레드 작업 큐 관리 방법





