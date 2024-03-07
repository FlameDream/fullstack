## java.lang.NoClassDefFoundError: javax/servlet/ServletContext


方法1：把SpringBoot中main方法所在的class不再继承org.springframework.boot.context.web.SpringBootServletInitializer即可

因为继承org.springframework.boot.context.web.SpringBootServletInitializer，并重写里面的configure方法，即可将这个项目打成war，并部署到tomcat或其它jee容器中。

protected SpringApplicationBuilder configure(SpringApplicationBuilder builder) {
    return builder.sources(Ch623Application.class);
}
方法2：

将此项目运行在一个jee容器下，譬如tomcat

2016-09-13 07:45:57.198 ERROR [main][org.springframework.boot.SpringApplication] Application startup failed
java.lang.NoClassDefFoundError: javax/servlet/ServletContext
    at java.lang.Class.getDeclaredMethods0(Native Method) ~[na:1.8.0_65]
Exception in thread "main" java.lang.NoClassDefFoundError: javax/servlet/ServletContext
    at java.lang.Class.privateGetDeclaredMethods(Class.java:2701) ~[na:1.8.0_65]
    at java.lang.Class.getDeclaredMethods0(Native Method)
    at java.lang.Class.getDeclaredMethods(Class.java:1975) ~[na:1.8.0_65]
    at java.lang.Class.privateGetDeclaredMethods(Class.java:2701)
    at org.springframework.core.type.StandardAnnotationMetadata.getAnnotatedMethods(StandardAnnotationMetadata.java:140) ~[spring-core-4.2.0.RC1.jar:4.2.0.RC1]
    at java.lang.Class.getDeclaredMethods(Class.java:1975)
    at org.springframework.context.annotation.ConfigurationClassParser.doProcessConfigurationClass(ConfigurationClassParser.java:289) ~[spring-context-4.2.0.RC1.jar:4.2.0.RC1]
    at org.springframework.core.type.StandardAnnotationMetadata.getAnnotatedMethods(StandardAnnotationMetadata.java:140)    at org.springframework.context.annotation.ConfigurationClassParser.processConfigurationClass(ConfigurationClassParser.java:229) ~[spring-context-4.2.0.RC1.jar:4.2.0.RC1]
    at org.springframework.context.annotation.ConfigurationClassParser.parse(ConfigurationClassParser.java:196) ~[spring-context-4.2.0.RC1.jar:4.2.0.RC1]
    at org.springframework.context.annotation.ConfigurationClassParser.parse(ConfigurationClassParser.java:165) ~[spring-context-4.2.0.RC1.jar:4.2.0.RC1]
    at org.springframework.context.annotation.ConfigurationClassPostProcessor.processConfigBeanDefinitions(ConfigurationClassPostProcessor.java:321) ~[spring-context-4.2.0.RC1.jar:4.2.0.RC1]

    at org.springframework.context.annotation.ConfigurationClassPostProcessor.postProcessBeanDefinitionRegistry(ConfigurationClassPostProcessor.java:243) ~[spring-context-4.2.0.RC1.jar:4.2.0.RC1]
    at org.springframework.context.annotation.ConfigurationClassParser.doProcessConfigurationClass(ConfigurationClassParser.java:289)
    at org.springframework.context.support.PostProcessorRegistrationDelegate.invokeBeanDefinitionRegistryPostProcessors(PostProcessorRegistrationDelegate.java:269) ~[spring-context-4.2.0.RC1.jar:4.2.0.RC1]
    at org.springframework.context.support.PostProcessorRegistrationDelegate.invokeBeanFactoryPostProcessors(PostProcessorRegistrationDelegate.java:98) ~[spring-context-4.2.0.RC1.jar:4.2.0.RC1]
    at org.springframework.context.support.AbstractApplicationContext.invokeBeanFactoryPostProcessors(AbstractApplicationContext.java:651) ~[spring-context-4.2.0.RC1.jar:4.2.0.RC1]
    at org.springframework.context.annotation.ConfigurationClassParser.processConfigurationClass(ConfigurationClassParser.java:229)
    at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:503) ~[spring-context-4.2.0.RC1.jar:4.2.0.RC1]
    at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:678) [spring-boot-1.3.0.M1.jar:1.3.0.M1]
    at org.springframework.boot.SpringApplication.doRun(SpringApplication.java:339) [spring-boot-1.3.0.M1.jar:1.3.0.M1]
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:274) [spring-boot-1.3.0.M1.jar:1.3.0.M1]
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:931) [spring-boot-1.3.0.M1.jar:1.3.0.M1]
    at org.springframework.context.annotation.ConfigurationClassParser.parse(ConfigurationClassParser.java:196)
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:920) [spring-boot-1.3.0.M1.jar:1.3.0.M1]
    at com.Ch623Application.main(Ch623Application.java:36) [classes/:na]
    at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method) ~[na:1.8.0_65]
    at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62) ~[na:1.8.0_65]
    at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43) ~[na:1.8.0_65]
    at java.lang.reflect.Method.invoke(Method.java:497) ~[na:1.8.0_65]
    at com.intellij.rt.execution.application.AppMain.main(AppMain.java:147) [idea_rt.jar:na]
