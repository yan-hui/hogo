---
title: "SpringBoot知识梳理"
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
