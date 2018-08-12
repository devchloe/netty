# Bootstrap & ServerBootstrap

* 부트스트랩
  * 용어 의미
    * 들오는 연결을 수신하기 위해 지정된 포트로 프로세스를 바인딩하는 작업
      * ServerBootstrap \(서버용 부트스트랩\)
    * 혹은 자기 자신 프로세스를 다른 프로세스, 즉 원 호스트 와 포트에서 실행 중인 프로세스로 연결 요청하는 작업
      * Bootstrap \(클라이언트용 부트스트랩\)
    * 단 이러한 '연결' 보장 작업은 TCP와 같은 연결 기반 프로토콜에서만 적용됨
* Bootstrap 유
  * ServerBootstrap
    * 서버는 연결 요청을 수신해야 하므로 프로세스를 포트에 바인딩하는 작업이 필요함
      * ServerBootstrap.bind\(port\)
    * EventLoopGroup 수: 2 \(동일한 인스턴스일 수 있음\)
  * Bootstrap
    * 클라이언트는 원격 피어로 연결을 수행해야 함
      * Bootstrap.connect\(remoteaddress\)
    * EventLoopGroup 수: 1
  * 

