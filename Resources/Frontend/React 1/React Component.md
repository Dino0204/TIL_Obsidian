## JSX(JavaSciprt XML)
---
자바스크립트에 XML 문법을 추가한 확장형 문법.

HTML과 자바스크립트를 한번에 작성하여 편리하다.

return 함수 내에 HTML을 표현하고 HTML 태그의 끝에 `/>` 마침 표시가 있다는 차이점이 있다.

## Component와 구성 요소
---
React로 만들어진 앱을 이루는 최소 단위.

데이터(props)를 입력받아 View(state) 상태에 따라 DOM N
ode를 출력하는 함수.

> **Component의 등장 배경**
> 웹 사이트에는 반복되는 패턴이 많다.
> 하지만, 기존의 프레임워크는 [[MVC 패턴]]으로 동작하여 재사용이 어렵다는 단점이 있었다.
> React는 이 문제점을 해결하기 위해서 재사용성이 높은 Component 패턴을 도입하였다.

> **Component 패턴**
> MVC 패턴의 View를 Component를 통해 독립적으로 구성하는 패턴.

### Component 구성 요소

| 데이터 구성 요소 | 특징                           |
| --------- | ---------------------------- |
| Property  | 하위 컴포넌트로 전달 되는 읽기 전용 데이터.    |
| State     | 컴포넌트의 상태를 저장하고 변경할 수 있는 데이터. |
| Context   | 모든 자식 컴포넌트로 전달되는 데이터.        |

### Component 작성 규칙

첫 글자는 대문자로 작성해야 한다.
-> React는 소문자로 시작하는 Component를 DOM 요소를 다루는 태그로 취급한다.

재사용 가능한 코드로 작성해야 한다.
-> UI를 개별적인 여러 조각으로 나눈다.

## Props
---
상위 컴포넌트가 하위 컴포넌트에 수정할 수 없는 값을 전달할 때 사용한다.

```jsx
<Profile name=”Dino”/>
```

이 값은 하위 컴포넌트에서 참조할 수 있습니다. 

## State
---
값을 저장하거나 변경할 수 있는 객체.

```jsx
const [data,setData] = useState(True)
```

state 객체를 통해 상태 관리를 할 수 있습니다.

## LifeCycle(생명주기)
---
나중에 찾아보자

## Class Component
---

나중에 찾아보자

## Function Component
---
나중에 찾아보자

## Array Component
---
```jsx
const mixedList = [1,’string’,<Component/>]
```

이 처럼 자바스크립트의 배열에는 다양한 자료형을 저장할 수 있습니다.

### map()
배열을 통해 저장된 데이터를 바로 JSX로 변경할 수 있습니다.

  ```JavaScript
const todoList = [
	{taskName: '운동하기', finished: true},
	{taskName: '공부하기', finished: false}
];

// 1. Object -> JSX
const todos = todoList.map(todo => <div>{todo.taskName}</div>)

// 2. Object -> Component
const todos = todoList.map(todo => <TodoTask/>)

// 3. Object -> Props
const todos = todoList.map(todo => <TodoTask taskName={todo.taskName}/>)
```

> 배열 컴포넌트를 사용 시 주의점
> key값을 사용해야 리렌더링이 일어나지 않는다.

## Callback과 Event
---
전달 받은 Props를 수정하려면 Callback 함수를 통해 원본 데이터를 수정할 수 있다.

> **Callback 함수란?**  
> 다른 코드의 인수로서 실행하는 함수.
> 필요에 따라 호출 시기가 달라진다.

### Props 수정하기

`ex) 버튼 카운터`
```jsx
// 1. 상위 컴포넌트
const [count, setCount] = useState(0);

return(
	<div>	
		<Counter count={count} onChange={setCount}/>
		<p>{count}</p>
	</div>
)

// 2. 하위 컴포넌트

return(
	<div>
		<button onClick={setCount(count + 1)}>➕</button>
	</div>
)
```

 Callback 함수 호출 시 상위 컴포넌트에서 원본 데이터를 수정한 후 다시 자식 컴포넌트로 값을 전달해 준다.

### DOM Event

| 이벤트 명     | 이벤트 호출 시점            | JSX DOM 이벤트 프로퍼티 |
| --------- | -------------------- | ---------------- |
| click     | 요소에 마우스, 키보드가 클릭될 때  | onClick          |
| submit    | 폼에 데이터가 전송될 때        | onSubmit         |
| mousemove | 요소 위의 마우스 커서가 움직일 때  | onMouseMove      |
| mouseover | 요소 위로 마우스 커서가 돌아다닐 때 | onMouseOver      |
| mouseout  | 요소 위의 마우스 커서가 떠날 때   | onMouseOut       |
| keydown   | 키보드가 눌렸을 때           | onKeyDown        |
| keypress  | 키보드 입력이 완료 되었을 때     | onKeyPress       |

### 단방향 흐름 방식
원본 데이터의 무결성을 지켜주고 데이터 수정으로 인한 데이터 파편화를 줄여준다.