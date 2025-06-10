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
이 때 [[Zod]]에서만 작동하기 때문에 사용할 때 조심해야 한다.

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
