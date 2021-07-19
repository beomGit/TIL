Lambda Expressions
===============================
    간결한 코드를 작성할 수 있게 해주며, 지연 연산(Lazy evaluation)을 통해 필요한 연산만을 처리할 수있다.
    또한, 순수 함수(Pure function)를 통해 Side-Effect에 대해서 안정성을 가지므로 멀티 쓰레드를 활용하여 병렬 처리가 가능하다.

1.특징(Characteristic)
-------------------------------
 + [익명 함수](https://namu.wiki/w/%EB%9E%8C%EB%8B%A4%EC%8B%9D?from=%EC%9D%B5%EB%AA%85%ED%95%A8%EC%88%98)(Anonymous functions)로서 [일급 객체](https://ko.wikipedia.org/wiki/%EC%9D%BC%EA%B8%89_%EA%B0%9D%EC%B2%B4)(First class citizen)이다.
 + 제네릭(Generic) 타입을 보고 컴파일러가 인자의 타입을 추론할 수 있다.
 + 로컬 클래스, 익명 클래스와는 다르게 람다가 선언된 메소드 범위(scope) 밖의 참조 변수는 쉐도윙할 수 없다.
 
2.변수 캡쳐(Variable Capture)
--------------------------------
 + 로컬 변수 캡쳐
   - 변수가 final 혹은 effectively final인 경우에만 참조할 수 있다.
   - 위 조건에 해당하지 않는 변수를 참조할 경우 컴파일러가 이를 방지한다.
 + Effectively final
   - 자바 8부터 지원하는 변수로, final이 명시되지 않더라도 초기 할당된 값이 변하지 않은 변수

