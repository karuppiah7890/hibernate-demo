# Story

I'm following this

http://hibernate.org/orm/documentation/getting-started/

Right, it doesn't have much at all, except for how
to add the gradle dependency

They recommend checking this out for newbies

https://docs.jboss.org/hibernate/orm/current/quickstart/html_single/

For more thorough information, here -

https://docs.jboss.org/hibernate/orm/current/userguide/html_single/Hibernate_User_Guide.html

---

Following the newbie guide
https://docs.jboss.org/hibernate/orm/current/quickstart/html_single/

ORM Hate -
https://martinfowler.com/bliki/OrmHate.html

ORM Wikipedia
https://en.wikipedia.org/wiki/Object-relational_mapping

List of ORMs Wikipedia
https://en.wikipedia.org/wiki/List_of_object-relational_mapping_software

Java ones -
https://en.wikipedia.org/wiki/List_of_object-relational_mapping_software#Java

I don't see the guide exactly helping me. I'm going to
try out some other short tutorial to see how to get
started with Hibernate, as I can already see some demo
code and it does NOT have the things the guide says
and I think the code I'm seeing works.

I noticed quite some YouTube videos. Gonna checkout
text tutorials first for now

I'm actually going to be using Hibernate in a spring
boot application. So, maybe I should checkout tutorials
based on that

I think I also need to do more of text tutorials
than videos. It's just that some stuff is hard to
explain in text and is easier shown visually through
an image or video. Mostly installation related stuff.
But yeah, text can be done too, with proper
instructions on where to find something on the
screen when it's GUI applications. CLI is pretty
easy I guess ;) :D We can use asciinema for CLI
recording ;)

Back to spring boot and hibernate!

https://www.baeldung.com/spring-boot-hibernate

```bash
$ cd hibernate-demo
$ spring init --java-version 14 --dependencies web,data-jpa,postgresql --type gradle-project example-project
$ mv example-project/* .
$ mv example-project/.gitignore .
$ rm -rfv example-project/
```

I had to do that as I couldn't use `.` as argument. It
failed saying `.` already exists.

I'm using Postgres instead of H2. I have to see how
that differs.

I just realized that this article is just too small.
Should have read it as an overview before going with
it. Hmm

I'm using some help from this article too

https://dzone.com/articles/spring-boot-jpa-hibernate-oracle 

This too
https://techblogstation.com/spring-boot/spring-boot-mysql-hibernate/#Configure_the_MySQL_Database_/_Data_Source

https://medium.com/coding-blocks/creating-user-database-and-adding-access-on-postgresql-8bfcd2f4a91e

```bash
$ psql -h localhost
psql (10.13, server 12.3)
WARNING: psql major version 10, server major version 12.
         Some psql features might not work.
Type "help" for help.

karuppiahn=# create database book;
CREATE DATABASE
karuppiahn=# create user book_user with encrypted password 'book123';
CREATE ROLE
karuppiahn=# grant all privileges on database book to book_user ;
GRANT
```

Now, I tried to run the application after putting
the following `application.properties`

```properties
# create and drop tables and sequences, loads import.sql
spring.jpa.hibernate.ddl-auto=create-drop

# Example Oracle settings

#spring.datasource.url=jdbc:oracle:thin:@localhost:1522:orcl
#spring.datasource.username=HIBERNATE_TEST
#spring.datasource.password=HIBERNATE_TEST
#spring.datasource.driver.class=oracle.jdbc.driver.OracleDriver

# Postgres settings

spring.datasource.url=jdbc:postgres://localhost:5432/book
spring.datasource.username=book_user
spring.datasource.password=book123

# logging

logging.pattern.console=%d{yyyy-MM-dd HH:mm:ss} %-5level %logger{36} - %msg%n
logging.level.org.hibernate.SQL=debug
```

```shell script
$ ./gradlew bootRun
  
  > Task :bootRun
  
    .   ____          _            __ _ _
   /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
  ( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
   \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
    '  |____| .__|_| |_|_| |_\__, | / / / /
   =========|_|==============|___/=/_/_/_/
   :: Spring Boot ::        (v2.3.3.RELEASE)
  
  2020-08-26 23:34:52 INFO  c.e.exampleproject.DemoApplication - Starting DemoApplication on Karuppiah-N.local with PID 16979 (/Users/karuppiahn/oss/github.com/karuppiah7890/hibernate-demo/build/classes/java/main started by karuppiahn in /Users/karuppiahn/oss/github.com/karuppiah7890/hibernate-demo)
  2020-08-26 23:34:52 INFO  c.e.exampleproject.DemoApplication - No active profile set, falling back to default profiles: default
  2020-08-26 23:34:52 INFO  o.s.d.r.c.RepositoryConfigurationDelegate - Bootstrapping Spring Data JPA repositories in DEFERRED mode.
  2020-08-26 23:34:52 INFO  o.s.d.r.c.RepositoryConfigurationDelegate - Finished Spring Data repository scanning in 43ms. Found 1 JPA repository interfaces.
  2020-08-26 23:34:53 INFO  o.s.b.w.e.tomcat.TomcatWebServer - Tomcat initialized with port(s): 8080 (http)
  2020-08-26 23:34:53 INFO  o.a.catalina.core.StandardService - Starting service [Tomcat]
  2020-08-26 23:34:53 INFO  o.a.catalina.core.StandardEngine - Starting Servlet engine: [Apache Tomcat/9.0.37]
  2020-08-26 23:34:53 INFO  o.a.c.c.C.[Tomcat].[localhost].[/] - Initializing Spring embedded WebApplicationContext
  2020-08-26 23:34:53 INFO  o.s.b.w.s.c.ServletWebServerApplicationContext - Root WebApplicationContext: initialization completed in 1061 ms
  2020-08-26 23:34:53 WARN  o.s.b.w.s.c.AnnotationConfigServletWebServerApplicationContext - Exception encountered during context initialization - cancelling refresh attempt: org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'org.springframework.boot.autoconfigure.orm.jpa.HibernateJpaConfiguration': Unsatisfied dependency expressed through constructor parameter 0; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'dataSource' defined in class path resource [org/springframework/boot/autoconfigure/jdbc/DataSourceConfiguration$Hikari.class]: Bean instantiation via factory method failed; nested exception is org.springframework.beans.BeanInstantiationException: Failed to instantiate [com.zaxxer.hikari.HikariDataSource]: Factory method 'dataSource' threw exception; nested exception is org.springframework.boot.autoconfigure.jdbc.DataSourceProperties$DataSourceBeanCreationException: Failed to determine a suitable driver class
  2020-08-26 23:34:53 INFO  o.a.catalina.core.StandardService - Stopping service [Tomcat]
  2020-08-26 23:34:53 INFO  o.s.b.a.l.ConditionEvaluationReportLoggingListener -
  
  Error starting ApplicationContext. To display the conditions report re-run your application with 'debug' enabled.
  2020-08-26 23:34:53 ERROR o.s.b.d.LoggingFailureAnalysisReporter -
  
  ***************************
  APPLICATION FAILED TO START
  ***************************
  
  Description:
  
  Failed to configure a DataSource: no embedded datasource could be configured.
  
  Reason: Failed to determine a suitable driver class
  
  
  Action:
  
  Consider the following:
          If you want an embedded database (H2, HSQL or Derby), please put it on the classpath.
          If you have database settings to be loaded from a particular profile you may need to activate it (no profiles are currently active).
  
  
  > Task :bootRun FAILED
  
  FAILURE: Build failed with an exception.
  
  * What went wrong:
  Execution failed for task ':bootRun'.
  > Process 'command '/usr/local/Cellar/openjdk/14.0.1/libexec/openjdk.jdk/Contents/Home/bin/java'' finished with non-zero exit value 1
  
  * Try:
  Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.
  
  * Get more help at https://help.gradle.org
  
  BUILD FAILED in 7s
  3 actionable tasks: 3 executed
```

