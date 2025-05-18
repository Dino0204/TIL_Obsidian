## [[Node.js]]에서 Middleware 사용하기
---
### 모든 요청에 미들웨어 실행하기
아래 코드로 요청을 하게 되면 모든 클라이언트 요청-응답 사이에 미들웨어가 작동하게 된다. 
```js
app.use(path, middleware)
```

### 각 요청에 미들웨어 실행하기
아래 코드로 요청을 하게 되면 이 `path`와 `HTTP Method`로 접근하는 클라이언트 요청-응답 사이에 미들웨어가 작동하게 된다.
```js
app.HTTP_METHOD(path, middleware)
```

> HTTP_METHOD | GET, POST...

### JWT로 미들웨어 알아보기

1. 해당 요청에 JWT 인증을 요구하는 Middleware를 인자로 넣어준다.
```js
// routes/room.route
const express = require("express");
const router = express.Router();
const authJWT = require("../middleware/authJWT");
const { create } = require("../controllers/room.controller");

router.post("/create", authJWT, create);

module.exports = router;
```

2.  해당 경로로 유저가 토큰과 함께 요청을 보내면 토큰이 유효한지 판단하여 응답을 해준다.
   아래 코드에서 미들웨어 함수의 콜백 매개변수로 `next()`라는 함수가 보일 것이다.
   이 함수를 실행하면 다음 미들웨어로 응답을 넘길 수 있게 된다. 미들웨어가 여러 개라면 상황에 따라 사용해보자.

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

3. JWT AccessToken 발급과 검증을 하는 코드이다.
```js
// jwt-util
const jwt = require("jsonwebtoken");
require("dotenv").config();

module.exports = {
  // access token 발급
  sign: (user) => {
    const { email, password } = user;
    const payload = {
      email,
      password,
    };

    return jwt.sign(payload, process.env.JWT_SECRET, {
      algorithm: "HS256",
      expiresIn: process.env.JWT_AT_EXPIRES_IN,
    });
  },

  // access token 검증
  verify: (token) => {
    try {
      const decoded = jwt.verify(token, process.env.JWT_SECRET);
      return {
        ok: true,
      };

    } catch (err) {
      return {
        ok: false,
        message: err.message,
      };
    }
  }
};
```

### 미들웨어 `next()` 더 알아보기
미들웨어는 한 요청-응답 사이에 많이 끼워 넣을 수 있다. 이 때 미들웨어는 모두 동일한 요청 및 응답 개체를 사용하기 때문에 클라이언트로 응답을 보내면(`res.json()`) 다음 미들웨어들은 모두 건너뛰게 된다. 이 때 `next()`를 호출하여 다음 미들웨어들의 작업을 실행할 수 있지만 `res.json()`은 모든 응답 스트림을 종료하기 때문에 응답을 추가로 클라이언트에 전송할 수는 없다.

유의할 점으로는 응답이 없는 미들웨어 함수에서는 반드시 `next()`를 호출해주어야 한다. 호출해주지 않는다면 해당 요청은 정지된 채로 방치되게 된다.

```js
app.use(cors, authJWT)
```

cors, JWT 요청을 미들웨어 함수로 받아 동시에 처리하는 과정이다. cors 미들웨어에는 `next()`가 내장되어 있기 때문에 authJWT에서 응답을 받아 작업을 수행할 수 있다.