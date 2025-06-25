## 불필요한 쿼리 함수 재생성 방지

---
쿼리 함수를 불필요하게 재호출하지 않도록 useCallback으로 [[Memoization]]등을 하여 최적화 할 수 있다.

> **Memoization이란?**
> 계산 결과를 메모리에 저장해 두고 동일한 계산이 요청될 때 저장된 값을 반환하는 최적화 기법이다.

> **useCallback이란?**  
> 함수와 의존성 배열을 인자로 받아 메모이징된 함수를 반환하며 의존성 배열의 값이 변경되지 않았을 경우 이전에 생성된 함수를 재사용한다.

### select
쿼리에서 받아온 데이터 중 일부만을 선택적으로 가져올 수 있는 함수.

### 예제
```JavaScript
// 특정 데이터만 선택하여 반환하는 훅
export const useTodos = (select) => {
  return useQuery({
    queryKey: ['todos'],
    queryFn: fetchTodos,
    select, // 데이터 변환 함수
  });
	}
// useCallback으로 메모이제이션
export const useTodoCount = () => {
  return useTodos(useCallback((data) => data.length, []));
}
```

## **병렬 쿼리 및 종속 쿼리**
---
### useQueries
여러 데이터를 동시에 가져와야 하는 경우 병렬 요청을 하여 최적화 할 수 있다.

```JavaScript
const todoIds = [1, 2, 3]
const todosDetails = useQueries({
  queries: todoIds.map((id) => ({
    queryKey: todoKeys.detail(id),
    queryFn: () => fetchTodoDetail(id),
  })),
});
```

### 종속 쿼리

## 그 외의 UX 개선
---
## [[무한 스크롤]]
## 낙관적 업데이트(Optimistic Update)
