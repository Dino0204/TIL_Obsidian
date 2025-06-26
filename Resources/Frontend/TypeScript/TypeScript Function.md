## Call signatures
---
함수 위에 마우스를 올렸을 때 나타나는 것

call signature type
```TypeScript
type Add = (a:number, b:number) => number

const add:Add = (a,b) => a + b
```

함수를 설명하는 부분과 따로따로 나눌 수 있게 되어 생각의 깊이가 깊어짐

## 오버로딩(Overloading)
---
외부 라이브러리들은 패키지와 라이브러리를 많이 오버로딩 해서 사용하게 됨

```JavaScript
type Add = {
	(a:number, b:number) : number
	(a:number, b:number, c:number) : number
}

const add:Add = (a,b,c?:number) => {
	if(c) return a + b + c
	return a + b
}
```

1. 여러개의 call sinatures를 가지는 함수를 오버로딩이 발생했다고 함
2. 파라미터의 개수가 다를 때에는 optional type으로 만들어 줘야 함  
    (Next.js의 Router.push를 생각해보면 쉬움)  

## 다형성(Polymorphism) & 제네릭(Generics)
---

> **Poly란?**  
>   
> 뜻) 많은, 다수의  
> ex) Polygon : 다각형  

> **Morpho란?**  
>   
> 뜻) 형태, 구조

→ Polymorphism : 여러가지 다른 모양들

concrete type을 사용하여 작성한 call signatures
```TypeScript
type SuperPrint = {
	(arr: number[]): void
	(arr: boolean[]): void
	(arr: string[]): void
	(arr: (number | boolean)[]): void
}
```

generic을 사용하여 작성한 call signatures

```TypeScript
type SuperPrint = {
	<Generic>(arr: Generic[]): Generic
}
```

```TypeScript
const superPrint: SuperPrint = (arr) => arr[0]
const a = superPrint([1,2,3,4])
const b = superPrint([true,false,true])
const c = superPrint(["a","b","c"])
const d = superPrint([1,2,true,false])
```

concreate type는 여러 경우의 수에 모두 대응해야 하는 문제점이 있음 따라서 generic type을 사용해야 함!

type을 확실하게 모르는 상태에서 call signature를 작성할 때 generic을 사용함(대체로 T,V로 표기함)

이를 통해 타입스크립트가 타입을 유추하고 타입을 적용해줌

제네릭은 여러개를 사용할 수 도 있음
```TypeScript
type SuperPrint = {
	<Generic1, Generic2>(arr1: Generic1[], arr2: Generic2 ): Generic1
}
```

> **generic 대신 any를 쓰면 안되는걸까?**  
>   
> any, generic은 모두 다양한 타입을 받을 수 있지만 any를 사용하게 되면 타입스크립트의 보호를 받을 수 없고 타입 불일치로 오류가 나게됨