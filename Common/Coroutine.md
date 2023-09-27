# Coroutine

Asynchronus / Non-Blocking Programming

- 단일 스레드 사용
- 서브루틴 (내부의 함수)의 실행 상태에 대한 정보를 가지고 있음
  - 일시중지(suspend), 재개(resume) 이 가능
- runBlocking: Coroutine 환경을 구성하는 빌더
  - > coroutine builder that bridges the non-coroutine world
- launch: 독립적으로 실행되는 Coroutine을 생성하는 빌더
- suspend: Coroutine에서 해당 키워드를 갖는 함수가 호출될 경우, 해당 함수부터 처리 후 나머지 동작을 수행하게 된다.
  - 물론 그럼에도, 비동기로 처리할 수 있는 다양한 방법이 있다. ([Suspend Function](https://kotlinlang.org/docs/composing-suspending-functions.html))
  - 주의할 사항에 대한 인지 또한 필요하다. ([Async Style](https://kotlinlang.org/docs/composing-suspending-functions.html#async-style-functions)) 