It says `Reason: Failed to determine a suitable driver class`

I added this to `application.properties`

```properties
spring.datasource.driver-class-name=org.postgresql.Driver
```

```shell script
$ ./gradlew bootRun

> Task :bootRun

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.3.3.RELEASE)

2020-08-26 23:38:51 INFO  c.e.exampleproject.DemoApplication - Starting DemoApplication on Karuppiah-N.local with PID 26215 (/Users/karuppiahn/oss/github.com/karuppiah7890/hibernate-demo/build/classes/java/main started by karuppiahn in /Users/karuppiahn/oss/github.com/karuppiah7890/hibernate-demo)
2020-08-26 23:38:51 INFO  c.e.exampleproject.DemoApplication - No active profile set, falling back to default profiles: default
2020-08-26 23:38:52 INFO  o.s.d.r.c.RepositoryConfigurationDelegate - Bootstrapping Spring Data JPA repositories in DEFERRED mode.
2020-08-26 23:38:52 INFO  o.s.d.r.c.RepositoryConfigurationDelegate - Finished Spring Data repository scanning in 43ms. Found 1 JPA repository interfaces.
2020-08-26 23:38:52 INFO  o.s.b.w.e.tomcat.TomcatWebServer - Tomcat initialized with port(s): 8080 (http)
2020-08-26 23:38:52 INFO  o.a.catalina.core.StandardService - Starting service [Tomcat]
2020-08-26 23:38:52 INFO  o.a.catalina.core.StandardEngine - Starting Servlet engine: [Apache Tomcat/9.0.37]
2020-08-26 23:38:52 INFO  o.a.c.c.C.[Tomcat].[localhost].[/] - Initializing Spring embedded WebApplicationContext
2020-08-26 23:38:52 INFO  o.s.b.w.s.c.ServletWebServerApplicationContext - Root WebApplicationContext: initialization completed in 1056 ms
2020-08-26 23:38:52 INFO  o.s.s.c.ThreadPoolTaskExecutor - Initializing ExecutorService 'applicationTaskExecutor'
2020-08-26 23:38:52 INFO  o.h.jpa.internal.util.LogHelper - HHH000204: Processing PersistenceUnitInfo [name: default]
2020-08-26 23:38:52 WARN  o.s.b.a.o.j.JpaBaseConfiguration$JpaWebConfiguration - spring.jpa.open-in-view is enabled by default. Therefore, database queries may be performed during view rendering. Explicitly configure spring.jpa.open-in-view to disable this warning
2020-08-26 23:38:52 INFO  org.hibernate.Version - HHH000412: Hibernate ORM core version 5.4.20.Final
2020-08-26 23:38:53 INFO  o.h.annotations.common.Version - HCANN000001: Hibernate Commons Annotations {5.1.0.Final}
2020-08-26 23:38:53 INFO  com.zaxxer.hikari.HikariDataSource - HikariPool-1 - Starting...
2020-08-26 23:38:53 WARN  o.h.e.j.e.i.JdbcEnvironmentInitiator - HHH000342: Could not obtain connection to query metadata : Driver org.postgresql.Driver claims to not accept jdbcUrl, jdbc:postgres://localhost:5432/book
2020-08-26 23:38:53 INFO  o.s.b.w.e.tomcat.TomcatWebServer - Tomcat started on port(s): 8080 (http) with context path ''
2020-08-26 23:38:53 INFO  o.s.d.r.c.DeferredRepositoryInitializationListener - Triggering deferred initialization of Spring Data repositories…
2020-08-26 23:38:53 WARN  o.s.b.w.s.c.AnnotationConfigServletWebServerApplicationContext - Exception encountered during context initialization - cancelling refresh attempt: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'bookRepository' defined in com.example.exampleproject.repositories.BookRepository defined in @EnableJpaRepositories declared on JpaRepositoriesRegistrar.EnableJpaRepositoriesConfiguration: Cannot resolve reference to bean 'jpaMappingContext' while setting bean property 'mappingContext'; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'jpaMappingContext': Invocation of init method failed; nested exception is org.hibernate.service.spi.ServiceException: Unable to create requested service [org.hibernate.engine.jdbc.env.spi.JdbcEnvironment]
2020-08-26 23:38:53 INFO  o.s.o.j.LocalContainerEntityManagerFactoryBean - Closing JPA EntityManagerFactory for persistence unit 'default'
2020-08-26 23:38:53 WARN  o.s.b.f.s.DisposableBeanAdapter - Invocation of destroy method failed on bean with name 'entityManagerFactory': org.hibernate.service.spi.ServiceException: Unable to create requested service [org.hibernate.engine.jdbc.env.spi.JdbcEnvironment]
2020-08-26 23:38:53 INFO  o.s.s.c.ThreadPoolTaskExecutor - Shutting down ExecutorService 'applicationTaskExecutor'
2020-08-26 23:38:53 INFO  o.a.catalina.core.StandardService - Stopping service [Tomcat]
2020-08-26 23:38:53 INFO  o.s.b.a.l.ConditionEvaluationReportLoggingListener -

Error starting ApplicationContext. To display the conditions report re-run your application with 'debug' enabled.
2020-08-26 23:38:53 ERROR o.s.boot.SpringApplication - Application run failed
org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'bookRepository' defined in com.example.exampleproject.repositories.BookRepository defined in @EnableJpaRepositories declared on JpaRepositoriesRegistrar.EnableJpaRepositoriesConfiguration: Cannot resolve reference to bean 'jpaMappingContext' while setting bean property 'mappingContext'; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'jpaMappingContext': Invocation of init method failed; nested exception is org.hibernate.service.spi.ServiceException: Unable to create requested service [org.hibernate.engine.jdbc.env.spi.JdbcEnvironment]
        at org.springframework.beans.factory.support.BeanDefinitionValueResolver.resolveReference(BeanDefinitionValueResolver.java:342)
        at org.springframework.beans.factory.support.BeanDefinitionValueResolver.resolveValueIfNecessary(BeanDefinitionValueResolver.java:113)
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.applyPropertyValues(AbstractAutowireCapableBeanFactory.java:1697)
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.populateBean(AbstractAutowireCapableBeanFactory.java:1442)
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:593)
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:516)
        at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:324)
        at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:226)
        at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:322)
        at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:202)
        at org.springframework.beans.factory.support.DefaultListableBeanFactory.getBeansOfType(DefaultListableBeanFactory.java:624)
        at org.springframework.beans.factory.support.DefaultListableBeanFactory.getBeansOfType(DefaultListableBeanFactory.java:612)
        at org.springframework.data.repository.config.DeferredRepositoryInitializationListener.onApplicationEvent(DeferredRepositoryInitializationListener.java:51)
        at org.springframework.data.repository.config.DeferredRepositoryInitializationListener.onApplicationEvent(DeferredRepositoryInitializationListener.java:36)
        at org.springframework.context.event.SimpleApplicationEventMulticaster.doInvokeListener(SimpleApplicationEventMulticaster.java:172)
        at org.springframework.context.event.SimpleApplicationEventMulticaster.invokeListener(SimpleApplicationEventMulticaster.java:165)
        at org.springframework.context.event.SimpleApplicationEventMulticaster.multicastEvent(SimpleApplicationEventMulticaster.java:139)
        at org.springframework.context.support.AbstractApplicationContext.publishEvent(AbstractApplicationContext.java:404)
        at org.springframework.context.support.AbstractApplicationContext.publishEvent(AbstractApplicationContext.java:361)
        at org.springframework.context.support.AbstractApplicationContext.finishRefresh(AbstractApplicationContext.java:898)
        at org.springframework.context.support.AbstractApplicationContext.refresh(AbstractApplicationContext.java:554)
        at org.springframework.boot.web.servlet.context.ServletWebServerApplicationContext.refresh(ServletWebServerApplicationContext.java:143)
        at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:758)
        at org.springframework.boot.SpringApplication.refresh(SpringApplication.java:750)
        at org.springframework.boot.SpringApplication.refreshContext(SpringApplication.java:397)
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:315)
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:1237)
        at org.springframework.boot.SpringApplication.run(SpringApplication.java:1226)
        at com.example.exampleproject.DemoApplication.main(DemoApplication.java:10)
Caused by: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'jpaMappingContext': Invocation of init method failed; nested exception is org.hibernate.service.spi.ServiceException: Unable to create requested service [org.hibernate.engine.jdbc.env.spi.JdbcEnvironment]
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.initializeBean(AbstractAutowireCapableBeanFactory.java:1794)
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.doCreateBean(AbstractAutowireCapableBeanFactory.java:594)
        at org.springframework.beans.factory.support.AbstractAutowireCapableBeanFactory.createBean(AbstractAutowireCapableBeanFactory.java:516)
        at org.springframework.beans.factory.support.AbstractBeanFactory.lambda$doGetBean$0(AbstractBeanFactory.java:324)
        at org.springframework.beans.factory.support.DefaultSingletonBeanRegistry.getSingleton(DefaultSingletonBeanRegistry.java:226)
        at org.springframework.beans.factory.support.AbstractBeanFactory.doGetBean(AbstractBeanFactory.java:322)
        at org.springframework.beans.factory.support.AbstractBeanFactory.getBean(AbstractBeanFactory.java:202)
        at org.springframework.beans.factory.support.BeanDefinitionValueResolver.resolveReference(BeanDefinitionValueResolver.java:330)
        ... 28 common frames omitted
Caused by: org.hibernate.service.spi.ServiceException: Unable to create requested service [org.hibernate.engine.jdbc.env.spi.JdbcEnvironment]
        at org.hibernate.service.internal.AbstractServiceRegistryImpl.createService(AbstractServiceRegistryImpl.java:275)
        at org.hibernate.service.internal.AbstractServiceRegistryImpl.initializeService(AbstractServiceRegistryImpl.java:237)
        at org.hibernate.service.internal.AbstractServiceRegistryImpl.getService(AbstractServiceRegistryImpl.java:214)
        at org.hibernate.id.factory.internal.DefaultIdentifierGeneratorFactory.injectServices(DefaultIdentifierGeneratorFactory.java:152)
        at org.hibernate.service.internal.AbstractServiceRegistryImpl.injectDependencies(AbstractServiceRegistryImpl.java:286)
        at org.hibernate.service.internal.AbstractServiceRegistryImpl.initializeService(AbstractServiceRegistryImpl.java:243)
        at org.hibernate.service.internal.AbstractServiceRegistryImpl.getService(AbstractServiceRegistryImpl.java:214)
        at org.hibernate.boot.internal.InFlightMetadataCollectorImpl.<init>(InFlightMetadataCollectorImpl.java:176)
        at org.hibernate.boot.model.process.spi.MetadataBuildingProcess.complete(MetadataBuildingProcess.java:118)
        at org.hibernate.jpa.boot.internal.EntityManagerFactoryBuilderImpl.metadata(EntityManagerFactoryBuilderImpl.java:1224)
        at org.hibernate.jpa.boot.internal.EntityManagerFactoryBuilderImpl.build(EntityManagerFactoryBuilderImpl.java:1255)
        at org.springframework.orm.jpa.vendor.SpringHibernateJpaPersistenceProvider.createContainerEntityManagerFactory(SpringHibernateJpaPersistenceProvider.java:58)
        at org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean.createNativeEntityManagerFactory(LocalContainerEntityManagerFactoryBean.java:365)
        at org.springframework.orm.jpa.AbstractEntityManagerFactoryBean.buildNativeEntityManagerFactory(AbstractEntityManagerFactoryBean.java:391)
        at java.base/java.util.concurrent.FutureTask.run(FutureTask.java:264)
        at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1130)
        at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:630)
        at java.base/java.lang.Thread.run(Thread.java:832)
Caused by: org.hibernate.HibernateException: Access to DialectResolutionInfo cannot be null when 'hibernate.dialect' not set
        at org.hibernate.engine.jdbc.dialect.internal.DialectFactoryImpl.determineDialect(DialectFactoryImpl.java:100)
        at org.hibernate.engine.jdbc.dialect.internal.DialectFactoryImpl.buildDialect(DialectFactoryImpl.java:54)
        at org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator.initiateService(JdbcEnvironmentInitiator.java:137)
        at org.hibernate.engine.jdbc.env.internal.JdbcEnvironmentInitiator.initiateService(JdbcEnvironmentInitiator.java:35)
        at org.hibernate.boot.registry.internal.StandardServiceRegistryImpl.initiateService(StandardServiceRegistryImpl.java:101)
        at org.hibernate.service.internal.AbstractServiceRegistryImpl.createService(AbstractServiceRegistryImpl.java:263)
        ... 17 common frames omitted

> Task :bootRun FAILED

FAILURE: Build failed with an exception.

* What went wrong:
Execution failed for task ':bootRun'.
> Process 'command '/usr/local/Cellar/openjdk/14.0.1/libexec/openjdk.jdk/Contents/Home/bin/java'' finished with non-zero exit value 1

* Try:
Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.

* Get more help at https://help.gradle.org

BUILD FAILED in 3s
3 actionable tasks: 2 executed, 1 up-to-date
```

