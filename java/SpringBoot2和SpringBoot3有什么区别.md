Spring Boot 2和Spring Boot 3的区别

Spring Boot是一个流行的Java开发框架，它旨在简化Spring应用程序的创建和部署。近年来，Spring Boot已经发布了两个主要版本：Spring Boot 2和Spring Boot 3。在本文中，我们将探讨Spring Boot 2和Spring Boot 3之间的主要区别。

一、Java版本依赖

Spring Boot 2基于Java 8，同时支持Java 9。这意味着使用Spring Boot 2的项目可以使用Java 8或更高版本进行编译和运行。然而，Spring Boot 3对Java版本的要求有所不同。Spring Boot 3决定使用Java 17作为最低版本，并支持Java 19。因此，如果您计划升级到Spring Boot 3，您的项目将需要使用Java 17或更高版本进行编译和运行。

二、模块化支持

在模块化方面，Spring Boot 2的支持有限。然而，Spring Boot 3将更加注重模块化，并提供更好的模块化支持。这意味着开发人员能够更轻松地构建和维护模块化的应用程序。Spring Boot 3的模块化支持有助于实现更清晰的代码结构，提高了代码的可读性和可维护性。

三、Spring Framework版本

Spring Boot 2基于Spring Framework 5开发，而Spring Boot 3则构建在Spring Framework 6之上。这意味着Spring Boot 3使用了更新版本的Spring Framework，可能包含一些新的特性和改进。升级到Spring Framework 6可能带来一些优势，例如性能提升、安全性增强以及新的API和功能。然而，这也可能意味着需要更新项目中使用的其他Spring组件，以确保与新的Spring Framework版本兼容。

四、总结

总的来说，Spring Boot 2和Spring Boot 3之间的主要区别在于Java版本依赖、模块化支持和Spring Framework版本。升级到Spring Boot 3可能需要一些额外的工作，例如更新Java版本和Spring Framework版本，以及调整项目以支持模块化。然而，通过这样做，开发人员可以利用新的特性和改进，提高应用程序的性能和可维护性。在决定是否升级到Spring Boot 3时，开发人员应该权衡这些因素，并根据项目的需求和目标做出决策。



1.最低环境的区别
SpringBoot2的最低版本要求为Java8，支持Java9；而SpringBoot3决定使用Java17作为最低版本，并支持Java19。

Spring Boot2基于Spring Framework5开发；而SpringBoot3构建基于Spring Framework6之上，需要使用Spring Framework6。

2.GraalVM支持的区别
相比SpringBoot2，SpringBoot3的Spring Native也是升级的一个重大特性，支持使用GraalVM将Spring的应用程序编译成本地可执行的镜像文件，可以显著提升启动速度、峰值性能以及减少内存使用。

3.图片Banner支持的区别
在SpringBoot2中，自定义Banner支持图片类型；而现在Spring Boot3自定义Banner只支持文本类型（banner.txt），不再支持图片类型。

4.依赖项的区别
相比SpringBoot2，Spring Boot3.0.0-M1删除了对一些附加依赖项的支持，包括Apache ActiveMQ、Atomikos、EhCache2和HazelCast3。Jersey是另一个值得注意的弃用，在它提供对Spring Framework6的支持之前已被删除。

除了上述内容外，相比SpringBoot2，SpringBoot3还增加了很多其它的新特性，如：Java EE已经变更为Jakarta EE、Log4j2增强、三方包升级等。

延伸阅读

SpringBoot框架有哪些优点
1.可快速构建独立的Spring应用

Spring Boot是一个依靠大量注解实现自动化配置的全新框架。在构建Spring应用时，我们只需要添加相应的场景依赖，Spring Boot就会根据添加的场景依赖自动进行配置，在无须额外手动添加配置的情况下快速构建出一个独立的Spring应用。

2.内嵌web服务器，无须部署WAR文件

传统的Spring应用部署时，通常会将应用打成WAR包形式并部署到Tomcat、Jetty或Undertow 服务器中。Spring Boot框架内嵌了Tomcat、Jetty和Undertow 服务器，而且可以自动将项目打包，并在项目运行时部署到服务器中。

3.自动starter依赖，简化构建配置

在Spring Boot项目构建过程中，无须准备各种独立的JAR文件，只需在构建项目时根据开发场景需求选择对应的依赖启动器“starter”，在引入的依赖启动器“starter”内部已经包含了对应开发场景所需的依赖，并会自动下载和拉取相关JAR包。例如，在Web开发时，只需在构建项目时选择对应的Web场景依赖启动器spring-boot-starter-web,Spring Boot项目便会自动导入spring-webmvc、spring-web、spring-boot-starter-tomcat等子依赖，并自动下载和获取Web开发需要的相关JAR包。

4.自动配置Spring以及第三方功能

Springboot简化了很多配置,例如工厂、整合SpringMVC 、Mybatis 之类的固定配置，创建工程后可直接开发业务逻辑。另外，第三方工具的使用，也只需引入starter，配置文件配置一下账号密码，有种开箱即用的感觉。

5.提供生产就绪功能

Spring Boot提供了一些用于生产环境运行时的特性，例如指标、监控检查和外部化配置。其中，指标和监控检查可以帮助运维人员在运维期间监控项目运行情况;外部化配置可以使运维人员快速、方便地进行外部化配置和部署工作。

6.极少的代码生成和XML配置

Spring Boot框架内部已经实现了与Spring以及其他常用第三方库的整合连接，并提供了默认优异化的整合配置，使用时基本上不需要额外生成配置代码和XML配置文件。在需要自定义配置的情况下，Spring Boot更加提倡使用Java config(Java 配置类)替换传统的XML配置方式，这样更加方便查看和管理。