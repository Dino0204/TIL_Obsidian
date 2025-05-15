  

## Fetch

---

  

- 개념 : JS 기본 라이브러리
- 사용이유 : API 연동을 하기 위해서 사용

  

### 특징

- promise 객체 반환
- json으로 바꿔주어야 함 (수동)
- then, catch, finally  
    : promise의 후속 처리 메서드  
    

  

### 문법 구성

  

GET (Default)

- 자원을 가져올 때

```JavaScript
fetch("https://jsonplaceholder.typicode.com/posts/1")
  .then((response) => response.json())
  .then((data) => console.log(data))
  
  // 응답 Promise의 body객체를 json형태로 바꾸어 출력
```

  

POST

- 자원을 생성할 때

```JavaScript
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "POST", // 메서드 옵션 설정
  headers: { // Json 포맷을 사용한다고 알려줌 -> 종종 못 읽을 수 있음
    "Content-Type": "application/json",
  },
  body: JSON.stringify({ // 자원 생성 요청 본문
    title: "Test",
    body: "I am testing!",
    userId: 1,
  }),
})
  .then((response) => response.json())
  .then((data) => console.log(data))
  
```

  

PUT

- 자원 변경을 요청할 때

```JavaScript
fetch("https://jsonplaceholder.typicode.com/posts", {
  method: "PUT", // 메서드 옵션 설정
  headers: {
    "Content-Type": "application/json",
  },
  body: JSON.stringify({
    title: "Test",
    body: "I am testing!",
    userId: 1,
  }),
})
  .then((response) => response.json())
  .then((data) => console.log(data))
```

  

DELETE

- 자원을 삭제할 때

```JavaScript
fetch("https://jsonplaceholder.typicode.com/posts/1", {
  method: "DELETE",
  // 보낼 데이터가 없기 때문에 header, body가 필요 없음
})
  .then((response) => response.json())
  .then((data) => console.log(data))
```

  

예시

```JavaScript
fetch('https://jsonplaceholder.typicode.com/todos/1')
 .then(response => response.json())   // 응답을 json으로 변경한 promise 반환 
 .then(json => {
   console.log(`${json} ...fetch 데이터`)
 })
```

  

  

### 장단점

- 장점
    - 별다른 설치가 필요없음
- 단점
    - 코드가 길어짐
    - 직관적이지 않음

  

## Axios

---

  

- 개념 : Promise 기반 HTTP 비동기 통신 외부 라이브러리
- 사용이유 : Front - Back 간 통신을 쉽게 하기 위해서  
    Ajax와 함께 사용  
    

  

### 특징

- XMLHttpRequest , http api (운영환경에 따라서 사용)
- ES6 Promise API 사용
- HTTP Methods 사용
- Request , Response 데이터 변형
- HTTP 요청 취소 가능
- Response JSON형태로 자동 변형

  

  

  

### 설치

  

```JavaScript
$npm install axios
```

```JavaScript
import axios from 'axios';
```

### 문법 구성

  

|   |   |   |
|---|---|---|
|속성|설명|부가 설명|
|method|HTTP 요청 방식 (GET, POST 등)|.get() / .post()|
|url|요청을 보낼 서버 URL|.get(url)|
|baseURL|URL 앞에 붙는 기본 경로|baseUrl + url|
|headers|요청 헤더 설정|무슨 형식을 보낼 건지|
|data|요청 본문에 포함될 데이터|보내는 데이터|
|params|URL 파라미터로 보낼 데이터||
|timeout|요청 제한 시간||
|responseType|응답 데이터 타입||
|responseEncoding|응답 인코딩||
|transformRequest|요청 데이터 변환 함수||
|transformResponse|응답 데이터 변환 함수||
|withCredentials|자격 증명 포함 여부||
|auth|기본 인증 정보||
|maxContentLength|최대 컨텐츠 길이||
|validateStatus|응답 상태 유효성 검사 함수||
|maxRedirects|최대 리다이렉트 횟수||
|httpAgent / httpsAgent|사용자 정의 에이전트||
|proxy|프록시 설정||

```JavaScript
axios({
	url : `웹문서`,
	method : 'get' // Default: get
	// 보낼 데이터
	data: {
		doorIsOpen : 1
	}
});
```

  

### 장단점

- 장점  
    1. 많은 기능 지원  
    2. 문법 간소화 → ex) Json 변환 필요없음  
    
- 단점  
    설치 필요  
    

→ 간단할 때는 Fetch , 복잡할 때는 Axios

  

  

## Axios Vs Fetch

---

  

|   |   |   |
|---|---|---|
||Axios|Fetch|
|설치여부|x|o|
|보호|XSRF|x|
|속성|data|body|
|속성에 포함|object|stringify()|
|성공 여부|200 / OK|OK|
|JSON|자동 변환|.json() 사용|
|요청|취소, 타임아웃 가능|x|
|HTTP 요청 가로챔|o|x|
|다운로드|o|x|

  

## 프로젝트

---

  

https://github.com/Dino0204/React-Axios-Fetch-Project

  

## 참고 자료

- [https://axios-http.com/kr/docs/intro](https://axios-http.com/kr/docs/intro)
- [https://velog.io/@dusunax/AXIOS란-feat.-React](https://velog.io/@dusunax/AXIOS란-feat.-React)
- [https://velog.io/@chaeshee0908/React-Axios로-User-데이터-받아-출력하기](https://velog.io/@chaeshee0908/React-Axios로-User-데이터-받아-출력하기)
- [https://jsonplaceholder.typicode.com/](https://jsonplaceholder.typicode.com/)
- [https://kindjjee.tistory.com/145](https://kindjjee.tistory.com/145)