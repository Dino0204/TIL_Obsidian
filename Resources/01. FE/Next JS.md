- 풀 스택 프로그램을 구축하기 위한 React 프레임 워크
- 번들링, 컴파일과 같은 작업을 추상화하고 자동으로 구성
- SSR,SSG,ISR과 같은 다양한 렌더링 방식을 제공

```python
추상화 (구체화의 반대)
자식 컴포넌트에서 공통된 부분을 뽑아내 부모컴포넌트를 제작함

SSR (Server side rendering)
서버 측에서 화면을 렌더링하는 아키텍쳐
https://toss.tech/article/ssr-server

CSR (Client side rendering)

SSG
https://velog.io/@ka0son/%EB%A0%8C%EB%8D%94%EB%A7%81-%EC%82%BC%ED%98%95%EC%A0%9C-CSR-SSR-SSG-%EC%9D%B4%ED%95%B4%ED%95%98%EA%B8%B0

ISR

```

### 개발 환경 설정
```jsx
npx create-next-app@latest
```

### 배포
- 기본적인 환경에서는 불필요한 파일 등이 많기 때문에 속도 & 성능 저하에 원인이 되어 불필요한 파일들을 삭제함

- 빌드 후 배포
    
    ```java
    npm run build
    -> .next 폴더 내에 배포 시 파일이 생성됨(리소스를 적게 먹음)
    ```
    
    ```java
    npm run start
    -> build 후 실행
    ```
    

### 뼈대 만들기
- layout.js에서 페이지 전체에 해당하는 공통 레이아웃을 만듦
- page.js 반환 값을 {children} 으로 가져옴

- title 등의 정보 → metadata

### 라우팅
```java
http://a.com/dashboard/analytics/
			--------------------------
		  domain segment   segment
								   path
```

- 라우팅 : 경로에 따라서 어떤 콘탠츠를 어떤 방식으로 보여 줄 것인지
- 폴더 구조에 따라서 링크를 가짐
    1. 이름에 맞는 폴더를 찾음
    2. 내부에 page.js 를 찾음
    3. 내부에 layout.js가 있다면 그곳에 결합 ( 그 후 부모 layout.js에 결합 )
    없다면 부모 layout.js애 결합
- react-router-dom 설치 필요 없음
    
    → routes , route 같은 컴포넌트 필요 없음(js 전혀 안씀)
    
    → 설정된 폴더구조로부터  route를 도출함
    
    → **APP Directory 라우팅 구조 (동적 경로 : [id].js와 같은 파일을 통해 지정)**
    

- App Router
    - 서버 중심 라우팅
    - React Server Components기반
    - 경로 이동시 페이지를 재렌더링하지 않고, SPA처럼 URL만 업데이트함
    - **APP Directory**
        - root 레이아웃 필수
        - 경로 정의
        - 페이지 파일        → page.js
        - server-side API → route.js
    - 우선순위 : Pages Router보다 높음
    - Data Fetching 동시에 가능
    - Parallel Routes
        - 동일한 레이아웃에서 하나 이상의 페이지를 동시/조건부 렌더링이 가능
    - Interceipting Routes
        - 현재 페이지의 컨텍스트를 유지하며 현재 레이아웃 내에서 경로를 로드
    
    ```python
    src/app
    ├─layout.js // root layout. 필수
    ├─page.js // root page
    ├─a-page
       └─page.js
    └─b-page
      └─page.js
      └─component.js // 라우팅과 관련없는 코드. 라우팅의 대상이 되지 않습니다
        └─b-subpage
        └─page.js
    ```
    
- Pages Router
    - 클라이언트 중심 라우팅 (CSR)
    - **Pages Directory**
        - 하위 Js파일이 모두 페이지 / API의 경로
    - 라우팅 필요없는 파일도 경로가 생김
    - Data Fetching과 component를 함께 배치 불가능

```python
src/pages
├─_app.js // root layout
├─index.js // root page
├─a-page.js
└─b-page
  └─index.js
   └─component.js // 라우팅과 관련없는 코드지만 b-page/component라는 경로가 생깁니다.
   └─b-subpage.js
```

- 다이나믹 라우팅
    - 모든 페이지를 경로로 삼는 것이 아닌 동적으로 추가함
        
        ```java
        app
        | page
         | [id]
        	 | page.js
        ```
        
    - id  추가 하기  page.js에 props
        
        ```
        export default function Read(props) {
          return (
            <>
              <h2>Read</h2>
              {props.params.id}
            </>
          );
        }
        
        ```
        

