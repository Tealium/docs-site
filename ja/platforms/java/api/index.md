---
title: APIリファレンス
description: TealiumがJava向けに提供するクラスメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/java/api/
---
## クラス: `Tealium`

以下は、Javaの `Tealium` クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| `addPersistentData()` | `DataManager`を使用して、複数のアプリセッションセッションでデータを利用可能にします |
| `deletePersistentData()` | `DataManager`を使用して、削除するキーのリストを提供することで、以前に永続化されたデータを削除します |
| `getDataManager()` | コールタイムデータを処理し、永続データを処理する`DataManager`オブジェクトを取得します |
| `getPersistentData()` | `DataManager`を使用して、永続化されたデータを取得します |
| `getSessionId()` | `DataManager`を使用して、現在のセッションIDを取得します  |
| `resetSessionId()` | `DataManager`を使用して、セッションIDをリセットします |
| `track()` | イベントをトラックします |

### `addPersistentData()`

`DataManager`を使用して、複数のアプリセッションセッションでデータを利用可能にします。

```java
addPersistentData(data)
```

| パラメータ | タイプ | 説明  | 例 |
| --- | --- | --- | --- |
| `data` | `Map&lt;String, Object&gt;` | 既存の永続的な`Udo`に追加するための必須のマップデータ | `[&#34;key&#34;:&#34;value&#34;]` |

```java
Udo data = new Udo();
data.put(&#34;KEY&#34;, &#34;VALUE&#34;);
tealium.getDataManager().addPersistentData(data);
```

### `deletePersistentData()`

`DataManager`を使用して、削除するキーのリストを提供することで、以前に永続化されたデータを削除します。

```java
deletePersistentData(list)
```

| パラメータ |  タイプ |説明 | 例 |
| --- | --- | --- | --- |
| `list` |  `List&lt;String&gt;` | 文字列としてのキーのリスト | `[&#34;key1&#34;, &#34;key2&#34;]` |

```java
List&lt;String&gt; list = new List&lt;&gt;();
list.append(&#34;key_to_delete&#34;);
tealium.getDataManager().deletePersistentData(list);
```

### `getDataManager()`

コールタイムデータを処理し、永続データを処理する`DataManager`オブジェクトを取得します。

```java
getDataManager()
```

| 戻り値のタイプ | 説明 |
| --- | --- |
| `DataManager` | Tealiumの `DataManager` オブジェクトのインスタンス |

```java
DataManager dm = tealium.getDataManager()
```


### `getPersistentData()`

`DataManager`を使用して、永続化されたデータを取得します。

```java
getPersistentData()
```

| 戻り値のタイプ | 説明 | 例 |
| --- | --- | --- |
| `Udo` | 永続データのユニバーサルデータオブジェクト (UDO) | `[&#34;key1&#34;, &#34;key2&#34;]` |

```java
Udo persistentData = tealium.getDataManager().getPersistentData()
```

### `getSessionId()`

`DataManager`を使用して、現在のセッションIDを取得します。セッションIDは、`Tealium`オブジェクトの初期化時に作成されます。

```java
getSessionId()
```

| 戻り値のタイプ | 説明 | 例  |
| --- | --- | --- |
| `String` | ミリ秒単位のタイムスタンプの表現 | `&#34;1473371215123&#34;` |

```java
tealium.getDataManager().getSessionId() 
```


### `resetSessionId()`

`DataManager`を使用して、セッションIDをリセットします。アプリの起動時以外に新しいセッションを開始する必要がある場合に使用します。

```java
resetSessionId()
```

| 戻り値のタイプ | 説明 | 例 |
| --- | --- | --- |
| `String` | ミリ秒単位のタイムスタンプの新しい文字列表現。これは、現在のセッションの残りの期間、すべてのディスパッチに追加されます。このメソッドが呼び出されると、自動的に揮発性データストアに追加されるため、返される文字列は監視の便宜上です。 | `&#34;1473371215123&#34;` |

```java
tealium.getDataManager().resetSessionId()
```


### `track()`

イベントをトラックします。

```java
track(eventTitle)
```

データとコールバックのオプションパラメータを持つイベントをトラックします。

```java
track(eventTitle, data, callback)
```

| パラメータ | タイプ | 説明 |  例 |
|-----------|-------------|------| --- |
| `eventTitle` | `String` |イベントのタイトル（`tealium_event`と`event_name`イベント属性値になります） |  `&#34;Some Event&#34;` |
| `data`    | `Udo` |  (オプション) キーと値のペアとしてのイベントデータを持つユニバーサルデータオブジェクト (UDO)| `udoObject` |
| `callback`| `DispatchCallback` |(オプション) &#34;callback&#34;キーに関数が割り当てられたオブジェクト | `dispatchCallbackObject` |


## クラス: `Tealium.Builder`

以下は、Javaの `Tealium.Builder` クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| `build()` | ビルドを実行し、永続データと収集ディスパッチャを構成します |
| `Builder()` | Tealiumオブジェクトをインスタンス化するためのコンストラクタ |
| `setDatasource()` | データソースキー |
| `setEnvironment()` | Tealiumの環境名を構成します |  
| `setPersistentData()` | 永続データを構成します |

### `build()`

ビルドを実行します。`setPersistentData()`メソッドで明示的に構成されていない場合、永続データを構成します。setCollectDispatcher()メソッドで明示的に構成されていない場合、収集ディスパッチャを構成します。

```java
tealium.build();
```

### `Builder()`

Tealiumオブジェクトをインスタンス化するためのコンストラクタ。

```java
Tealium.Builder(account, profile, environment).build()
```

```java
// Init Tealium
Tealium tealium = new Tealium.Builder(account, profile)
    .setEnvironment(environment)
    .setDatasource(datasource)
    .build();
```

| パラメータ |  タイプ | 説明 |  例 |
| --- | --- | --- | --- |
| `account` |  `String` |Tealiumのアカウント名 | `&#34;companyXYZ&#34;` |
| `profile` |  `String` |Tealiumのプロファイル名  | `&#34;main&#34;` |
| `environment` |  `String` |Tealiumの環境名  | [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |
| `datasource` |  `String` |(オプション) データソースキー（ない場合は`null`に構成）  | `&#34;abc123&#34;` |

### `setDatasource() `  

データソースキーを構成します。ない場合は`null`に構成します。

```java
tealium.setEnvironment(datasource);
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `datasource` | `String` | データソースキー（ない場合は`null`に構成）  |  `&#34;abc123&#34;` |

### `setEnvironment()`   

Tealiumの環境名を構成します

```java
tealium.setEnvironment(environment);
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `environment` | `String` |Tealiumの環境名 |  [`&#34;dev&#34;`, `&#34;qa&#34;`, `&#34;prod&#34;`] |


### `setPersistentData()`   

永続データを構成します。

```java
tealium.setPersistentData(persistentData);
```

| パラメータ | タイプ | 説明 |  例 |
| --- | --- | --- | --- |
| `persistentData` | `PersistentUdo` | 永続的なUdoデータオブジェクト | `persistentUdoObj` |
