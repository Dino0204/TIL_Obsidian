## JSON(JavaScript Object Notation)이란?
---
JSON은 JavaScript 객체 문법으로 구조화된 데이터를 표현하기 위한 문자 기반의 표준 포맷이다. 웹, 앱에서 데이터를 전송할 때 이 포맷을 사용하여 전송한다.

JSON은 문자열 형태로 존재한다. 따라서 네트워크를 통해 전송할 때 효율적으로 전송할 수 있다. 다만 이로 인해 데이터에 접근할 때 JSON 객체로의 변환 과정을 거쳐야 하는데 이는 JavaScript에서 JSON 전역 객체를 통해 문자열 - JSON 객체간의 변환을 할 수 있다.

> **Parsing, Stringfication**  
>   
> 데이터를 사용 할 수 있도록 문자열 → 객체 변환을 거치는 것을 Parsing  
> 네트워크에서 전송 할 수 있도록 객체 → 문자열 변환을 거치는 것을 Stringfication
## JSON 객체
---
JSON 객체 내부에는 JavaScript의 객체 문법을 사용할 수 있다.
```JSON
{
  "name": "아트록스",
  "title": "다르킨의 검",
  "role": ["탑","미드"],
  "difficulty": 4,
  "abilities": {
    "passive": "피의 우물",
    "Q": "다르킨의 검",
    "W": "지옥의 사슬",
    "E": "어둠의 돌진",
    "R": "세계의 종말"
  }
}
```