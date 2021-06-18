---
title: Part 1. 기초
weight: 1
---

## **1 장 자바 8, 9, 10, 11 : 무슨 일이 일어나고 있는가?**

- 스트림 API

    스트림이란? 한번에 한 개씩 만들어지는 연속적인 데이터 항목들의 모임

    스트림의 특징 

    - 스레드를 직접 구현하지 않으면서도 멀티스레딩
    - shared mutable data 에 접근하지 않고 안전한 코드 실행
    - 반복적인 코드 블록으로 인한 외부 반복에서 내부 반복으로 전환함

    ![Stream](/images/stream.png)
    
- 메서드에 코드르 전달하는 기법

    동작의 파라미터화 (메서드를 전달함)

    메서드를 일급으로 함수를 일급으로

    메서드참조 (method reference)

    람다: 익명함수

- 인터페이스의 디폴트 메소드

    인터페이스 내부에 새로운 메소드를 구현

- 함수형 프로그래밍

## **2 장 동적 파라미터화 코드전달하기**

변화하는 요구 사항에 대응하기 (예제로 동적 파라미터화 이해하기)

첫번째 시도 : 녹색사과 필터링

```java
List<Apple> inventory = Arrays.asList(
        new Apple(80, Color.GREEN),
        new Apple(155, Color.GREEN),
        new Apple(120, Color.RED));

public static List<Apple> filterGreenApples(List<Apple> inventory) {
    List<Apple> result = new ArrayList<>();
    for (Apple apple : inventory) {
      if ("green".equals(apple.getColor())) {
        result.add(apple);
      }
    }
    return result;
  }

  public static List<Apple> filterHeavyApples(List<Apple> inventory) {
    List<Apple> result = new ArrayList<>();
    for (Apple apple : inventory) {
      if (apple.getWeight() > 150) {
        result.add(apple);
      }
    }
    return result;
  }
```

두번째 시도 : 색을 파라미터화

- Color enum으로 일급 객체화

```java
public static List<Apple> filterApplesByColor(List<Apple> inventory, Color color) {
    List<Apple> result = new ArrayList<>();
    for (Apple apple : inventory) {
      if (apple.getColor() == color) {
        result.add(apple);
      }
    }
    return result;
  }

List<Apple> greenApples = filterApplesByColor(inventory, Color.GREEN);
    System.out.println(greenApples);
```

세번째 시도: 가능한 모든 속성을 필터링

네번째 시도: 추상적 조건으로 필터링

```java
//인터페이스로 추상화
interface ApplePredicate {
    boolean test(Apple a);
}

//인터페이스를 구현
static class AppleWeightPredicate implements ApplePredicate {

  @Override
  public boolean test(Apple apple) {
    return apple.getWeight() > 150;
  }

}

static class AppleColorPredicate implements ApplePredicate {

  @Override
  public boolean test(Apple apple) {
    return apple.getColor() == Color.GREEN;
  }

}

static class AppleRedAndHeavyPredicate implements ApplePredicate {

  @Override
  public boolean test(Apple apple) {
    return apple.getColor() == Color.RED&& apple.getWeight() > 150;
  }

}
```

```java
public static List<Apple> filter(List<Apple> inventory, ApplePredicate p) {
  List<Apple> result = new ArrayList<>();
  for (Apple apple : inventory) {
    if (p.test(apple)) {
      result.add(apple);
    }
  }
  return result;
}

// [Apple{color=GREEN, weight=80}, Apple{color=GREEN, weight=155}]
List<Apple> greenApples2 = filter(inventory, new AppleColorPredicate());
System.out.println(greenApples2);

// [Apple{color=GREEN, weight=155}]
List<Apple> heavyApples = filter(inventory, new AppleWeightPredicate());
System.out.println(heavyApples);

// []
List<Apple> redAndHeavyApples = filter(inventory, new AppleRedAndHeavyPredicate());
System.out.println(redAndHeavyApples);
```

다섯번째 시도: 익명클래스 사용

```java
List<Apple> redApples = filter(inventory, new ApplePredicate() {
      @Override
      public boolean test(Apple a) {
        return RED.equals(apple.getColor());
      }
    });
```

여섯번째 시도 : 람다 표현식

```java
List<Apple> result = filterApples(inventory, (Apple apple) -> RED.equals(apple.getcolor()));
```

일곱번째 시도: 리스트 형식의 추상화

```java
public static <T> List<T> filter(List<T> list, Predicate<T> p ) {
	List<T> result = new ArrayList<>;
	for(T e: list) {
		if(p.test(e)) {
			result.add(e);
		}
	}
	return result;
}
```

## 3장 람다 표현식

![lambda](/images/lambda.png)

- 익명 : 보통 메서드와 달리 이름이 없으므로 익명이라 표현한다.
- 함수 : 특정 클래스에 종속되지 않으므로 메서드 대신 함수라고 표현한다.
- 전달 : 람다 표현식을 메서드 인수로 전달하거나 변수로 저장할 수 있다.
- 간결성 : 익명 클래스처럼 많은 코드를 구현할 필요가 없다.

```java
Comparator<Apple> byWeight = new Comparator<Apple>() {
    public int compare(Apple a1, Apple a2) {
        return a1.getWeight().compareTo(a2.getWeight());
    }
}

Compartor<Apple> byWeight = (Apple a1, Apple a2) ->  a1.getWeight().compareTo(a2.getWeight());
```

함수형 인터페이스라는 문맥에서 람다 표현식을 사용할수 있다.

**함수형 인터페이스**

- 함수형 인터페이스는 정확히 하나의 추상메서드를 지정하는 인터페이스이다.

