
#  Spring Boot – Senior Level Interview Questions


#  1. Core Spring & Boot Internals
````
## Q1. How does Spring Boot auto-configuration work?
**Expect:**
- `@EnableAutoConfiguration` → triggers auto-config
- Reads `spring.factories` / `AutoConfiguration.imports`
- Conditional loading via:
  - `@ConditionalOnClass`
  - `@ConditionalOnMissingBean`
- Classpath-driven configuration

---

## Q2. What happens during Spring Boot startup?
**Expect flow:**
1. `SpringApplication.run()`
2. Create ApplicationContext
3. Load environment & properties
4. Auto-configuration kicks in
5. Bean creation + dependency injection
6. Embedded server starts (Tomcat/Jetty)

---

## Q3. Bean lifecycle in Spring?
**Expect:**
- Instantiation
- Dependency Injection
- `@PostConstruct`
- Ready to use
- `@PreDestroy`

Advanced:
- BeanPostProcessor
- InitializingBean

---

## Q4. Difference: `@Component`, `@Service`, `@Repository`
**Expect:**
- All are stereotypes
- `@Repository` → exception translation
- `@Service` → business logic
- `@Component` → generic

---
````

#  2. Dependency Injection & Design
````
## Q5. Constructor vs Field Injection?
**Answer:**
- Constructor → preferred (immutable, testable)
- Field → bad for testing

---

## Q6. How does Spring resolve circular dependencies?
**Expect:**
- Works for setter/field injection
- Fails for constructor injection
- Uses early bean references (3-level cache)

---

## Q7. What is `@Primary` vs `@Qualifier`?
- `@Primary` → default bean
- `@Qualifier` → explicit selection

---
````

#  3. Spring MVC / REST
```
## Q8. Request flow in Spring Boot REST API?
**Expect:**
Client → DispatcherServlet → Controller → Service → Repo → DB

---

## Q9. Difference: `@RestController` vs `@Controller`
- `@RestController = @Controller + @ResponseBody`

---

## Q10. How do you handle global exceptions?
**Expect:**
```java
@ControllerAdvice
@ExceptionHandler

---

## Q11. How does validation work?

**Expect:**

* `@Valid`
* Hibernate Validator
* Custom validators
```
---

#  4. Spring Data & Transactions
```
## Q12. How does Spring Data JPA work internally?

**Expect:**

* Proxy-based implementation
* Generates queries dynamically
* Uses EntityManager

---

## Q13. What is transaction propagation?

**Key types:**

* REQUIRED (default)
* REQUIRES_NEW
* SUPPORTS

---

## Q14. Isolation levels?

* READ_COMMITTED
* REPEATABLE_READ
* SERIALIZABLE

---

## Q15. What is Lazy vs Eager loading?

* Lazy → fetched when needed
* Eager → fetched immediately
```
---

#  5. Spring Security
```
## Q16. How does Spring Security filter chain work?

**Expect:**

* Filters before controller
* Authentication → Authorization

---

## Q17. How would you implement JWT in Spring Boot?

**Expect flow:**

1. Login → generate JWT
2. Client sends token
3. Filter validates token
4. Set authentication in context

---

## Q18. Difference: Authentication vs Authorization?

* Auth → identity
* AuthZ → permissions
```
---

#  6. Microservices & Production
```
## Q19. How do you make a Spring Boot service scalable?

**Expect:**

* Stateless design
* Horizontal scaling
* Externalized config
* Load balancer

---

## Q20. How do you handle configuration across environments?

* `application-{env}.properties`
* Spring Cloud Config (advanced)

---

## Q21. How do you implement rate limiting?

* Redis + token bucket / leaky bucket

---

## Q22. How do you handle inter-service communication?

* REST (Feign)
* Kafka (async)
```
---

#  7. Kafka + Spring Boot
```
## Q23. How does Spring Boot integrate with Kafka?

**Expect:**

* `@KafkaListener`
* Producer/Consumer config

---

## Q24. How do you handle retries in Kafka consumers?

* Retry topics
* Dead Letter Queue (DLQ)

```
---

#  8. Performance & Optimization
```
## Q25. How do you improve Spring Boot performance?

**Expect:**

* Connection pooling (HikariCP)
* Caching (Redis)
* Async processing
* Reduce reflection / startup time

---

## Q26. How do you debug slow APIs?

**Expect:**

* Logs
* APM tools
* DB query analysis
* Thread dumps
```
---

#  9. Testing
```
## Q27. Difference: `@SpringBootTest` vs `@WebMvcTest`

* Full context vs slice test

---

## Q28. How do you mock dependencies?

* Mockito
* `@MockBean`

---

## Q29. How do you test REST APIs?

* MockMvc
* TestRestTemplate
```
---

#  10. Advanced (Senior Differentiators)
```
## Q30. What are Spring Boot Actuator endpoints?

* Health
* Metrics
* Info

---

## Q31. What is AOP in Spring?

* Cross-cutting concerns
* Logging, transactions

---

## Q32. How does Spring handle concurrency?

* Singleton beans → must be stateless
* Thread safety is developer’s responsibility

---

## Q33. How do you design a fault-tolerant service?

**Expect:**

* Retry
* Circuit breaker (Resilience4j)
* Timeout
* Fallback
```
---


# ⚡ Final Tip

At senior level:

* Don’t give definitions
* Talk in **architecture + trade-offs**
* Always relate to **production experience**

```
