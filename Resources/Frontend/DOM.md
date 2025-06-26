Document Object Model
페이지에 접근하기 위한 객체.  

## DOM의 구성과 HTML과의 관계
---
HTML은 문자열이다. 문자열은 파싱등의 작업을 거쳐야 하기 때문에 조작하기 어렵다는 단점이 있다.
이를 다루기 쉽게 HTML을 파싱하여 구성되는 객체의 집합 형태가 바로 DOM이다.

## DOM을 조작하는 방법
---
DOM을 조작하려면 DOM 에서 자체적으로 정의하는 인터페이스와 객체를 사용하여 조작해야 한다.

```JavaScript
// document 객체에 getElementById()로 접근
document.getElementById()
```

## DOM의 문제점?
---
**Js로 DOM을 조작할 때 HTML의 구조를 파악하기 힘들다!**

아래 코드가 수억 개가 있다고 생각해보자 일일히 코드를 파악하는데 얼마나 많은 시간이 걸리겠는가? DOM은 이와 같이 구조를 파악하며 조작하기 어렵다는 단점이 있다.

```JavaScript
const my_profile = document.getElementById("MyProfile")

document.createElement(my_profile)
```

**일관성이 없다!**
DOM API는 Live Collection, Static Collection이라는 상태가 존재한다.

Live Collection은 DOM의 실시간 상황에 따라 값이 바뀌는 상태를 뜻하고 Static Collection은 그 반대 상태를 뜻한다. 따라서 일관성이 없다는 것이다.

### DOM의 문제점을 어떻게 해결할 수 있을까?
가장 쉽고 명료한 해결책이 있다. 바로 DOM을 직접 사용하지 않는 것이다.
React는 DOM 조작과 같은 어렵고 복잡한 작업을 직접 수행하며 다루기 쉬운 API를 제공해준다.
즉, HTML의 조작이 어려워 DOM을 사용하는 것이고 DOM 조작이 불편하여 React를 사용하는 것이다.