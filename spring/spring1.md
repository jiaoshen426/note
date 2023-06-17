

## BeanDefinition



BeanDefinition表示Bean定义，BeanDefinition中存在很多属性用来描述一个Bean的特点。比如：

- class，表示Bean类型

- scope，表示Bean作用域，单例或原型等

- lazyInit：表示Bean是否是懒加载

- initMethodName：表示Bean初始化时要执行的方法

- destroyMethodName：表示Bean销毁时要执行的方法

- 还有很多...

在Spring中，我们经常会通过以下几种方式来定义Bean：
1. <bean/>
2. @Bean
3. @Component(@Service,@Controller)
这些，我们可以称之申明式定义Bean。

我们还可以编程式定义Bean，那就是直接通过BeanDefinition，比如：



```java
AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);

// 生成一个BeanDefinition对象，并设置beanClass为User.class，并注册到ApplicationContext中
AbstractBeanDefinition beanDefinition = BeanDefinitionBuilder.genericBeanDefinition().getBeanDefinition();
beanDefinition.setBeanClass(User.class);
context.registerBeanDefinition("user", beanDefinition);
System.out.println(context.getBean("user"));
```
我们还可以通过BeanDefinition设置一个Bean的其他属性
```java
beanDefinition.setScope("prototype"); // 设置作用域
beanDefinition.setInitMethodName("init"); // 设置初始化方法
beanDefinition.setLazyInit(true); // 设置懒加载
```

和申明式事务、编程式事务类似，通过<bean/>，@Bean，@Component等申明式方式所定义的Bean，最终都会被Spring解析为对应的BeanDefinition对象，并放入Spring容器中。

  

