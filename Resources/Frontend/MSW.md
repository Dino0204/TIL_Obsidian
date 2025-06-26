Mock Service Worker
## 목적

---

팀 프로젝트에서 개발을 하던 도중 백엔드의 서버 구축이 끝날 때까지 프론트엔드 개발자는 무엇을 해야 할까? 하는 고민이 들어서 공부해보게 되었다.

  
## Mocking이란?

---

**Mocking**은 테스트를 위해 실제 객체 대신 가짜 객체를 사용하는 기법.

  

### 왜 Mocking이 필요할까?

**Mocking**은 주로 테스트 코드와 백엔드 측의 서버 개발이 완료되기 전 더 정확하고 신속하게 개발을 끝내기 위해서 사용된다.

  

### 테스트를 위한 Mocking VS 개발을 위한 Mocking

테스트를 위한 Mocking은 테스트 코드에서 외부 의존성을 대체 하여 다양한 시나리오의 정해진 값으로 시나리오를 검증하는 작업 기법이다.

  

개발을 위한 Mocking은 말 그대로 백엔드 개발이 끝나지 않은 시점에서 데이터를 불러온 후 사용하기 위해 사용되는 기법이다.

  

  

### 언제 Mocking을 사용해야 할까?

1. 개발 기간이 짧아 속도가 중시 될 때
2. 원하는 형태의 데이터를 테스트해보고 싶을 때
3. 백엔드와 병렬작업을 수행해야 할 때

  

## 다양한 Mocking 방식들

---

### 로컬 JSON 파일 사용

말 그대로 프론트엔드 측에서 서버의 응답값과 같은 **JSON** 파일을 직접 작성하여 사용하는 방식이다.

아주 가벼운 개인 프로젝트등에서 사용하면 유용하다.

  

### 라이브러리 사용

**Vitest**, **Jest**와 같은 라이브러리를 사용하여 진행할 수 있다.

Vitest는 빠른 테스트 속도를 자랑하는 Vite에 최적화 된 라이브러리이고 Jest는 다양한 테스트 기법과 간단한 사용법으로 사용하기 쉬운 라이브러리라고 한다.

  

### Mock 서버 사용

Mock 서버는 실제 서버처럼 가짜 서버를 만들어 테스팅을 할 수 있는 서버로 이 중 **JSON 서버**는 실제 서버와 같은 Restful API를 사용하여 테스트를 진행할 수 있다.

  

## MSW란?

---

위 방법들은 메서드 요청에 따른 응답을 모두 구현하기 어렵거나 실제 환경과 일치하지 않거나 서버를 구현할 때 많은 자원이 든다는 **문제점**등이 있는데 이를 모두 해결 할 수 있는 Moking 방식이다.

  

네트워크 레벨에서 서버에 대한 요청을 가로채 작동하기 때문에 axios, react-query와 같은 많은 라이브러리를 모두 사용할 수 있다. 또한 테스트를 위한 환경, 개발을 위한 브라우저 환경에서 모두 사용할 수 있다.

  

### MSW 어떻게 동작할 수 있는걸까?

바로 **Service Worker**를 사용하여 HTTP 요청을 가로채기 때문에 이다.

  

> **Service Worker란?**  
>   
> 프록시 서버와 같은 역할을 수행하는 스크립트  
> 오프라인에서도 실행할 수 있다.  
> 네트워크를 가로채 실행되는 특징 때문에 반드시 **HTTPS** 환경(localhost 제외)이어야 한다.

  

MSW는 클라이언트 측에서 보낸 요청을 가로채서 해당하는 요청의 응답을 넘겨주게 된다.  
해당하는 요청은 핸들러를 통해 직접 모의 응답을 지정해 줄 수 있다.  
  

  

### 설치

개발 환경에서만 실행되어야 하기 때문에 반드시 개발 종속성으로 설치해주도록 하자.

```JavaScript
npm install msw --save-dev
```

  

