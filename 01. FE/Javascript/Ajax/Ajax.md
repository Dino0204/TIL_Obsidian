---

  

- ==A==synchronous ==J==avaScript ==A==nd ==X==ml
    
    - 개념 : JavaScript와 Xml을 이용한 비동기적 정보 교환 기법
    - 분류 : JavaSciprt Library
    - 특징
        - 페이지 일부를 변경할 수 있음
        - JavaSciprt내에 HTML , CSS , DATA등을 담아 서버에 요청함 → HTML , CSS 먼저 실행 후 데이터를 가져와 로딩함
    - 방식
        
        - Http 프로토콜 : XMLHttpRequest
        - 위를 이용해 서버에 XML 데이터만을 비동기적으로 요청하는 기법
        - 코드
        
        ```JavaScript
        // XHR 객체 생성
        const XHR = new XMLHttpRequest()
        
        // 이벤트 감지
        XHR.addEventListener("load",응답함수)
        
        // GET 또는 POST
        XHR.open("GET", '주소')
        
        // 요청
        XHR.send()
        
        // 받아온 응답 값 콘솔에 출력
        const 응답함수 = (event) => {
        	console.log(event.currentTarget.response)
        
        }
        ```
        
    
      
    
    - 사용 : 요즘에는 XML 대신 JSON을 사용함
    
    > 참고 : Xml 이란?
    > 
    > - React Jsx 문법에서도 나오는 Xml
    > - 많은 종류의 데이터를 기술할 수 있는 마크업 언어
    > - 시스템끼리의 데이터를 쉽게 주고 받을 수 있게 설계 → HTML 한계를 극복
    
      
    
    - 장점
        - jQuery를 이용한 쉬운 구현 → 간단하고 직관적임
        - 상태(Error, Success, Complete)를 통한 실행 흐름 조정
    - 단점
        - jQuery를 사용하지 않으면 복잡함
        - Promise 기반이 아님

  

### 참고자료

[https://velog.io/@dusunax/AXIOS란-feat.-React](https://velog.io/@dusunax/AXIOS%EB%9E%80-feat.-React)

[https://jbground.tistory.com/4](https://jbground.tistory.com/4)

[https://cocoon1787.tistory.com/756](https://cocoon1787.tistory.com/756)