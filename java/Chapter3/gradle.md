# 第1节：gradle

## 编译ribbon项目

#### 项目基本信息
- ribbon版本：2.7.18
- gradle插件：
    - nebula.netflixoss  version:8.8.1
    - nebula.test-jar  version:17.3.2
    - nebula.facet  version: 7.0.9
- gradle版本: 6.6-bin

#### 遇到的问题 
###### gradle的版本过低导致ide无法编译项目
ide不管是idea还是eclipse都是需要2.6以及其往上的版本
所以放弃使用官方配置文件中的2.2.1的gradle版本
但是升级为2.6还是有问题 通过下面的解决方式解决

###### gradle相关插件版本过低 且没有做引入 导致找不到插件
升级gradle版本后依旧有错，将nebula.netflixoss 的版本改为最新的 就不会有问题了
但是在编译其他模块的时候，报有些插件找不到 
去gradle的插件官网搜索并下载 在项目总的build.gradle引入
坑：build.gradle中插件也许是因为太老了，所以插件的名字都跟现在找到的不一致
所以根据官网搜索到的插件进行rename，继续。
报什么插件没有，那就在总的build.gradle中添加

###### gradle版本问题导致配置缓存找不到
因为在插件都配好之后，会报一个provider找不到。
百度了之后发现，这是一个配置缓存的机制，又注意到是gradle6.6才开始提供这个实验性的功能。
所以又把gradle的版本从6.3换为6.6解决了问题

期间还有，gradle在ribbon项目中版本不能太高，如果换成最高版本的，会报部分语法已被废弃，还是编译不通过


