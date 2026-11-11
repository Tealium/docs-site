---
title: Adobe Target コネクタ構成ガイド
description: この記事では、Adobe Target コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-target-connector/
---
## API 情報

このコネクタは、次のベンダー API を使用します。

* API 名：Adobe Profile API
* API エンドポイント：`https://your-client-code.tt.omtrdc.net/m2/client/profile/update`。`your-client-code` は Adobe Target インスタンス ID です。
* ドキュメント：[Adobe：Profile API の構成](https://experienceleague.adobe.com/en/docs/target-dev/developer/implementation/methods/profile-api-settings)

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加したら、次の項目を構成します。

* **認証トークン**：（任意）Profile API の構成で **Require Authentication** が有効になっている場合は、認証トークンを指定します。トークンの有効期限は Profile API の構成に表示されます。詳細については、[Adobe Target：Profile API の構成](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/methods/profile-api-settings.html)を参照してください。

コネクタを構成したら、**完了**をクリックします。


<blockquote>
新しいサイト訪問のビジタープロファイルを作成するための十分な時間を Adobe Target に与えるため、トリガーを **訪問終了時にオーディエンスに属している** に構成するか、1 時間の[遅延アクション](https://docs.tealium.com/about-delayed-actions/)を使用することをお勧めします。
</blockquote>


## アクション

| アクション名 | ビジタープロファイル | イベントデータ |
| --- | :---: | :---: |
| 単一プロファイルの更新 | ✓ | ✗ |

アクションの名前を入力し、**アクションタイプ**を選択します。

次のセクションでは、各アクションのパラメーターとオプションを構成する方法について説明します。

### 単一プロファイルの更新

#### パラメーター

|**パラメーター**| **説明**|
|---| ---|
|Client| <ul><li>Adobe から提供されたクライアントコード。この値は、API エンドポイント内に次のように表示されます：`https://your-client-code.tt.omtrdc.net/m2/client/profile/update`</li></ul> |
|mboxpcID| <ul><li>mboxpcID または mbox3rdPartyId のいずれかが必要です。詳細については、[Adobe Target：プロファイルの更新](https://experienceleague.adobe.com/en/docs/target-dev/developer/api/profile-apis/profile-single-api)を参照してください。</li></ul> |
|mbox3rdPartyId| <ul><li>mboxpcID または mbox3rdPartyId のいずれかが必要です。詳細については、[Adobe Target：プロファイルの更新](https://experienceleague.adobe.com/en/docs/target-dev/developer/api/profile-apis/profile-single-api)を参照してください。</li></ul> |
|Attributes| <ul><li>パラメーターの形式は `profile.paramName` です。</li><li>すべての pcId または mbox3rdPartyId に、すべてのパラメーター値が存在する必要はありません。</li><li>パラメーターと値では大文字と小文字が区別されます。</li><li>現在の GET のサイズ上限は 8 KB です。</li><li>プロファイル更新 API の呼び出しは、mbox の課金対象には含まれません。</li></ul> |