**함수 디스크립터**

- 함수 디스크립터는 람다에서의 메소드 시그니처를 표현하는 메서드를 말한다.

**람다 활용** 

실행 어라운드 패턴

자원 처리(예를 들면 DB의 파일 처리)에 사용하는 순환 패턴은 자원을 열고, 처리한 다음에, 자원을 닫는 순서로 이루어진다. 설정과 정리 과정은 대부분 비슷하다. 즉, 실제 자원을 처리하는 코드를 설정과 정리 두 과정이 둘러싸는 형태를 갖는데 이 같은 형식의 코드를 실행 어라운드 패턴이라고 부른다. 

```java
private static final String FILE = ExecuteAround.class.getResource("./data.txt").getFile();

    public static String processFileLimited() throws IOException {
    try (BufferedReader br = new BufferedReader(new FileReader(FILE))) {
        return br.readLine();
    }
    }

    //(1) 실행 어라운트 패턴의 구현
    public static String processFile(BufferedReaderProcessor p) throws IOException {
    try (BufferedReader br = new BufferedReader(new FileReader(FILE))) {
        return p.process(br);
    }
    }

    public interface BufferedReaderProcessor {
    String process(BufferedReader b) throws IOException;
    }

    public static void main(String... args) throws IOException {
    // 더 유연하게 리팩토링할 메서드
    String result = processFileLimited();
    System.out.println(result);

    System.out.println("---");

    String oneLine = processFile((BufferedReader b) -> b.readLine());
    System.out.println(oneLine);

    String twoLines = processFile((BufferedReader b) -> b.readLine() + b.readLine());
    System.out.println(twoLines);
    }
```

**함수형 인터페이스의 사용**

- Predicate

```java
@FunctionalInterface
public interface Predicate<T> {

    /**
     * Evaluates this predicate on the given argument.
     *
     * @param t the input argument
     * @return {@code true} if the input argument matches the predicate,
     * otherwise {@code false}
     */
    boolean test(T t);
}
```

- Consumeer

```java
@FunctionalInterface
public interface Consumer<T> {

    /**
     * Performs this operation on the given argument.
     *
     * @param t the input argument
     */
    void accept(T t);
}
```

- Function

```java
@FunctionalInterface
public interface Function<T, R> {

    /**
     * Applies this function to the given argument.
     *
     * @param t the function argument
     * @return the function result
     */
    R apply(T t);
}
```

람다의 형식 검사, 형식 추론, 제약

- **형식검사**

```java
filter (inventory, (Apple apple) -> apple.getWeight() > 150)
```

![형식검사](/images/lambda_test.png)

```java
//같은 람다, 다른 함수형 인터페이스
Callable<Integer> c = () -> 42;
PrivilegedAction<Integer> p = () -> 42;
```

- **형식 추론**

```java
filter (inventory, (Apple apple) -> apple.getWeight() > 150)
filter (inventory,  apple -> apple.getWeight() > 150)  //Apple 은 생략 가능하다.
```

- **제약**

람다에서 지역변수는 람다 캡처링에 의해서 final 변수와 동일하게 사용해야 한다.

```java
int portNumber = 1337;
Runnable r = () -> System.out.prinln(portNumber); 
portNumber = 31337; 
//컴파일 오류 발생
```

**메서드 참조**

메소드 참조(method reference)는 람다 표현식이 단 하나의 메소드만을 호출하는 경우에 해당 람다 표현식에서 불필요한 매개변수를 제거하고 사용할 수 있다.

```java
inventory.sort((a1, a2) -> a1.getWeight().compareTo(a2.getWeight)); 
inventory.sort(comparing(Apple::getWeight));
```

**생성자 참조**

단순히 객체를 생성하고 반환하는 람다 표현식은 생성자 참조로 변환

```java
Supplier<Apple> c1 = Apple::new;
Supplier<Apple> c1 = () -> new Apple();
Apple a1 = c2.get();

Function<Integer, Apple> c2 = Apple::new;
Function<Integer, Apple> c2 = (weight) -> new Apple(weight);
Apple a2 = c2.aply(110);
```

**람다 표현식을 조합할 수 있는 유용한 메소드**

- Comparator 조합

```java
// 비교를 이용해 Comparator를 반환
Comparator<Apple> c = Comparator.comparing(Apple::getWeight);

// 역정렬
inventory.sort(comparing(Apple::getWeight).reversed()); // <- 무게 내림차순으로 정렬

// 연결
inventory.sort(comparing(Apple::getWeight)
					.reversed() // <- 무게 내림차순으로 정렬
					.thenComparing(Apple::getCountry)); // 두 사과의 무게가 같은면 국가 별로 정렬

```

Predicate 조합

```java
//기존 프레디케이트 객체결과를 반전시킨 결과
Predicate<Apple> notRedApple = redApple.negate();

// 두개 연결
Predicate<Apple> redAndHeavyApple = redApple.and(apple -> apple.getWeight() > 150);

// 연결해서 복잡한 결과
Predicate<Apple> redAndHeavyApple = redApple.and(apple -> apple.getWeight() > 150)
																						.or(GREEN.equals(a.getColor()));
```

Funtion 조합

```java
Function<Integer, Integer> f = x -> x + 1; 
Function<Integer, Integer> g = x -> x * 5; 
Function<Integer, Integer> h = f.andThen(g); 
int result = h.appy(1); //4 반환

Function<Integer, Integer> f = x -> x + 1; 
Function<Integer, Integer> g = x -> x * 5; 
Function<Integer, Integer> h = f.compose(g); 
int result = h.appy(1); //3 반환
```