# Inbox

#### Service discovery

동적인 ip와 port로 이루어진 여러개의 서비스가 있을 때 클라이언트가 원하는 정보를 얻으려면 어떻게 해야할까?

앞단(Client or API Gateway)에서 변경된 정보들을 지속적으로 적용해서 배포할 수는 없는 노릇일 것이다.

Service registry 서버를 따로 두고 변경되는 인스턴스들을 동적으로 관리하면 해당 문제를 해결할 수 있다

Service discovery 는 Client-side와 Server-side로 나뉠 수 있다. Eureka 가 Client-side이고 Server-side는 앞에 로드밸런서를 두는 방법인데 자세히는 모르겠다.
