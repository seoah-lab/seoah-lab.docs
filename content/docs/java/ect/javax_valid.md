---
title: javax @Valid
---

# javax @Valid



```
implementation 'org.springframework.boot:spring-boot-starter-validation'
```

@NotNull : The annotated element must not be null. Accepts any type.
- null 을 허용하지않고 모든 타입에 사용할수 있다.
- "" 이나 " " 은 허용한다.

@NotEmpty: The annotated element must not be null nor empty
- null 과 "" 은 허용하지 않는다.
- " " 은 허용
- 문자열, 콜랙션, 맵, 배열 타입에 활용할 수 있다.

- CharSequence (length of character sequence is evaluated)
- Collection (collection size is evaluated)
- Map (map size is evaluated)
- Array (array length is evaluated)


@NotBlank : The annotated element must not be null and must contain at least one non-whitespace character. Accepts 
- null 과 "" 과 " " 모두 허용하지 않는다.


@Null : The annotated element must be null
- null을 허용한다.


출처  
[Java EE ](https://javaee.github.io/javaee-spec/javadocs/javax/validation/class-use/Constraint.html) 
