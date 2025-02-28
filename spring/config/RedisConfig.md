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

2. 필드 변수

```java
@Value("${spring.data.redis.host}")
private String host;
@Value("${spring.data.redis.port}")
private int port;
설명:
@Value("${spring.data.redis.host}"): application.properties 또는 application.yml 파일에 설정된 Redis의 호스트를 가져와 host 변수에 주입합니다.
@Value("${spring.data.redis.port}"): application.properties 또는 application.yml 파일에 설정된 Redis의 포트를 가져와 port 변수에 주입합니다.


3. RedisConnectionFactory Bean 설정
@Bean
public RedisConnectionFactory redisConnectionFactory(){
    return new LettuceConnectionFactory(host, port);
}
설명:
@Bean: 이 메서드는 Spring IoC 컨테이너에 의해 관리되는 빈을 생성한다는 것을 의미합니다. 메서드가 반환하는 객체는 Spring의 ApplicationContext에 의해 관리됩니다.
LettuceConnectionFactory: Redis와 연결하기 위해 Lettuce 클라이언트를 사용한 연결 팩토리를 생성합니다. Redis에 연결하기 위해 호스트와 포트를 지정합니다.
Lettuce는 Redis와의 연결을 관리하는 클라이언트 라이브러리입니다. Jedis와 함께 Redis 클라이언트로 자주 사용됩니다.
이 메서드는 Redis 서버에 대한 연결을 설정하는 역할을 합니다. redisConnectionFactory 메서드를 통해 Redis와의 연결을 관리할 수 있는 객체를 Spring 컨테이너에 등록합니다.


4. RedisTemplate Bean 설정
@Bean
public RedisTemplate<String, String> redisTemplate(){
    RedisTemplate<String, String> redisTemplate = new RedisTemplate<>();
    redisTemplate.setConnectionFactory(redisConnectionFactory());
    redisTemplate.setKeySerializer(new StringRedisSerializer());
    redisTemplate.setValueSerializer(new StringRedisSerializer());
    return redisTemplate;
}
설명:
RedisTemplate<String, String>: Redis에 데이터를 저장하거나 조회할 때 사용할 RedisTemplate 객체를 생성합니다. String 타입의 데이터를 저장하고 읽어오는 용도로 설정되어 있습니다.
RedisTemplate은 Spring Data Redis에서 제공하는 핵심 클래스입니다. Redis와의 데이터 입출력을 처리합니다.
redisTemplate.setConnectionFactory(redisConnectionFactory()): 이전에 설정한 RedisConnectionFactory 객체를 RedisTemplate에 설정하여, Redis와의 연결을 처리할 수 있도록 합니다.
redisTemplate.setKeySerializer(new StringRedisSerializer()): Redis에서 저장된 키가 바이트 배열로 처리되므로, 이를 문자열로 직렬화/역직렬화하기 위한 설정입니다.
StringRedisSerializer는 Redis의 키와 값을 문자열로 직렬화/역직렬화하는 데 사용됩니다.
redisTemplate.setValueSerializer(new StringRedisSerializer()): Redis에 저장될 값 역시 문자열이므로, 값에 대한 직렬화/역직렬화를 StringRedisSerializer로 처리합니다.
yaml

