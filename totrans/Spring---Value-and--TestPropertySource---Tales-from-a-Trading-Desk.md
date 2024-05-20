<!--yml
category: 未分类
date: 2024-05-18 05:34:28
-->

# Spring: @Value and @TestPropertySource | Tales from a Trading Desk

> 来源：[https://mdavey.wordpress.com/2016/04/12/spring-value-and-testpropertysource/#0001-01-01](https://mdavey.wordpress.com/2016/04/12/spring-value-and-testpropertysource/#0001-01-01)

## Spring: @Value and @TestPropertySource

Recently I had a few issues getting this working in a Spring boot application.  Here’s a simple sample.  Make sure the SomeTestProperties.properties is in the resources folder under test 🙂

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

~ by mdavey on April 12, 2016.

Posted in [Java](https://mdavey.wordpress.com/category/languages/java/)