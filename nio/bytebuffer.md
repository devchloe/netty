# ByteBuffer



[https://www.javamex.com/tutorials/io/nio\_buffer\_direct.shtml](https://www.javamex.com/tutorials/io/nio_buffer_direct.shtml)

NIO supports a type of [ByteBuffer](https://www.javamex.com/tutorials/io/nio_buffers.shtml) usually known as a direct buffer. Direct buffers can essentially be used like any other ByteBuffer \(and are implemented as a ByteBuffer subclass\), but have the property that their underlying memory is **allocated outside the Java heap**. More specifically, direct buffers have the following properties:

* once allocated, their memory address is fixed for the lifetime of the buffer;
* because their address is fixed, the kernel can safely access them directly and hence direct buffers can be used more efficiently in I/O operations;
* in some cases, accessing them from Java can be more efficient \(there's potentially less overhead in looking up the memory address and/or other housekeeping required before accessing a Java object\)— see the example [NIO buffer performance](https://www.javamex.com/tutorials/io/nio_buffer_performance.shtml) measurements made in Hotspot under Windows;
* via the Java Native Interface, you can actually set the address arbitrarily if required \(e.g. to access hardware at a particular address, or to perform the allocation yourself\).



| 구분  |  Non-direct buffer |  Direct buffer  |
| :--- | :--- | :--- |
|   사용하는 메모리 공간  |   JVM의 힙 메모리  |   운영체제의 메모리  |
|   버퍼 생성 시간  |   버퍼 생성이 빠르다  |   버퍼 생성이 느리다  |
|   버퍼의 크기  |   작다  |   크다  |
|   입출력 성능  |   낮다  |   높다  |

  
  
출처: [http://palpit.tistory.com/641](http://palpit.tistory.com/641) \[palpit's log-b\]

