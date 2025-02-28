
# RedisConfig 클래스 설명

이 클래스는 Spring Boot 애플리케이션에서 Redis를 설정하기 위한 `RedisConfig` 클래스입니다. Redis는 인메모리 데이터베이스로, 주로 캐시나 세션 관리 등에 사용됩니다. 이 클래스는 Redis와의 연결을 설정하고 데이터를 직렬화하는 방법을 정의합니다.

## 1. 클래스 선언부

```java
@Getter
@Configuration
@RequiredArgsConstructor
@EnableRedisRepositories
public class RedisConfig {
