---
layout: post
title:  Swagger
date:   2021-12-27 21:02:12 +0800
categories: java doc
parent: Java
nav_order: 3
---

# springboot + swagger

###### 版本：

- gradle

- 'org.springframework.boot' version '2.5.8'

- 'io.springfox:springfox-boot-starter:3.0.0'

---------------

###### 步骤：

- gradle 引入 [springfox](https://github.com/springfox/springfox)

```
implementation 'io.springfox:springfox-boot-starter:3.0.0'
```


- 加swagger配置

```
package com.example.demo;

import org.springframework.boot.autoconfigure.condition.ConditionalOnProperty;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import springfox.documentation.builders.ApiInfoBuilder;
import springfox.documentation.builders.PathSelectors;
import springfox.documentation.builders.RequestHandlerSelectors;
import springfox.documentation.service.ApiInfo;
import springfox.documentation.service.Contact;
import springfox.documentation.spi.DocumentationType;
import springfox.documentation.spring.web.plugins.Docket;
import springfox.documentation.swagger2.annotations.EnableSwagger2;

@Configuration
@EnableSwagger2
@ConditionalOnProperty(name = "swagger.enable",  havingValue = "true")
public class SwaggerConfig {
    // controller package path 包路径
    private static final String controllerPath = "com.example.demo.controller";

    @Bean
    public Docket createRestApi() {
        return new Docket(DocumentationType.SWAGGER_2)
                .apiInfo(apiInfo())
                .select()
                .apis(RequestHandlerSelectors.basePackage(controllerPath))
                .paths(PathSelectors.any())
                .build();
    }

    private ApiInfo apiInfo() {
        return new ApiInfoBuilder()
                .title("Spring Boot + Swagger2 => RestFul API")
                .contact(new Contact("Nemo",  "www.baidu.com",  "my@eamil.com"))
                .version("1.0")
                .description("API Desc")
                .build();
    }
}

```

- application.properties 配置

```
#是否激活 swagger true or false
swagger.enable=true
```

- 效果

```
http://localhost:8080/swagger-ui/index.html
```
---------
