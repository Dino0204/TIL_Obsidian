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

html과 같은 정적 콘텐츠를 미리 로딩하고 동적 콘텐츠를 나중에 로딩한다.

## 어떻게 사용할 수 있을까?

---

PWA는 기본적으로 웹을 기반으로 구성되기 때문에 웹 기술을 사용하여 개발 할 수 있다.

가장 기본적인 HTML, CSS, JS부터 React까지 다양하게 사용할 수 있다.

이 때 웹과 앱을 모두 지원하기 위해 반응형 웹 디자인을 해야하는 것을 유의해두자.

## 설치와 초기 설정

---

필자는 이번에 Next.js의 PWA를 구성하게 도와주는 next-pwa를 사용하였다.

만약 최신 버전에서 호환성 문제가 일어난다면 최신 버전을 더 잘 지원하는 [**@ducanh2912/next-pwa](https://ducanh-next-pwa.vercel.app/docs/next-pwa)** 를 설치하도록 하자.

### 설치

1. Next.js 설치

```jsx
npx create-next-app@latest
```

1. next-pwa 설치

```jsx
npm install next-pwa
```

### manifest.json

[Manifest Generator](https://progressier.com/pwa-manifest-generator)에서 쉽게 manifest 파일을 설정해준 뒤 사용해보자.

```sql
{
  "theme_color": "#1B1A55",
  "background_color": "#FFFFFF",
  "icons": [
    {
      "purpose": "maskable",
      "sizes": "512x512",
      "src": "/icon512_maskable.png",
      "type": "image/png"
    },
    {
      "purpose": "any",
      "sizes": "512x512",
      "src": "/icon512_rounded.png",
      "type": "image/png"
    }
  ],
  "orientation": "portrait",
  "display": "standalone",
  "dir": "auto",
  "lang": "ko-KR",
  "name": "NASA",
  "short_name": "nasa",
  "description": "nasa open api for study"
}
```


|색상|설명|
|---|---|
|Theme Color|탭 부분의 보라 컬러|
|Background color|스플래시 이미지, 로딩 화면의 배경색|

|display 속성|설명|
|---|---|
|Standalone(추천)|주소 표시줄, UI 요소가 제거된 네이티브 앱과 가장 비슷한 환경|
|FullScreen|콘텐츠 이외의 모든 요소가 숨겨지는 환경|
|Minimal-ui|뒤로가기, 새로고침등의 최소한의 UI 요소가 표시되는 환경|
|Browser|일반 브라우저와 동일한 환경|

### next.config.ts

Next.js에 PWA를 적용해보자.

```sql
import withPWA from "next-pwa";

const nextConfig = {
	// Next.js 외부 이미지 접근 허용
  images: {
    remotePatterns: [
      {
        protocol: "http" as const,
        hostname: "**",
      },
      {
        protocol: "https" as const,
        hostname: "**",
      },
    ],
  },
};

export default withPWA({
	// build 시 Service Worker, Workbox 파일 public 폴더에 생성
	// (루트 경로에서 동작하게 하려면 무조건 public 폴더에 생성해야함)
  dest: "public",
  
  // Service Worker 등록
  register: true,
  
  // 새로운 Service Worker 생성 시 원래의 Service Worker와 바로 교체
  skipWaiting: true,
  
  // 개발 환경에서 실행 시 PWA 비활성화
  disable: process.env.NODE_ENV === "development",
})(nextConfig);
```


### 배포 및 실행

PWA가 잘 적용되었는지 확인해주기 위해 Vercel로 배포하여 확인 하여 보니 잘 작동하는 것을 확인 할 수 있었다. 앱이 궁금하다면 [이 주소](https://pwa-dino-nasa.vercel.app/apod)로 접속하면 된다. (시간이 지나면 닫혀있을 수도 있다.)

## 예제

---

### [Pinterest](https://kr.pinterest.com)

### [StarBucks](https://app.starbucks.com)

위 사이트에 접속하여 개발자 도구를 열고 manifest 파일을 확인하면 PWA로 구현된 것을 알 수 있다.

## 결론

---

PWA는 모바일 + 웹 환경을 구성해야 할 때 개발 시간과 비용을 아낄 수 있는 좋은 방법 중 하나인 것 같다.

다음 시간에는 React Native를 공부해봐도 좋을 것 같다.

## 참고 자료

---

[https://f-lab.kr/insight/importance-of-pwa-in-frontend-development](https://f-lab.kr/insight/importance-of-pwa-in-frontend-development)

[https://ssow93.tistory.com/56](https://ssow93.tistory.com/56)

[https://p-web.co.kr/server/bbs/board.php?bo_table=free&wr_id=90&page=6](https://p-web.co.kr/server/bbs/board.php?bo_table=free&wr_id=90&page=6)

[https://nextjs.org/docs/app/building-your-application/configuring/progressive-web-apps](https://nextjs.org/docs/app/building-your-application/configuring/progressive-web-apps)

[https://gist.github.com/cdnkr/25d3746bdb35767d66c7ae6d26c2ed98](https://gist.github.com/cdnkr/25d3746bdb35767d66c7ae6d26c2ed98)

[https://api.nasa.gov/](https://api.nasa.gov/)