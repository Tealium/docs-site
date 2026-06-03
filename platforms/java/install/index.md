---
title: Install
description: Learn to install Tealium for Java.
url: https://docs.tealium.com/platforms/java/install/
---
## Requirements

* [Tealium Customer Data Hub account]()
* Java IDE such as Eclipse or NetBeans
* Java JDK 7&#43;

## Install

Install Tealium for Java with Maven or manually.

### Maven

To install the Tealium library for Java with Maven, make the following changes to your `pom.xml` file:

1. Add the repository:
      ```xml
      &lt;repository&gt;    
        &lt;id&gt;maven-tealium&lt;/id&gt;
        &lt;url&gt;https://maven.tealiumiq.com/java/releases/&lt;/url&gt;
      &lt;/repository&gt;
      ```

2. Add the dependency:
      ```xml
      &lt;groupId&gt;com.tealium&lt;/groupId&gt;
      &lt;artifactId&gt;java&lt;/artifactId&gt;
      &lt;version&gt;1.4.0&lt;/version&gt;
      ```

### Manual

To install the Tealium library for Java manually:

1. Clone the [Tealium for Java](https://github.com/tealium/tealium-java) code from GitHub. Cloning the library, rather than downloading, makes it easier to update to future releases.

2. Import all of the Java files from the `src/main/java/com/tealium/` directory.

3. Add the following import statement in your code:  
      ```java
      import com.tealium.*
      ```

## Initialize

To initialize the `Tealium` instance with the [`Builder()`](/platforms/java/api/#builder) method, add the following code to your `main` or `util` class and ensure that it initializes before any calls to it are made:

```java
Tealium tealium = new Tealium.Builder(&#34;ACCOUNT&#34;, &#34;PROFILE&#34;)
    .setEnvironment(&#34;ENVIRONMENT&#34;)
    .setDatasource(&#34;DATASOURCE&#34;)
    .build();
```
