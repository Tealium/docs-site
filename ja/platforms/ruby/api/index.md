---
title: APIリファレンス
description: TealiumがRuby向けに提供するクラスとメソッドのリファレンスガイド。
url: https://docs.tealium.com/ja/platforms/ruby/api/
---
## クラス: `Tealium`

以下は、Rubyライブラリの`Tealium`クラスの一般的に使用されるメソッドをまとめたものです。

| メソッド | 説明 |
| ----- | ------ |
| `initialize()` | Tealiumインスタンスを初期化します。`Tealium.new `を介して呼び出されます。|
| `track()` | イベントを追跡します。 |



### `initialize()`

Tealiumインスタンスを初期化します。

```ruby
initialize(account, profile, datasource)
```

| パラメータ | タイプ | 説明 | 例 |
| --- | --- | --- | --- |
| `account` | `String` | Tealiumのアカウント名 | `&#34;account123&#34;` |
| `profile` | `String` | Tealiumのプロファイル名 | `&#34;main&#34;` |
| `datasource` | String | データソースキー（提供されていない場合は`nil`） | `&#34;abc123&#34;` |

 `Tealium.new`のようにTealiumクラスに`new`メソッドを呼び出すと、クラスは自身の新しいインスタンスを作成します。その後、内部的に新しいオブジェクトの`initialize()`メソッドを呼び出します。これにより、`new`に渡したすべての引数が`initialize()`メソッドに渡されます。

### `track()`

イベントを追跡します。

```ruby
track(event_name, data)
```

| パラメータ | タイプ |  説明 | 例 |
|------|------|-------| ------|
| `event`   | `String` |追跡されるイベントのタイトル |  `&#34;some event&#34;` |
| `data`    | `Hash` | (オプション) キーと値のペアとしてのイベントデータ |  `{:key =&gt; &#34;value&#34;}` |

