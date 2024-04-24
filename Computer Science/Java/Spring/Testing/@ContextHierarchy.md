---
tags:
  - java/spring/testing
---
# Description
Чтобы кэшировать и переиспользовать кусочки контекста в разных тестах, можно использовать аннотацию ***@ContextHeirarchy***:
```java
@ContextHeirarchy({
	@ContextConfiguration(classes = GenericConfig.class),
	@ContextConfiguration(classes = ServiceConfig.class)
})
```

***Внимание***: порядок важен

# Useful Links
- [documentation](https://docs.spring.io/spring-framework/reference/web/webmvc/mvc-servlet/context-hierarchy.html)

# Related Topics
- [[Spring Boot]]
- [[@Configuration]]