---
layout:     post
title:      Git指令整理2
subtitle:   Spring Framework
date:       2018-02-15
author:     Jr
header-img: img/post-bg-ios9-web.jpg
catalog: true
tags:
    - Spring
    - SpringBoot
    - Kafka
	- SpringCloud
	- Eurka
---

>随便整理的一些自用的Git指令


# Spring Boot

## Spring Boot三大特性

* 组件自动装配：Web MVC，Web Flux,JDBC等
* 嵌入式Web容器：Tomcat，Jetty，Undertow
* 生产准备特性：指标，健康检查，外部化配置等


### 组件自动装配
* 激活：@EnableAutoConfiguration
* 配置：/META-INF/spring.factories
* 实现：XXXAutoConfiguartion

###嵌入式Web容器
* Web Servlet:Tomcat,Jetty,Undertow
* Web Reactive:Netty Web Server

###生产准备特性
* 指标：/actuator/metrics
* 健康检查：/actuator/health
* 外部化配置：/actuator/configprops

##传统的Servlet应用
* Servlet组件：Servlet，Filter，Listener
* Servlet注册：Servlet注解，Spring Bean，RegistrationBean
* 异步非阻塞：异步Servlet，非阻塞Servlet

###依赖

```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-web</artifactId>			
</dependency>
		
```
###Servlet组件
* 实现
extends HttpServlet
* URL映射
@WebServlet(urlPatterns = "")
* 注册
@ServletComponentScan(basePackages = "")

### 异步非阻塞Servlet ###
```
@WebServlet(urlPatterns = "/my/servlet", asyncSupported = true)
javax.servlet.AsyncContext asyncContext = req.startAsync();

```
##Spring Web MVC应用
* Web MVC视图：模版引擎，内容协商，异常处理等
* Web MVC REST：资源服务，资源跨域，服务发现等
* Web MVC核心：核心架构，处理流程，核心组件

###Web MVC 视图
* ViewResolver
* View

###模板引擎
* Thymeleaf
* FreeMaker
* JSP

###内容协商
* ContentNegotiationConfigurer
* ContentNegotiationStrategy

###异常处理
* @ExceptionHandler

###Web MVC REST
####资源服务
* @RequestMapping
* GetMapping
* DeleteMapping
* PostMapping
* @ResponseBody 
* @RequestBody

### 核心组件 ###
- DispatcherServlet
- HandlerMapping
- HanderAdapter
- ViewResolver

## Spring Web Flux应用 ##
- Reactor基础：Java Lambda，Mono，Flux
- Web Flux核心：Web MVC注解，函数式声明，异步非阻塞
- 使用场景：Web Flux优势与限制

#### 函数式声明 ####

- RouterFunction

异步非阻塞
- Servlet 3.1+
- Nettty Reactor

#### 性能测试 ####
[https://blog.ippon.tech/spring-5-webflux-performance-tests/](https://blog.ippon.tech/spring-5-webflux-performance-tests/)

## Web Server应用 ##
- 切换Web Server
- 自定义Servlet Web Server
- 自定义Reactive Web Server

### 切换其他Servlet容器 ###
- Tomcat to Jetty
```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-web</artifactId>
	<exclusions>
		<exclusion>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-tomcat</artifactId>
		</exclusion>
	</exclusions>
</dependency>
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-jetty</artifactId>
</dependency>
```

- Web Flux
```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-webflux</artifactId>
	<version>unknown</version>
</dependency>
```

### 数据相关 ###

#### 关系型数据库 ####
- JDBC:数据源，JdbcTemplate，自动装配
- JPA：实体映射关系，实体操作，自动装配
- 事务：Spring事务抽象，JDBC事务处理，自动装配

#### JDBC ####
```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
```
#### 数据源 ####
- ``` javax.sql.DataSource ```
```
JdbcTemplate
```

#### 自动装配 ####

#### JPA ####
```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

#### 实体映射关系 ####
- @javax.persistence.OneToOne
- @javax.persistence.OneToMany
- @javax.persistence.ManyToOne
- @javax.persistence.ManyToMany

#### 实体操作 ####
- javax.persistence.EntityManager

#### 自动装配 ####
- HibernateJpaAutoConfiguration

### Spring事务 ###
```
<dependency>
	<groupId>org.springframework</groupId>
	<artifactId>spring-tx</artifactId>
</dependency>
```

### Spring Boot Actuator ###
```
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```


- JMX Endpoints
- 健康检查(Health Checks)