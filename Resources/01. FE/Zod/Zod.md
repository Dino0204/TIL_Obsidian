[[TypeScript]] 우선 스키마 검증 라이브러리
문자열부터 중첩 객체에 이르기까지 다양한 데이터의 유효성을 검증하는데 사용하는 스키마를 정의할 수  있다.

## Zod를 사용해야 하는 이유?
---
TypeScript는 컴파일 과정에서만 동작하기 때문에 실제 프로그램이 실행 될 때 유효성을 보장할 수 없다.
따라서 유효성 검증 로직을 직접 구현하게 되는데 이처럼 기존의 방식은 굉장히 번거롭다. 따라서 런타임에서 동작하는 유효성 검증인 Zod를 사용해야 한다.

## 특징
---
런타임 검증: 컴파일 타임에만 타입을 검사하는 TypeScript의 타입 시스템을 런타임으로 확장
-> ex) API 응답, 사용자 입력은 런타임에 따라 결정되기 때문에 런타임 시 검증해야 안전하다.

1. 외부 종속성 없음
2. 작은 번들 크기: 2kb
3. 간결한 인터페이스

## 설치
---

```
npm i zod
```

## 요구 사항
---
TypeScript v5.5 이상 버전을 사용하는 것을 권장한다.

`tsconfig.json`의 `strict` 모드를 활성화하는 것을 권장한다.

```json
// tsconfig.json
{
  // ...
  "compilerOptions": {
    // ...
    "strict": true
  }
}
```

## [[스키마]] 정의
---
사용할 데이터의 구조를 정의해준다.

```ts
import { z } from 'zod'

const UserSchema = z.object({
  name: z.string().min(2, "이름은 2자 이상이어야 합니다."),
  age: z.number().positive("나이는 양수여야 합니다."),
})
```

## 유호성 검증과 에러 핸들링
---
Zod 스키마가 주어질 때 `.parse`를 사용하여 사용자 입력의 유효성을 검사하면 사용자 입력의 깊은 복사본을 반환한다. 

### `parse()`
```ts
try {
  const user = UserSchema.parse({
    name: 'John',
    age: 20,
  })
  // -> return { name: 'John', age: 20 }
} catch (error) {
  if (error instanceof z.ZodError) {
    console.log(error.issues)
  }
}
```

검증 실패 시 `ZodError instance`를 던진다.
-> 정확히 어느 부분에서 어떤 검증을 실패하였는지 알려준다!
	
```ts
ZodError: [
  {
    code: "invalid_type",
    expected: "string",
    received: "number",
    path: ["name"],
    message: "Expected string, received number",
  }
];
```

검증 성공 시 반환 객체에는 검증에 통과한 속성만 포함된다.
-> 스키마에 정의되지 않은 속성을 포함시켰을 때 스키마에 정의한 대로 출력되는 모습을 볼 수 있다.

```ts
try {
  const user = UserSchema.parse({
    name: 'John',
    age: 20,
    email: 'john@example.com',
  })
} catch (error) {
  if (error instanceof z.ZodError) {
    console.log(error.issues)
  }
}

// return -> { age: 20, name: "John" }
```
### `safeParse()`
```ts
const user_safe = UserSchema.safeParse({
  name: 'John',
  age: 20,
})

if(!user_safe.success){
	user_safe.error // ZodError Instance
} else {
	user_safe.data // data...
}
```

 `parse()`와의 차이점은 결과와 함께 성공 여부인 `success: boolean`를 반환한다는 점이다.
 -> 이를 통해 `try - catch`문이 아닌 조건문을 사용하여 데이터를 처리할 수 있다.
 
 ```json
 {
	error: (...),
	success: false
 }
```

## 타입 추론
---
스키마를 기준으로 TypeScript 타입을 추론해준다. 

### `기존 TS`
```ts
interface User {
	email: string,
	password: number
}

const Auth = (user: User) => {
	User.parse(user)
}
```

### `Zod 타입 추론`
`infer`와 `typeof`를 사용하여 정의된 스키마로부터 타입 추론을 할 수 있다.
```ts
type User = z.infer<typeof User>

const Auth = (user: User) => {
	User.parse(user)
}
```


## 참고 자료
---
https://zod.dev
https://www.daleseo.com/?tag=Zod
https://mycodings.fly.dev/blog/2025-04-19-ultimate-zod-v-4-guide-for-typescript-developers
https://jforj.tistory.com/380