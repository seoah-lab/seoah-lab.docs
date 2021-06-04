---
title: Part3. 스트림과람다...
weight: 1
---

# Part3. 스트림과 람다를 이용한 효과적인 프로그래밍

## 8장 컬렉션 API 개선

**컬렉션 팩토리**

적은 요소를 가지고 있는 리스트를 생성

```java

List<String> friends = Arrays.asList("Rapheal", "Olivia");

```

UnsupportedOperationException 내부적으로 고정된 크기의 변환할 수 있는 배열로 구현 되었기 때문에 발생한다.


집합을 생성

```java
Set<String> friends = new HashSet<>(Arrays.asList("Rapheael", "Olivia", "Thibaut"));
```

스트림 API 로 집합을 생성

```java
Set<String> friends = Stream.of("Raphael", "Olivia", "THibat").collect(Collectors.toSet());
```

**리스트 팩토리**

List.of() 로 간단한 리스트 생성

```java
ListM<String> friend = List.of("Raphael", "Olivia", "Thibat");
```

List.of() 로 생성한 리스트에 요소를 추가하거나 변경하려고 하면 UnsupportedOperationException 이 발생한다.

스트림으로도 리스트를 생성할 수 있다. 데이터 처리 형식을 설정하거나 데이터를 변환할 필요가 없다면 사용하기 편한 팩토리 메서드를 이용할 것을 권장한다.

**집합 팩토리**

집합 팩토리로 집합으로 생성

```java
Set<String> friends = Set.of("Raphael", "Olivia", "Thibat");
```

**맵 팩토리**

맵팩토리를 활용하여 생성
```java
import java.util.Mpa.entry;

Map<String, Integer> ageOfFriends 
                    = Mpa.ofEntries(entry("Raphael", 30),
                                    entry("Oliva", 25),
                                    entry("Thibat", 30));
```


**리스트와 집합의 처리**





