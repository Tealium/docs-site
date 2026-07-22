---
title: FullStoryコネクタ構成ガイド
description: この記事では、FullStoryコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/fullstory-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|ユーザー削除| ✓| ✓|

## 構成の構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタの追加方法については、[コネクタ概要](https://docs.tealium.com/about-connectors/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **APIキー**

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - ユーザー削除

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|ユーザーID|  <ul><li>ユーザーIDは、FullStoryタグを通じてユーザーに渡された、あなたのアプリケーション固有のIDです。</li><li>この機能を使用して、エンドユーザーからの忘れられる権利/消去の権利の要求に対応します。</li><li>このエンドポイントについての詳細は、[FullStoryのドキュメンテーション](https://help.fullstory.com/develop-rest/deleteindividual-api)を参照してください。</li><li>推奨されるベストプラクティス：  <ul><li>FullStoryタグのユーザーIDにマップされる識別子としてハッシュ化されたメールを選択します。</li><li>この推奨事項やユーザーIDの選択に関する代替的なアプローチについての詳細は、TealiumまたはFullStoryの担当者にお問い合わせください。</li></ul> </li></ul> |
