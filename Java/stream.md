Stream
===============================


1.특징(Characteristic)
-------------------------------
 + 스트림은 데이터를 담는 저장소가 아니다.
 + 스트림이 처리하는 데이터 소스를 변경하지 않는다.
 + 스트림으로 처리하는 데이터는 오직 한번만 처리한다.
 + 스트림은 무제한일 수 있으며, Short Circuit 메소드를 사용하여 제한이 가능하다.
 + 중개 오퍼레이션은 근본적으로 lazy하다.
 + 손쉽게 병렬 처리가 가능하다.
 
1.1.스트림 파이프라인(Stream pipeline)
-------------------------------
 + 스트림 파이프라인은 중개 연산과 종료 연산으로 구성되어 있습니다.
 + 중개 연산은 Lazy하므로 종료 연산이 실행되기 이전까지는 실행되지 않습니다.
      
구분|메소드(Method)
-----|-----
중개 연산|.map(), .filter(), .flatMap(), .peek(), .findFirst(), .limit(), .distinct(), .sorted(), ...
종료 연산|.collect(), .anyMatch(), .noneMatch(), .forEach(), .max(), .min(), .count(), ...

1.2.병렬 처리(Parallel Processing)
-------------------------------
 + 스트림 API를 사용하여 병렬 처리를 손쉽게 이루어낼 수 있습니다.
 + 병렬 처리를 하기 위해 발생하는 비용(생성, 수집, 스위칭, ...)으로 인해 성능이 저하될 수 있으므로, 적재적소에 사용되어야 합니다.
<pre>
<code>
        List<String> foods = Arrays.asList("apple","eggs","banana");

        List<String> fruits = foods.parallelStream().filter(s -> !s.equals("eggs")).map((s) -> {
            System.out.println("Added " + s);
            System.out.println("thread name is " + Thread.currentThread().getName());

            return s.toUpperCase();
        }).collect(Collectors.toList());
        System.out.println("--- result ---");
        fruits.forEach(System.out::println);

=== 실행 결과 ===

Added apple
Added banana
thread name is ForkJoinPool.commonPool-worker-5
thread name is main
--- result ---
APPLE
BANANA

</code>
</pre>

2.1.중개 연산(Intermediate Operation)
 + **Stream을 리턴한다.**
 + 스트림을 리턴 받으므로 연속해서 중개 연산이 가능하다.
 + 중개 연산은 필터-맵(filter-map) 기반의 API를 사용함으로써 지연(lazy) 연산을 사용하여 성능 최적화가 가능하다.
 + Stateless / Stateful 오퍼레이션으로 더 상세하게 구분할 수도 있다.
 
2.2.종료 연산(Terminal Operation)
 + **Stream을 리턴하지 않는다.**
 + 중개 연산을 통해 변환된 스트림을 마지막으로 연산하여 각 요소를 소모하여 결과를 표시한다.
 + 모든 요소를 소모한 스트림은 추가 사용이 불가하다.
