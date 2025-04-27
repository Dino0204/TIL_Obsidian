## 목적

---

K-PaaS 대회에 친구들과 함께 출전하게 되어 새롭게 배워야 할 기술이다.

## Progressive Web App이란?

---

PWA는 Progressive Web App 그대로 해석하면 진보적인 웹 앱이라는 뜻으로 웹과 앱의 장점을 결합한 기술이다. PWA는 기본적으로 Web으로 구성되지만 네이티브 앱의 특성인 오프라인 실행, 빠른 로딩 시간, 홈 화면 위젯 추가 기능등을 지원한다.

## PWA, 왜 사용할까?

---

### 높은 사용자 경험 제공

네이티브 앱의 장점인 오프라인에서의 사용과 같은 높은 사용자 경험을 제공한다.

### 빠른 성능

기본적으로 브라우저에서 실행되기 때문에 초기, 로드 시 속도가 모두 빠르다.

### 번거롭지 않은 배포

앱 스토어와 같은 검토 과정이 필요한 절차를 거치지 않고 빠르게 배포할 수 있다.

## 핵심 기술

---

PWA를 구성하는 핵심 기술들을 알아보자.

### 서비스 워커(Service Worker)

네트워크 요청을 가로채고 캐싱하는 역할을 수행하며 백그라운드에서 실행되는 스크립트

오프라인 지원, 데이터 캐싱, 푸시 알림 등의 기능을 구현할 수 있다.

### 매니페스트

PWA에 대한 메타데이터를 제공하는 JSON 파일

홈 화면 위젯 아이콘, 이름, 시작 URL 등을 정의한다.

### 셸 아키텍쳐

콘텐츠가 로딩되기 전 UI의 기본 구조를 미리 로딩하여 높은 UX를 제공하는 아키텍쳐

## 어떻게 사용할 수 있을까?

---

PWA는 기본적으로 웹을 기반으로 구성되기 때문에 웹 기술을 사용하여 개발 할 수 있다.

가장 기본적인 HTML, CSS, JS부터 React까지 다양하게 사용할 수 있다.

이 때 웹과 앱을 모두 지원하기 위해 반응형 웹 디자인을 해야하는 것을 유의해두자.

## 설치와 초기설정

---

필자는 이번에 Next.js와 PWA를 구성하게 도와주는 next-pwa를 사용하였다.

1. Next.js 설치

```jsx
npx create-next-app@latest
```

1. next-pwa 설치

```jsx
npm install next-pwa
```

## 예제

---

## 결론

---

## 참고 자료

---

[https://f-lab.kr/insight/importance-of-pwa-in-frontend-development](https://f-lab.kr/insight/importance-of-pwa-in-frontend-development)

[https://ssow93.tistory.com/56](https://ssow93.tistory.com/56)

[https://p-web.co.kr/server/bbs/board.php?bo_table=free&wr_id=90&page=6](https://p-web.co.kr/server/bbs/board.php?bo_table=free&wr_id=90&page=6)

[https://nextjs.org/docs/app/building-your-application/configuring/progressive-web-apps](https://nextjs.org/docs/app/building-your-application/configuring/progressive-web-apps)

[https://gist.github.com/cdnkr/25d3746bdb35767d66c7ae6d26c2ed98](https://gist.github.com/cdnkr/25d3746bdb35767d66c7ae6d26c2ed98)