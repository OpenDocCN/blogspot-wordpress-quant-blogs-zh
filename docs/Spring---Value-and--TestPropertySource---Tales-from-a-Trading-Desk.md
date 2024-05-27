<!--yml

分类：未分类

日期：2024-05-18 05:34:28

-->

# Spring: @Value 和 @TestPropertySource | 交易桌边的传说

> 来源：[`mdavey.wordpress.com/2016/04/12/spring-value-and-testpropertysource/#0001-01-01`](https://mdavey.wordpress.com/2016/04/12/spring-value-and-testpropertysource/#0001-01-01)

## Spring: @Value 和 @TestPropertySource

最近我在一个 Spring Boot 应用程序中遇到几个问题。这是一个简单的示例。确保 SomeTestProperties.properties 文件在 test 文件夹下的 resources 文件夹中。

```
@RunWith(SpringJUnit4ClassRunner.class)
@SpringApplicationConfiguration(SomeTest.class)
@TestPropertySource("classpath:SomeTestProperties.properties")
//@TestPropertySource(properties = {"Text=abc"})
@Configuration
public class PropertyLoadTest {
    @Autowired
    private Environment environment;

    @Value("${Text}")
    private String text;

    static class Config {
        @Value(&amp;amp;quot;${Text}&amp;amp;quot;)
        private String text;

        public String getText() {
            return text;
        }
        @Bean
        public static PropertySourcesPlaceholderConfigurer propertyPlaceholderConfigurer() {
            return new PropertySourcesPlaceholderConfigurer();
        }
    }

    @Test
    public void propertyLoadTest() {
        System.out.println(&amp;amp;quot;Text= &amp;amp;quot; + this.environment.getProperty(&amp;amp;quot;Text&amp;amp;quot;));
        System.out.println(&amp;amp;quot;Text= &amp;amp;quot; + text);
    }
}

```

~ mdavey 于 2016 年 4 月 12 日。

发布于[Java](https://mdavey.wordpress.com/category/languages/java/)
