---
title: javax @Valid
---

# javax @Valid

```
implementation 'org.springframework.boot:spring-boot-starter-validation'
```

@NotNull
- The annotated element must not be null. Accepts any type.

@NotEmpty: The annotated element must not be null nor empty
- CharSequence (length of character sequence is evaluated)
- Collection (collection size is evaluated)
- Map (map size is evaluated)
- Array (array length is evaluated)

@NotBlank 
- The annotated element must not be null and must contain at least one non-whitespace character. Accepts 

@Null
- The annotated element must be null


출처
[Java EE ](https://javaee.github.io/javaee-spec/javadocs/javax/validation/class-use/Constraint.html) 
