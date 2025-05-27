실시간 웹 애플리케이션을 위한 이벤트 기반 라이브러리
웹 클라이언트 - 서버 간의 실시간 양방향 통신을 가능하게 한다.

## 장점
---
### 자유로운 이벤트명 작명
WebSocket에서 Type에 맞춰서 조건문으로 메시지를 분류해야 했다면 이벤트명으로 간단하게 분류할 수 있다.

### 자유로운 데이터 전송
String 데이터에만 국한되지 않고 모든 데이터를 원할 때마다 전송할 수 있다.

### 호횐성
WebSocket을 사용하지 못하는 경우에는 다른 대체 방법을 사용한다.

### 재연결
서버와의 연결이 끊기거나 불안정하다면 Socket.io는 재연결을 시도한다.

### Callback 함수 실행
클라이언트 측의 함수를 서버에서 실행 시킬  수 있다. 이때 함수는 마지막 인자여야만 한다.

1. 클라이언트가 마지막 인자로 콜백 함수를  넘긴다.
2. 서버 측에서 함수를 호출한다.
3. 클라이언트 측에서 콜백 함수를 실행한다.

### 다양한 기능 제공
WebSocket에서는 일일이 개발하여 사용해야 하는 기능들을 많이 제공한다.
대표적으로 room 기능이 있다. 다양한 기능들을 더 알아보고 싶다면 [공식문서](https://socket.io/docs/v4/)를 참고하자.


## 설치
---
```bash
npm i socket.io
```

## Socket.io Admin UI
---
[Admin UI](https://admin.socket.io/#/) 이 주소에서 나의 사이트에 대한 통계 분석 자료를 확인할 수 있다.
접속한 Client, 생성된 Rooms(private 포함)등등...


### 설치
```bash
npm i @socket.io/admin-ui
```

### 설정
```js
import { instrument } from "@socket.io/admin-ui";

const wsServer = new Server(httpServer, {
  cors: {
    origin: ["https://admin.socket.io"],
    credentials: true,
  },
});

instrument(wsServer, {
  auth: false,
});
```



## 참고 자료
---
https://www.daleseo.com/socket-io/