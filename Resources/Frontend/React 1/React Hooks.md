## 목적

---

저번 시간에 이어서 무한 스크롤을 이해하기 위한 두번째 과정이다.

  

## 리엑트 훅이란?

---

리엑트의 함수형 컴포넌트에서 State와 생명주기 기능을 연동할 수 있게 해주는 함수이다.

리엑트에서 제공하는 내장 훅과 개발자가 직접 정의할 수 있는 커스텀 훅이 있다.

  

### 리엑트 훅을 왜 사용하게 되었을까?

리엑트에 훅이 나타나기 이전에는 생명 주기를 관리하기 위해 클래스형 컴포넌트를 사용했다고 한다. 하지만 이와 관련한 많은 문제가 있었다.

  

1. 컴포넌트 간 상태 로직 재사용이 어렵다.
2. 복잡한 컴포넌트들의 이해가 어렵다.
3. Class형 컴포넌트 사용이 어렵다.

  

이러한 문제들로 인해서 리엑트에 훅이 추가 되었다.

## 리엑트 훅 규칙

---

리엑트에서 훅을 사용할 때에는 아래와 같은 규칙들을 지키며 사용해야 한다.

  

### 같은 종류의 훅을 여러번 호출할 수 있다.

아래 코드는 useState를 이용하여 각각의 상태를 관리하는 코드이다.

```JavaScript
const [email, setEmail] = useState("Dino")

const [title, setTitle] = useState("개발 일지")
```

  

### 컴포넌트의 최상위 레벨에서만 사용할 수 있다.

반복문, 조건문, 중첩 함수 내에서는 훅을 사용할 수 없다.

⇒ 이를 통해 렌더링 시 항상 동일한 순서로 Hook이 호출 되는 것이 보장된다.

  

```JavaScript
// ------------
// 첫 번째 렌더링
// ------------

useState('Mary')           
// 1. 'Mary'라는 name state 변수를 선언합니다.

useEffect(persistForm)     
// 2. 폼 데이터를 저장하기 위한 effect를 추가합니다.

useState('Poppins')        
// 3. 'Poppins'라는 surname state 변수를 선언합니다.

useEffect(updateTitle)     
// 4. 제목을 업데이트하기 위한 effect를 추가합니다.

// -------------
// 두 번째 렌더링
// -------------

useState('Mary')           
// 1. name state 변수를 읽습니다.(인자는 무시됩니다)

useEffect(persistForm)     
// 2. 폼 데이터를 저장하기 위한 effect가 대체됩니다.

useState('Poppins')       
 // 3. surname state 변수를 읽습니다.(인자는 무시됩니다)
 
useEffect(updateTitle)     
// 4. 제목을 업데이트하기 위한 effect가 대체됩니다.

// ...
```

  

**반복문**

```JavaScript
for(let i = 0; i <= 3; i++){
	const [email,setEmail] = useState("")
	console.log(email)
}

[eslint]
React Hook "useState" may be executed more than once. 
Possibly because it is called in a loop. 
React Hooks must be called in the exact same order 
in every component.
```

  

**조건문**

```JavaScript
if(isValid){
	const [email,setEmail] = useState("")
	console.log(email)
}

[eslint]
React Hook "useState" is called conditionally. 
React Hooks must be called in the exact same order 
in every component render.
```

  

**중첩된 함수**

```JavaScript
function ExampleComponent() {
  // 올바른 사용: 최상위 레벨에서 Hook 호출
  const [count, setCount] = useState(0);
  
  function handleClick() {
    // 잘못된 사용: 중첩 함수 내에서 Hook 호출
    const [name, setName] = useState("");
  }
  return <button onClick={handleClick}>{count}</button>;
}
```

  

### 비동기 함수는 콜백함수로 사용될 수 없다.

```JavaScript
export default function App(){
  // useEffect Hook 내부에 비동기 함수가 들어가므로 에러 발생
  useEffect(async () => {
    await Promise.resolve(1)
  }, [])
  
  return {
	  <div>
	    <div>Test</div>
	  </div>
 }
```

  

### 함수형 컴포넌트와 커스텀 훅에서만 호출할 수 있다.

클래스 함수, 자바스크립트 함수에서 호출 해서는 안된다.

  

  

## 기본 리엑트 훅

---

리엑트에서 지원하는 기본적인 훅들을 알아보자.

  

### useState

컴포넌트 상태를 관리할 수 있는 `useState`

  

### useEffect

컴포넌트 생애 주기에 개입할 수 있는 `useEffect` 

  

### useContext

컴포넌트 간의 전역 상태를 관리하는 `useContext` 

  

## useRef

---

DOM 요소에 접근 할 수 있게 해주는 참조 훅이다.

렌더링과 상관 없이 컴포넌트가 언마운트 되기 전까지 값을 계속해서 유지 할 수 있다.

  

### 왜 사용할까?

요소 변경 시 렌더링을 발생시키지 말아야 하는 값을 다룰 때 사용한다.

→ 성능 향상을 위해 사용된다.

  

### 생성

요소 참조 시 { current: 초기값 } 을 지닌 객체를 반환한다.

```JavaScript
const inputRef = useRef(초기값);
```

  

### 참조

해당 하는 요소를 ref 속성으로 참조할 수 있다.

```JavaScript
<input ref={inputRef} />
```

  

### 다루기

값을 변경할 때 current 속성을 이용해서 변경해야 한다.

```JavaScript
inputRef.current
```

  

  

## useMemo & useCallback

---

메모이제이션 기법으로 컴포넌트를 최적화하는 훅이다.

  
  

useMemo는 함수의 반환 값을 메모이제이션 한다.

```JavaScript
useMemo(() => {
	return value;
}, [item])
```

  

useCallback은 함수 자체를 메모이제이션 한다.

```JavaScript
useCallback(() => {
	return value;
}, [item])
```

  

메모이제이션 기법을 사용하여 함수 호출 수를 줄인 예제이다.

  

## 마치며…

---

리엑트의 훅 규칙과 메모이제이션 기법들을 공부하며 다시 한번 정리할 수 있어서 좋았다.

다음 시간에는 리엑트 쿼리를 활용한 무한 스크롤을 알아보자.

  

## 참고 자료

---

[https://velog.io/@minw0_o/%EB%A6%AC%EC%95%A1%ED%8A%B8-hook-%EC%B4%9D-%EC%A0%95%EB%A6%AC](https://velog.io/@minw0_o/%EB%A6%AC%EC%95%A1%ED%8A%B8-hook-%EC%B4%9D-%EC%A0%95%EB%A6%AC)

[https://ko.react.dev/reference/react/useRef](https://ko.react.dev/reference/react/useRef)

[https://ko.react.dev/learn/reusing-logic-with-custom-hooks](https://ko.react.dev/learn/reusing-logic-with-custom-hooks)

[https://jong6598.tistory.com/40](https://jong6598.tistory.com/40)