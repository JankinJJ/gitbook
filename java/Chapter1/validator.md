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

#### 需要注意的几个注解的区分
###### @NotNull @NotEmpty @NotBlank
- @NotNull 作用于任何类型的数据 即 验证元素值不是null
- @NotEmpty 作用于字符串、集合、Map、数组 即 验证注解的元素值不为null且不为空（字符串长度不为0，集合大小不为0）
- @NotBlank 作用于字符串 即 验证注解的元素值并不为空（不为null 并且**去除首位空格**后长度为0）


