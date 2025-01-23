# HotswapAgent Gretty Issue

## Steps for reproducing the issue:
   
 1. Make sure you use JetBrains Java 17:
    ```
    java -version
    ```
   
    The output should be something like this:
   
    ```
    openjdk version "17.0.12" 2024-07-16
    OpenJDK Runtime Environment JBR-17.0.12+1-1087.25-jcef (build 17.0.12+1-b1087.25)
    OpenJDK 64-Bit Server VM JBR-17.0.12+1-1087.25-jcef (build 17.0.12+1-b1087.25, mixed mode)
    ```
   
 2. Clone and start the application:
    ```
    git clone git@github.com:haba713/hotswapagent-gretty-issue.git
    cd hotswapagent-gretty-issue/
    ./gradlew appRun
    ```
   
    See the exception: `ERROR (org.hotswap.agent.annotation.handler.PluginClassFileTransformer) - InvocationTargetException in transform method on plugin 'class org.hotswap.agent.plugin.jetty.JettyPlugin' class 'org/eclipse/jetty/webapp/WebXmlConfiguration' of classLoader 'java.net.URLClassLoader'`
   
 3. In [build.gradle], change the servlet container:
    `servletContainer = 'jetty11'` → `servletContainer = 'tomcat10'`
   
 4. Start the application:
    ```
    ./gradlew appRun
    ```
   
    See the exception: `ERROR (org.hotswap.agent.annotation.handler.PluginClassFileTransformer) - InvocationTargetException in transform method on plugin 'class org.hotswap.agent.plugin.tomcat.TomcatPlugin' class 'org/apache/catalina/webresources/StandardRoot' of classLoader 'java.net.URLClassLoader'`

## Environment

```
$ hotswapagent-gretty-issue/gradlew -v

------------------------------------------------------------
Gradle 8.12
------------------------------------------------------------

Build time:    2024-12-20 15:46:53 UTC
Revision:      a3cacb207fec727859be9354c1937da2e59004c1

Kotlin:        2.0.21
Groovy:        3.0.22
Ant:           Apache Ant(TM) version 1.10.15 compiled on August 25 2024
Launcher JVM:  17.0.12 (JetBrains s.r.o. 17.0.12+1-b1087.25)
Daemon JVM:    /Users/u0/.sdkman/candidates/java/17.0.12-jbr (no JDK specified, using current Java home)
OS:            Mac OS X 14.7.2 aarch64
```


[build.gradle]: build.gradle