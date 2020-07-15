

JDBC 也是一种规范和接口，不过 JDBC 是面向 SQL 的，使用起来比较繁琐。所以就有了 ORM 框架，建立了 Java 对象与数据库表之间的映射关系，可以通过直接操作对象来实现持久化，简化了操作的繁杂度。而 JPA 就是 ORM 框架的规范，值得一提的是 Hibernate 是符合 JPA 规范的，而 MyBatis 却不符合，因为 MyBatis 还是需要写 SQL 的