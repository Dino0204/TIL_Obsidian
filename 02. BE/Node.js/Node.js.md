[[Javascript]]를 서버 사이드에서 실행할 수 있게 해주는 [[런타임]] 환경
크롬의[[ V8 엔진]]을 [[브라우저]] 밖에서 실행할 수 있게 해준다.

## Node.js 프론트 - 백엔드 동일한 언어 사용의 장점
---
1. 코드 재사용성이 높다.
2. 러닝 커브가 낮다.
3. 동일한 [[코드 컨밴션]], 라이브러리 등을 적용할 수 있기 때문에 일관성이 높다.
4. 서버와 클라이언트 간의 데이터 전송량이 감소하며 로딩 시간이 빨라진다.

## Node.js의 작동 방식
---
![[Pasted image 20250508003308.png]]
### Single Thread
Node.js는 메인 [[스레드]]라고 불리는 싱글 스레드로 구성되어 있다.
Event Loop, Call Stack을 관리 한다.

### Event Loop
Node.js가 싱글 스레드 환경에서 비동기 I/O를 가능하게 하는 핵심 요소이다.
1. Node.js에서 Event Loop가 실행되면 이벤트가 발생할 때까지 대기 상태에 돌입한다.
2. 이벤트가 동기 / 비동기 이벤트 중 무슨 이벤트인지 판별한다.
	1.  동기 이벤트라면 Call Stack으로 이벤트를 Push 한다.
		1. Call Back 함수를 지니고 있다면 Event Queue에 Enqueue하여 작업을 반복 한다.
	2.  비동기 이벤트라면 O/S Kernel에 이벤트를 위임한다.

### [[Call Stack]]
이벤트 루프에서 Push 된 동기(Synchronous) 이벤트의 작업을 수행한다.
작업을 수행하는 동안 이벤트 루프는 Blocked(Call Stack이 비어있는지 확인하는) 상태가 된다.

### Event Queue
Call Stack이 작업을 수행하는 동한 해당하는 작업의 Call Back 이 대기하는 공간이다.

1. Call Back 함수를 지닌 이벤트를 Enqueue 한다.
2. 해당 이벤트가 Call Stack에서 작업을 수행 하면 Dequeue를 통해 남아있는 Call Back 이벤트를 Call Stack에 Push 한다.

### O/S Kernel
이벤트 루프에서 위임 된 비동기(Asynchronous) 이벤트의 작업을 수행한다.
Node.js의 환경이 아닌 외부 환경으로 비동기 작업을 싱글 스레드로 작업하기 위해서 필요하다.
이를 통해 이벤트 루프는 non-blocking I/O 상태를 유지 할 수 있다.

## 참고 자료
---
https://velog.io/@kon6443/NodeJS-node.js-%EA%B0%9C%EB%85%90-%EC%9E%91%EB%8F%99%EB%B0%A9%EC%8B%9D-%ED%8A%B9%EC%A7%95-%EA%B5%AC%EC%A1%B0




