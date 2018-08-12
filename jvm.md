# JVM

참고 [http://stophyun.tistory.com/37](http://stophyun.tistory.com/37)

* JVM 구조 
* JVM 작동원리
* 트랜잭션 응답시간, 처리량 계산

### JVM

* 특징
  * 스택기반 동작
  * 가비지 컬렉션 역할 
* 컴포넌트
  * Class Loader
  * Runtime Data Areas
    * JVM 프로그램이 OS로부터 할당받는 메모리 영
    * 메소드 영역
      * 메소드의 바이트 코드, 클래스 변수 
      * 모든 스레드가 공유하는 영역으로 JVM 시작될 때 생
    * 힙 영역
      * 객체를 저장하는 공간, 가비지 컬렉션 대상
      * 모든 스레드에 공유됨 
    * 스택 영역
      * 매개변수, 지역변수 저장 공간
      * 스레드마다 하나씩 존재, 스레드 시작될 때 생성
      * 스레드의 수행 정보를 기록
    * PC 레지스터
      * 스레드마다 하나씩 존재, 스레드 시작될 때 생성
      * 현재 수행 중인 JVM 명령의 주소를 가짐
      * 연산 결과를 메모리로 전달하기 전에 잠시 저장하는 공간 
    * Native 메서드 스
      * 스레드마다 하나씩 존재, 스레드 시작될 때 생성
      * Native 실행하기 위한 공간
  * Execution Engine
* 실행 과정
  * OS가 JVM 프로그램 실행
  * JVM이 Java 프로그램을 실행
    * 자바소스를 컴파일러가 바이트 코드로 변환 \(.class 파일\)
    * Class loader에 의해 JVM 안으로 .class 파일이 로드됨
      * 이 파일들은 Runtime Data Areas에 배치됨 
    * 로딩된 .class 파일들은 Execution Engine에 의해 해석하고 실행
    * 실행과정에서 JVM이 Thread Synchroniztion과 가비지 콜렉션과 같은 작업 수행 



