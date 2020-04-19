#### SL4j使用
1. 如何在系统中使用SL4j

[SL4j的使用](http://www.slf4j.org/manual.html) 

以后在开发中,日志记录方法的调用,不应该来直接调用日志的实现类,而是调用日志抽象层里面的方法:
给系统中导入算了se4j的jar
```java
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class HelloWorld {
  public static void main(String[] args) {
    Logger logger = LoggerFactory.getLogger(HelloWorld.class);
    logger.info("Hello World");
  }
}
```

2. 配置文件中的配置

```properties

#指定日志级别
logging.level.cn.demo=info
#制定日志文件路径
logging.file.path=/home/yang/Document/Demo
#指定输出格式
logging.pattern.console=
logging.pattern.file=
```

```xml
<appender name="stdout" class="ch.qos.logback.core.ConsoleAppender">
        <!--
        日志输出格式：
			%d表示日期时间，
			%thread表示线程名，
			%-5level：级别从左显示5个字符宽度
			%logger{50} 表示logger名字最长50个字符，否则按照句点分割。 
			%msg：日志消息，
			%n是换行符
        -->
        <layout class="ch.qos.logback.classic.PatternLayout">
            <springProfile name="dev">
                <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} ----> [%thread] ---> %-5level %logger{50} - %msg%n</pattern>
            </springProfile>
            <springProfile name="!dev">
                <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} ==== [%thread] ==== %-5level %logger{50} - %msg%n</pattern>
            </springProfile>
        </layout>
    </appender>
```

<++>
