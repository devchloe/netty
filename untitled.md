# Channel 인터페이스

### Channel 메서드

| 메서드명 | 설명 |
| :--- | :--- |
| id | 채널 식별자 |
| eventLoop | 채널에 할당된 EventLoopif SocketChannel, 연결을 수락하고 클라이언트와 채널을 생성하는 EventLoop 반환if Channel, 연결 수락 후 생성된 채널들을 관리하는 EventLoop 반환 |
| pipeline | 채널에 할당된 ChannelPipeline |
| isActive | Socket 전송 경우, 원격 피어로 연결되면 trueDatagram 전송 경우, 열리면 true |
| localAddress | 로컬 SocketAddress |
| remoteAddress | 원격 피어 SocketAddress |
| write | 원격 피어로 데이터 출력ChannelPipeline에 전달되어 맨 뒤 Handler에서부터 실행flush되기 전까지 큐에 저장됨 |
| flush | 이전 큐에 저장된 데이터를 클라이언트로 출력 |
| writeFlush | write, flush 한번에 수행 |

### 전송 방식 

* 전송 방식은 Channel 타입에 따라 달라진다
  * NIO
    * java.nio.channels API 이용
  * OIO
    * java.net API 이
  * Local
    * VM에서 파이프를 통해 통신하는데 이
  * Epoll
  * Embedded
* 프로토콜을 지원하는 전송 방식을 택해야 한다
  * NIO
    * 셀렉터 기반 API 활용
    * 모든 입출력 작업을 완전한 비동기로 구현
    * 셀렉터 개념
      * Channel registry
      * Channel 상태가 변경되면 요청이 알림을 받을 수 있게 함
      * Channel 상태변경 종류
        * 새로운 Channel 수락된 상
        * Channel 연결이 완료된 상
        * Channel에 읽은 데이터가 있는 상태
        * Channel에 데이터를 기록할 수 있는 상태
  * OIO
    * 입출력 작업 완료시간 지정 SO\_TIMEOUTSocket
  * Local
    * 동일한 JVM 내에서 실행되는 클라이언트와 서버 간 비동기 통신을 목적으로 함
    * 네트워크 상에 서비스를 노출할 필요가 없는 경우
  * Epoll, Embedded 



{% page-ref page="nio/selector.md" %}



