---
title: Part2. 함수형 데이터 처리
weight: 2
---

# Part2. 함수형 데이터 처리

### 4장 스트림 소개
**스트림이란 무엇인가**
Stream 자바 8 API 새로 추가된 기능이다.

자바 7의 코드
```java
List<Dish> lowCaloricDishes = new ArrayList<>();
for(Dish dish: menu) {
    if(dish.getCalories() < 400) {
        lowCaloricDishes.add(dish);
    }
}

Collections.sort(lowCaloricdishes, new Comparator<Dish>() { // 익명 클래스로 요리 정렬
    pulbic int compare(Dish dish1, Dish dish2) {
        return Integer.compare(dish1.getCalories(), dish2.getCalories());
    }
});

List<String> lowCaloricDishesName = new ArrayList();
for(DIsh dish: lowCaloricDishes) {
    lowCaloricDishesName.add(dish.getName());
}

```

자바 8 후의 코드
```java
import static java.util.Comparator.comparing;
import static java.util.stream.Collectors.toList;

List<String> lowCaloricDishesName =
                menu.stream() //parallelStream 을 사용하면 병렬 
                    .filter(d -> d.getCalories() < 400>) //400 칼로리 미만의 요리 선택
                    .sorted(comparing(Dishes::getCalories)) // 칼로리로 정렬
                    .map(Dish::getName) // 요리명 추출
                    .collect(toList()); // 모든 요리명 리스트에 저장

```

자바 8 스트림 API 의 특징
- 선언형 : 더 간결하고 가독성이 좋아진다.
- 조립할 수 있음 : 유연성이 좋아진다.
- 병렬성 : 성능이 좋아진다.


**스트림 시작하기**

데이터 처리 연산을 지원하도록 소스에서 추출된 연속된 요소 (Squence of element)로 정의할 수 있다.
- 연속 된 요소 
- 소스
- 데이터 처리 연산

스트림의 주요 특징
- 파이프라이닝 : Laziness, short-circuiting
- 내부반복 

스트림의 주요 기능  
- filter : 람다를 인수로 받아 스트림에서 특정 요소를 제외시킨다.  
- map : 람다를 이용해서 한 요소를 다른 요소로 변환하거나 정보를 추출한다.  
- limit: 스트림 크기를 제한한다.  
- collect: 스트림을 다른 형식으로 변환한다.

![Stream](/images/stream.png)

**스트림의 연산**

- 중간연산 - 쇼트 서킷, 서로 다른 연산이지만 병합되는 기법 루프 퓨전(loop fusioin)
- 최종연산 


### 5장 스트림 활용

![중간연산과최종연산](/images/stream_연산.jpg)

**Optional?**  
Optional 값의 존재나 부재 여부를 표현하는 컨테이너 클래스  
null 은 쉽게 에러를 일으킬 수 있으므로 자바 8 라이브러리 설계자는 Optional<T>를 만들었다.

- isPresent(): 값이 있으면 참을 반환한다.
- T get() : 값이 존재하면 값을 반환하고 없으면 NoSuchElementException을 일으킨다.
- T orElse(T other): 값이 있으면 값을 반환하고, 값이 없으면 기본값을 반환한다.

**findFirst와 findAny 는 언제 사용하나?**  
병렬 스트림에서는 첫 번째 요소를 찾기 어렵다.
요소의 순서가 상관없다면 findAny를 사용한다.

**리듀싱**
모든 스트림 요소를 반복 처리해서 값으로 도출하는 리듀싱 연산을 한다.
함수형 프로그래밍 언어 용어로는 폴드라고 부른다.

```java
int sum = 0;
for (int x : number) {
    sum += x;
}

//초기 값 0 
int sum = numbers.stream().reduce(0, ( a,b,) -> a + b);

//초기 값 없이 사용
Optional<Integer> sum = numbers.stream().reduce((a,b) -> (a + b));

//최대값 최솟값
Optional<Integer> max = numbers.stream().reduce(Integer::max);
Optional<Integer> min = numbers.stream().reduce(Integer::min);
```

### 6장 스트림으로 데이터 수집
### 7장 병렬 데이터 처리와 성능