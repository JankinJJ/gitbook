# 第4节：validator

## 什么是javax.validation
-  是java bean参数校验的标准 定义了很多常用的校验注解
    - 所以多数用于java bean的属性上面
- 已经包含在Springboot的starter-web中了

## 实战
#### 在哪里开始校验
在controller层 在需要校验的bean处加上`@Validated`注解
```
public void useValidatedBean(@RequestBody @Validated User user){}
```

