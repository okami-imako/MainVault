---
tags:
  - java/spring/testing
  - mvc
---
# Description
Очень похож на [[@DataJpaTest]], но вместо репозиториев ищет [[@Controller|контроллеры]]
Реальный [[WebContext]] не создается.
Создает и настраивает [MockMvc](https://docs.spring.io/spring-framework/reference/testing/spring-mvc-test-framework.html), который маршрутизирует все запросы к нужным контроллерам

# Useful Links

# Related Topics
- [[Spring Boot]]
- [[Test]]
- [[Component Test]]