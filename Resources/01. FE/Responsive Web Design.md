## 목적
---
후에 다양한 프로젝트에서 사용할 **반응형 웹 디자인**에 대한 기초를 잡기 위해서 공부하게 되었다.

## 다양한 유형의 웹 페이지
---
반응형 웹 디자인을 알아보기 전 다양한 종류의 웹 페이지들을 간단하게 알아보자.

### 정적 웹 페이지(Static Web Page)

사용자가 웹 페이지를 요청하면 서버가 미리 저장된 웹 페이지를 보내주는 방식이다.

주로 회사나 개인의 소개 페이지에서 사용된다.

### 동적 웹 페이지(Dynamic Web Page)

사용자의 요청에 따라 서버가 동적으로 저장된 웹 페이지를 보내주는 방식이다.

주로 블로그, 뉴스 사이트에서 사용된다.


### 동적 웹 페이지를 구성하는 방식

1. **CSR(Client Side Rendering)**  
    정적 웹 페이지를 서버에서 가져온 후 이후 데이터를 요청하는 방식이다.  
    클라이언트에서 많은 부담을 가지게 된다.  
    
2. **SSR(Server Side Rendering)**  
    데이터가 삽입된 동적 웹 페이지를 서버에서 가져오는 방식이다.  
    
3. **MPA(Multi Page Application)**  
    새로운 페이지를 요청할 때마다 그 페이지에 해당하는 정적 페이지를 불러온 후 전체 페이지를 다시 렌더링하는 방식이다.  
    
4. **SPA(Single Page Application)**  
    모든 정적 페이지를 웹 페이지 최초 접속 시 한 번에 가져오고 새로운 페이지에 대한 요청마다 필요한 데이터를 전달 후 페이지를 갱신한다.  
    

### 인터렉티브 웹 페이지(Interective Web Page)
사용자와 **상호작용**하는 웹 페이지를 의미한다.
사용자와의 상호작용을 통해 실시간으로 웹 페이지가 변경된다.

## 반응형 웹 디자인(Responsive Web Design)
---
이제 본격적으로 반응형 웹 디자인에 대해서 알아보자.

반응형 웹 디자인은 다양한 화면 크기에 따라 자동으로 레이아웃이 뒤바뀌는 디자인 방식이다.

다양한 기기에서 최적화된 경험을 제공하며 주로 CSS의 **미디어 쿼리** 기능을 통해 구현한다.

### 왜 반응형 웹 디자인을 적용해야 할까?
첫 번째, 웹 페이지의 **가독성**을 높여준다.
크기를 조정하거나 요소의 배치를 바꾸어 가독성을 높여준다. **Viewport**를 통해 구현할 수 있다.

> **뷰포트(Viewport)란?**  
>   
> 웹 페이지의 가시 영역.  
> 기기마다 맞춤형 레이아웃을 제공하여 **가독성**을 높일 수 있다.

두 번째, 들어가는 **자원과 비용을 줄여준다**.

별도로 다양한 기기마다 다른 레이아웃을 만들지 않아도 된다.  
DB에서도 데이터의 중복은 최대한 피하라고 하듯이 중복되는 작업은 하지 않는 것이 좋다.  

## 미디어 쿼리(Media Query)
---
이제 반응형 웹 디자인을 구현하는 방법을 알아보자.
Viewport와 미디어 타입에 따라 CSS를 분기 시키는 기법이다.

### 사용 방법
미디어 쿼리의 기본 구조이다.
```CSS
@media (조건문) { 실행코드 }
```

### 예제 코드1
```CSS
// 모바일 기기 (화면 크기 < 480px) 
@media (max-width: 480px) { ... } 
 
// 태블릿 기기  (화면 크기 < 768px) 
@media (max-width: 768px) { ... } 
 
// 데스크탑 기기 (화면 크기 < 1220px) 
@media (max-width: 1220px) { ... } 

// Default CSS 작동(화면 크기 > 1220px)
```

위와 같이 화면 크기에 따라 기기를 구분 짓는 기준을 **BreakPoint**라고 한다.

