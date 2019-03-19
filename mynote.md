# 1. 概述
# 2. spring-cloud-eureka
## 单节点注册中心
启动后根据配置的端口访问，如：
http://localhost:8000/

## 双节点和集群
配置中defaultZone指向另外一台或多台机器即可

```java
@EnableEurekaServer 主类注解：表明注册中心
```

---

# 3. eureka-producer-consumer
## 服务启用
```java
@EnableDiscoveryClient  主类注解：表明服务提供者
```
启用了服务启动着注解的服务后，可以在`eureka`页面中看到该服务
## 服务调用方
启动类添加`@EnableDiscoveryClient`和`@EnableFeignClients`注解
```java
@EnableDiscoveryClient  启用服务注册与发现
@EnableFeignClients     启用feign进行远程调用
```
## 负载均衡（服务间调用时会负载均衡，每个服务做到负载均衡需要Zuul即gateway）
调用方以配置的 `spring.application.name` 为准：
`@FeignClient(name= "spring-cloud-producer")`
不管端口，启动多个即可。

# 4. 熔断 hystrix
`Feign`中依赖了`Hystrix`，只需在配置中开启，注解找中加回调即可。

# 5. 熔断监控（待验证）

# 6-9. 配置中心（待验证）

# 10. zuul 网关 初级
启动类添加
```java
@EnableZuulProxy  支持网关路由
```
加了gateway后可以走新的路由，原来的路由也可以。

# 11. zuul 网关 高级
