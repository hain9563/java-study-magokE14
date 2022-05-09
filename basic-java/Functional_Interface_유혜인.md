# 함수형 인터페이스

1개의 추상 메서드를 갖고 있는 인터페이스 = single abstract method

## Runnable

java에서 쓰레드를 작성하는 방법은 2가지가 존재

👉 Thread 클래스 상속

‘클래스’이기 때문에 thread 상속을 받으면 다른 클래스 상속이 불가

👉 Runnable 인터페이스 구현

더 정확히는 Runnable 인터페이스를 구현해서 thread 객체를 직접 만들어 사용

확장성이 더 중요한 클래스의 경우 runnable 방식을 채용하는 것이 적합 → 실제로도 많이 쓰임

예제 : [https://inor.tistory.com/8?category=708183](https://inor.tistory.com/8?category=708183)

## Supplier<T>

인자를 받지 않고 type T 객체를 리턴하는 함수형 인터페이스.

```java
				Supplier<Item> supplier= ()-> new Item(10, "Hello");

        Item result = supplier.get();   // supplier로부터 객체 리턴은 get()을 호출

        System.out.println(result.getId() + ", " + result.getValue());
```

- 추상 메서드 get()을 통해 Lazy evaluation이 가능해진다. = 불필요한 연산을 피한다.
    
    supplier를 사용하는 이유 예제 : [https://m.blog.naver.com/zzang9ha/222087025042](https://m.blog.naver.com/zzang9ha/222087025042)
    
    → 연산이 많은 함수를 매개변수로 사용하는 경우 supplier를 사용하면 이득 
    

예제 : [https://codechacha.com/ko/java8-supplier-example/](https://codechacha.com/ko/java8-supplier-example/)

## Consumer<T>

1개의 Type T 인자를 받고 리턴 값이 없는 함수형 인터페이스

```java
				List<String> fruits = Arrays.asList("apple", "kiwi", "orange");

        Consumer<List<String>> addNumber = list -> {
            for (int i = 0; i < list.size(); i++) {
                list.set(i, (i + 1) + ". " + list.get(i));
            }
        };

        Consumer<List<String>> printList = list -> {
            for (String fruit : list) {
                System.out.println(fruit);
            }
        };

        addNumber.andThen(printList).accept(fruits); // accept로 수행
```

예제 : [https://codechacha.com/ko/java8-consumer-example/](https://codechacha.com/ko/java8-consumer-example/)

chaining 메소드인 andThen() 메소드를 사용할 수 있는 특징이 있다.

## Function<T,R>

T - 함수에 대한 입력 유형이며

R - 함수 결과의 유형

![Untitled](%E1%84%92%E1%85%A1%E1%86%B7%E1%84%89%E1%85%AE%E1%84%92%E1%85%A7%E1%86%BC%20%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%90%E1%85%A5%E1%84%91%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%89%E1%85%B3%20d87d341609954e319e83147a02265111/Untitled.png)

compose() : before 함수를 먼저 적용 후 다음 함수 실행 - fun2 → fun

andThen() : after 함수를 먼저 적용 후 다음 함수 실행 - fun → fun2

![Untitled](%E1%84%92%E1%85%A1%E1%86%B7%E1%84%89%E1%85%AE%E1%84%92%E1%85%A7%E1%86%BC%20%E1%84%8B%E1%85%B5%E1%86%AB%E1%84%90%E1%85%A5%E1%84%91%E1%85%A6%E1%84%8B%E1%85%B5%E1%84%89%E1%85%B3%20d87d341609954e319e83147a02265111/Untitled%201.png)

identity() : 입력 인수를 그대로 반환하는 함수.

## Predicate

Type T 인자를 받고 boolean을 리턴하는 함수형 인터페이스

```java
				Predicate<Integer> predicate = (num) -> num > 10;

        boolean result = predicate.test(100);

        System.out.println(result);  // true
```

- and() : predicate1.and(predicate2).test(25) 인 경우 predicate 1, 2 모두 true일때 true 리턴
- or()
- isEqual()
- negate() : not
- filter()의 인자로 사용가능

- 위 and, or, negate 메서드는 ‘디폴트 메서드’이다.
    
    자바 8에서 추가된 기능
    
    인터페이스를 구현시 디폴트 메서드는 반드시 오버라이드하지 않아도 된다. 
    
    인터페이스의 구현의 강제성을 없앤 기능이다.
    
    인터페이스에 있는 특정 기능이 거의 모든 곳에 사용될 때, 그리고 굳이 오버라이드하지 않아도 되는 경우 디폴트 메서드를 추가하면 편리
    

예제 : [https://codechacha.com/ko/java8-predicate-example/](https://codechacha.com/ko/java8-predicate-example/)

## 출처

- [https://www.daleseo.com/java-thread-runnable/](https://www.daleseo.com/java-thread-runnable/)
- [https://codechacha.com/ko/java8-consumer-example/](https://codechacha.com/ko/java8-consumer-example/)
- [https://m.blog.naver.com/zzang9ha/222087025042](https://m.blog.naver.com/zzang9ha/222087025042)