> **BreakPoint란?**  
>   
> 해상도로 기기를 구분 짓는 기준을 뜻한다.  
> 보통 **모바일 기기는 480px, 테블릿 기기는 768px, 데스크탑 기기는 1220px을 기준**으로 한다.  
>   
> [기준 통계 사이트](https://gs.statcounter.com/screen-resolution-stats)를 통해 직접 디자인에 맞는 기준을 결정 할 수 있다.

### 미디어 쿼리 기초 속성
**미디어 타입 목록**

|미디어 타입|설명|
|---|---|
|all|모든 미디어 타입|
|print|프린터|
|screen|컴퓨터 화면|
|speach|스크린 리더|

**프로퍼티 목록**

|프로퍼티|설명|
|---|---|
|width|viewport 너비(px)|
|height|viewport 높이(px)|
|device-width|디바이스 물리적 너비(px)|
|device-height|디바이스 물리적 높이(px)|
|orientation|디바이스 방향 (가로 방향: landscape, 세로방향: portrait)|
|device-aspect-ratio|디바이스의 물리적 width/height 비율|
|color|디바이스에서 표현 가능한 최대 색상 비트 수|
|monochrome|흑백 디바이스의 픽셀 당 비트 수|
|resolution|디바이스 해상도|

**논리 연산자 목록**

|논리 연산자|설명|
|---|---|
|and|여러 조건을 모두 만족할 때|
|or|여러 조건 중 하나라도 만족할 때|
|not|조건의 부정을 나타낼 때|

### 예제 코드2
```CSS
@media 미디어 타입 논리 연산자 (프로퍼티: 값) { ... }

@media screen and (max-height: 300px) { ... }
```

## 무슨 단위를 사용해야 할까?
---
반응형 웹 디자인을 할 때에는 **상대적 단위**를 사용해야 한다.

상대적 단위는 고정되지 않으며 유동적으로 바뀌는 단위를 말한다.

이제 대표적인 상대적 단위들을 알아보자.

### em
em은 element의 약자로 요소의 글꼴 크기를 기준으로 하는 단위이다.
만약 요소에 글꼴 크기가 정해져 있지 않다면 부모 요소의 글꼴 크기를 기준으로 한다.

### rem
rem은 root element의 약자로 html 즉, root의 글꼴 크기를 기준으로 하는 단위이다.

### viewport
사용자가 볼 수 있는 가시 영역을 기준으로 하는 단위이다.
각각 vw는 너비, vh는 높이를 기준으로 한다.

### %
%는 부모 요소의 크기를 기준으로 하는 단위이다.

### **각 상대적 단위를 사용하는 경우**
1. 부모 요소에 따라서 사이즈가 변경되어야 한다면 `%`나 `em`을 사용하자.
2. 브라우저 사이즈에 따라서 사이즈가 변경되어야 한다면 `viewport`나 `rem` 을 사용하자.
3. 요소에 따라서 사이즈가 변경되어야 한다면 `%`나 `viewport` 을 사용하자.
4. 폰트 사이즈에 따라서 사이즈가 변경되어야 한다면 `em`, `rem` 을 사용하자.

## 마치며…
---
반응형 웹 디자인을 공부할 때 더 알아두면 좋을 정보들을 간단히 적어보았다.

> **Flex VS Grid 뭘 사용해야 할까?**
> 
> 이미 결정된 레이아웃을 만들고 싶을 때는? **Grid** 속성!
> 
> 자유로운 레이아웃을 만들고 싶을 때는? **Flex** 속성!

> **반응형 VS 적응형 차이점이 뭘까?**  
>   
> 반응형을 물 적응형을 얼음으로 생각하면 이해하기 쉽다.  
> 반응형은 기기에 맞게 웹이 반응하지만 적응형은 각 기기에 맞게 따로따로 제작해 주어야 한다.  
> 기기에 따라 담을 수 있는 정보량의 차이가 크기 때문에 기기에 따라 조절해 주는 것이다.  

> **React-responsive 라이브러리**  
>   
> 미디어 쿼리를 React 내에서 사용하기 편하게 해주는 라이브러리이다.  
> **useMediaQuery**라는 훅을 통해 미디어 쿼리를 사용 할 수 있다.  
> 또한 컴포넌트, 변수등을 사용하여 재사용성이 높은 코드를 작성할 수 있다.  

## 참고 자료
---
[https://velog.io/@river-m/%EC%9B%B9-%ED%8E%98%EC%9D%B4%EC%A7%80-%EC%A0%95%EC%A0%81-%EB%8F%99%EC%A0%81-%EB%B0%98%EC%9D%91%ED%98%95-%EC%9D%B8%ED%84%B0%EB%A0%89%ED%8B%B0%EB%B8%8C](https://velog.io/@river-m/%EC%9B%B9-%ED%8E%98%EC%9D%B4%EC%A7%80-%EC%A0%95%EC%A0%81-%EB%8F%99%EC%A0%81-%EB%B0%98%EC%9D%91%ED%98%95-%EC%9D%B8%ED%84%B0%EB%A0%89%ED%8B%B0%EB%B8%8C)

[https://velog.io/@dyunge_100/WEB-%EC%A0%95%EC%A0%81-%EC%9B%B9-%ED%8E%98%EC%9D%B4%EC%A7%80%EC%99%80-%EB%8F%99%EC%A0%81-%EC%9B%B9-%ED%8E%98%EC%9D%B4%EC%A7%80](https://velog.io/@dyunge_100/WEB-%EC%A0%95%EC%A0%81-%EC%9B%B9-%ED%8E%98%EC%9D%B4%EC%A7%80%EC%99%80-%EB%8F%99%EC%A0%81-%EC%9B%B9-%ED%8E%98%EC%9D%B4%EC%A7%80)


[https://poiemaweb.com/css3-responsive-web-design](https://poiemaweb.com/css3-responsive-web-design)

[https://duektmf34.tistory.com/29](https://duektmf34.tistory.com/29)

[https://velog.io/@hihijin/HTMLCSS-%EC%8B%AC%ED%99%94-%EB%B0%98%EC%9D%91%ED%98%95-%EC%9B%B9](https://velog.io/@hihijin/HTMLCSS-%EC%8B%AC%ED%99%94-%EB%B0%98%EC%9D%91%ED%98%95-%EC%9B%B9)

  

[https://velog.io/@uni/CSS-%EB%B0%98%EC%9D%91%ED%98%95-%EC%9B%B9%EC%9D%84-%EB%A7%8C%EB%93%A4%EB%95%8C-%EC%96%B4%EB%96%A4-%EB%8B%A8%EC%9C%84%EB%A5%BC-%EC%93%B0%EB%8A%94%EA%B2%8C-%EC%A2%8B%EC%9D%84%EA%B9%8C](https://velog.io/@uni/CSS-%EB%B0%98%EC%9D%91%ED%98%95-%EC%9B%B9%EC%9D%84-%EB%A7%8C%EB%93%A4%EB%95%8C-%EC%96%B4%EB%96%A4-%EB%8B%A8%EC%9C%84%EB%A5%BC-%EC%93%B0%EB%8A%94%EA%B2%8C-%EC%A2%8B%EC%9D%84%EA%B9%8C)

  

[https://poiemaweb.com/css3-flexbox](https://poiemaweb.com/css3-flexbox)

[https://creativevista.tistory.com/entry/CSS3Flexbox-%EB%A7%88%EC%8A%A4%ED%84%B0%ED%95%98%EA%B8%B0-CSS3%EB%A1%9C-%EB%B0%98%EC%9D%91%ED%98%95-%EC%9B%B9%EC%82%AC%EC%9D%B4%ED%8A%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0](https://creativevista.tistory.com/entry/CSS3Flexbox-%EB%A7%88%EC%8A%A4%ED%84%B0%ED%95%98%EA%B8%B0-CSS3%EB%A1%9C-%EB%B0%98%EC%9D%91%ED%98%95-%EC%9B%B9%EC%82%AC%EC%9D%B4%ED%8A%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0)

[https://velog.io/@ikkim01/CSS-Flex-VS-Grid](https://velog.io/@ikkim01/CSS-Flex-VS-Grid)

  

[https://m.blog.naver.com/thetteurae/222106295070](https://m.blog.naver.com/thetteurae/222106295070)

[https://myung-ho.tistory.com/86](https://myung-ho.tistory.com/86)