### Rendering
**SSR**

- **서버에서 페이지를 렌더링하여 완전히 렌더링된 HTML을 클라이언트로 전송하는 방식**
- 콘탠츠가 바뀌는 영역은 작지만 웹페이지는 다시 모두 다운로드함, 방문한 페이지도 다운로드함
    
    → Link로 해결
    
- SPA : 웹페이지가 여러개의 페이지를 가지고 있어도 한 페이지 처럼 동작하는 것
- 함수
    - getServerSideProps
    - getInitialProps
    - → 서버사이드 렌더링 구현
- DOM에 각 스크립트 코드를 하이드레이션
    - SSR이지만 페이지 새로고침 없이 웹 페이지와의 상호작용이 가능
    - → SPA처럼 작동하는 SSR웹앱
- 장점
    1. 안정성 증가
    페이지를 서버에서 렌더링하여 API호출, 키관리, 데이터 검증등르 서버에서 수행함
    2. 초기 로딩 속도 개선
    3. 검색 엔진 최적화(SEO)
    4. 웹사이트 제공 범위 확대
    서버에서 렌더링을 하기 때문에 Js 사용불가능 환경에서도 사용가능
- 단점
    1. 자원 소모, 서버 부하 증가
    2. 페이지 이동 시 처리 시간 증가
        - 페이지 렌더링 시마다 데이터, API 접근
        → 해결책 : Next js

```python
Hydration
브라우저에서 HTML을 렌더링할 때 페이지의 컴파일된 HTML에 
JavaScript 동작을 다시 추가하는 프로세스

SSR에서 HTML을 렌더링 시 정적인 화면만이 나타남( Js 렌더링 x)
그다음 Js 번들 다운로드 및 실행 
React Virtual DOM 생성 DOM과 비교하여 Js를 연결함
-> 정적 HTML과 React Component 동기화

장점 : 초기 페이지 로드가 빠름

단계
1. 초기 HTML 전송: 서버는 정적 HTML 파일을 전송하여 빠른 초기 페이지 로드를 보장함
2. JavaScript 번들 로드: 브라우저는 필요한 JavaScript 파일들을 다운로드하고 실행
3. Virtual DOM 생성: React는 서버에서 생성된 HTML과 동일한 구조의 가상 DOM을 제작
4. 동기화 : Virtual DOM과 실제 DOM을 비교하여 차이점을 찾아내고, 다시연결함

=> 이 과정이 수행되고 동적기능 사용가능
```

### 정적자원 사용하기

- pulblic 폴더에 집어넣고 사용

### CSS
- glbal.css에서 전역적인 css 수정

### Backend
- Routing
    - Route Handler → Next Js로 API 구축
    
- Json server
    
    ```java
    npx json-server@0.17.4 --port 9999 --watch db.json
    
    // port 9999에 json server 할당 , db.json이 바뀌면 즉각반영
    ```
    
- Webpage
    - fetch
    
    ```java
     fetch('http://localhost:9999/topics')
        .then((res)=>{
            return res.json();
        })
        .then(result=>{
            console.log(result)    
        });
    ```
    

### 글목록 가져오기
- 서버 컴포넌트 vs 클라이언트 컴포넌트 (React)
    
    ![image.png](image.png)
    
    - 서로 사용할 수 있는 API가 다름
    - 특별한 조치가 없으면 서버 컴포넌트로 간주함
        - useState는 클라이언트 컴포넌트만 사용할 수 있음
            
            ![image.png](image%201.png)
            
        - “use client”를 통해 클라이언트 컴포넌트로 변환 할 수 있음
            - metaData는 서버 컴포넌트에서만 사용할 수 있기에 layout.js에서는 오류가 남
            
            ![image.png](image%202.png)
            
    - 정보를 표현하는데 사용자와 상호작용이 없다면 서버 컴포넌트로 하는 것이 유리함
        
        → 사용자와 상호작용 시 클라이언트 컴포넌트
             사용자와 상호작용이 없을 시 서버 컴포넌트
        
    - Cannot read properties of undefined
        
        ![image.png](image%203.png)
        
        → topics && 를 통해 data 값이 있을 때만 출력하도록 하면 된다
        

→ 최종적으로는 비동기적 방식에서 동기적 방식으로 바꿈