It says

```shell script
Could not obtain connection to query metadata : Driver org.postgresql.Driver claims to not accept jdbcUrl, jdbc:postgres://localhost:5432/book
```

So, I gave the url wrong. I gave it as `jdbc:postgres://localhost:5432/book`, when in fact the correct one is
actually `jdbc:postgresql://localhost:5432/book`

Wow! Things work now!! :D :D

```shell script
$ ./gradlew bootRun

> Task :bootRun

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::        (v2.3.3.RELEASE)

2020-08-26 23:44:17 INFO  c.e.exampleproject.DemoApplication - Starting DemoApplication on Karuppiah-N.local with PID 35149 (/Users/karuppiahn/oss/github.com/karuppiah7890/hibernate-demo/build/classes/java/main started by karuppiahn in /Users/karuppiahn/oss/github.com/karuppiah7890/hibernate-demo)
2020-08-26 23:44:17 INFO  c.e.exampleproject.DemoApplication - No active profile set, falling back to default profiles: default
2020-08-26 23:44:17 INFO  o.s.d.r.c.RepositoryConfigurationDelegate - Bootstrapping Spring Data JPA repositories in DEFERRED mode.
2020-08-26 23:44:18 INFO  o.s.d.r.c.RepositoryConfigurationDelegate - Finished Spring Data repository scanning in 42ms. Found 1 JPA repository interfaces.
2020-08-26 23:44:18 INFO  o.s.b.w.e.tomcat.TomcatWebServer - Tomcat initialized with port(s): 8080 (http)
2020-08-26 23:44:18 INFO  o.a.catalina.core.StandardService - Starting service [Tomcat]
2020-08-26 23:44:18 INFO  o.a.catalina.core.StandardEngine - Starting Servlet engine: [Apache Tomcat/9.0.37]
2020-08-26 23:44:18 INFO  o.a.c.c.C.[Tomcat].[localhost].[/] - Initializing Spring embedded WebApplicationContext
2020-08-26 23:44:18 INFO  o.s.b.w.s.c.ServletWebServerApplicationContext - Root WebApplicationContext: initialization completed in 1017 ms
2020-08-26 23:44:18 INFO  o.s.s.c.ThreadPoolTaskExecutor - Initializing ExecutorService 'applicationTaskExecutor'
2020-08-26 23:44:18 INFO  o.h.jpa.internal.util.LogHelper - HHH000204: Processing PersistenceUnitInfo [name: default]
2020-08-26 23:44:18 WARN  o.s.b.a.o.j.JpaBaseConfiguration$JpaWebConfiguration - spring.jpa.open-in-view is enabled by default. Therefore, database queries may be performed during view rendering. Explicitly configure spring.jpa.open-in-view to disable this warning
2020-08-26 23:44:18 INFO  org.hibernate.Version - HHH000412: Hibernate ORM core version 5.4.20.Final
2020-08-26 23:44:18 INFO  o.h.annotations.common.Version - HCANN000001: Hibernate Commons Annotations {5.1.0.Final}
2020-08-26 23:44:18 INFO  com.zaxxer.hikari.HikariDataSource - HikariPool-1 - Starting...
2020-08-26 23:44:19 INFO  o.s.b.w.e.tomcat.TomcatWebServer - Tomcat started on port(s): 8080 (http) with context path ''
2020-08-26 23:44:19 INFO  o.s.d.r.c.DeferredRepositoryInitializationListener - Triggering deferred initialization of Spring Data repositories…
2020-08-26 23:44:19 INFO  com.zaxxer.hikari.HikariDataSource - HikariPool-1 - Start completed.
2020-08-26 23:44:19 INFO  org.hibernate.dialect.Dialect - HHH000400: Using dialect: org.hibernate.dialect.PostgreSQL10Dialect
2020-08-26 23:44:19 INFO  org.hibernate.tuple.PojoInstantiator - HHH000182: No default (no-argument) constructor for class: com.example.exampleproject.models.Book (class must be instantiated by Interceptor)
2020-08-26 23:44:19 DEBUG org.hibernate.SQL - drop table if exists book cascade
2020-08-26 23:44:19 WARN  o.h.e.jdbc.spi.SqlExceptionHelper - SQL Warning Code: 0, SQLState: 00000
2020-08-26 23:44:19 WARN  o.h.e.jdbc.spi.SqlExceptionHelper - table "book" does not exist, skipping
2020-08-26 23:44:19 DEBUG org.hibernate.SQL - drop sequence if exists hibernate_sequence
2020-08-26 23:44:19 WARN  o.h.e.jdbc.spi.SqlExceptionHelper - SQL Warning Code: 0, SQLState: 00000
2020-08-26 23:44:19 WARN  o.h.e.jdbc.spi.SqlExceptionHelper - sequence "hibernate_sequence" does not exist, skipping
2020-08-26 23:44:19 DEBUG org.hibernate.SQL - create sequence hibernate_sequence start 1 increment 1
2020-08-26 23:44:19 DEBUG org.hibernate.SQL - create table book (id int8 not null, name varchar(255), primary key (id))
2020-08-26 23:44:19 INFO  o.h.t.s.internal.SchemaCreatorImpl - HHH000476: Executing import script 'file:/Users/karuppiahn/oss/github.com/karuppiah7890/hibernate-demo/build/resources/main/import.sql'
2020-08-26 23:44:19 DEBUG org.hibernate.SQL - insert into book values(1, 'The Tartar Steppe')
2020-08-26 23:44:19 DEBUG org.hibernate.SQL - insert into book values(2, 'Poem Strip')
2020-08-26 23:44:19 DEBUG org.hibernate.SQL - insert into book values(3, 'Restless Nights: Selected Stories of Dino Buzzati')
2020-08-26 23:44:19 INFO  o.h.e.t.j.p.i.JtaPlatformInitiator - HHH000490: Using JtaPlatform implementation: [org.hibernate.engine.transaction.jta.platform.internal.NoJtaPlatform]
2020-08-26 23:44:19 INFO  o.s.o.j.LocalContainerEntityManagerFactoryBean - Initialized JPA EntityManagerFactory for persistence unit 'default'
2020-08-26 23:44:19 INFO  o.s.d.r.c.DeferredRepositoryInitializationListener - Spring Data repositories initialized!
2020-08-26 23:44:19 INFO  c.e.exampleproject.DemoApplication - Started DemoApplication in 2.781 seconds (JVM running for 3.086)
<=========----> 75% EXECUTING [28s]
> :bootRun
```

