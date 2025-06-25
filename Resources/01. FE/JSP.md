## **JSP(Java Server Pages)란?**

---

HTML 코드에 Java코드를 넣어 동적 웹페이지를 생성하는 도구.

JSP 실행 시 자바 서블릿으로 변환되어 서버에서 동작하여 클라이언트에 응답한다.

  

> **서블릿(Servlet)이란?**  
> 웹페이지를 동적으로 생성하기 위한 서버 측 프로그램을 말한다.  

  

## JSP vs Servlet

---

JSP와 Servlet은 하는 동작이 결과적으로는 같다.

하지만 JSP는 HTML 내부에 Java 코드가 들어가 HTML 코드를 작성하기 간편하다.

서블릿은 Java 내부에 HTML 코드가 들어가 일고 쓰기가 굉장히 불편하다.

  

## 동작원리

---

그렇다면 왜 JSP와 Servlet을 함께 배우는 걸까?

이는 JSP의 동작원리와 관련이 있다.

  

1. 클라이언트 측에서 JSP 파일 요청
2. JSP 컨테이너가 JSP 파일 읽기 작업 수행
3. JSP 컨테이너가 JSP 파일 변환 작업을 수행하여 Servlet 파일 생성
4. 위 파일 다시 Class 파일로 컴파일 수행
5. HTML을 생성하여 JSP 컨테이너에게 전달
6. JSP가 HTTP 프로토콜로 HTML 페이지 클라이언트에게 반환

  

이처럼 JSP로 작성된 프로그램은 서버에 요청 시 Servlet 파일로 변환되어 순수한 HTML을 반환하게 된다.

  

## 참고 자료

---

[https://javacpro.tistory.com/43](https://javacpro.tistory.com/43)