브라우저에서 MSW를 Service Worker에 등록해주기 위해서 public 폴더에 mockServiceWorker 파일을 추가해 주도록 하자.

```JavaScript
npx msw init public/ --save
```

  

### 브라우저 작성 방법

Service Worker에서 handler를 불러온다.

```JavaScript
import { setupWorker } from "msw/browser";
import { handlers } from "./handlers";

export const worker = setupWorker(...handlers);
```

  

### 핸들러 작성 방법

URL과 HTTP 요청에 따른 모의 응답을 지정해주자.

```JavaScript
// mocks/handlers.ts
import { http, HttpResponse } from "msw";
import { posts, users } from "./data";

export const handlers = [
  http.get("api/posts", () => {
    return HttpResponse.json(posts);
  }),
  http.get("/api/users", () => {
    return HttpResponse.json(users);
  }),
];
```

  

### 최상위 요소 작성 방법

아래 코드는 ReactQuery와 MSW를 결합하여 사용한 예시이다.

```JavaScript
// main.tsx
import { StrictMode } from 'react'
import { createRoot } from 'react-dom/client'
import './globals.css'
import Router from './router.tsx'
import { QueryClient, QueryClientProvider } from '@tanstack/react-query'
import { ReactQueryDevtools } from '@tanstack/react-query-devtools'

const queryClient = new QueryClient()

const enableMocking = async () => {
  if (process.env.NODE_ENV === 'development') {
    const { worker } = await import('./mocks/browser.ts')

    return worker.start({
      onUnhandledRequest: (request: Request, print) => {
        if (!request.url.includes('/example/')) {
          return console.warn('예시 요청 url', request.url)
        }

        // 그 외의 처리되지 않은 요청에 대해서는 경고 출력
        print.warning()
      }
    })
  }
  return

}

enableMocking().then(() => {
  createRoot(document.getElementById('root')!).render(

    <StrictMode>
      <QueryClientProvider client={queryClient}>
        <Router />
        <ReactQueryDevtools />
      </QueryClientProvider>
    </StrictMode>
  )
}) 
```

  

### 인스타그램 클론 코딩

Mocking Data를 활용해서 인스타그램 클론 코딩을 해보았다.

## 추가

---

### 테스트 기법

시간 부족으로 인해서 아직 다 알아보지는 못했지만 다음번에 알아보고 싶다.

  

  

## 참고 자료

---

[https://velog.io/@khy226/msw%EB%A1%9C-%EB%AA%A8%EC%9D%98-%EC%84%9C%EB%B2%84-%EB%A7%8C%EB%93%A4%EA%B8%B0](https://velog.io/@khy226/msw%EB%A1%9C-%EB%AA%A8%EC%9D%98-%EC%84%9C%EB%B2%84-%EB%A7%8C%EB%93%A4%EA%B8%B0)

[https://white-blank.tistory.com/185](https://white-blank.tistory.com/185)

[https://www.daleseo.com/react-search/](https://www.daleseo.com/react-search/)

  

[https://developer.mozilla.org/ko/docs/Web/API/Service_Worker_API](https://developer.mozilla.org/ko/docs/Web/API/Service_Worker_API)

  

[https://techblog.woowahan.com/17404/](https://techblog.woowahan.com/17404/)

[https://velog.io/@hamjw0122/FE-%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C%EC%97%90%EC%84%9C-TDD-%EA%B2%BD%ED%97%98%ED%95%B4%EB%B3%B4%EA%B8%B0-1-TDD%EB%9E%80](https://velog.io/@hamjw0122/FE-%ED%94%84%EB%A1%A0%ED%8A%B8%EC%97%94%EB%93%9C%EC%97%90%EC%84%9C-TDD-%EA%B2%BD%ED%97%98%ED%95%B4%EB%B3%B4%EA%B8%B0-1-TDD%EB%9E%80)

[https://tech.kakao.com/posts/458](https://tech.kakao.com/posts/458)