![[Pasted image 20250512031315.png]]
서로 다른 앱의 데이터를 통신하고 관리할 수 있도록 하는 소프트웨어
-> 즉 다른 소프트웨어와 소통하기 위한 [[인터페이스]] 역할을 하는 소프트웨어이다.

## Middleware의 역사
---
첫 출시 당시 레거시 시스템과 새로운 시스템을 잇는 다리 역할로 등장하였고
1980년대에 들어서 [[분산 시스템]]의 중요한 통신 및 데이터 관리 도구가 되었다.

## Middleware 왜 사용할까?
---
Middleware는 디자인 프로세스를 단순화하기 때문에 사용한다. 현대의 앱은 여러개의 마이크로서비스로 구성되어 있기 때문에 일일히 연결하는 것이 어렵다. Middleware을 사용하면 비즈니스 로직 및 기능에 중점을 두고 개발하여 작업 프로세스를 단순화 할 수 있기 때문에 사용한다.

1. 비즈니스 로직을 미들웨어 서버에서 동작하게 하여 클라이언트는 I/O만 담당하면 된다.
2. 애플리케이션 간의 의존성을 줄여 개발과 유지보수가 편해진다.
3. 분산 시스템에서 자원, 통신을 관리할 수 있다.

## Middleware의 기능
---
Middleware는 워낙 기능이 많기 때문에 사용할 때마다 필요한 기능을 골라서 사용하자.
요청-응답 사이클 동안 아래 기능들을 사용할 수 있다. 꼭 하나만 사용해야 하는 것이 아닌 한 요청-응답 사이에 많은 Middleware를 실행 시킬 수 있다.

- **[[프로토콜]] 변환 (Protocol Translation)**
- **메시지 큐 (Message Queuing)**
- **데이터베이스 연결 (Database Connectivity)**
- **보안 (Security)**
- **로깅 (Logging)**
- **인터페이스 (Interface)**
- **[[트랜잭션]] (Transaction)**
- **분산 처리 (Distributed Computing)**
- **서비스 (Service)**
- **모니터링 (Monitoring)**
- **[[배포]] (Deployment)**
- **[[라우팅]] (Routing)**

## Middleware 사용처
---
### 프론트엔드
예시) [[Next.js Middleware]],[[ Node.js Middleware]], [[Redux]]

### 백엔드
예시) WAS, 데이터베이스 연동 라이브러리

### 게임 개발
> "게임 개발 친구야 혹시 Middleware 써본 적 있니?"
> -> "오 그거 게임 개발할 때 써본 거야"

게임 개발 친구에게 Middleware 써본 적이 있냐고 물었더니 게임 개발은 실시간으로 서버와 이미지, 오디오, 비디오를 주고 받고 해야 하기 때문에 Middleware을 사용한다고 한다.



## 참고 자료
---
https://developer.mozilla.org/ko/docs/Glossary/Middleware
https://yejinlife.tistory.com/entry/%EC%9B%B9-%EB%B0%B1%EC%97%94%EB%93%9C-%EB%AF%B8%EB%93%A4%EC%9B%A8%EC%96%B4-MiddleWare
https://velog.io/@seosu2000/Middleware%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80