## Vite를 알기 앞서

---

먼저, Vite를 알기 위해서는 먼저 **Bundler** 와 **WebPack**이 무엇인지 알아야 한다.

웹 사이트를 구성할 때 수 많은 파일을 다운로드 및 로딩하기 때문에 느리게 로딩이 되고 여러파일에서 같은 이름, 함수등을 사용하면서 충돌이 일어나거나 의도치 않은 상황이 발생할 수 있다. 따라서 이러한 현상을 해결하기 위해 등장한 것이 번들러이다.

## Bundler
---

여러 개로 모듈화된 Js 파일을 하나로 합치는 도구

Bundler는 왜 필요할까?

번들화된 Js 파일은 웹페이지가 읽지 못하고 그로 인해 번들러가 필요하다.

번들러의 기능

1. Bundling: 파일을 번들링하여 배포와 실행이 가능하다.
2. Transpile : 브라우저가 읽지 못하는 확장자를 Js파일로 변환해준다.
3. Dependencies : **node_modules**에 패키지를 설치해준다.
4. Automatic Tasks: : linting, testing, building 등을 자동화해준다.

> **linting** : 잠재적 에러를 방지하기 위한 코드 분석 프로그램 실행 과정
   **testing** : 작성한 코드가 의도대로 동작하는지, 오류는 없는지 확인하는 과정

### WebPack
여러 파일을 합쳐주는 Js 번들러

WebPack은 왜 필요할까?

1. 성능 최적화 & 자동화

- tree shaking : 코드 축소 및 사용하지 않는 코드 제거
- -> 로딩 속도 , 웹사이트 성능 향상

2. 파일 단위 Js 모듈 관리

- 파일을 하나 하나 나눠서 모듈화하여 웹을 구성

3. 편의성

- 웹페이지가 이해하지 못하는 다른 확장등을 사용 시 번들러가 컴파일 과정에서 필요한 **Plugin**을 추가하고 번들러를 실행

4. 종속성

- 서버, 브라우저에서 원할하게 작동할 수 있는 코드를 함께 번들
- 참고**Plugin** : WebPack의 기본 동작에 추가적인 기능을 제공하는 속성

## Vite를 알아보자
---

이제 WebPack과 Bundler를 알았으니, 본격적으로 Vite를 알아보자.

Vite는 프랑스어로 빠르다를 의미하고 간결하고 빠른 웹 프로젝트 개발 빌드 도구이다. 

Vue,React등의 라이브러리, 프레임워크에서 사용한다.

ESM(ECMAScript Modules) 나오기 전까지는 라이브러리를 사용하지 않으면 모듈화가 불가능 했다.

그러다가 모듈화 문법(Import, Export)를 이용하여 번들링을 수행하는 번들러, 즉 WebPack이 나오게 되었다.

> **ESM** : 별도 도구 없이 브라우저에서 모듈화를 수행할 수 있는 방식

### Vite 설치
```bash
npm create vite@latest
```

### Vite 특징
**Vite**는 구동속도가 매우 빠르다.

그 속도는 **WebBack** 과 **Vite**를 비교 시 수십배 이상의 차이가 난다고 한다.

이렇게 속도차이가 나는 이유는 방식의 차이라고 볼 수 있다.

Vite는 번들링을 하지 않고 바로 구동하는 ESM방식을 사용하기 때문에 로컬 서버 구동속도가 매우 빠른 것이다.

반면에 WebPack은 모듈들을 번들링하는 시간이 필요하기 때문에 이러한 구동 시간의 차이가 난다.

또 Vite는 빌드 결과물 또한 ESM 방식을 사용하는데 서비스 규모가 매우 큰 경우 번들링을 하는 것이 더 유리할 때가 있다. 이를 위해서 추가적인 번들링 도구로 **rollUp**을 사용할 수 있다.

## 참고자료
---
[Vite JS 시작하기](https://ko.vitejs.dev/guide/)
[Bundler이란?](https://khys.tistory.com/31)
[WebPack이란?](https://velog.io/@gusdh2/Webpack%EC%9D%B4%EB%9E%80-%EC%99%9C-%ED%95%84%EC%9A%94%ED%95%A0%EA%B9%8C%EC%9A%94)
[Linting & Testing](https://jinchuu1391.tistory.com/28)
[Vite이란?](https://khys.tistory.com/31)
