## 입출력 데이터 변환하기
---

### 내장 트랜스포머
 `trim()`, `toLowerCase()`, `toUpperCase()`등의 트랜스포머를 통해 문자열 변환을 할 수 있다.
 
```ts
const Transformers = z.object({
  trimmed: z.string().trim(),
  lowerCased: z.string().toLowerCase(),
  upperCased: z.string().toUpperCase(),
});

const output = Transformers.parse({
  trimmed: " Hello, World! ",
  lowerCased: "Hello, World!",
  upperCased: "Hello, World!",
});

/* result ->
{
	lowerCased: "hello, world!"
	trimmed: "Hello, World!"
	upperCased: "HELLO, WORLD!"
}
*/
```

### 트랜스포머 직접 구현하기
`transform()`를 통해 직접 구현한 트랜스포머를 사용할 수 있다.

```ts
const ID = z
  .string()
  .or(z.number())
  .transform((id) => (typeof id === "number" ? String(id) : id));

const id = ID.parse(1);

// type -> string 1
```

이 때 `input`과 `output`의 자료형이 다른데 타입은 어떻게 추론될까?
`z.infer`로 타입을 추론 해보면 `output` 자료형을 기준으로 추론된다.

이 때 `input` 자료형으로 타입을 얻고 싶다면 `z.input`을 통해 타입을 얻을 수 있다.

## 고급 검증
---
### 조건부 검증
`refine()`으로 비밀번호등의 복잡한 필드를 검증할 수 있다.

```ts
const PasswordSchema = z
	.string()
	.refine( (val) => val.length >= 8 && /[A-Z]/.test(val), 
		"비밀번호는 8자 이상, 대문자 포함 필요" 
	);
```

## React Hook Form에서 Zod 사용하기
---
Zod를 사용할 때 자주 쓰이는 React-Hook-Form과 함께 사용해보자
### 설치
```bash
npm i react-hook-form @hookform/resolvers
```

### 사용
`Zod Resolver`를 통해서 `React-Hook-Form`과 결합하여 `Zod`를 사용할 수 있다.
```ts
import { z } from 'zod'
import { zodResolver } from '@hookform/resolvers/zod'
import { useForm } from 'react-hook-form'

const UserSchema = z.object({
  username: z.string().min(2, { message: "2글자 이상 입력해주세요." })
})

type User = z.infer<typeof UserSchema>

const App = () => {
  const { register, handleSubmit, formState: { errors } } = useForm<User>({
    resolver: zodResolver(UserSchema),
    defaultValues: {
      username: ""
    },
  })
  
  return (
    <form onSubmit={handleSubmit((e) => console.log(e))}>
      <h2>Simple Validation</h2>
      <div>
        <div>
          <input type="text" placeholder="이름을 입력해주세요." {...register('username')} />
          {errors.name && <p>{errors.name.message}</p>}
        </div>
      </div>
      {errors.username && <small>{errors.username.message}</small>}
      <button type="submit">submit</button>
    </form>
  )
}

export default App
```