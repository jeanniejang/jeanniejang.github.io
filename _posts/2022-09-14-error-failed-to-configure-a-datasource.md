---
title: "Failed to configure a DataSource: 'url' attribute is not specified and no embedded datasource could be configured."
categories: Error
tag: [Java, Spring, errors]
toc: true
---

🆘 How I solved the errors that I encountered
{: .notice--danger}

## Error message

![error message](https://i.imgur.com/6XPP3b1.png)

## Solution
This was easily solved by adding the following ```(exclude = DataSourceAutoConfiguration.class)``` next to ```@SpringBootApplication```. 

### Full code
```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.boot.autoconfigure.jdbc.DataSourceAutoConfiguration;

@SpringBootApplication (exclude = DataSourceAutoConfiguration.class)
public class YourApplication {

    public static void main(String[] args) {
        SpringApplication.run(YourApplication.class, args);
    }
}
```