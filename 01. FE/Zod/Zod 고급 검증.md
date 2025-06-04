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

/* 
{
	lowerCased: "hello, world!"
	trimmed: "Hello, World!"
	upperCased: "HELLO, WORLD!"
}
*/
```

### 트랜스포머 직접 구현하기
`transform()`를 통해 직접 구현한 트랜스포머를 사용할 수 있다.
