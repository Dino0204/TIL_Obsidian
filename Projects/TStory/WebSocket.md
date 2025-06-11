![](https://blog.kakaocdn.net/dn/3iRHa/btsN1MsIYT0/y4BOaEKPU9AC0oo5agT7E0/img.jpg)

장기 실행 연결을 통해 클라이언트와 서버 간의 양방향 통신을 가능하게 하는 프로토콜
데이터를 실시간으로 주고 받을 수 있어서 지연시간이 짧다.

## HTTP Protocol vs WebSocket
---
HTTP는 클라이언트의 요청에 따라 서버가 응답하는 형식인 스테이스리스(stateless) 프로토콜으로 단방향의 흐름을 지니기 때문에 스테이드풀(stateful) 프로토콜인 WebSocket이 등장하게 되었다.

## WebSocket 사용처
---
### 온라인 게임
사용자 간의 빠른 실시간 통신을 가능하게 하여 온라인 게임에서 쓰인다.

### 커뮤니케이션 플랫폼
실시간 채팅 및 정보 공유를 가능하게 하여 쓰인다.

### 라이브
스포츠, 콘서트와 같은 스트리밍 비디오를 가능하게 하여 쓰인다.

## WebSocket 통신 과정과 HandShake
---
HTTP의 GET 요청 헤더에 Connection, Upgrade을 추가하여 서버에 전송
-> WebSocket 프로토콜로 전환!
-> 이와 같이 WebSocket 통신 전 HTTP 메시지를 주고 받는 것을 **HandShake**라고 부른다.

```js
Connection: Upgrade  
Upgrade: websocket  
Sec-WebSocket-Key: blablablabla...  
Sec-WebSocket-Version: 13  
```

## WebSocket Client
---
WebSocket 통신을 하기 위해서는 ws, wss Protocol을 사용하여 서버의 URL을 넘겨주어야 한다.

> WebSocket Secure(wss)란?  
> SSL인증서를 통해 Websocket의 보안을 강화시킨 프로토콜

### WebSocket 객체
WebSocket을 사용하기 위해 객체를 생성해주자.

```js
const socket = new WebSocket("ws://example.com/socketserver")  
```

### WebSocket 이벤트
WebSocket의 다양한 이벤트들을 알아보자.

1. 연결이 성공하면 트리거된다.
```js
socket.onopen = (event) => { console.log("서버와 연결.") };
```

2. 연결이 닫히면 트리거된다.
```js
socket.onclose = (event) => { console.log("서버와 연결 종료.") };  
```

3. 서버로부터 메시지가 수신되면 트리거된다.
```js
socket.onmessage = (event) => { console.log("서버에서 받은 메시지:", event.data) }; 
```

4. 클라이언트에서 서버로 메시지를 보낼 수 있다.
```js
socket.send("서버 하이.")  
```

5. 통신 중 오류가 발생되면 트리거된다.
```js
socket.onerror = (event) => { console.error("에러:", event) };  
```

## Node.js
---
Node.js에서 WebSocket 이벤트들을 다뤄보자.

```js
const WebSocket = require("ws");  

const wss = new WebSocket.Server({ port: 8080 });  

wss.on("connection", (socket) => {  
  console.log("클라이언트가 접속하였습니다.");  

  socket.on("message", (message) => {  
    console.log("받은 메세지:", message);  
    socket.send("메세지 수신완료.");  
  });  

  socket.on("close", () => {  
    console.log("클라이언트가 접속을 끊었습니다.");  
  });  
});  
```

## Socket.io
---
WebSocket의 호환성 문제를 해결할 수 있게 도와주는 라이브러리
인터넷 브라우저와 같은 구버전의 브라우저에서도 WebSocket이 구동할 수 있게 해준다.

### 설치

```bash
npm add socket.io  
```

### 서버 구성

```js
import { createServer } from "node:http";
import { readFile } from "node:fs";
import { fileURLToPath } from "node:url";
import { dirname, join } from "node:path";
import { Server } from "socket.io";

// URL -> Path
const __dirname = dirname(fileURLToPath(import.meta.url));

// Server Option 설정
const server = createServer((req, res) => {
  readFile(join(__dirname, "index.html"), (err, data) => {
    res.writeHead(200, { "Content-Type": "text/html" });
    res.end(data);
  });
});

// Server 객체 생성
const io = new Server(server);

// socket -> 각 클라이언트
io.on("connection", (socket) => {
  // id -> 각 클라이언트 식별자
  io.emit("message", `${socket.id} 님이 연결되었습니다.`);

  socket.on("message", (msg) => {
    io.emit("message", `${socket.id}: ${msg}`);
  });

  socket.on("disconnect", () => {
    socket.broadcast.emit("message", `${socket.id} 님의 연결이 끊어졌습니다.`);
  });
});

// PORT 3000 Server Open
server.listen(3000, () => {
  console.log("http://localhost:3000 에서 서버 구동 중...");
});
```

### HandShake
node:http 모듈로 HTTP 서버를 생성 후 socket.io 모듈의 Server 클래스를 이용하여 WebSocket 서버를 생성한다.

### 클라이언트에 메시지 전송하기
클라이언트에서 이벤트를 수신하려면 이와 같은 이벤트 이름으로 일치시켜 수신할 수 있다. 
또한 각 socket 객체에는 고유한 id값이 들어있어서 각 클라이언트를 식별할 수 있다.

```js
io.emit("message", `${socket.id}: ${msg}`);
```

### 클라이언트 접속 해제 메시지 전송하기
해당하는 클라이언트를 제외한 모든 클라이언트에게 접속 해제 메시지를 전송할 수 있다.

```js
socket.broadcast.emit("message", `${socket.id} 님의 연결이 끊어졌습니다.`);
```


### 서버에 메시지 전송하기
클라이언트도 서버와 같이 메시지를 서버로 전송할 수 있다.

```js
<script type="module">
  import { io } from "https://cdn.socket.io/4.7.5/socket.io.esm.min.js";

  // Socket
  const socket = io();
  const ul = document.querySelector("ul");
  
  // Server에서 Message를 받아와 출력 -> GET
  socket.on("message", (msg) => {
    const li = document.createElement("li");
    li.textContent = msg;
    ul.appendChild(li);
    window.scrollTo(0, document.body.scrollHeight);
  });

  const form = document.querySelector("form");
  const input = document.querySelector("input");
  
  // Server에 Message 전송 -> POST
  form.addEventListener("submit", (event) => {
    event.preventDefault();
    if (input.value) {
      socket.emit("message", input.value);
      input.value = "";
    }
  });
</script>
```

## 참고 자료
---
[WebSocket](https://www.daleseo.com/websocket/)
[Socket.io](https://www.daleseo.com/socket-io/)
[WebSocket](https://appmaster.io/ko/blog/websocket-api-guseong-yoso-mic-gineung)
[Protocol](https://blog.leaphop.co.kr/blogs/56/WebSocket_%ED%86%B5%EC%8B%A0%EC%97%90_%EB%8C%80%ED%95%B4_%EC%95%8C%EC%95%84%EB%B3%B4%EA%B8%B0)
