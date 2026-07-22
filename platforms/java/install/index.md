---
title: Install
description: Learn to install Tealium for Java.
url: https://docs.tealium.com/platforms/java/install/
---
## Requirements

* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)
* Java IDE such as Eclipse or NetBeans
* Java JDK 7+

## Install

Install Tealium for Java with Maven or manually.

### Maven

To install the Tealium library for Java with Maven, make the following changes to your `pom.xml` file:

1. Add the repository:
      ```xml
      <repository>    
        <id>maven-tealium</id>
        <url>https://maven.tealiumiq.com/java/releases/</url>
      </repository>
      ```

2. Add the dependency:
      ```xml
      <groupId>com.tealium</groupId>
      <artifactId>java</artifactId>
      <version>1.4.0</version>
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

To initialize the `Tealium` instance with the [`Builder()`](https://docs.tealium.com/platforms/java/api/#builder) method, add the following code to your `main` or `util` class and ensure that it initializes before any calls to it are made:

```java
Tealium tealium = new Tealium.Builder("ACCOUNT", "PROFILE")
    .setEnvironment("ENVIRONMENT")
    .setDatasource("DATASOURCE")
    .build();
```
