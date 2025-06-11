## 목적
---
작년 아이디어 페스티벌부터 시작해서 현재까지 **styled 컴포넌트**와 같은 라이브러리를 내 머리 속에서 완전히 대체 해버린 TailWind가 연초에 업데이트를 진행했다고 들어서 한번 더 개념을 정리하고자 작성하게 되었다.

## TailWind란?
---
HTML, JSX등의 class 속성에 많은 유틸리티 클래스들을 조합하여 스타일링을 하는 CSS 프레임워크이다.

> 유틸리티 클래스란?
> 단 한가지의 기능만 수행하는 매우 적은 양의 CSS 코드를 담은 클래스를 뜻한다.

```css
.rounded-full{
	border-radius: 100%;
}

.font-bold {
  font-weight: 700;
}

.bg-blue-500{
	background-color: rgb(37 99 235);
}
```

## TailWind 설치하기
---

### 일반 설치
```jsx
npm install tailwindcss
```

### Vite를 사용할 경우 설치
```jsx
npm install tailwindcss @tailwindcss/vite
```

```css
/* vite.config.ts */
import { defineConfig } from 'vite'
import tailwindcss from '@tailwindcss/vite'
export default defineConfig({
  plugins: [
    tailwindcss(),
  ],
})
```

### Import
```css
/* globals.css */

@import "tailwindcss";
```

### TailWind를 설치하다보면…
PostCSS와 AutoPrefixer라는 단어들을 찾아 볼 수 있을 것이다. 이를 간단하게 알아보자.

> PostCSS
> JS 플러그인을 통해 스타일을 변환하는 도구.
> 지원하는 수많은 플러그인이 있으며 이를 통해 린팅등의 작업을 수행 할 수 있다.
> 

> AutoPrefixer
> PostCSS의 플러그인 중 하나.
> CSS를 파싱하여 VendorPreFixer를 자동으로 추가하여 준다.
> 

> VendorPrefixer(공급업체 접두사)
> CSS3 표준으로 기능이 확정되기 이전에 브라우저 측에서 실험적으로 제공하는 기능을 사용할 때 사용해야하는 접두사. 
> 브라우저 별 지원하지 않는 기능을 사용할 수 있다.

**VendorPrefixer**

| Browser            | Vendor Prefix |
| ------------------ | ------------- |
| IE or Edge         | -ms-          |
| Chrome             | -webkit-      |
| Firefox            | -moz-         |
| Safari             | -webkit-      |
| Opera              | -o-           |
| iOS Safari         | -webkit-      |
| Android Browser    | -webkit-      |
| Chrome for Android | -webkit-      |

## 인라인 CSS와의 차이점?
---

### 인라인 CSS 문법
```css
style = "
	border-radius: 0.25rem;
	background-color: rgb(59 130 246); 
	padding-top: 0.5rem; 
	padding-bottom: 0.5rem; 
	padding-left: 1rem; 
	padding-right: 1rem; 
"
```

### TailWind 문법
```css
className = "rounded bg-blue-500 px-4 py-2"
```

색상 클래스와 같은 유틸리티 클래스를 설정해준 모든 코드에서 공유하기 때문에 코드의 양을 획기적으로 줄일 수 있다.

## TailWind 처음에만 어렵다!
---

### 호불호가 갈리는 이유
TailWind는 사실 호불호가 굉장히 갈리는 편이다. 나는 호불호가 갈리는 가장 큰 이유를 가독성 때문이라고 생각한다. TailWind는 다른 CSS 라이브러리와 다르게 class 속성에 직접 스타일링 작업을 하기 때문에 HTML 코드가 굉장히 길어져서 알아보기 힘들게 된다. 하지만 나는 TailWind는 단점보다 장점이 더 많다고 생각한다.

### 클래스 기반 스타일링
필자도 처음에 같이 개발하는 동료의 권유로 TailWind를 접하게 되었을 때 이 말도 안되는 길이의 class는 뭐지 하며 불만을 토했던 적이 있었다. 하지만 이 불만은 TailWind를 많이 사용해보며 생각이 바뀌게 되었다.

TailWind의 인라인 CSS와 같은 class 속성에 직접 작성하는 방식은 장점으로도 볼 수 있다. HTML 태그와 구조에 맞게 바로바로 작성하고 클래스명 중복이 나지 않도록 고민하는 시간 자체가 사라지기 때문에 코드를 작성하는 시간이 매우 줄어들게 된다. 

### 사전 정의
TailWind가 4.0 version으로 업데이트 된 이후 이 파일을 더 이상 사용하지 않지만 참고용으로 들고 와봤다.

TailWind는 이와 같이 강력한 사전 정의 기능을 지원한다. 디자이너와 협업할 때 색상코드를 이 곳에 정의 하면 좋다.

