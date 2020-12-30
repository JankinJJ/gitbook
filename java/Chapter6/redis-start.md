# 第1节：redis-start
在项目中学习 所以对于redis的开始是从实战开始 
对于实战中的redis的问题也会在使用中总结

## springboot 整合redis
#### pom引入相关配置
```
<!--redis依赖配置-->
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-data-redis</artifactId>
</dependency>
```
#### 配置文件的相关配置
```
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mall?useUnicode=true&characterEncoding=utf-8&serverTimezone=Asia/Shanghai
    username: root
    password: 12345678
  redis:
    host: localhost #redis服务地址
    database: 0 #redis数据库索引
    port: 6379 # 端口号
    password: #密码
    jedis:
      pool:
        max-active: 8 #连接池最大连接数 负值表示没有限制
        max-wait: -1 #连接池最大的阻塞时间 负值为没有限制
        max-idle: 8 #连接池最大空闲连接数
        min-idle: 0 #连接池最小空闲连接数
    timeout: 3000ms #连接超时时间（毫秒）
```
#### 在RedisTemplate基础上封装接口
###### String
使用``org.springframework.data.redis.core``包下的StringRedisTemplate对String类型进行操作


