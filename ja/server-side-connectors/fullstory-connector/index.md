---
title: FullStoryコネクタ構成ガイド
description: この記事では、FullStoryコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/fullstory-connector/
---
## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|ユーザーの削除| ✓| ✓|

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、次の構成を行います。

* **APIキー**

## アクション構成 - パラメータとオプション

**続行**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### アクション - ユーザーの削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ユーザーID| <ul><li>ユーザーIDは、FullStoryタグを介して渡される、ユーザーに割り当てたアプリケーション固有のIDです。</li><li>この機能を使用して、エンドユーザーからの「忘れられる権利」または「消去権」に基づく要求に対応します。</li><li>このエンドポイントの詳細については、[FullStoryのドキュメント](https://help.fullstory.com/develop-rest/deleteindividual-api)を参照してください。</li><li>推奨されるベストプラクティス：<ul><li>FullStoryタグでユーザーIDにマッピングする識別子として、ハッシュ化されたメールアドレスを選択します。</li><li>この推奨事項またはユーザーIDを選択する別の方法について詳しくは、TealiumまたはFullStoryの担当者にお問い合わせください。</li></ul> </li></ul> |