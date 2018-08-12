# ChannelPipeline & ChannelHandler

* 관련 패키지
  * io.netty.channel
* ChannelPipile
  * ChannelHandler 체인 관리
  * 구성된 체인에 따라 인바운드, 아웃바운드 이벤트, 데이를 전파하기 위한 API 제공
* ChannelHandler
  * 어플리케이션 논리 컨테이
  * 인바운드, 아웃바운드 이벤트가 발생 했을 때 이벤트 종류에 따라 Handler 메서드가 트리거
  * 커스텀 Handler가 ChannelPipeline에 설치되는 시점
    * Channel이 생성되면 자동으로 ChannelPipeline 할당
    * ServerBootstrap 생성 시 ChannelInitializer를 구현하여 ChannelPipeline에 등록할 커스텀 ChannelHandler 집합을 정의함
      * childHandler\(new ChannelInitializer\(\)\)
    * Channel이 생성되었을 때 ChannelInitializer.initChannel\(\)이 호출되면서 ChannelInitializer가 Channel에 할당된 ChannelPipeline에 커스텀 Handler 집합을 설치함
      * 즉 initChannel에서 해당 Channel에 할당된 파이프라인을 꺼내어 핸들러를 add
  * 다음 Handler로 이벤트 전달은 인자로 받은 ChannelHandlerContext의 메서드를 호출해서 한다
  * ChannelHandlerAdapter를 이용해서 의미없는 이벤트는 다음으로 전달하지 않도록 구현하는 등 커스텀 구현이 가능하다
    * 네티에서는 기본적으로 ChannelInboundHandler, ChannelOutboundHandler 인터페이스를 구현한 ChannelInbonudHandlerAdapter, ChannelOutboundHandlerAdapter 구현체를 제공하기 때문에 체인의 다음 핸들러로 이벤트를 전달하는 행위를 자동으로 해준다.
    * 필요한 메서드와 이베트만 재정의하면 된다
    * 커스텀 핸들러 만들 때 자주 이용되는 어댑터
      * ChannelHandlerAdapter
      * ChannelInboundHandlerAdapter
      * ChannelOutboundHandlerAdapter
      * ChannelDuplexHandlerAdapter
  * 관련 컴포넌트 
    * Channel, ChannelPipeline
    * ServerBootstrap, ChannelInitializer, ChannelHandler
    * ChannelInitializer.initChannel\(\)
    * ChannelInboundHandler, ChannelOutboundHandler
    * ChannelXXXHandler 인터페이스는 상위 Handler 인터페이스를 확장 
    * ChannelXXXHandlerAdapter 클래스는 ChannelXXXHandler 인터페이스와 ChanelHandlerAdaper를 확장해서 커스텀 ChannelXXXHandler를 완성함
  * ChannelHandler 용도
    * 데이터 포맷 변환
    * 예외에 대한 알림 제공
    * 채널 활성화 또는 비활성화에 대한 알림 제공
    * 채널을 이벤트루프에 등록할 대 또는 등록 해제할 때 알림 제공
    * 사용자 정의 이벤트에 대한 알림 제공
  * ChannelHandler 인스턴스를 필요에 따라 추가하거나 제거해서 ChannelPipeline을 바로바로 변경할 수 있다.
    * 예를 들어 특정 프로토콜이 요청될 때마다 요청된 프로토콜을 처리하는  ChannelHandler\(SslHandler\)를 ChannelPipeline에 삽입시키는 방법 \(STARTTLS 프로토콜 지\)
* ChannelHandlerContext
  * ChannelHandler와 ChannelPipeline 간 바인딩 정보
  * ChannelHandler를 ChannelPipeline에 추가할 때 ChannelHandlerContext 하나가 할당됨
  * 이용방법
    * channel을 가져온다
    * 아웃바운드 데이터를 기록할 때 주로 이용
  * 메시지를 보내는 방법 두가지
    * 채널에 직접 기록
      * 채널파이프라인 뒤쪽에서 부터 시작됨
    * 채널핸들러와 연결된 ChannelHandlerContext 객체에 기록하는 ㅎ방법
      * ChannelPipeline 체인상에서 다음 핸들러에서부터 시작됨
* 인코더와 디코더
  * 네티에서 기본 제공하는 모두 채널인바운드/아웃바운드핸들러를 구현
    * io.netty.handler.codec 패키지에서 제공
  * 채널이니셜라이저에서 파이프라인에 핸들러 등록하는 메커니즘은 동일하게 사용 가능
  * 인바운드 메시지는 디코딩해서 다음 핸들러로 전달 \(decode\(\)\)
  * 아웃바운드 메시지는 인코딩해서 내보냄 \(encode\(\)\)
* SimpleChannelInboundHandler 추상 클래스
  * 디코딩된 메시지를 수신하고 다음 비즈니스 로직 실행을 위한 핸들러로 전달할 때 이용하는 클래스
  * 다른 기본 InboundHandler와 차이는 channelRead0 메서드이다
  * ChannelHandlerContext를 인수로 받으며 특정한 클래스 타입의 메시지만을 받아서 처리한다.
  * 처리하려는 메시지의 클래스 타입을 SimpleChannelInboundHandler&lt;T&gt;에서 T로 선언하고 channelRead0의 msg 타입으로 T를 선언한다
  * 이 때 channelRead0은 개발자 마음대로 구현할 수 있지만 현재 입출력 스레드를 블로킹하지 않아야 한다.

{% code-tabs %}
{% code-tabs-item title="nia.chapter12.HttpRequestHandler.java" %}
```java
public class HttpRequestHandler extends SimpleChannelInboundHandler<FullHttpRequest> {
    private final String wsUri;
    ...

    @Override
    public void channelRead0(ChannelHandlerContext ctx,
        FullHttpRequest request) throws Exception {
        if (wsUri.equalsIgnoreCase(request.getUri())) {
            ctx.fireChannelRead(request.retain());
        } else { 
        ...
```
{% endcode-tabs-item %}
{% endcode-tabs %}

* 인바운드 이벤트 종류

  채널파이프라인 만드는 과정

* 어댑터 패



