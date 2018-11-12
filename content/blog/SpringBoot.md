---
title: "SpringBoot2.1知识梳理"
date: 2018-11-12T16:03:36+08:00
draft: false
---

### 1. war包启动配置方式
1. 将启动类型改成war启动
`<packaging>war</packaging>`</br>
2. 在`<build>`里面加入`<finalName>springbootstudy</finalName>`,构建项目名称
3. 修改启动类，继承SpringBootServletInitializer 类，重写configure方法：
```
public class ClientApplication extends SpringBootServletInitializer {
    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
        return application.sources(ClientApplication.class);
    }

    public static void main(String[] args) {
        SpringApplication.run(ClientApplication.class, args);
    }
}
```

### 2. 将指定文件/文件夹加入到springboot启动加载资源中
在`application.properties`文件中加入配置,比如将 test文件夹加入到默认加载文件中
`spring.resources.static-locations=classpath:/META-INF/resources/,classpath:/resources/,classpath:/static/,classpath:/public/,classpath:/test/`

### 3. 实体类配置文件
1. 添加 `@Component` 注解
2. 使用@PropertySource 注解指定文件位置
3. 使用@ConfigurationProperties直接，设置相关属性,当使用了 prefix属性之后可以不使用@Value注解，只需要与配置文件中的字段一一对应即可，比如：

```
@Component
@PropertySource({"classpath:application.properties"})
@ConfigurationProperties(prefix = "test")
public class MySetting {}

```

### 4. 使用@ConfigurationProperties时IDEA弹出错误提示
提示内容为：`Spring Boot Configuration Annotation Proessor not found in classpath`

虽然不影响运行，可在`pom.xml`中加入如下依赖：
```
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-configuration-processor</artifactId>
            <optional>true</optional>
        </dependency>
```

### 5. 过滤器

使用`@WebFilter`注解过滤器文件 并实现`javax.servlet.Filter`接口
 ```
@WebFilter(urlPatterns = "/api/*",filterName = "LoginFilter")
public class LoginFilter implements Filter {}
```

其中`urlPatterns`表示需要过滤的地址规则

### 6. 监听器
使用`@WebListener`注解监听器文件，并实现`ServletRequestListener`接口或者`ServletContextListener`接口。</br>
`ServletContextListener`上下文监听器，一般用于资源加载</br>
`ServletRequestListener`请求监听，一般用于统计

### 7. 拦截器
1. 自定义一个拦截器文件，实现`org.springframework.web.servlet.HandlerInterceptor`接口
2. 新增一个配置文件使用`@Configuration`,实现`WebMvcConfigurer`接口
3. 复写`addInterceptors()`方法
比如：

```
@Configuration
public class UserWebMvcConfigurer implements WebMvcConfigurer {
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        //拦截/api2下除了anni下的所有方法,
        registry.addInterceptor(new FirstInteceptor()).addPathPatterns("/api2/*/**").excludePathPatterns("/api2/anni/**");
         registry.addInterceptor(new SecondInteceptor()).addPathPatterns("/api2/*/**");
        WebMvcConfigurer.super.addInterceptors(registry);
    }
}

```

### 7. 文件上传大小限制
新增配置类，添加如下配置

```
@Configuration
public class FileConfig {
    /**
     * 设置文件上传的大小限制
     * @return
     */
    @Bean
    public MultipartConfigElement multipartConfigElement() {
        MultipartConfigFactory factory = new MultipartConfigFactory();
        //2014KB,单个文件最大限制
        DataSize size = DataSize.ofKilobytes(1024);
        factory.setMaxFileSize(size);
        //2MB，总上传的数据大小限制
        factory.setMaxRequestSize(DataSize.ofMegabytes(2));
        return factory.createMultipartConfig();
    }
}
```

## 8. 自定义异常
