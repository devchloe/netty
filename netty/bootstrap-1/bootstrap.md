# Bootstrap & ServerBootstrap

* 부트스트랩
  * 용어 의미
    * 들오는 연결을 수신하기 위해 지정된 포트로 프로세스를 바인딩하는 작업
      * ServerBootstrap \(서버용 부트스트랩\)
    * 혹은 자기 자신 프로세스를 다른 프로세스, 즉 원 호스트 와 포트에서 실행 중인 프로세스로 연결 요청하는 작업
      * Bootstrap \(클라이언트용 부트스트랩\)
    * 단 이러한 '연결' 보장 작업은 TCP와 같은 연결 기반 프로토콜에서만 적용됨
* Bootstrap 유형
  * ServerBootstrap
    * 서버는 연결 요청을 수신해야 하므로 프로세스를 포트에 바인딩하는 작업이 필요함
      * ServerBootstrap.bind\(port\)
    * EventLoopGroup 수: 2 \(동일한 인스턴스일 수 있음\)
      * 첫번째 EventLoopGroup \(Boos\)
        * 하나는 들어오는 연결을 수신하기 위한 소켓, ServerChannel 하나를 포함
          * 즉 ServerChannel은 프로세스 포트를 기준으로 하나씩 생성된다고 생각함
          * ServerBootstrap 객체는 하나 아닐까..
      * ServerChannel과 연결된 EventLoopGroup은 클라이언트 연결 요청을 수락하고 클라이언트 요청을 처리하기 위한 **Channel 생성 작업**을 담당하는 EventLoop 하나를 ServerChannel에 할당
      * 두번째 EventLoopGroup \(Worker\)
        * 다른 하나는 서버가 수락한 연결마다 요청을 처리하기 위해 생성된 모든 Channel을 포함
        * 연결이 수락되면 두번째 EventLoopGroup이 생성된 Channel에 EventLoop를 할당함
      * 참고 [https://groups.google.com/forum/\#!topic/netty-ko/-liUw3162kI](https://groups.google.com/forum/#!topic/netty-ko/-liUw3162kI)
  * Bootstrap
    * 클라이언트는 원격 피어로 연결을 수행해야 함
      * Bootstrap.connect\(remoteaddress\)
    * EventLoopGroup 수: 1
  * 

