

## 제어 컴포넌트
---
요소에 입력되는 값을 state로 관리하는 컴포넌트

### 특징
사용자가 요소에 입력하는 값과 저장되는 값이 실시간으로 동기화된다. 
-> 이 과정에서 리렌더링이 일어난다.

```jsx
import React, { useState } from 'react';

function MyInput() {
  const [inputValue, setInputValue] = useState(null);

  const handleChange = (e) => {
    setInputValue(e.target.value);
  };

  return <input onChange={(e) => handleChange(e)} value={inputValue} />;
}
```


## 비제어 컴포넌트
---
요소에 입력되는 값을 DOM API로 관리하는 컴포넌트

### 특징
바닐라 JS와 유사한 방식으로  ref를 통해 DOM을 직접 조작해 값을 얻는다.
-> 값이 실시간으로 동기화 되지 않는다.

> useRef()를 사용할 경우 Heap 영역에 JS 객체가 저장되게 되는데, 렌더링 시마다 동일한 객체를 제공한다.
> Heap에 저장되어 있기 때문에 참조 시 마다 같은 메모리 값을 지닌다.
> -> 따라서 변경사항을 감지할 수 없기 때문에 리렌더링이 일어나지 않는다. 

```jsx
import React, { useRef } from 'react';

function Test() {
  return <MyInput />;
}

function MyInput() {
  const inputNode = useRef(null);

  return <input ref={inputNode} />;
}

export default MyInput;
```


## 참고 자료
---
[제어 컴포넌트 vs 비제어 컴포넌트](https://velog.io/@thumb_hyeok/%EC%A0%9C%EC%96%B4-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-vs-%EB%B9%84%EC%A0%9C%EC%96%B4-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8)
[비제어 컴포넌트 저장 방식](https://whales.tistory.com/126)