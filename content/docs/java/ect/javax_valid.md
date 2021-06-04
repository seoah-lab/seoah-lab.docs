---
title: javax @Valid
---

# javax @Valid

```
implementation 'org.springframework.boot:spring-boot-starter-validation'
```

@NotBlank 
- null 이 아닌 값이다.
- 공백이 아닌 문자를 하나 이상 포함한다

@NotEmpty
- Type : CharSequence (length of character) Collection (collection size) Map (map size Array (array length)
- null 이거나 empty(빈 문자열)가 아니어야 한다.

@NotNull
- Type : 
- null 이 아닌 값이다.

@Null
- Type :어떤 타입이든 수용한다.
- null 값이다.

