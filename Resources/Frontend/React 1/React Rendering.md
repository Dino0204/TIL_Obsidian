## [[DOM]]
## [[VDOM]]

## 리엑트에서의 렌더링이란?
---
이제 본격적으로 리엑트에서의 렌더링에 대해 알아보자. 
리엑트가 컴포넌트에게 **Props**와 **State**를 기반으로 너의 UI는 어떻게 생겨야 해? 라고 물어보는 과정이다.

이 컴포넌트들과 상호작용하려면 UI에 내재된 데이터 모델(State)를 변경하는 것으로 상호작용할 수 있다.

이 데이터 모델이 업데이트되면 React 컴포넌트는 비로소 렌더링이 되게 되는 것이다.

## 렌더링 페이즈
---
리액트의 렌더링 과정인 렌더링 페이즈에 대해서 간단하게 알아보자.

### Render Phase
컴포넌트를 렌더링하고 **변경 사항을 계산**하는 단계(VDOM을 조작하는 단계)

### Commit Phase
변경 사항을 실제로 **DOM에 적용**하는 단계

이 때 유의할 점은 **렌더링과 DOM을 업데이트하는 것의 차이**이다. 부모 컴포넌트가 렌더링되어 컴포넌트가 다시 렌더링 되더라도 최종적으로 생성된 React Element가 동일하다면 DOM 업데이트는 발생하지 않게 된다.

## Reconciliation(재조정)
---
리엑트가 렌더링을 최적화하는 방법을 알아보자.

리엑트는 기존 컴포넌트와 현재 컴포넌트의 상태를 비교하여 업데이트가 필요한지 판단하는데 이 때 업데이트가 필요하다고 판단된 렌더링을 수행하게 된다.

이 때 유의할 점은 부모 컴포넌트가 렌더링될 시 자식 컴포넌트도 같이 렌더링된다는점이다.

## 애플리케이션 상태 관리
---
리엑트에서 렌더링이 일어나는 경우를 알아보자.
리엑트에서 렌더링은 상태 또는 프롭스가 변할 때 일어난다.
  
### 상태 끌어올리기
**상위 컴포넌트 → 하위 컴포넌트(단방향 데이터 흐름)**
하위 컴포넌트로 동일한 상태를 변경 해야 한다면 Props를 통해 상태를 전달해주면 된다.

  
**하위 컴포넌트 → 상위 컴포넌트(역방향 데이터 흐름)**
상위 컴포넌트의 상태를 변경 해야 한다면 Props로 상태를 업데이트하는 함수를 전달해주면 된다.

## 참고 자료
---

[https://velog.io/@hyunjine/%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%A0%8C%EB%8D%94%EB%A7%81%EC%97%90-%EB%8C%80%ED%95%9C-%EC%9D%B4%ED%95%B4](https://velog.io/@hyunjine/%EB%A6%AC%EC%95%A1%ED%8A%B8-%EB%A0%8C%EB%8D%94%EB%A7%81%EC%97%90-%EB%8C%80%ED%95%9C-%EC%9D%B4%ED%95%B4)

[https://velog.io/@hyunjine/Thinking-in-React#reconciliation%EC%9E%AC%EC%A1%B0%EC%A0%95](https://velog.io/@hyunjine/Thinking-in-React#reconciliation%EC%9E%AC%EC%A1%B0%EC%A0%95)

[https://joong-sunny.github.io/react/react2/#%EF%B8%8F%EA%BC%AC%EB%A6%AC%EC%A7%88%EB%AC%B81-vdom%EC%97%86%EC%9C%BC%EB%A9%B4-%EA%B7%B8%EB%A0%87%EA%B2%8C-%EC%95%88%EB%90%98%EB%82%98%EC%9A%94](https://joong-sunny.github.io/react/react2/#%EF%B8%8F%EA%BC%AC%EB%A6%AC%EC%A7%88%EB%AC%B81-vdom%EC%97%86%EC%9C%BC%EB%A9%B4-%EA%B7%B8%EB%A0%87%EA%B2%8C-%EC%95%88%EB%90%98%EB%82%98%EC%9A%94)