# Autoconfiguration


Q1. What is the difference between regular configuration and autoconfiguration ?

-> **Regular Configuration:**

In regular configuration, developers manually configure various components, dependencies, and settings of the software system.
This involves explicitly defining configuration files, properties, annotations, or code to wire together different parts of the application and set up dependencies.
Developers have full control over the configuration process, allowing them to customize and fine-tune the application according to specific requirements.
Regular configuration can be more flexible and provide better visibility into the inner workings of the application, making it easier to debug and troubleshoot issues.

**Autoconfiguration:**

Autoconfiguration, on the other hand, relies on automated processes to configure the software system based on predefined conventions, best practices, or defaults.
Frameworks like Spring Boot provide autoconfiguration features that automatically configure various components and dependencies based on the dependencies present in the project's classpath.
Autoconfiguration simplifies the setup process by reducing the amount of manual configuration required from developers.
It often involves scanning the classpath for specific libraries or components and automatically configuring them based on predefined rules or algorithms.
While autoconfiguration can speed up the development process and reduce boilerplate code, it may lead to less visibility and control over the configuration, making it harder to understand and troubleshoot complex setups.


Q2. Would all conditional annotations on bean definitions work in regular configuration classes ? Elaborate.

-> When it comes to regular configuration classes, such as those used in traditional Spring applications where beans are configured manually, the usage of conditional annotations is not as common. However, in theory, you can use conditional annotations in regular configuration classes as well.

Here's how conditional annotations would work in regular configuration classes:

Manual Configuration: In regular configuration classes, developers manually define bean definitions using Java configuration (using @Configuration classes) or XML configuration files.
Conditional Annotations: You can use conditional annotations like @Conditional, @ConditionalOnProperty, @ConditionalOnClass, etc., to conditionally include or exclude certain beans based on specific conditions.
Condition Evaluation: When the Spring application context is being initialized, Spring evaluates the conditions specified in the conditional annotations. If the conditions are met, the corresponding bean definitions are included in the application context; otherwise, they are excluded.

In summary, while conditional annotations can be used in regular configuration classes, their usage in such contexts is less common and may not always be the most appropriate approach. They are more commonly associated with autoconfiguration classes in Spring Boot applications, where they can help conditionally include or exclude beans based on various conditions.


Q3. How can we customize the auto configuration process ?

-> Customizing the autoconfiguration process in Spring Boot allows you to modify or extend the default behavior of autoconfigured beans and components. Here are several ways to customize the autoconfiguration process:

Custom Autoconfiguration Classes:
You can create your own autoconfiguration classes by annotating them with @Configuration and @Conditional annotations.
Use @Conditional annotations to conditionally enable or disable your custom autoconfiguration based on specific conditions.
Define beans and configuration settings in your custom autoconfiguration classes to override or complement the default autoconfiguration provided by Spring Boot.
Exclude Specific Autoconfiguration Classes:
Use the @EnableAutoConfiguration annotation on your main application class and specify which autoconfiguration classes to exclude using the exclude attribute.
This approach allows you to exclude specific autoconfiguration classes provided by Spring Boot and replace them with your custom configurations.
Property-Based Configuration:
Customize the autoconfiguration process based on external configuration properties.
Define properties in the application.properties or application.yml files to control the behavior of autoconfigured beans and components.
Spring Boot provides extensive support for externalized configuration, allowing you to customize various aspects of autoconfiguration using properties.
Bean Post-Processing:
Implement BeanPostProcessor or BeanFactoryPostProcessor interfaces to customize the initialization and configuration of beans created during autoconfiguration.
With bean post-processing, you can modify the behavior of autoconfigured beans before or after they are instantiated by the Spring context.
Conditional Annotations:
Use conditional annotations such as @ConditionalOnProperty, @ConditionalOnClass, @ConditionalOnBean, etc., to conditionally enable or disable autoconfiguration based on specific conditions.
These annotations allow you to fine-tune the autoconfiguration process and control which beans are included based on the presence of certain classes, properties, or beans in the application context.
Custom Starter Dependencies:
Create custom starter dependencies that bundle your custom autoconfiguration classes, dependencies, and configurations.
This approach allows you to package and reuse custom configurations across multiple projects or modules.


Q4. What is the condition that causes a tomcat server to start on port 8080 when the application starts ?

-> In a typical Spring Boot application, if you don't explicitly configure the server port, Tomcat will default to port 8080. This behavior occurs due to Spring Boot's default configuration and autoconfiguration mechanisms.

**ConditionalOnMissingBean** Condition: Spring Boot's autoconfiguration classes often use conditions like @ConditionalOnMissingBean to ensure that autoconfigured beans are only created if certain conditions are met. If you don't explicitly configure a server port, there will be no conflicting bean definition for the server port, allowing the autoconfigured embedded servlet container to start on port 8080.


Q5. Find a way to debug autoconfiguration on application startup. What information can you see ? Try and find a way to disable the auto configuration based on the conditions.

-> To debug autoconfiguration on application startup in a Spring Boot application, you can enable debug logging for the org.springframework.boot.autoconfigure package. This will provide detailed information about the autoconfiguration process, including which autoconfiguration classes are being applied and the conditions under which they are being applied.

In your application.properties file, add the following line to enable debug logging for autoconfiguration:

                        **logging.level.org.springframework.boot.autoconfigure=DEBUG**


**Disable Autoconfiguration Based on Conditions:**

If you want to disable certain autoconfiguration classes based on specific conditions, you can use the exclude attribute of the @EnableAutoConfiguration annotation.
For example, let's say you want to disable autoconfiguration for a class called MyAutoConfiguration if a certain property is set. You can do this as follows:

@SpringBootApplication
@EnableAutoConfiguration(exclude = MyAutoConfiguration.class)
public class MyApplication {
public static void main(String[] args) {
SpringApplication.run(MyApplication.class, args);
}
}