It even created the table and put some data in the table using the `import.sql`

```shell script
$ psql -h localhost -U book_user book
psql (10.13, server 12.3)
WARNING: psql major version 10, server major version 12.
         Some psql features might not work.
Type "help" for help.

book=> \dt
         List of relations
 Schema | Name | Type  |   Owner
--------+------+-------+-----------
 public | book | table | book_user
(1 row)

book=> select * from book ;
 id |                       name
----+---------------------------------------------------
  1 | The Tartar Steppe
  2 | Poem Strip
  3 | Restless Nights: Selected Stories of Dino Buzzati
(3 rows)

book=>
```

I tried to run it again. Somehow it knows that it shouldn't try to create the
table again and also not import the `import.sql`. I think it's only a one time
thing when a table is created. If table is already present, I think it won't be
done. Hmm

Describe table didn't work though, weirdly. It gave some error
https://www.postgresqltutorial.com/postgresql-describe-table/

Oh wait. Hmm. I just tried to get into the database to see the table after
stopping the service, there were no tables!! It gets created only when the 
service starts and the importing is done everytime. Right. The table is
also destroyed on stopping the service. That's weird. Hmm

Gotta check what this means

```properties
# create and drop tables and sequences, loads import.sql

spring.jpa.hibernate.ddl-auto=create-drop
```

