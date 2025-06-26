## JSON 서버 사용이유
---
임시서버를 만들어 테스트 및 작업량, 작업속도 감소

## Data 준비
--- 
`root`
```JSON
//db.json
{
  "token": {
    "access_token": "1234",
    "userId": 123
  },
  "test": [
    {
      "id": 1,
      "title": "json-server",
      "body": "굿"
    },
    {
      "id": 2,
      "title": "백엔드가 없을때는",
      "body": "json-server"
    }
  ]
}
```

## 서버 열기
---
###  서버 설치
```bash
npm -g add json-server
```

### 서버 열기
```node
json-server ./db.json —port xxxx
json-server --watch db.json —port xxxx
```

```bash
http://localhost:4000/token
http://localhost:4000/test
```

## 참고 자료
---
[JSON-Server](https://sewonzzang.tistory.com/3)