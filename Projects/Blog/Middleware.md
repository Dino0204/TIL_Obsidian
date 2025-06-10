![](https://blog.kakaocdn.net/dn/ctOuQ9/btsNSN7cjbo/hyWuyR9f6nmFKwGUeQAFdK/img.png)

  

 서로 다른 앱의 **양 쪽**을 연결하여 데이터를 주고 받을 수 있도록 **중간에서 매개 역할** 하는 소프트웨어 -> 요청을 중간 지점에서 가로채기 때문에 Intercepter라고도 한다.


## 목적

---

디스코드 클론 코딩 토이 프로젝트를 위한 첫 걸음으로 Node.js로 서버를 구성하는 중 "Token을 자동으로 설정해주는 소프트웨어가 없을까?"하고 찾게 되었다.

## Middleware의 기능

---
- **프로토콜 변환 (Protocol Translation)**
- **메시지 큐 (Message Queuing)**
- **데이터베이스 연결 (Database Connectivity)**
- **보안 (Security)**
- **로깅 (Logging)**
- **인터페이스 (Interface)**
- **트랜잭션 (Transaction)**
- **분산 처리 (Distributed Computing)**
- **서비스 (Service)**
- **모니터링 (Monitoring)**
- **배포 (Deployment)**
- **라우팅 (Routing)**
- 기타등등...

-> 다수의 Middleware를 동시에 사용할 수도 있다.

## Middleware 왜 사용할까?
---
### Middleware를 사용하는 이유
요청과 응답을 쉽게 처리할 수 있고 코드의 중복성을 줄여주며 확장성이 높기 때문이다.

### Middleware를 자주 사용하는 로직
- 인증 ex) 로그인, 회원가입
- 로깅 및 모니터링 ex) 토큰 인증 중 발생한 오류 처리
- 라우팅 및 URL 재작성 ex) 로그인 전 콘텐츠로 접근 시 로그인 화면으로 리다이렉션


## Node.js에서 Middleware 사용해보기

---
### 각 요청 마다 Middleware 실행하기
`authJWT`라는 Middleware가 `create` 요청 시마다 중간의 요청을 가로채어 작동하게 된다.

```js
// routes/room.route
const express = require("express");
const router = express.Router();
const authJWT = require("../middleware/authJWT");
const { create } = require("../controllers/room.controller");

router.post("/create", authJWT, create);

module.exports = router;
```

### authJWT Middleware
해당 Middleware를 작동 시키고 싶은 부분에 추가하여 사용할 수 있다.

```js
// middleware/authJWT
const { verify } = require("../util/jwt-util");

const authJWT = (req, res, next) => {
  if (req.headers.authorization) {
    const token = req.headers.authorization.split("Bearer ")[1];
    const result = verify(token); 

    if (result.ok) {
      req.name = result.name;
      req.email = result.email;
      next();
    }

    else {
      res.status(401).send({
        ok: false,
        message: result.message,
      });
    }
  }
};

module.exports = authJWT;
```

### Node.js에서 다수의 Middleware 사용하기
Middleware 내부에서 `next()`를 호출하여 다음 미들웨어의 작업을 실행할 수 있다.
유의할 점으로는 응답이 없는 미들웨어 함수에서는 반드시 `next()`를 호출해주어야 한다는 점이다. 
호출해주지 않는다면 해당 요청은 정지된 채로 방치되게 되어 오류를 초래할 수 있다.
 
## 참고 자료

---

https://velog.io/@seosu2000/Middleware%EB%9E%80-%EB%AC%B4%EC%97%87%EC%9D%B8%EA%B0%80 
https://velog.io/@nemo/node-middleware-next
https://dev.to/hasanelsherbiny/what-is-middleware-26mk