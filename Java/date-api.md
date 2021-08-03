Date & Time
===============================   
 + 자바 8에 새로운 날짜와 API가 생긴 이유
   - java.util.Date 클래스는 mutable하기 때문에 thread safe하지 않다.
     + .setTime()의 경우, 해당 인스턴스가 가진 값이 변경된다.
   - 메서드를 포함한 클래스의 명칭이 명확하지 않다.
     + Date 클래스는 날짜 데이터를 비롯하여 TimeStamp도 표현할 수 있다.
   - 버그가 발생할 여지가 많다.
     + new GregorianCalendar(1970, 1, 1);
     + 두 번째 인자인 1의 경우, month는 0부터 시작하기 때문에 상수 값 사용이 권장된다.

1.디자인 철학
-------------------------------
 + Clear
   - API 메소드는 명확해야 한다.
     + 기존의 Date 클래스는 기계용 시간(Machine time)과 인류용 시간(Human time)을 사용하므로 명확하지 않다.
 + Fluent
   - 메소드가 null을 반환하지 않기 때문에 메소드 체이닝이 가능하다.
 + Immutable
   - 새로운 값(시간/날짜)을 설정할 때 기존의 인스턴스에 값을 변경하는 것이 아닌 새로운 인스턴스로 생성이 된다.
 + Extensible
   - 나라별 시간에 확장성을 가진다. (양력, 음력, Thai, ...)

2.주요 API 특징
-------------------------------
 + 기계용 시간(Machine time)과 인류용 시간(Human time)으로 나눌 수 있다.
 + 기계용 시간 EPOCK (1970년 1월 1일 0시 0분 0초)부터 현재까지의 타임스탬프를 표현한다.
 + 인류용 시간은 우리가 흔히 사용하는 연,월,일,시,분,초 등을 표현한다.
 + 타임 스탬프는 Instant를 사용한다.
 + 특정 날짜(LocalDate), 시간(LocalTime), 일시(LocalDateTime)를 사용할 수 있다.
 + 기간을 표현할 때는 Duration(시간 기반)과 Period(날짜 기반)를 사용할 수 있다.
 + DateTimeFormatter를 사용해서 일시를 특정한 문자열로 포매팅할 수 있다.

3.Date & Time API
-------------------------------
 + 기계용 시간(Machine Time)
   - Instant.now(); 현재 UTC(GMT)를 반환합니다. (기준시)
   - Universal Time Coordinated == Greenwich Mean Time
 + 인류용 시간(Human Time)
   - LocalDateTime.now(): 현재 시스템 Zone에 해당하는(로컬) 일시를 리턴한다.
   - LocalDateTime.of(int, Month, int, int, int, int): 로컬의 특정 일시를 리턴한다.
   - ZoneDateTime.of(int, Month, int, int, int, int, ZoneId): 특정 Zone의 일시를 리턴한다.
 + 기간을 표현하는 방법
   - Period / Duration .between
    ```
    LocalDate today = LocalDate.now();
    LocalDate thisYearBirthday = LocalDate.of(2020, Month.JULY, 15);
    
    
    Period period = Period.between(today, thisYearBirthday);
    System.out.println(period.getDays());
    
    Period until = today.until(thisYearBirthday);
    System.out.println(until.get(ChronoUnit.DAYS));
    
    ```
   - Period.between(today, birthDay)
     + 현재 날짜와 생일 날짜간의 차이 나는 시간을 Period 타입의 인스턴스로 생성한다.
   
 + 파싱 또는 포매팅
   - 정의된 포맷
     + https://docs.oracle.com/javase/8/docs/api/java/time/format/DateTimeFormatter.html#predefined
   - LocalDateTime.parse(String, DateTimeFormatter);
   - DateTimeFormatter
   ```
   DateTimeFormatter formatter = DateTimeFormatter.ofParttern("MM/dd/yyyy")
   LocalDate date = LocalDate.parse("07/15/1982", formatter);
   System.out.println(date);
   System.out.println(today.format(formatter));
   
   LocalDateTime now = LocalDateTime.now();
   System.out.println(now.format(MMddyyyy));
   ```
 + 레거시 API 지원
   - Java8에 추가된 LocalDate, LocalDateTime, Instant는 이전에 사용되던 Date 클래스와 호환이 가능하다.
   ```
   Date date = new Date();
   Instant instant = date.toInstant();
   Date newDate = Date.from(instant);
   
   ```