I think that's what is controlling stuff. 

Describe not working -

```shell script
book=> \d book
ERROR:  column c.relhasoids does not exist
LINE 1: ...riggers, c.relrowsecurity, c.relforcerowsecurity, c.relhasoi...
                                                             ^
book=> \d+ book
ERROR:  column c.relhasoids does not exist
LINE 1: ...riggers, c.relrowsecurity, c.relforcerowsecurity, c.relhasoi...
                                                             ^
book=>
```

I created repository and service. It gives an error

```shell script
org.springframework.orm.jpa.JpaSystemException: No default constructor for entity:  : com.example.exampleproject.models.Book; nested exception is org.hibernate.InstantiationException: No default constructor for entity:  : com.example.exampleproject.models.Book
	at org.springframework.orm.jpa.vendor.HibernateJpaDialect.convertHibernateAccessException(HibernateJpaDialect.java:353)
	at org.springframework.orm.jpa.vendor.HibernateJpaDialect.translateExceptionIfPossible(HibernateJpaDialect.java:255)
	at org.springframework.orm.jpa.AbstractEntityManagerFactoryBean.translateExceptionIfPossible(AbstractEntityManagerFactoryBean.java:528)
	at org.springframework.dao.support.ChainedPersistenceExceptionTranslator.translateExceptionIfPossible(ChainedPersistenceExceptionTranslator.java:61)
	at org.springframework.dao.support.DataAccessUtils.translateIfNecessary(DataAccessUtils.java:242)
	at org.springframework.dao.support.PersistenceExceptionTranslationInterceptor.invoke(PersistenceExceptionTranslationInterceptor.java:153)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186)
	at org.springframework.data.jpa.repository.support.CrudMethodMetadataPostProcessor$CrudMethodMetadataPopulatingMethodInterceptor.invoke(CrudMethodMetadataPostProcessor.java:178)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186)
	at org.springframework.aop.interceptor.ExposeInvocationInterceptor.invoke(ExposeInvocationInterceptor.java:95)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186)
	at org.springframework.aop.framework.JdkDynamicAopProxy.invoke(JdkDynamicAopProxy.java:212)
	at com.sun.proxy.$Proxy94.findAll(Unknown Source)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:564)
	at org.springframework.aop.support.AopUtils.invokeJoinpointUsingReflection(AopUtils.java:344)
	at org.springframework.aop.framework.JdkDynamicAopProxy.invoke(JdkDynamicAopProxy.java:205)
	at com.sun.proxy.$Proxy68.findAll(Unknown Source)
	at com.example.exampleproject.services.BookService.list(BookService.java:17)
	at com.example.exampleproject.services.BookServiceTest.whenApplicationStarts_thenHibernateCreatesInitialRecords(BookServiceTest.java:20)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:564)
	at org.junit.platform.commons.util.ReflectionUtils.invokeMethod(ReflectionUtils.java:686)
	at org.junit.jupiter.engine.execution.MethodInvocation.proceed(MethodInvocation.java:60)
	at org.junit.jupiter.engine.execution.InvocationInterceptorChain$ValidatingInvocation.proceed(InvocationInterceptorChain.java:131)
	at org.junit.jupiter.engine.extension.TimeoutExtension.intercept(TimeoutExtension.java:149)
	at org.junit.jupiter.engine.extension.TimeoutExtension.interceptTestableMethod(TimeoutExtension.java:140)
	at org.junit.jupiter.engine.extension.TimeoutExtension.interceptTestMethod(TimeoutExtension.java:84)
	at org.junit.jupiter.engine.execution.ExecutableInvoker$ReflectiveInterceptorCall.lambda$ofVoidMethod$0(ExecutableInvoker.java:115)
	at org.junit.jupiter.engine.execution.ExecutableInvoker.lambda$invoke$0(ExecutableInvoker.java:105)
	at org.junit.jupiter.engine.execution.InvocationInterceptorChain$InterceptedInvocation.proceed(InvocationInterceptorChain.java:106)
	at org.junit.jupiter.engine.execution.InvocationInterceptorChain.proceed(InvocationInterceptorChain.java:64)
	at org.junit.jupiter.engine.execution.InvocationInterceptorChain.chainAndInvoke(InvocationInterceptorChain.java:45)
	at org.junit.jupiter.engine.execution.InvocationInterceptorChain.invoke(InvocationInterceptorChain.java:37)
	at org.junit.jupiter.engine.execution.ExecutableInvoker.invoke(ExecutableInvoker.java:104)
	at org.junit.jupiter.engine.execution.ExecutableInvoker.invoke(ExecutableInvoker.java:98)
	at org.junit.jupiter.engine.descriptor.TestMethodTestDescriptor.lambda$invokeTestMethod$6(TestMethodTestDescriptor.java:212)
	at org.junit.platform.engine.support.hierarchical.ThrowableCollector.execute(ThrowableCollector.java:73)
	at org.junit.jupiter.engine.descriptor.TestMethodTestDescriptor.invokeTestMethod(TestMethodTestDescriptor.java:208)
	at org.junit.jupiter.engine.descriptor.TestMethodTestDescriptor.execute(TestMethodTestDescriptor.java:137)
	at org.junit.jupiter.engine.descriptor.TestMethodTestDescriptor.execute(TestMethodTestDescriptor.java:71)
	at org.junit.platform.engine.support.hierarchical.NodeTestTask.lambda$executeRecursively$5(NodeTestTask.java:135)
	at org.junit.platform.engine.support.hierarchical.ThrowableCollector.execute(ThrowableCollector.java:73)
	at org.junit.platform.engine.support.hierarchical.NodeTestTask.lambda$executeRecursively$7(NodeTestTask.java:125)
	at org.junit.platform.engine.support.hierarchical.Node.around(Node.java:135)
	at org.junit.platform.engine.support.hierarchical.NodeTestTask.lambda$executeRecursively$8(NodeTestTask.java:123)
	at org.junit.platform.engine.support.hierarchical.ThrowableCollector.execute(ThrowableCollector.java:73)
	at org.junit.platform.engine.support.hierarchical.NodeTestTask.executeRecursively(NodeTestTask.java:122)
	at org.junit.platform.engine.support.hierarchical.NodeTestTask.execute(NodeTestTask.java:80)
	at java.base/java.util.ArrayList.forEach(ArrayList.java:1510)
	at org.junit.platform.engine.support.hierarchical.SameThreadHierarchicalTestExecutorService.invokeAll(SameThreadHierarchicalTestExecutorService.java:38)
	at org.junit.platform.engine.support.hierarchical.NodeTestTask.lambda$executeRecursively$5(NodeTestTask.java:139)
	at org.junit.platform.engine.support.hierarchical.ThrowableCollector.execute(ThrowableCollector.java:73)
	at org.junit.platform.engine.support.hierarchical.NodeTestTask.lambda$executeRecursively$7(NodeTestTask.java:125)
	at org.junit.platform.engine.support.hierarchical.Node.around(Node.java:135)
	at org.junit.platform.engine.support.hierarchical.NodeTestTask.lambda$executeRecursively$8(NodeTestTask.java:123)
	at org.junit.platform.engine.support.hierarchical.ThrowableCollector.execute(ThrowableCollector.java:73)
	at org.junit.platform.engine.support.hierarchical.NodeTestTask.executeRecursively(NodeTestTask.java:122)
	at org.junit.platform.engine.support.hierarchical.NodeTestTask.execute(NodeTestTask.java:80)
	at java.base/java.util.ArrayList.forEach(ArrayList.java:1510)
	at org.junit.platform.engine.support.hierarchical.SameThreadHierarchicalTestExecutorService.invokeAll(SameThreadHierarchicalTestExecutorService.java:38)
	at org.junit.platform.engine.support.hierarchical.NodeTestTask.lambda$executeRecursively$5(NodeTestTask.java:139)
	at org.junit.platform.engine.support.hierarchical.ThrowableCollector.execute(ThrowableCollector.java:73)
	at org.junit.platform.engine.support.hierarchical.NodeTestTask.lambda$executeRecursively$7(NodeTestTask.java:125)
	at org.junit.platform.engine.support.hierarchical.Node.around(Node.java:135)
	at org.junit.platform.engine.support.hierarchical.NodeTestTask.lambda$executeRecursively$8(NodeTestTask.java:123)
	at org.junit.platform.engine.support.hierarchical.ThrowableCollector.execute(ThrowableCollector.java:73)
	at org.junit.platform.engine.support.hierarchical.NodeTestTask.executeRecursively(NodeTestTask.java:122)
	at org.junit.platform.engine.support.hierarchical.NodeTestTask.execute(NodeTestTask.java:80)
	at org.junit.platform.engine.support.hierarchical.SameThreadHierarchicalTestExecutorService.submit(SameThreadHierarchicalTestExecutorService.java:32)
	at org.junit.platform.engine.support.hierarchical.HierarchicalTestExecutor.execute(HierarchicalTestExecutor.java:57)
	at org.junit.platform.engine.support.hierarchical.HierarchicalTestEngine.execute(HierarchicalTestEngine.java:51)
	at org.junit.platform.launcher.core.DefaultLauncher.execute(DefaultLauncher.java:248)
	at org.junit.platform.launcher.core.DefaultLauncher.lambda$execute$5(DefaultLauncher.java:211)
	at org.junit.platform.launcher.core.DefaultLauncher.withInterceptedStreams(DefaultLauncher.java:226)
	at org.junit.platform.launcher.core.DefaultLauncher.execute(DefaultLauncher.java:199)
	at org.junit.platform.launcher.core.DefaultLauncher.execute(DefaultLauncher.java:132)
	at org.gradle.api.internal.tasks.testing.junitplatform.JUnitPlatformTestClassProcessor$CollectAllTestClassesExecutor.processAllTestClasses(JUnitPlatformTestClassProcessor.java:99)
	at org.gradle.api.internal.tasks.testing.junitplatform.JUnitPlatformTestClassProcessor$CollectAllTestClassesExecutor.access$000(JUnitPlatformTestClassProcessor.java:79)
	at org.gradle.api.internal.tasks.testing.junitplatform.JUnitPlatformTestClassProcessor.stop(JUnitPlatformTestClassProcessor.java:75)
	at org.gradle.api.internal.tasks.testing.SuiteTestClassProcessor.stop(SuiteTestClassProcessor.java:61)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:564)
	at org.gradle.internal.dispatch.ReflectionDispatch.dispatch(ReflectionDispatch.java:36)
	at org.gradle.internal.dispatch.ReflectionDispatch.dispatch(ReflectionDispatch.java:24)
	at org.gradle.internal.dispatch.ContextClassLoaderDispatch.dispatch(ContextClassLoaderDispatch.java:33)
	at org.gradle.internal.dispatch.ProxyDispatchAdapter$DispatchingInvocationHandler.invoke(ProxyDispatchAdapter.java:94)
	at com.sun.proxy.$Proxy2.stop(Unknown Source)
	at org.gradle.api.internal.tasks.testing.worker.TestWorker.stop(TestWorker.java:133)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:564)
	at org.gradle.internal.dispatch.ReflectionDispatch.dispatch(ReflectionDispatch.java:36)
	at org.gradle.internal.dispatch.ReflectionDispatch.dispatch(ReflectionDispatch.java:24)
	at org.gradle.internal.remote.internal.hub.MessageHubBackedObjectConnection$DispatchWrapper.dispatch(MessageHubBackedObjectConnection.java:182)
	at org.gradle.internal.remote.internal.hub.MessageHubBackedObjectConnection$DispatchWrapper.dispatch(MessageHubBackedObjectConnection.java:164)
	at org.gradle.internal.remote.internal.hub.MessageHub$Handler.run(MessageHub.java:414)
	at org.gradle.internal.concurrent.ExecutorPolicy$CatchAndRecordFailures.onExecute(ExecutorPolicy.java:64)
	at org.gradle.internal.concurrent.ManagedExecutorImpl$1.run(ManagedExecutorImpl.java:48)
	at java.base/java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1130)
	at java.base/java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:630)
	at org.gradle.internal.concurrent.ThreadFactoryImpl$ManagedThreadRunnable.run(ThreadFactoryImpl.java:56)
	at java.base/java.lang.Thread.run(Thread.java:832)
Caused by: org.hibernate.InstantiationException: No default constructor for entity:  : com.example.exampleproject.models.Book
	at org.hibernate.tuple.PojoInstantiator.instantiate(PojoInstantiator.java:85)
	at org.hibernate.tuple.PojoInstantiator.instantiate(PojoInstantiator.java:105)
	at org.hibernate.tuple.entity.AbstractEntityTuplizer.instantiate(AbstractEntityTuplizer.java:704)
	at org.hibernate.persister.entity.AbstractEntityPersister.instantiate(AbstractEntityPersister.java:5165)
	at org.hibernate.internal.SessionImpl.instantiate(SessionImpl.java:1599)
	at org.hibernate.internal.SessionImpl.instantiate(SessionImpl.java:1583)
	at org.hibernate.loader.Loader.instanceNotYetLoaded(Loader.java:1799)
	at org.hibernate.loader.Loader.getRow(Loader.java:1660)
	at org.hibernate.loader.Loader.getRowFromResultSet(Loader.java:745)
	at org.hibernate.loader.Loader.getRowsFromResultSet(Loader.java:1044)
	at org.hibernate.loader.Loader.processResultSet(Loader.java:995)
	at org.hibernate.loader.Loader.doQuery(Loader.java:964)
	at org.hibernate.loader.Loader.doQueryAndInitializeNonLazyCollections(Loader.java:350)
	at org.hibernate.loader.Loader.doList(Loader.java:2887)
	at org.hibernate.loader.Loader.doList(Loader.java:2869)
	at org.hibernate.loader.Loader.listIgnoreQueryCache(Loader.java:2701)
	at org.hibernate.loader.Loader.list(Loader.java:2696)
	at org.hibernate.loader.hql.QueryLoader.list(QueryLoader.java:506)
	at org.hibernate.hql.internal.ast.QueryTranslatorImpl.list(QueryTranslatorImpl.java:400)
	at org.hibernate.engine.query.spi.HQLQueryPlan.performList(HQLQueryPlan.java:219)
	at org.hibernate.internal.SessionImpl.list(SessionImpl.java:1415)
	at org.hibernate.query.internal.AbstractProducedQuery.doList(AbstractProducedQuery.java:1565)
	at org.hibernate.query.internal.AbstractProducedQuery.list(AbstractProducedQuery.java:1533)
	at org.hibernate.query.Query.getResultList(Query.java:165)
	at org.hibernate.query.criteria.internal.compile.CriteriaQueryTypeQueryAdapter.getResultList(CriteriaQueryTypeQueryAdapter.java:76)
	at org.springframework.data.jpa.repository.support.SimpleJpaRepository.findAll(SimpleJpaRepository.java:355)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at java.base/jdk.internal.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at java.base/jdk.internal.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.base/java.lang.reflect.Method.invoke(Method.java:564)
	at org.springframework.data.repository.core.support.ImplementationInvocationMetadata.invoke(ImplementationInvocationMetadata.java:72)
	at org.springframework.data.repository.core.support.RepositoryComposition$RepositoryFragments.invoke(RepositoryComposition.java:382)
	at org.springframework.data.repository.core.support.RepositoryComposition.invoke(RepositoryComposition.java:205)
	at org.springframework.data.repository.core.support.RepositoryFactorySupport$ImplementationMethodExecutionInterceptor.invoke(RepositoryFactorySupport.java:549)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186)
	at org.springframework.data.repository.core.support.QueryExecutorMethodInterceptor.doInvoke(QueryExecutorMethodInterceptor.java:155)
	at org.springframework.data.repository.core.support.QueryExecutorMethodInterceptor.invoke(QueryExecutorMethodInterceptor.java:130)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186)
	at org.springframework.data.projection.DefaultMethodInvokingMethodInterceptor.invoke(DefaultMethodInvokingMethodInterceptor.java:80)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186)
	at org.springframework.transaction.interceptor.TransactionAspectSupport.invokeWithinTransaction(TransactionAspectSupport.java:367)
	at org.springframework.transaction.interceptor.TransactionInterceptor.invoke(TransactionInterceptor.java:118)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:186)
	at org.springframework.dao.support.PersistenceExceptionTranslationInterceptor.invoke(PersistenceExceptionTranslationInterceptor.java:139)
	... 104 more
```

