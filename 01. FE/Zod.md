TypeScript 우선 스키마 검증 라이브러리
문자열부터 중첩 객체에 이르기까지 다양한 데이터의 유효성을 검증하는데 사용하는 스키마를 정의할 수  있다.

## 특징
---
런타임 검증: 컴파일 타임에만 타입을 검사하는 TypeScript의 타입 시스템을 런타임으로 확장
-> ex) API 응답, 사용자 입력은 런타임에 따라 결정되기 때문에 런타임 시 검증해야 안전하다.

외부 종속성 없음

작은 번들 크기: 2kb

간결한 인터페이스

TypeScript및 JavaScript와 호환

내장 JSON 스키마 변환

## 설치
---

```bash
npm i zod
```

## 요구 사항
---
TypeScript v5.5 이상 버전을 공식적으로 지원함

`tsconfig.json`의 `strict` 모드를 활성화해야함

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

## 스키마 정의
---
```ts
import { z } from 'zod'

const UserSchema = z.object({
  name: z.string().min(2, "이름은 2자 이상이어야 합니다."),
  age: z.number().positive("나이는 양수여야 합니다."),
})
```

## 데이터 파싱과 에러 핸들링
---
Zod 스키마가 주어질 때 `.parse`를 사용하여 사용자 입력의 유효성을 검사하면 사용자 입력의 깊은 복사본을 반환한다. 

### `parse()`
검증 실패 시 `ZodError instance`를 던진다.
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


###  `safeParse()`
 결과와 함께 성공 여부인 `success: boolean`를 반환 한다.

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

### `asyncParse(), asyncSafeParse()`
비듕기적으로 파싱해야하는 상황(API...) 에 쓰인다.

```ts
```