### 글 읽기
- Unexpected token N in JSON at position 0 오류 → id 값 문자열로 바꾸기

### 글  생성하기
- onSubmit → 사용자와 상호작용 하므로 use client 사용
- submit 시 페이지 교체 방지

```java
preventDefault()
```

- target → form을 가리킴
    - 각각 name이 가리키는 값을 가져옴
- undefined가 뜨는 경우 → return 값이 없어서 그럼 (arrow function 사용 시 주의!!)
- Redirection → client 컴포에서만 사용 가능
    - Redirection : 경로를 다시 바꿔주는 기능
    
    ```java
    useRouter()
    
    // router가 아닌 navigation 경로에서 가져올 것!
    // -> App Router 이전에 쓰던 page Router와 이름이 같기 때문 
    ```
    

### Cache
- 문제점 : 링크가 업데이트 되지 않음 → cache와 관련!
    - fetch (최초접속)시 가져온 정보를 저장함 (in .next)
    - Revalidating으로 해결 가능  (cache 삭제)
        
        ```java
        Revalidating Data
        
        fetch('url',{next : { revalidate : 0 }}
        // 0s 동안  데이터 유지
        ```
        
    - but, Cache에 저장하지 않는 것으로 해결 (cache에 저장x)
        
        ```java
        Dynamic Data Fetching
        
        cache: "no-store"
        // cache에 데이터 저장 x
        
        router.refresh();
        // server component 강제 재 렌더링
        ```
        
    

### Update & Delete
- useParams
    - clientComponent
    - 매개변수를 통해 URL에서 넘겨반은 페이지에서 사용할 수 있도록 해주는 훅
- 문제점 : 서버 컴포넌트에서 사용이 불가능
→ 부분 client component화

### 글 수정
- Update = Update + Create
    - Read : 원본도 불러와야함
- useState로 상태관리
- PATCH, PUT으로 글수정
- useEffect 사용 시 []로 의존성 배열 추가
- 상세보기가 변경되지 않는 이유 → cache를 사용했기 때문
    
    ```java
     cache: "no-store" 로 캐쉬 저장x
    ```
    

### 글 삭제
- DELETE로 삭제
- Router로 Redirection
    
    ```java
    push('url') -> Redirection
    
    refresh()   -> 새로고침
    ```
    

### 환경변수
- .env.local

```java
.env.local

API_URL = http://localhost:9999/
```

```java
.env.local.example

예시 알려주기
```

- 서버 컴포, 클라 컴포 방법이 각각 다름
    - 환경변수는 서버 컴포넌트에서만 접속이 가능함 (정보 유출 방지)
    - NEXT_PUBLIC 을 통해 클라이언트 컴포넌트에서도 사용가능
- 환경변수를 설정하여 원하는 것으로 설정 가능
    
    ```java
    
    사용 예시
    
      const res = await fetch(`${process.env.API_URL}${"topics"}`, {
        cache: "no-store",
      });
      
    ```
    
- 정보를 은닉할 수 있음

## 출처
---

[Next.js 13 - 1. 설치와 실행](https://www.youtube.com/watch?v=smAU6-ZdcoQ&list=PLuHgQVnccGMCwxXsQuEoG-JJ7RlwtNdwJ&index=2)

[NextJS 특징과 차별점은 무엇일까?](https://velog.io/@hyumapr/NextJS-%ED%8A%B9%EC%A7%95%EA%B3%BC-%EC%B0%A8%EB%B3%84%EC%A0%90%EC%9D%80-%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C)

[6) 객체지향 프로그래밍7 - 추상화](https://velog.io/@dev-mage/hello-java-world-oop-abstraction)

[[Next.js 13] 폴더 구조 + 이쁜 잡기술](https://velog.io/@baby_dev/Next.js-13-%ED%8F%B4%EB%8D%94-%EA%B5%AC%EC%A1%B0-%EC%9D%B4%EC%81%9C-%EC%9E%A1%EA%B8%B0%EC%88%A0)

[React + Typescript 프롭스 타입 정의 하기](https://velog.io/@ovogmap/React-Typescript-2)

### 클론코딩
[Apple Music 웹 플레이어](https://music.apple.com/kr/new)

[Top 26 K-Pop MVs That Deserve More Views: Female Edition](https://trends.kpopmap.com/top-26-kpop-mvs-that-deserve-more-views-female-edition/)