After creating a default constructor for `Book` class, it worked. It's an empty constructor

```shell script
$ ./gradlew test

> Task :test
2020-08-27 00:04:34 INFO  o.s.o.j.LocalContainerEntityManagerFactoryBean - Closing JPA EntityManagerFactory for persistence unit 'default'
2020-08-27 00:04:34 INFO  o.h.t.s.i.SchemaDropperImpl$DelayedDropActionImpl - HHH000477: Starting delayed evictData of schema as part of SessionFactory shut-down'
2020-08-27 00:04:35 DEBUG org.hibernate.SQL - drop table if exists book cascade
2020-08-27 00:04:35 DEBUG org.hibernate.SQL - drop sequence if exists hibernate_sequence
2020-08-27 00:04:35 INFO  o.s.s.c.ThreadPoolTaskExecutor - Shutting down ExecutorService 'applicationTaskExecutor'
2020-08-27 00:04:35 INFO  com.zaxxer.hikari.HikariDataSource - HikariPool-1 - Shutdown initiated...
2020-08-27 00:04:35 INFO  com.zaxxer.hikari.HikariDataSource - HikariPool-1 - Shutdown completed.

BUILD SUCCESSFUL in 5s
4 actionable tasks: 2 executed, 2 up-to-date
```

Now, what's pending is, trying to understand what ALL happened BEHIND the scenes.

