# RedisConfig 클래스 설명

## 1. 클래스 선언부

```java
@Getter
@Configuration
@RequiredArgsConstructor
@EnableRedisRepositories
public class RedisConfig {

@Configuration: 이 클래스는 Spring의 설정 클래스임을 나타냅니다. Spring IoC 컨테이너에 의해 관리될 설정을 정의합니다.
@Getter: Lombok 어노테이션으로, 클래스의 모든 필드에 대해 자동으로 getter 메서드를 생성합니다.
@RequiredArgsConstructor: Lombok 어노테이션으로, final 또는 @NonNull로 선언된 필드에 대해 생성자를 자동으로 생성합니다.
@EnableRedisRepositories: Redis를 사용하여 Spring Data의 리포지토리 기능을 활성화합니다. Redis를 데이터 저장소로 사용할 수 있도록 설정합니다.

## 2. 필드변수

```java
@Value("${spring.data.redis.host}")
private String host;

@Value("${spring.data.redis.port}")
private int port;
