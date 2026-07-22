---
title: Crazy Eggタグ構成ガイド
description: この記事では、Crazy Eggタグの構成方法について説明します。
url: https://docs.tealium.com/ja/client-side-tags/crazy-egg-tag/
---
## タグの仕様と要件

### 仕様

**名前**: Crazy Egg

**ベンダー**: Crazy Egg

**タイプ**: その他: ヒートマッピング

##### 必須

**サービス**: Crazy Eggアカウント

**構成**:

* アカウント

## Tealium iQでのタグ構成

### タグを追加する

Tealium iQのタグマーケットプレイスは、さまざまなタグを提供しています。プロファイルにタグを追加する方法については、[こちら](https://docs.tealium.com/manage-tags/)をクリックしてください。

### タグを構成する

Crazy Eggタグをロードするための必須のタグ構成のリストは以下の通りです:

1. **タイトル** (必須): タグを識別するための記述的なタイトルを入力します。
1. **アカウント** (必須): Crazy Eggのアカウント番号を入力します。

**ヒント**: このタグを**タグ**タブのリストの上部近くに配置することで、できるだけ早くロードされるようにします。タグが早くロードされるほど、訪問の活動を早くキャプチャできます。

### ロードルールを適用する

[ロードルール](https://docs.tealium.com/about-load-rules/)は、このタグのインスタンスをいつ、どこでロードするかを決定します。**すべてのページに表示**ルールは、デフォルトのロードルールです。特定のページでこのタグをロードするには、関連する条件で新しいロードルールを作成します。

**注**: ヒートマップを生成しようとしているページだけでこのタグをロードするためのロードルールを作成することをお勧めします。

### マッピングの構成

[マッピング](https://docs.tealium.com/about-data-mappings/)は、データレイヤーのデータソースからベンダータグの対応する宛先変数にデータを送信するプロセスです。

Crazy Eggの場合、Tealium iQではマッピングはサポートされていません。デフォルトでは、Crazy Eggのライブラリはデータをキャプチャし、それをCrazy Eggのレポートに送信します。カスタムユーザー変数1から5を使用するには、次のメソッド定義をコールバック関数に渡す必要があります:

```
window.CE_READY = function CE_READY() {
CE2.set(1, 'some string');
CE2.set(2, 'another value');
CE2.set(3, 'yet another value');
CE2.set(4, 'more');
CE2.set(5, 'and more');
}
```

----

## ベンダーのドキュメンテーション

* [Crazy Eggサポート](http://support.crazyegg.com/)