---

https://www.callicoder.com/spring-boot-jpa-hibernate-postgresql-restful-crud-api-example/

Adding this to the `application.properties`

```properties
# The SQL dialect makes Hibernate generate better SQL for the chosen database
spring.jpa.properties.hibernate.dialect = org.hibernate.dialect.PostgreSQLDialect
```

Auditing related fields - `createdAt`, `updatedAt` - How spring helps with it
https://docs.spring.io/spring-data/jpa/docs/current/reference/html/#jpa.auditing

EntityListeners
https://docs.oracle.com/javaee/7/api/javax/persistence/EntityListeners.html

EnableJpaAuditing Annotation
https://docs.spring.io/spring-data/jpa/docs/current/api/org/springframework/data/jpa/repository/config/EnableJpaAuditing.html

There's something called "Configuration Classes"

I understand there are models which are domain models - classes that map to tables in the
database. 

For generating ID, there's a SequenceGenerator being used
https://docs.oracle.com/javaee/7/api/javax/persistence/SequenceGenerator.html

There's a relationship being defined with `@ManyToOne` and how to join the tables
using a foreign key column, and what to do when a related question is deleted - 
cascade the delete to delete the answers too `@OnDelete(action = OnDeleteAction.CASCADE)`
and question is present as a field in `Answer` class and it's ignored in the Json for
serialization in responses I think

Have to check what are the features provided by `JpaRepository`

There's something called `ResponseEntity` for responses in Spring

There's something called `Page` and `Pageable` and it allows pagination,
along with sorting, page size too!

Some more articles
https://developer.okta.com/blog/2018/12/13/build-basic-app-spring-boot-jpa#add-a-domain-class-with-spring-data-and-jpa
https://mkyong.com/spring-boot/spring-boot-spring-data-jpa-postgresql/

---

I heard that the `AutoWired` annotation is not a good thing. Gotta check that too.
