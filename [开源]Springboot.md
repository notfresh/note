# 1 Spring学习





# 适合阅读



## 从0搭建一个脚手架项目

- 为什么脚手架项目一般都是后台管理系统？
- 为什么这样的脚手架项目会受到大家的追捧

因为每个项目都需要一个后台来管理所有资源，必不可少，其中权限模块，文件模块，监控模块、基础数据模块等是几乎是一个完善的后台管理系统的必备功能。而业务是不一定的，每个公司需要开发的业务都不一样，所以无法做到统一，这需要公司定制。

但虽然业务不一样，但是还有些技术上的实现是共同的，比如文件上传、token机制、预防攻击、防注入、动态数据源等等，这些很多业务技术支持上都需要用到，于是，脚手架系统就诞生了。

至于一个脚手架项目为什么会受欢迎，可以总结一下几点：

- 可插拔式功能拓展，需要与不需要的功能通过一键注解或配置文件控制
- 基础功能封装完善，可尽量少些代码
- 安全、性能方面有考虑
- 主流的框架组合、大量的文档可以搜索
- 完善的项目文档，让开发者快速入手
- 代码生成，提高基本功能的开发效率
- 等等

所以，通常我们从0开始设计一个项目，一般也不会真正从0开始写代码，而是先选择脚手架，然后在基础上添加业务代码，这样可以大大提高项目的开发效率，从而减少成本。



# 推荐阅读

第一篇入门资料

http://www.ityouknow.com/springboot/2016/01/06/spring-boot-quick-start.html

详细的入门资料 感觉不错

https://github.com/dyc87112/SpringBoot-Learning/tree/master/2.1.x 有时候挺卡的

https://gitee.com/didispace/SpringBoot-Learning/tree/master/2.1.x 备用



RESTFUL 基础教程与测试

http://blog.didispace.com/spring-boot-learning-21-2-1/

Mybatis的初体验

http://blog.didispace.com/spring-boot-learning-21-3-5/



实战：用springboot做一个个人博客玩玩，感觉很有意思，阅读别人的代码开始

https://blog.csdn.net/u013967175/category_9273727.html



纯洁的微笑 springboot 系列文章 比较粗糙，不推荐优先看

http://www.ityouknow.com/spring-boot.html



springboot demos

https://github.com/ityouknow/spring-boot-examples

第二学习链接 面试常见问题
https://github.com/Snailclimb/JavaGuide#springspringboot





# lombok

注意：相比[1.x版本教程](http://blog.didispace.com/springbootrestfulapi/)中自定义set和get函数的方式，这里使用`@Data`注解可以实现在编译器自动添加set和get函数的效果。该注解是lombok提供的，只需要在pom中引入加入下面的依赖就可以支持：

初次介绍 http://blog.didispace.com/spring-boot-learning-21-2-1/ 

详细介绍 http://blog.didispace.com/java-lombok-how-to-use/

```
@Data
public class User {

    private Long id;
    private String name;
    private Integer age;

}
```





# 参考

如何从0搭建一个spring开源项目

https://zhuanlan.zhihu.com/p/137549713

springboot学习资源大集合

https://github.com/ityouknow/awesome-spring-boot

github springboot 搜索结果

[https://github.com/search?q=springboot+%E6%95%99%E7%A8%8B+stars%3A%3E1000](https://github.com/search?q=springboot+教程+stars%3A>1000)

lombok的介绍

http://blog.didispace.com/java-lombok-how-to-use/

jdbc template的使用

http://blog.didispace.com/spring-boot-learning-21-3-1/



# 问题

1 2020-07-21 不会spring可以直接学springboot吗？

