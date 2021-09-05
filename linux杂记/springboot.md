#### 1.Spring Boot HelloWorld
实现一个功能：
    流浪器发送呢Hello请求，服务器接受并处理，
### 1.创建一个Maven工程
### 2.导入spring boot相关依赖

```xml
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.2.6.RELEASE</version>
    </parent>
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>
```

### 3.编写一个主程序：启动sprnig boot的应用
```java
/**
 * @SpringBootApplication 标注一个主程序，说明这是一个springboot应用
 */
@SpringBootApplication
public class HelloWorldApplication {
    public static void main(String[] args) {
        SpringApplication.run(HelloWorldApplication.class, args);
    }
}
```
### 2.编写相关的Contruller,Service


#### Hello world探究
- POM文件
    - 父项目
        ```xml
            <parent>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-parent</artifactId>
                <version>2.2.6.RELEASE</version>
            </parent>
            
            他的父项目是
          <parent>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>2.2.6.RELEASE</version>
            <relativePath>../../spring-boot-dependencies</relativePath>
          </parent>
          它来真正管理Spring Boot应用里面的所有版本依赖
        ```
        Spring Boot的版本仲裁中心;
        导入依赖默认不需要版本(除了dependencies里面没有声明管理的版本号)
    - 导入的依赖
        ```xml
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter-web</artifactId>
            </dependency>
        ```
        *spring-boot-starter*-**web** 
            spring-boot-starter:spring-boot场景启动器;帮我们导入了web模块正常运行的依赖模块

        Spring Boot将所有的功能场景抽取出来,做成一个starter(启动器)
                    
- 主程序类,入口类
    ```java
    /**
     * @SpringBootApplication 标注一个主程序，说明这是一个springboot应用
     */
    @SpringBootApplication
    public class HelloWorldApplication {
        public static void main(String[] args) {
            SpringApplication.run(HelloWorldApplication.class, args);
        }
    }
    ```
    ```java
    @Target({ElementType.TYPE})
    @Retention(RetentionPolicy.RUNTIME)
    @Documented
    @Inherited
    @SpringBootConfiguration
    @EnableAutoConfiguration
    @ComponentScan(
        excludeFilters = {@Filter(
        type = FilterType.CUSTOM,
        classes = {TypeExcludeFilter.class}
    ), @Filter(
        type = FilterType.CUSTOM,
        classes = {AutoConfigurationExcludeFilter.class}
    )}
    )
    ```
    @SpringBootConfiguration:Spring Boot的配置类;
        标注在某个类上,标识这是一个SpringBoot的配置类;
        @Configuration:配置类上标注这是一个注解
        配置类也会容器中的一个组件
    @EnableAutoConfiguration: 开启自动配置

    @AutoConfigurationPackage:自动配置包
    将主配置类(@SpringBootApplicaton标注的类)的所在包及下面所有子包里面的所有
    组件扫描到spring容器;

3.Spring Initializer创建Spring Boot项目
- 已生成主程序
- resources文件夹中目录结构
    - static:保存所有静态资源:js css images
    - templates:保存所有的模板页面(Spring Boot默认jar包使用嵌入式的Tomcat
        默认不支持jsp页面);可以使用模板引擎
    - application.properties:Spring Boot应用的配置文件
