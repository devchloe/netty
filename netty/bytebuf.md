# ByteBuf

* 데이터 컨테이너
* 데이터 처리 기법 이해에 기반이 됨
* 제로 카피
* flip\(\) 호출 필요 없음
* 읽기와 쓰기 인덱스 적용
* 참조 카운팅
* 풀링
* 메서드 체인 

### ByteBuf 데이터 접근 

* readerIndex, writerIndex 제공 \( 0 &lt;= index &lt;= capacity &lt;= Integer.MAX\_VALUE \)
* readerIndex &gt; writerIndex
  * IndexOutOfBoundException 발생
* read, write prefix 메서드는 index를 증가시키지만 set, get은 증가시키지 않

### ByteBuf 사용

* 힙버퍼
* 
{% page-ref page="../nio/bytebuffer.md" %}