```css
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ['./src/**/*.{html,js}'],
  theme: {
    colors: {
      'blue': '#1fb6ff',
      'purple': '#7e5bef',
      'pink': '#ff49db',
      'orange': '#ff7849',
      'green': '#13ce66',
      'yellow': '#ffc82c',
      'gray-dark': '#273444',
      'gray': '#8492a6',
      'gray-light': '#d3dce6',
    },
    fontFamily: {
      sans: ['Graphik', 'sans-serif'],
      serif: ['Merriweather', 'serif'],
    },
    extend: {
      spacing: {
        '8xl': '96rem',
        '9xl': '128rem',
      },
      borderRadius: {
        '4xl': '2rem',
      }
    }
  },
}
```

### 공식 문서
[공식 문서](https://tailwindcss.com)가 굉장히 잘 작성 되어 있다. 

![image.png](image.png)

TailWind의 단점 중 유틸리티 클래스명을 알아야 스타일링을 진행 할 수 있다는 단점이 있는데 공식 문서에서 최신 유틸리티 클래스명을 알 수 있고, 라이브러리 별 설치하는 방법, CSS 변수를 사용하여 글로벌 스타일링을 하는 방법 등 TailWind 공식 문서 하나 만으로도 설치 & 개발을 진행 할 수 있을 정도이다. 최신 유행하는 라이브러리 답게 업데이트가 빠르다는 것도 장점이다.

## TailWind version 4.0 뭐가 달라 졌을까?
---

출시날짜: **2025년 1월 23일**

### 빠른 빌드 속도
아래의 표를 보면 버전 업그레이드 후 얼마나 속도가 빨라졌는지 알 수 있다.

엔진 교체등의 작업을 통하여 속도를 높였다고 하는데 아직은 공부하지 않아도 될 듯 하다.

| 유형 | v3.4 | v4.0 | 개선 비율 |
| --- | --- | --- | --- |
| 전체 빌드 | 378ms | 100ms | 3.78x |
| 새로운 CSS 포함 증분 빌드 | 44ms | 5ms | 8.8x |
| 새로운 CSS 없는 증분 빌드 | 35ms | 192µs | 182x |

### 자동 콘텐츠 감지
이전에는 **tailwind.config.ts** 파일에 직접 경로를 설정하는 방법이었다면

```jsx
content: ['./src/**/*.{html,js,jsx,ts,tsx}']
```

현재는 휴리스틱 탐지 기법을 사용하여 자동으로 탐지하는 방식으로 변경되었다.

### 내장 Import 지원
**@import**를 사용하려면 **postcss.config.ts**에서 **postcss-import**와 같은 플러그인을 설치하여 설정하는 방법이었지만

```jsx
 export default {
  plugins: [
    "postcss-import",
    "@tailwindcss/postcss",
  ],
};
```

현재는 TailWind 내부에 통합된 **@import**로 CSS 파일을 가져올 수 있다. 

### CSS Configuration 간편화
**tailwind.config.ts** 파일에서 설정하던 CSS 관련 설정(ex 사전 정의 색깔등)을 직접 정의 할 수 있도록 바뀌었다.

```css
@theme {
  --font-display: "Satoshi", "sans-serif";
  --breakpoint-3xl: 1920px;
  --color-avocado-100: oklch(0.99 0 0);
  --color-avocado-200: oklch(0.98 0.04 113.22);
  --color-avocado-300: oklch(0.94 0.11 115.03);
  --color-avocado-400: oklch(0.92 0.19 114.08);
  --color-avocado-500: oklch(0.84 0.18 117.33);
  --color-avocado-600: oklch(0.53 0.12 118.34);
  --ease-fluid: cubic-bezier(0.3, 0, 0, 1);
  --ease-snappy: cubic-bezier(0.2, 0, 0, 1);
  /* ... */
}
```

### 그 외…
3D 요소 변환, 그라데이션등의 기능들이 남았지만 전부 다 소개할 수 없는 관계로  [TailWind 4.0](https://tailwindcss.com/blog/tailwindcss-v4) 공식 문서를 보며 쓰고 싶은 기능을 찾아보자!

## 참고 자료
---

https://tailwindcss.com/

https://jake-seo-dev.tistory.com/126

https://jake-seo-dev.tistory.com/127

https://poiemaweb.com/css3-vendor-prefix

https://caniuse.com/

https://blog.wonkooklee.com/docs/libraries-and-frameworks/tailwindcss-4

https://velog.io/@yeon0731/Tailwind-CSS-v4-%EB%8F%84%EC%9E%85%EA%B3%BC-%EC%84%A4%EC%A0%95