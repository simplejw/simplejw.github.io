---
layout: post
title:  SpringBoot
date:   2021-12-27 21:02:12 +0800
categories: java doc
parent: Java
nav_order: 1
---

# 安装 Spring Boot CLI

软件开发工具管理包(Software Development Kit Manager，SDKMAN，曾用简称GVM)也能用来安装和管理多版本Spring Boot CLI。使用前，你需要先从[SDKMAN](https://sdkman.io/install)获取并安装SDKMAN。最简单的安装方式是使用命令行:

```
curl -s "https://get.sdkman.io" | bash

source "$HOME/.sdkman/bin/sdkman-init.sh"
```

一旦安装好了SDKMAN，就可以用下面的方式 来安装Spring Boot CLI了:

```
sdk install springboot

// Spring Boot的当前版本号
spring --version

// 使用SDKMAN的list命令可以找到可用的版本
sdk list springboot

// 指定版本号安装
sdk install springboot 1.3.0.RELEASE

// 切换到另一个版本
sdk use springboot 1.3.0.RELEASE

// 默认版本，可以使用default命令
sdk default springboot 1.3.0.RELEASE
```

-----

# 使用 Spring Initializr 初始化 Spring Boot 项目

用浏览器打开[start.spring.io](http://start.spring.io)

----

# 使用Profile进行配置

1. 如果你正在使用application.properties，可以创建额外的属性文件，遵循application-{profile}. properties这种命名格式，这样就能提供特定于Profile的属性了。

```
spring.profiles.active=production
```

2. 使用多ProfileYAML文件进行配置:如果使用YAML来配置属性，则可以遵循与配置文件相同的命名规范，即创建application-{profile}.yml这样的YAML文件，并将与Profile无关的属性继续放在application.yml里。

```
spring:
  profiles:
    active: production

```

但既然用了YAML，你就可以把所有Profile的配置属性都放在一个application.yml文件里。举例来说，我们可以像下面这样声明日志配置:

```
logging:
  level:
    root: INFO
---
spring:
  profiles: development
logging:
  level:
    root: DEBUG
---
spring:
  profiles: production
logging:
  path: /tmp/
  file: BookWorm.log 
  level:
    root: WARN
```

如你所见，这个application.yml文件分为三个部分，使用一组三个连字符(---)作为分隔符。第二段和第三段分别为spring.profiles指定了一个值，这个值表示该部分配置应该应用在哪 个Profile里。第二段中定义的属性应用于开发环境，因为spring.profiles设置为development。与之类似，最后一段的spring.profile设置为production，在production Profile被激活时生效.另一方面，第一段并未指定spring.profiles，因此这里的属性对全部Profile都生效，或者对那些未设置该属性的激活Profile生效。

# 自定义 application.properties 里的变量

- 配置类文件

```
// PropertiesConfig.java

@Component
@Data
@ConfigurationProperties(prefix = "my.properties")
public class PropertiesConfig {
    private String apiJWTKey;
}
```

- 自定义变量

```
// application.properties

my.properties.apiJWTKey=zOaXPmyWVTcQL3Y
```

- 使用变量

```
@Resource
private PropertiesConfig propertiesConfig;

propertiesConfig.getApiJWTKey();
```

# 配置自定义异常

- 获取全局异常格式化出参 SpringExceptionHandler.java BusinessException.java

```
@RestControllerAdvice
@Slf4j
public class SpringExceptionHandler {

    @ExceptionHandler(value = {AppException.class})
    @ResponseStatus(HttpStatus.OK)
    @ResponseBody
    public BusinessException handleHttpException(HttpServletRequest req, AppException ex) {

        BusinessException businessException = new BusinessException();
        businessException.setCode(ex.getCode());
        businessException.setMsg(ex.getMsg());
        businessException.setInfo(ex.getInfo());

        log.info("URL:{}  businessException:{}", req.getRequestURI(), businessException);

        return businessException;
    }

}
```

```
@Data
@NoArgsConstructor
@AllArgsConstructor
public class BusinessException {

    private String code;

    private String msg;

    private Object info;

}
```


- 自定义异常类 AppException.java

```
@Data
@EqualsAndHashCode(callSuper=false)
public class AppException extends RuntimeException {
    private String code;

    private String msg;

    private Object info;


    public AppException(String code, String msg, Object info) {
        this.code = code;
        this.msg  = msg;
        this.info = info;
    }

    public AppException(ErrorCodeDefine errorCodeDefine) {
        this.code = errorCodeDefine.getExternalCode();
        this.msg  = errorCodeDefine.getExternalMsg();
        this.info = errorCodeDefine.getExternalInfo();
    }
}
```

- 自定义错误码 ErrorCodeDefine.java LoginException.java

```
public interface ErrorCodeDefine {
    String getExternalCode();

    String getExternalMsg();

    Class<?> getExternalInfo();
}
```

```
public enum LoginException implements ErrorCodeDefine {
    WECHAT_CODE_SESSION("60001", "codeTwoSession error", null);

    @Getter
    private String externalCode;

    @Getter
    private String externalMsg;

    @Getter
    private Class<?> externalInfo;

    LoginException(String externalCode, String externalMsg, Class<?> externalInfo) {
        this.externalCode = externalCode;
        this.externalMsg = externalMsg;
        this.externalInfo = externalInfo;
    }

}
```

- 使用自定义枚举的异常

```
throw new AppException(LoginException.WECHAT_CODE_SESSION);
```

