## 특징

---
### 강타입 프로그래밍 언어
C#, Java의 컴파일러와 같이 코드를 컴파일하여 기계가 실행 할 수 있는 코드로 변환하여 실행하는 언어, 타입스크립트의 경우에는 브라우저가 이해할 수 있는 자바스크립트로 컴파일 작업을 수행함

> **타입스크립트와 다른 강타입 프로그래밍 언어의 차이점이 뭘까?**  
> _”명시적 타입 정의”_ + _“묵시적 타입 정의”_  
> _→ 타입스크립트가 타입을 추론해주기 때문에 가능한 것_  

**묵시적 타입 정의**
```JavaScript
let str = "hello" <string>

str = "bye" <string>

str = 1 <string> <- <number>
```

-> 타입스크립트가 타입을 알고 있기 때문에 추론하게 나둬도 됨

**명시적 타입 정의**
```JavaScript
let bool1 : boolean = "hello" <boolean> <- <string>

let bool2 : boolean = false <boolean>

let a : number[] = []
-> 이 경우에는 타입을 추론할 수 없기 때문에 명시적으로 타입을 지정 해 주어야 함!
(최소한으로 사용)
```

-> 구체적(명시적)으로 타입을 지정해줌

### 코드를 자바스크립트로 변환해줌
변환하기 전에 코드 검사를 함 → 만약 코드에 에러가 있다면 자바스크립트로 컴파일 되지 않음

코드 검사기가 유저가 코드를 실행하는 런타임 시간에 작동 되는 것이 아님

컴파일이 잘 되었다면 → 코드, 타입에 에러가 없었다는 뜻!

```JavaScript

1) function error
	const dino = { nickname: "Dino0204" }
	dino.hello()
		Property 'hello' does not exist on type '{ nickname: string; }'.
	
	
2) type error
	[1,2,3,4] + false
		Operator '+' cannot be applied to types 'number[]' and 'boolean'.
	
3) argument error
	function divide(a,b) return a / b
		Parameter 'a','b' implicitly has an 'any' type.
	
	divide("hello")
		Expected 2 arguments, but got 1.
```

### 다양한 타입
==**: type**== 순으로 타입을 작성함

**basic type**
number, string등의 기본적인 타입을 말함

**optional type**
타입 작성 시 ==**?:**==순으로 적게 되면 ==**type | undefined**==인 타입을 지정할 수 있음

이 타입을 후에 사용하게 된다면 이 타입이 있는지 검사 후 사용해야 함

**alias type**
반복되는 타입에 대한 정의(과하게 재사용 하지는 말아야 함)

```JavaScript
type Player = {
	readonly name : string,
	age? : number
}

function playerMaker(name : string) : Player return { name } 

const playerMaker = (name : string) : Player => { name }

const dino : Player = { name : "dino" }
const cat : Player = { name : "choco" }
const dino2 = playerMaker("dino2")
```

any
타입스크립트의 보호장치들을 비활성화 시키는 타입

unknown
무슨 타입인지 모를 때 쓰는 타입

typeof를 통해 타입을 검사한 후 그 타입과 관련된 작업을 수행할 수 있음

void
아무 리턴값이 없는 함수의 타입

never
함수가 리턴을 하지 않을 때(예외를 발생 시킬 때)
타입이 2가지일 때

## 장점
---
1. 개발자 경험 개선
2. 버그 감소
3. 런타임 에러 감소
4. 생산성 증가