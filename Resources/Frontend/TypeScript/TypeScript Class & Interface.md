## 접근 제한자
---
private, public, protected 을 통해 접근방식을 설정할 수 있음.
→ ts에만 있고 js는 없음.

📌 접근 가능한 위치

|   |   |   |   |
|---|---|---|---|
|구분|선언한 클래스 내|상속받은 클래스 내|인스턴스|
|private|⭕|❌|❌|
|protected|⭕|⭕|❌|
|public|⭕|⭕|⭕|

## Abstract Class(추상 클래스)
---
다른 클래스가 상속 받을 수 있는 클래스. 직접 새로운 인스턴스를 만들 수는 없음.

### Abstract Method
메소드를 만들고 내부를 비워두면 됨
추상 메소드는 상속받은 클래스에서 무조건 구현해야함
반환값 void
private로 접근 제한자를 설정하면 상속받은 클래스에서도 사용할 수 없음

```TypeScript
abstract class User {
    constructor(
        private frist_name : string,
        private last_name : string,
        protected nick_name: string,
    ){}
    abstract getNickName(): void

    public getFullName(){
        return `${this.frist_name} ${this.last_name}`
    }
}

class Player extends User{
    getNickName(){
        return this.nick_name
    }
}

const dino = new Player("di","no","디노")

dino.getFullName()
dino.getNickName()
```

## 인터페이스 vs 타입
---
📌 인터페이스 vs 타입

|                               |       |             |
| ----------------------------- | ----- | ----------- |
| 구분                            | 타입    | 인터페이스       |
| 오브젝트의 모양을 설명해 줄 수 있음          | ⭕     | ⭕           |
| 타입이 무슨 타입인지 알려줄 수 있음          | ⭕     | ❌           |
| 지정된 옵션의 타입으로 제한할 수 있음         | ⭕     | ❌           |
| 상속 사용 가능                      | ⭕ (&) | ⭕ (extends) |
| 속성 축적 가능(같은 이름의 Interface 축적) | ❌     | ⭕           |

```TypeScript
// 특정 값으로 제한
type Team = "red" | "blue" | "yellow" 
type Health = 1 | 5 | 10

// type vs interface
type Player = {
    nickname: string,
    healthBar: Health,
    team: Team
}

interface Player {
    nickname: string,
    healthBar: Health,
    team: Team
}

type Friends = string[] // Array<string>

const dino : Player = {
    nickname : "dino",
    healthBar : 10,
    team: "red"
}

type Food = string
const kimchi:Food = "delicious"
const myFriends:Friends = ["nico","las"]
```

```TypeScript
interface User {
    name : string
}

interface User {
    last_name : string
}

interface User {
    nick_name : string
}

interface Player extends User{}

type Player2 = User & {}

const dino : Player = {
    name : "dino",
    last_name : "no",
    nick_name : "디노!"
}
```