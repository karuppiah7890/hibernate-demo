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
2020-08-26 23:38:53 WARN  o.s.b.w.s.c.AnnotationConfigServletWebServerApplicationContext - Exception encountered during context initialization - cancelling refresh attempt: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'bookRepository' defined in com.example.exampleproject.repository.BookRepository defined in @EnableJpaRepositories declared on JpaRepositoriesRegistrar.EnableJpaRepositoriesConfiguration: Cannot resolve reference to bean 'jpaMappingContext' while setting bean property 'mappingContext'; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'jpaMappingContext': Invocation of init method failed; nested exception is org.hibernate.service.spi.ServiceException: Unable to create requested service [org.hibernate.engine.jdbc.env.spi.JdbcEnvironment]
2020-08-26 23:38:53 INFO  o.s.o.j.LocalContainerEntityManagerFactoryBean - Closing JPA EntityManagerFactory for persistence unit 'default'
2020-08-26 23:38:53 WARN  o.s.b.f.s.DisposableBeanAdapter - Invocation of destroy method failed on bean with name 'entityManagerFactory': org.hibernate.service.spi.ServiceException: Unable to create requested service [org.hibernate.engine.jdbc.env.spi.JdbcEnvironment]
2020-08-26 23:38:53 INFO  o.s.s.c.ThreadPoolTaskExecutor - Shutting down ExecutorService 'applicationTaskExecutor'
2020-08-26 23:38:53 INFO  o.a.catalina.core.StandardService - Stopping service [Tomcat]
2020-08-26 23:38:53 INFO  o.s.b.a.l.ConditionEvaluationReportLoggingListener -

Error starting ApplicationContext. To display the conditions report re-run your application with 'debug' enabled.
2020-08-26 23:38:53 ERROR o.s.boot.SpringApplication - Application run failed
org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'bookRepository' defined in com.example.exampleproject.repository.BookRepository defined in @EnableJpaRepositories declared on JpaRepositoriesRegistrar.EnableJpaRepositoriesConfiguration: Cannot resolve reference to bean 'jpaMappingContext' while setting bean property 'mappingContext'; nested exception is org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'jpaMappingContext': Invocation of init method failed; nested exception is org.hibernate.service.spi.ServiceException: Unable to create requested service [org.hibernate.engine.jdbc.env.spi.JdbcEnvironment]
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
