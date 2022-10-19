# Java 멀티 쓰레드 디자인패턴

## Introduction 01

### 쓰레드란 무엇인가

* start 메소드를 실행해야 자바에서 새로운 쓰레드를 만들어준다
* start 메소드가 실행되면서 run 메소드를 같이 실행해준다
* 따라서 run 메소드를 실행하면 쓰레드가 생성되지 않는다



순차(sequential), 병렬(parallel), 병행(concurrent) 용어 정리

* 순차: 말그대로 순차적으로 실행
* 병렬: 10개의 업무를 2개가 분담하여 실행
* 병행: 어떤 한 task를 어떤 순서로 처리해도 상관없이 여러개의 작업으로 분할, 아래 이미지 참고
  * 예를 들어 cpu가 하나라면 두개의 업무를 마치 하나의 병렬처리하듯이 왔다갔다...
  * cpu가 두개라면 두번째 이미지처럼 같은 시간동안에 task를 말그대로 동시에 실행할 수 있다

<figure><img src="../.gitbook/assets/2022-10-19_18-15-06.png" alt=""><figcaption></figcaption></figure>
