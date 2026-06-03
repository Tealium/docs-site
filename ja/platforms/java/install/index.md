---
title: インストール
description: Java用Tealiumのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/java/install/
---
## 要件

* [Tealium Customer Data Hubアカウント]()
* EclipseやNetBeansなどのJava IDE
* Java JDK 7&#43;

## インストール

Mavenを使用してJava用Tealiumをインストールするか、手動で行います。

### Maven

Java用のTealiumライブラリをMavenでインストールするには、`pom.xml`ファイルに以下の変更を加えます：

1. リポジトリを追加します：
      ```xml
      &lt;repository&gt;    
        &lt;id&gt;maven-tealium&lt;/id&gt;
        &lt;url&gt;https://maven.tealiumiq.com/java/releases/&lt;/url&gt;
      &lt;/repository&gt;
      ```

2. 依存関係を追加します：
      ```xml
      &lt;groupId&gt;com.tealium&lt;/groupId&gt;
      &lt;artifactId&gt;java&lt;/artifactId&gt;
      &lt;version&gt;1.4.0&lt;/version&gt;
      ```

### 手動

Java用のTealiumライブラリを手動でインストールするには：

1. GitHubから[Java用のTealium](https://github.com/tealium/tealium-java)コードをクローンします。ダウンロードするのではなく、ライブラリをクローンすることで、将来のリリースに簡単に更新できます。

2. `src/main/java/com/tealium/`ディレクトリからすべてのJavaファイルをインポートします。

3. コードに以下のインポート文を追加します：  
      ```java
      import com.tealium.*
      ```

## 初期化

[`Builder()`](/ja/platforms/java/api/#builder)メソッドを使用して`Tealium`インスタンスを初期化するには、以下のコードを`main`または`util`クラスに追加し、それが呼び出される前に初期化されることを確認します：

```java
Tealium tealium = new Tealium.Builder(&#34;ACCOUNT&#34;, &#34;PROFILE&#34;)
    .setEnvironment(&#34;ENVIRONMENT&#34;)
    .setDatasource(&#34;DATASOURCE&#34;)
    .build();
```