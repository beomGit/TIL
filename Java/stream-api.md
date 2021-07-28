Stream API
===============================

1.스트림 생성(Generate Stream)
-------------------------------
1.1.Collection 인터페이스 내에는 stream() 메소드가 정의 되어 있습니다. 그러므로 List와 Set 컬렉션 클래스 내에서 사용이 가능합니다.   
1.2.Arrays 클래스 내에는 IntStream, LongStream, DoubleStream 인터페이스로 각각 제공됩니다.    
1.3.iterate()는 시드(seed)로 명시된 값을 람다 표현식에 사용하여 반환된 값을 재사용하여 무한 스트림을 생성합니다.   
1.4.generate()는 매개변수가 없는 람다 표현식을 사용하여 반환된 값으로 무한 스트림을 생성합니다.   

<hr/>

2.중개 연산 메소드(Intermediate Operation Method)
-------------------------------
구분|메소드(Method)
-----|-----
필터링|.filter(), .distinct()
변환|.map(), .flatMap()
제한|.limit(), .skip()
정렬|.sorted()
연산결과 확인|.peek()



3.종료 연산 메소드(Terminal Operation Method)
-------------------------------
구분|메소드(Method)
-----|-----
출력|.forEach()
소모|.reduce()
검색|.findFirst(), .findAny()
검사|.anyMatch(), .allMatch(), .noneMatch()
통계|.count(), .min(), .max()
연산|.sum(), .average()
수집|.collect() 

