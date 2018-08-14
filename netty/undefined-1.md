# 메모

* 서버
  * Bootstrap
  * ServerBootstrap
    * handler
      * ServerChannel에 의해 처리되는 핸들러 추가
      * 서버가 리스닝하는 포트로 접속하면 연결을 처리하는 Channel
    * childHandler
      * 원격 피어에 바인딩된 소켓을 나타내는 Channel에 의해 처리되는 핸들러 추가
      * 연결 이후에 원격 피어와 주고 받은 데이터를 처리하는 Channel
* * 클라이언트 or 비연결 어플리케이
  * Bootstrap

