---
tags:
  - java/spring/testing
---
# Description
Это аннотация [[Spring Boot|спринг бута]], которая создаст in-memory [[Database|базу данных]] и применит конфигурацию, релевантную для [[JPA|jpa]] [[Test|тестов]]

Работает по похожей схеме как и [[@SpringBootTest#🚩Сценарий 1|первый сценарий @SpringBootTest]] - идет наверх по пакетам, пока не наткнется на `@SpringBootConfiguration`, потом делает то, что вместе с ней указано, т.е. если над классом вместе с `@SpringBootConfiguration` стоит, скажем, `@ComponentScan`, то спринг пойдет сканировать пакеты, ❗***игнорируя*** все бины, которые не являются [[Repository|репозиторями]]

Еще создает [TestEntityManager](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/autoconfigure/orm/jpa/TestEntityManager.html) при помощи которого можно чет с базой делать удобно

# Useful Links
- [documentation](https://docs.spring.io/spring-boot/docs/current/api/org/springframework/boot/test/autoconfigure/orm/jpa/DataJpaTest.html)

# Related Topics
- [[Test]]
- [[Component Test]]