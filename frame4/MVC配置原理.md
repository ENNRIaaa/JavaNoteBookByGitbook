# 5.11 MVC配置原理

Spring Boot为Spring MVC提供了自动配置，可与大多数应用程序完美配合。

自动配置在Spring的默认值之上添加了以下功能：

- 包含`ContentNegotiatingViewResolver`和`BeanNameViewResolver`。
- 支持提供静态资源，包括对WebJars的支持。
- 自动注册`Converter`，`GenericConverter`和`Formatter`豆类。
- 支持`HttpMessageConverters`。
- 自动注册`MessageCodesResolver`。
- 静态`index.html`支持。
- 定制`Favicon`支持。
- 自动使用`ConfigurableWebBindingInitializer`bean。

如果您想保留Spring Boot MVC功能并想添加其他MVC配置（拦截器，格式化程序，视图控制器和其他功能），则可以添加自己`@Configuration`的type类， `WebMvcConfigurer`但**不添加** `@EnableWebMvc`。如果您希望提供，或的 自定义实例`RequestMappingHandlerMapping`，则可以声明一个 实例来提供此类组件。`RequestMappingHandlerAdapter` `ExceptionHandlerExceptionResolver` `WebMvcRegistrationsAdapter`

如果您想完全控制Spring MVC，可以使用添加自己的`@Configuration` 注释`@EnableWebMvc`。



#### 了解：扩展视图解析器

官方文档说了：如果您想保留Spring Boot MVC功能并想添加其他MVC配置（拦截器，格式化程序，视图控制器和其他功能），则可以添加自己`@Configuration`的type类。

```java
//定义一个Spring配置类，实现WebMvcConfigurer接口，来扩展MVC配置
@Configuration
public class MyMvcConfig implements WebMvcConfigurer {

    //2.将自定义的视图解析器MyViewResolver注册到Spring
    @Bean
    public ViewResolver myViewResolver(){
        return new MyViewResolver();
    }

    //1.自定义一个视图解析器（这里定义了一个静态内部类）
    public static class MyViewResolver implements ViewResolver{
        @Override
        public View resolveViewName(String viewName, Locale locale) throws Exception {
            return null;
        }
    }
}
```

自定义的视图解析器定义完之后，来测试一下：

所有的request和response都要经过DispatcherServlet，在doDispatch()方法这里打一个断点：

![image-20200705150116474](https://images.shiguangping.com/imgs/20200705150116.png)

当请求过来之后，可以看到，当前DispatcherServlet对象的viewResolvers属性（List），包含了我们刚刚定义的视图解析器，说明自定义的视图解析器已经被SpringBoot自动配置了。

