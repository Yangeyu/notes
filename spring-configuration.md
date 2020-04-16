#### 配置文件
- SpringBoot使用一个全局配置文件,配置文件名是固定的
    - application.properties
    - application.yml
    
    配置文件的作用: 修改SpringBoot默认配置的值
    yaml -- 以数据为中心
    ```yml
    server:
      port: 8081
    k: v -- 需要有一个空格,左对齐的属于统一层级
    ```

- YAML的语法
    - 字面量
        - "": 双引号 "kd \n ds" --> kd 换行 ds
        - '': 单引号 "kd \n ds" --> kd \n ds
        - 对象
            ```yml
            friends:
                name: name
                age: 20
            ----------------
            friends: {name: name,age: 20}
            ```
        - 数组(List, Set)
            ```yml
            pets:
                - cat
                - dog
                - pig
            ----------------
            pets: [cat,dog,pig]
            ```
    - 样例
    配置文件
    ```yml
    person:
      name: zhangsan
      age: 12
      boss: false
      birth: 2012/23/32
      maps: {k1: vd,k2: vf}
      lists:
        - ll
        - ds
        - df
      dog:
        name: 小狗
        age: 2
    ```
    javabean
    ```java
/**
 * 将配置文件中属性的值映射到组件中
 * @ConfigurationProperties: 告诉SpringBoot将本类中的所有属性和配置文件中的值进行映射
 * 只有这个是容器中的组件才能使用@ConfigurationProperties功能
 */
@Component
@ConfigurationProperties(prefix = "person")
public class Person {
    private String name;
    private Integer age;
    private Boolean boss;
    private Date birth;

    private Map<String, Object> maps;
    private List<Object> lists;
    private Dog dog;
    ```

    导入配置文件处理器,以后编写配置文件就有提示
    ```xml
<!--        导入配置文件处理器,配置文件进行绑定就会有提示-->
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-configuration-processor</artifactId>
            <optional>true</optional>
        </dependency>
    ```

- @Value赋值和@ConfigurationProperties赋值比较
  
       |              | @ConfigurationProperties | @Value   |
       |--------------|--------------------------|----------|
       | 功能         | 批量注入                 | 单个变量 |
       | 松散语法绑定 | 支持                     | 不支持   |
       | SpEL(表达式) | 不支持                   | 支持     |
       | 数据校验     | 支持                     | 不支持   |
       | 复杂类型封装 | 支持                     | 不支持   |
       
    配置文件yml还是properties都可以获取值
    如果只是为了获取配置文件中的某一项值就使用@Value;
    
    ```java
 @Value("TOM")
    private String name;
    @ResponseBody
    @RequestMapping("/hello")
    public String hello(){
        return "hello " + name;
    }
}
    ```

    
    如果是要将JavaBean与配置文件进行映射就使用@ConfigurationProperties
- 配置文件注入值校验
    ```java
@Component
@ConfigurationProperties(prefix = "person")
@Validated
public class Person {
//    @Value("${person.name}")
    @Email
    private String name;
    ```

- @PropertySource&@ImportResource&@Bean
    - PropertySource:加载指定的配置文件
    ```java
/**
 * 将配置文件中属性的值映射到组件中
 * @ConfigurationProperties: 告诉SpringBoot将本类中的所有属性和配置文件中的值进行映射
 * 只有这个是容器中的组件才能使用@ConfigurationProperties功能
 * @ConfigurationProperties(prefix = "person")默认从全局配置文件中获取值
 * @PropertySource(value = {"classpath:person.properties"})指明配置文件的路径
 * 支持properties类型的配置文件,yml测试失败
 */
@PropertySource(value = {"classpath:person.properties"})
@Component
@ConfigurationProperties(prefix = "person")
//@Validated

public class Person {
    ```

    - @ImportResource: 导入Spring的配置文件,让配置文件(传统的xml)里面的内容生效
- SpringBoot推荐用配置类来加载组件
```java
/**
 * @Configuration: 指明当前类是一个配置类,来代替Spring的配置文*.xml
 * 在配置文件中用<bean></bean>标签添加组件,这里用@Bean
 */
@Configuration
public class MyConfig {
    //将方法的返回值添加到容器中;容器中这个组件默认id就是方法名
    @Bean
    public HelloService helloService(){
        System.out.println("配置类@Bean给容器中添加组件了");
        return new HelloService();
    }
}
//1.编写HelloService组件(类)
//2.在配置类中给容器加上该组件
//-----------------------------
    @Autowired
    ApplicationContext ioc;
    @Autowired
    HelloService helloService;
    @Test
    void testHelloService(){
//        boolean b = ioc.containsBean("helloService");
//        System.out.println(b);

        if(helloService!=null){
            System.out.println("ok");
        }
    }
```