Caused by: java.lang.ClassNotFoundException: javax.servlet.ServletContext
    at java.net.URLClassLoader.findClass(URLClassLoader.java:381) ~[na:1.8.0_65]
    at java.lang.ClassLoader.loadClass(ClassLoader.java:424) ~[na:1.8.0_65]
    at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:331) ~[na:1.8.0_65]
    at java.lang.ClassLoader.loadClass(ClassLoader.java:357) ~[na:1.8.0_65]
    ... 25 common frames omitted
    at org.springframework.context.annotation.ConfigurationClassParser.parse(ConfigurationClassParser.java:165)
    at org.springframework.context.annotation.ConfigurationClassPostProcessor.processConfigBeanDefinitions(ConfigurationClassPostProcessor.java:321)
    at org.springframework.context.annotation.ConfigurationClassPostProcessor.postProcessBeanDefinitionRegistry(ConfigurationClassPostProcessor.java:243)
    at org.springframework.context.support.PostProcessorRegistrationDelegate.invokeBeanDefinitionRegistryPostProcessors(PostProcessorRegistrationDelegate.java:269)
    at org.springframework.context.support.PostProcessorRegistrationDelegate.invokeBeanFactoryPostProcessors(PostProcessorRegistrationDelegate.java:98)
    at org.springframework.context.support.AbstractApplicationContext.invokeBeanFactoryPostProcessors(AbstractApplicationContext.java:651)
    at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:503)
    at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:678)
    at org.springframework.boot.SpringApplication.doRun(SpringApplication.java:339)
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:274)
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:931)
    at org.springframework.boot.SpringApplication.run(SpringApplication.java:920)
    at com.Ch623Application.main(Ch623Application.java:36)
    at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
    at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
    at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
    at java.lang.reflect.Method.invoke(Method.java:497)
    at com.intellij.rt.execution.application.AppMain.main(AppMain.java:147)
Caused by: java.lang.ClassNotFoundException: javax.servlet.ServletContext
    at java.net.URLClassLoader.findClass(URLClassLoader.java:381)
    at java.lang.ClassLoader.loadClass(ClassLoader.java:424)
    at sun.misc.Launcher$AppClassLoader.loadClass(Launcher.java:331)
    at java.lang.ClassLoader.loadClass(ClassLoader.java:357)
    ... 25 more
2016-09-13 07:45:57.211 INFO  [Thread-1][org.springframework.context.annotation.AnnotationConfigApplicationContext] Closing org.springframework.context.annotation.AnnotationConfigApplicationContext@b48321: startup date [Tue Sep 13 07:45:54 CST 2016]; root of context hierarchy
2016-09-13 07:45:57.213 WARN  [Thread-1][org.springframework.context.annotation.AnnotationConfigApplicationContext] Exception thrown from LifecycleProcessor on context close
java.lang.IllegalStateException: LifecycleProcessor not initialized - call 'refresh' before invoking lifecycle methods via the context: org.springframework.context.annotation.AnnotationConfigApplicationContext@b48321: startup date [Tue Sep 13 07:45:54 CST 2016]; root of context hierarchy
    at org.springframework.context.support.AbstractApplicationContext.getLifecycleProcessor(AbstractApplicationContext.java:398) ~[spring-context-4.2.0.RC1.jar:4.2.0.RC1]
    at org.springframework.context.support.AbstractApplicationContext.doClose(AbstractApplicationContext.java:932) ~[spring-context-4.2.0.RC1.jar:4.2.0.RC1]
    at org.springframework.context.support.AbstractApplicationContext$1.run(AbstractApplicationContext.java:859) [spring-context-4.2.0.RC1.jar:4.2.0.RC1]
2016-09-13 07:45:57.214 DEBUG [Thread-1][org.springframework.beans.factory.support.DefaultListableBeanFactory] Destroying singletons in org.springframework.beans.factory.support.DefaultListableBeanFactory@1fe63b9: defining beans [org.springframework.context.annotation.internalConfigurationAnnotationProcessor,org.springframework.context.annotation.internalAutowiredAnnotationProcessor,org.springframework.context.annotation.internalRequiredAnnotationProcessor,org.springframework.context.annotation.internalCommonAnnotationProcessor,org.springframework.context.event.internalEventListenerProcessor,org.springframework.context.event.internalEventListenerFactory,ch623Application,org.springframework.context.annotation.ConfigurationClassPostProcessor.importAwareProcessor,org.springframework.context.annotation.ConfigurationClassPostProcessor.enhancedConfigurationProcessor,authorSettings,settingsConfig,threadSettings,eventBusConfig,observer1,observer2,subject,businessService,helloJob,quartzConfig,quartzMain,scheduledTaskService,schedulerConfig,asyncTaskService,taskExecutorConfig]; root of factory hierarchy



The issue was with the build.gradle file:

provided "org.springframework.boot:spring-boot-starter-tomcat"
IntelliJ IDEA wasn't happy with the provided.

As soon as I switched to

compile "org.springframework.boot:spring-boot-starter-tomcat"


问题出在build.gradle上

provided "org.springframework.boot:spring-boot-starter-tomcat"
复制
Intellij对所提供的

一旦我切换到

compile "org.springframework.boot:spring-boot-starter-tomcat"
复制
该应用程序工作正常

