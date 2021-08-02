Optional Class
===============================   
 + 개발을 하면서 예상하지 못한 NullPointerException 에러를 방지하기 위한 클래스이다.
 + 래퍼 타입 클래스이므로, null에 대한 처리가 가능하다.
 + return에 명시하는 것을 권장한다.
 + Primitive 타입 전용 메서드가 따로 있다.
 + Collection, Map, Stream, Array은 Optional로 감싸지 않고, 해당 객체 고유의 방식으로 예외처리를 해야한다.

1.Optional 객체의 생성
-------------------------------
 + of(), ofNullable() 메서드를 사용하여 생성
 + of() 메서드는 null이 아닌 명시된 값을 가진 Optional 객체를 반환
 + ofNullable() 메서드는 명시된 값이 null이 아니면 명시된 값을 가지는 Optional 객체를 반환하며, null이면 비어있는 Optional 객체를 반환

2.Optional 객체에 접근
-------------------------------
 + get() 메서드를 사용하면 저장된 값에 접근
 + NoSuchElementException을 방지하기 위해 isPresent() 메서드를 사용하여 값이 있는지 우선 확인
 + orElse(T): 지정된 값이 존재하면 그 값을 반환하고, 없을 경우 인수로 전달된 값을 반환
 + orElseGet(Supplier): 저장된 값이 존재하면 그 값을 반환하고, 없을 경우 인수로 전달된 람다 표현식의 결과값을 반환
 + orElseThrow(): 저장된 값이 존재하면 그 값을 반환하고, 없을 경우 인수로 전달된 예외를 발생
   - orElse()의 경우 전달되는 인스턴스가 매번 실행이 되기 때문에, 인스턴스가 생성되어 있는 경우에 사용
   - orElseGet()의 경우 전달되는 인스턴스가 Supplier가 전달되므로 지연 연산이 가능하므로, 동적으로 처리해야 하는 경우에 사용하기 적합.
 + isEmpty(): 값이 있는지 확인. (java 11부터 사용 가능)
 + ifPresent(Consumer): Optional에 값이 있으면 그 값으로 ~하라. 
 + filter(Predicate): Optional 안에 들어 있는 값을 필터링
 + flatMap(Function): Optional 안에 들어 있는 인스턴스가 Optional인 경우에 사용하면 편리하다.
 
        public static void main() {
             List<OnlineClass> springClasses = new ArrayList<>();
             springClasses.add(new OnlineClass(1, "spring boot", true)) // id, title, closed
             springClasses.add(new OnlineClass(5, "rest api development", false)) // id, title, closed
             
             Optional<OnlineClass> spring = springClasses.stream()
                            .filter(oc -> oc.getTitle().startsWith("spring"))
                            .findFirst();
                            
             boolean present = spring.isPresent; // true
             OnlineClass = optional.get(); // NoSuchException 발생 가능성이 있는 코드
             optional.ifPresent(oc -> System.out.println(oc.getTitle()));
             OnlineClass onlineClass = optional.orElse(createNewClass()); // 저장된 값이 없을 경우, 전달된 OnlineClass 타입의 인스턴스를 반환
             
             OnlineClass onlineClass2 = optional.orElseThrow(IllegalStateException::new); // supplier
             
        }

3.기본 타입의 Optional 클래스
--------------------------------
 + 래퍼 타입이 아닌 기본 타입의 클래스
 + OptionalInt, OptionalLong, OptionalDouble
 + 클래스별로 접근이 가능한 메소드를 제공

클래스|저장된 값에 접근하는 메서드
-----|-----
Optional| T get()
OptionalInt| int getAsInt()
OptionalLong| long getAsLong()
OptionalDouble| double getAsDouble()
