## 특징
---
1. 호환성: Socket.io는 WebSocket을 "사용"하는 것이기 때문에 WebSocket을 사용하지 못하는 경우에는 HTTP long polling등과 같은 대체 방법을 사용하여 호환성을 증대시킨다.
2. 재연결: WIFI 연결이 잠시 끊겨도 Socket.io는 재연결을 시도한다.



## 설치
---
```bash
npm i socket.io
```

## 서버 구성
---
### HandShake
node:http 모듈로 HTTP 서버를 생성 후 socket.io 모듈의 Server 클래스를 이용하여 WebSocket 서버를 생성한다.


## 참고 자료
---
https://www.daleseo.com/socket-io/