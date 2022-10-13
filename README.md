# main inbox



Q) 비동기 컴포넌트 추적 221006

모듈 ABC가 있을 때 비동기가 아니라면 쓰레드 아이디가 하나 일거고 해당 트랜잭션에 대해서는 추적이 가능할 것이다

근데 비동기라면 각각의 모듈들이 비동기처리되면서 쓰레드가 달라지면서 추적을 하려면 어디에 저장을 해야할것이다

이것을 지원하는 것이 비동기 컴포넌트이고 와탭에서 플러그인으로 제공해준다





프록시

* 주로 보안상 직접 통신할 수 없는 두점 사이를 통신할경우 중계기로서 대리로 통신을 수행하는 기능을 가리켜 프록시
* 그 중계기능을 하는 것을 프록시 서버라고 한다
* 프록시 서버는 요청된 내용들을 캐시를 이용해 저장해둔다
  * 내부에서 캐시 안에 있는 정보를 요구하는 요청에 대해서는 원격 서버에 접속하여 데이터를 가져올 필요가 없게 됨으로써 전송 시간을 절약할 수있다
  * 즉 외부와의 트래픽을 줄인다 -> 병목현상 감소

Forward 프록시

* 원격 서버로부터 (와탭-Agent서버) 요청된 리소스를 가져와 요청한 사용자에게 돌려주는 역할
  * 캐시가 남아있다면 캐시를 준다
