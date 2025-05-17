## [[HTTP]] Protocol의 문제점과 WebSocket의 등장 배경
---
현재 Web 통신의 기반인 HTTP는 클라이언트의 요청에 따라 서버가 응답하는 형식으로 항상 클라이언트의 요청이 존재해야 서버가 응답을 할 수 있게 됩니다. 이는 HTTP의 가장 큰 특징으로 실시간 통신이 필요 없는 Web에서는 최적화된 방식입니다. 하지만 실시간으로 통신을 해야 하는 경우 서버에서 변경 사항을 클라이언트 측에 반영해 줄 수 없기 때문에 다른 추가적인 방식을 사용해야 합니다. 이는 자원 낭비를 초래하기 때문에 실시간 양방향 통신을 지원하는 새로운 프로토콜인 WebSocket Protocol이 등장하게 되었습니다.

## WebSocket 통신 과정
---
WebSocket = HTTP(Upgrade)
WebSocket Protocol을 사용하기 위해서는 HTTP의 GET 요청과 헤더에 Connection, Upgrade을 추가하여 서버에 전송합니다.

### 헤더
```bash
GET /chat HTTP/1.1
Host: www.test.com
Connection: Upgrade
Upgrade: websocket
Sec-WebSocket-Key: blablablabla...
Sec-WebSocket-Version: 13
```

서버가 WebSocket을 지원하는 경우 [[101 ]]상태 코드를 반환하게 됩니다.
-> 이렇게 WebSocket 통신 전 HTTP 메시지를 주고 받는 것을 HandShake라고 부릅니다.

## WebSocket Client
---
본격적으로 Client에서 WebSocket을 사용해봅시다. WebSocket 통신을 하기 위해서는 http가 아닌  ws, wss Protocol을 사용하여 서버의 URL을 넘겨주어야 합니다.

ws vs wss
wss는 ssl인증서로 암호화된 ws

```js
const socket = new WebSocket("ws://www.test.com")
```


WebSocket 객체를 통해 4종류의 이벤트를 다룰 수 있습니다.

### open, message, error, close

```js
socket.onopen = (event) => {
  console.log("서버와 연결.");
};

socket.onmessage = (event) => {
  console.log("서버에서 받은 메시지:", event.data);
};

socket.onerror = (event) => {
  console.error("에러:", event);
};

socket.onclose = (event) => {
  console.log("서버와 연결 종료.");
};
```

### send
```js
socket.send("서버 하이.")
```

## WebSocket Server
---

### Node.js
```js
const WebSocket = require("ws");

const ws_server = new WebSocket.Server({ port: 8080 });

ws_server.on("connection", (socket) => {
  console.log("클라이언트가 접속하였습니다.");

  socket.on("message", (message) => {
    console.log("받은 메세지:", message);
    socket.send("메세지 잘 받았습니다!");
  });

  socket.on("close", () => {
    console.log("클라이언트가 접속을 끊었습니다.");
  });
});
```

## 라이브러리
---
### [[Socket.io]]


## 참고 자료
---
[WebSocket](https://www.daleseo.com/websocket/)
