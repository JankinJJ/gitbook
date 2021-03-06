# 第1节：builder

## 主要问题
遇到多个构造器参数时要考虑使用**构建器**

举例：在签章系统中 往对象中set值的地方（制章后将对应的值set到Eseal对象中 再存入数据库）此处就可以使用构建器

#### 多参数构造器的劣势
往往有些值不想通过构造器的方式set值 但是因为定义的构造器是多参数的 只能硬着头皮set
另外多参数就涉及到参数的顺序问题 
总之 在此情况下 effective java 的作者推荐使用**构建器**来替代多参数构造器

#### 构建器模式的优点
- 构建器可以根据需要设置必须的属性，而不需要因为参数的不同而新增构造方法
- 同时传入的属性可读性较高 
- 可以实现链式编程 体验更好

#### 构建器的缺点
多了几乎一倍的代码 增加了代码的复杂程度

#### 构建器的本质
###### 构建器的核心原理
**链式编程**
```
public class User {
    private Long id;
    private String name;

    public static Builder builder(){
        return new Builder();
    }

    public User(Long id, String name) {
        this.id = id;
        this.name = name;
    }

    public static class Builder(){
        private Long id;
        private String name;

        public Builder id(Long id){
            this.id = id;
            return this;
        }

        public Builder name(String name){
            this.name = name;
            return this;
        }

        public User build(){
            return new User(this.id,this.name);
        }
    }
}
```
- Builder内部类的属性与外层对象的属性相同
- 客户端调用外层类的builder，获得某个类的Builder实例
- 调用builder实例的每个赋值函数，而赋值函数执行属性赋值后，会返回this作为返回值
- 最后调用无参的build方法 此时builder 对象已经持有所需属性的值 调用外层构造函数构造外层对象

疑问：到最后不是还是调用外层的构造器吗？那有啥区别啊 还多那么多代码 不用不用太傻逼

###### 构建器的本质
是建造者模式的一种形式 即使用方将自己参数传递给建造者 由建造者负责构造所需对象

问题：构造器方法缺点已经说了是因为参数要传太多哦 那解决办法就是使用setter方法 但是
setter方法会造成对象状态的不一致
所以构建器是在某种程度上来说是对setter的一种改造
```
User user = User.builder().name("yu").build()
```

**通过构建器作为中间对象 提高构造外层对象的可读性 同时保持创建外层对象时的状态一致性**

#### 构建器模式升级
