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
| `account` | `String` | Tealiumのアカウント名 | `"account123"` |
| `profile` | `String` | Tealiumのプロファイル名 | `"main"` |
| `datasource` | String | データソースキー（提供されていない場合は`nil`） | `"abc123"` |


<blockquote>
`Tealium.new`のようにTealiumクラスに`new`メソッドを呼び出すと、クラスは自身の新しいインスタンスを作成します。その後、内部的に新しいオブジェクトの`initialize()`メソッドを呼び出します。これにより、`new`に渡したすべての引数が`initialize()`メソッドに渡されます。
</blockquote>


### `track()`

イベントを追跡します。

```ruby
track(event_name, data)
```

| パラメータ | タイプ |  説明 | 例 |
|------|------|-------| ------|
| `event`   | `String` |追跡されるイベントのタイトル |  `"some event"` |
| `data`    | `Hash` | (オプション) キーと値のペアとしてのイベントデータ |  `{:key => "value"}` |

