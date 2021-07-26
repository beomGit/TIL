Stream API
===============================

1.스트림 생성(Generate Stream)
-------------------------------


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

