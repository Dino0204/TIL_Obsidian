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
4. TypeScript및 JavaScript와 호환
5. 내장 JSON 스키마 변환

## 설치
---

```bash
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

 결과와 함께 성공 여부인 `success: boolean`를 반환 한다.
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

## 자료형
---
### 기본 자료형 명시
스키마를 정의할 때 자료형을 명시하는데 이 때 검증자 함수를 이용하여 명시할 수 있다.
JS의 기본 타입뿐만 아니라 Date와 같은 내장 클래스 타입 또한 지원한다.

```ts
const UserSchema = z.object({
  name: z.string(),
  age: z.number(),
  createdAt: z.date(),
})
```

### 필수/선택
`optional` 검증자를 사용하여 선택 입력을 사용할 수 있다.

```ts
const UserSchema = z.object({
  name: z.string(),
  age: z.number().optional(),
  createdAt: z.date(),
})
```

### 기본값
`default()` 검증자를 사용하여 누락 속성에 기본값을 줄 수 있다.

```ts
const UserSchema = z.object({
  name: z.string().default('Anonymous'),
  age: z.number(),
  createdAt: z.date(),
})
```

### 배열
배열을 정의 할 때는 특이하게 2가지 문법을 사용할 수 있다.

```ts
const IPs = z.string().array();  // 첫 번째 방법
const IPs = z.array(z.string()); // 두 번째 방법
```

### 객체
TypeScript의 `Record<Keys, Type>` 타입 처럼 Zod에도 `z.record()` 검증자로 객체를 정의할 수 있다.

```ts
const Numbers = z.record(z.number());
```

### 이넘
TypeScript의 `Union` 타입 처럼 Zod에도 `z.enum()` 검증자로 제한된 값을 정의할 수 있다.

```ts
const Rank = z.enum(["GOLD", "SILVER", "BRONZE"]);
```

### 고정값
`z.literal()` 검증자로 특정값을 제한할 수 있다.

```ts
const GoldUser = z.object({
  email: z.string().email(),
  level: z.literal("GOLD"),
});
```

### 문자열 포맷
특정 포맷에 맞는 문자열 유효성 검증을 할 수 있다.
이 때 Zod에서만 작동하기 때문에 사용할 때 조심해야 한다.

```ts
const User = z.object({
  email: z.string().email(),
  image: z.string().url(),
  ips: z.string().ip().array(),
});
```

### 숫자형 지정
정수, 실수와 같은 숫자의 타입을 지정해 줄 수 있다.
```ts
const Age = z.number().int(); 

Age.parse(12);     // ✅
Age.parse(12.345); // ❌ 
```

### 범위 
값의 범위를 `min()`, `max()`를 통해 지정해 줄 수 있다.

```ts
const Age = z.number().int().min(18).max(80);
```

## 참고 자료
---
https://zod.dev
https://www.daleseo.com/?tag=Zod