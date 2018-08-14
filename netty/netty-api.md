# Netty 공통 API

* 블로킹 -&gt; 논블로킹 전송으로 전환
  * 네티에서는 공통 API를 기반 레이어로 활용하므로 JDK를 직접 이용할 때보다 변환이 훨씬 간단함



* Java 블로킹 방식 &gt; Java 논블로킹 방식 \(using channel, selector\)
* Netty 블로킹 방식, Netty 논블로킹 방식
  * 이벤트 그룹과 채널 유형만 바꾸면 다른 비즈니스 로직에 영향을 주지 않음
  * 즉 네트워크 전송 레이어를 비즈니스 로직으로부터 분리

{% page-ref page="blocking.md" %}

{% page-ref page="../nio/channel.md" %}

{% page-ref page="../nio/selector.md" %}



