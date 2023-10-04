# Reactive

### Sync / Async, Blocking / Non-Blocking
1. Sync / Async
   - Sync : `Main`이 `Sub`의 결과 반환을 **대기**
   - Async: `Sub`가 작업이 완료된 시점에 `Main`에게 **Callback 등으로 전달**
   - 즉, `Main`작업의 Flow가 `Sub`작업에 얼마나 의존적인가 정도로 구분이 가능할 것
    > ※ `Sub`작업의 결과값에 대한 의존도가 아닌, `Sub`작업 그 자체에 대한 의존도를 의미한다.
2. Blocking / Non-Blocking
   - Blocking : `Main`은 `Sub`의 수행이 완료된 이후에 재개된다.
   - Non-Blocking : `Main`과 `Sub`의 수행은 별개로 분리되어 실행된다.
  
둘 다 유사한 내용이지만,   
Blocking / Non-Blocking은 전체적인 작업의 실행 Flow의 관점   
Sync / Async는 `Main` 작업의 관점 정도로 이해하면 된다.

### Reactor
Reactive Framework   
Flux와 Mono 같은 데이터 스트림을 통해서 발생하는 `Event`에 기반하여 Publish / Subscribe하여 데이터를 사용한다.

#### Flux & Mono
1. Flux : 0 ~ n개의 요소를 발행하는 데이터 스트림
2. Mono : 0 ~ 1개의 요소를 발행하는 데이터 스트림

### Methods
1. just : 데이터 스트림 생성
2. subscribe : 데이터스트림 구독
3. doOnSubscribe : 데이터스트림 구독 시 발생하는 이벤트
4. doOnNext : 데이터스트림 구독 시 구독자에게 넘어갈 데이터가 있는 경우 발생하는 이벤트
5. doOnComplete : 현재 데이터 스트림 내의 모든 데이터의 구독이 완료되었을 경우에 발생하는 이벤트
6. zip : 두개의 데이터스트림을 합친다. (기본적으로는 Tuple형태로 제공되나, 가공 가능) ... etc

### 주의사항

```
val t = Flux.just(1, 2, 3, 4)
    .doOnNext {
        println("NEXT : $it")
    }
    .doOnSubscribe {
        println("SUBSCRIBE")
    }
    .doOnComplete {
        println("COMPLETE")
    }


fun subscribeFlux( f: Flux<Int>){
    f.subscribe{
        println("SUBSCRIBING : $it")
    }
}

subscribeFlux(t)
println("-----------------")
subscribeFlux(
    t.map {
        it * 10
    }
)
```

상기 코드의 수행결과는 아래와 같다.
```
SUBSCRIBE
NEXT : 1
SUBSCRIBING : 1
NEXT : 2
SUBSCRIBING : 2
NEXT : 3
SUBSCRIBING : 3
NEXT : 4
SUBSCRIBING : 4
COMPLETE
-----------------
SUBSCRIBE
NEXT : 1
SUBSCRIBING : 10
NEXT : 2
SUBSCRIBING : 20
NEXT : 3
SUBSCRIBING : 30
NEXT : 4
SUBSCRIBING : 40
COMPLETE
```

> 기존의 Flux를 갱신할 경우 doOnNext의 값이 신규 값이 아닌 기존 값을 기준으로 나오는 점에 대해서 유의하고 인지하고 있어야한다.

