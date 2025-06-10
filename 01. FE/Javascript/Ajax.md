**Asynchronous** **JavaScript** **And** **XML**

JavaScript와 Xml을 이용한 비동기적 정보 교환 기법(JavaScript Library)

## 특징
---

### 페이지 일부 변경 가능
전체 페이지를 새로고침하지 않고도 웹 페이지의 일부분만 업데이트할 수 있다.

### 비동기적 데이터 처리
JavaScript 내에 HTML, CSS, DATA 등을 담아 서버에 요청한다. HTML, CSS를 먼저 실행한 후 데이터를 가져와 로딩한다.

### HTTP 프로토콜 활용
XMLHttpRequest를 이용해 서버에 XML 데이터만을 비동기적으로 요청하는 기법을 사용한다.

## 코드 예시
---
```javascript
// XHR 객체 생성
const XHR = new XMLHttpRequest()

// 이벤트 감지
XHR.addEventListener("load", 응답함수)

// GET 또는 POST
XHR.open("GET", '주소')

// 요청
XHR.send()

// 받아온 응답 값 콘솔에 출력
const 응답함수 = (event) => {
    console.log(event.currentTarget.response)
}
```

## 현재 사용 현황
---
요즘에는 XML 대신 **JSON**을 주로 사용한다.

> **XML이란?**
> 많은 종류의 데이터를 기술할 수 있는 마크업 언어
> 시스템끼리의 데이터를 쉽게 주고받을 수 있게 설계 → HTML 한계를 극복

## 장점
---
### jQuery를 이용한 쉬운 구현
간단하고 직관적인 구현이 가능하다.

### 상태 기반 실행 흐름 조정
상태(Error, Success, Complete)를 통한 실행 흐름을 조정할 수 있다.

## 단점
---
### jQuery 없이는 복잡함
jQuery를 사용하지 않으면 구현이 복잡해진다.

### Promise 기반이 아님
최신 JavaScript의 Promise 패턴을 지원하지 않는다.

## 참고 자료
---
- [AXIOS란? feat. React](https://velog.io/@dusunax/AXIOS%EB%9E%80-feat.-React)
- [AJAX 기본 개념](https://jbground.tistory.com/4)
- [AJAX 실습 가이드](https://cocoon1787.tistory.com/756)