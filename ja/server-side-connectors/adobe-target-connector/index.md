---
title: Adobe Target コネクタ構成ガイド
description: この記事では、Adobe Target コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/adobe-target-connector/
---
## API 情報

このコネクタは以下のベンダー API を使用します：

* API 名：Adobe Profile API
* API エンドポイント：`https://your-client-code.tt.omtrdc.net/m2/client/profile/update`、ここで `your-client-code` はあなたの Adobe Target インスタンス ID です。
* ドキュメント：[Adobe: Profile API 構成](https://experienceleague.adobe.com/en/docs/target-dev/developer/implementation/methods/profile-api-settings)

## 構成

コネクタマーケットプレイスにアクセスして新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタについて]() の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

* **認証トークン**：（オプション）Profile API 構成で **認証が必要** が有効になっている場合、認証トークンを提供します。トークンの有効期限は Profile API 構成に表示されます。詳細については、[Adobe Target: Profile API 構成](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/methods/profile-api-settings.html) を参照してください。

 訪問のプロファイルを新規サイト訪問に対して Adobe Target が作成するのに十分な時間を確保するために、**訪問終了時にオーディエンス内** にトリガーを構成するか、1時間の [遅延アクション]() を使用することをお勧めします。 

## アクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
| シングルプロファイル更新 | ✓ | ✗ |

アクションの名前を入力し、**アクションタイプ**を選択します。

次のセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### シングルプロファイル更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|クライアント|  &lt;ul&gt;&lt;li&gt;Adobe によって提供されるクライアントコード。この値は API エンドポイントに次のように表示されます：`https://your-client-code.tt.omtrdc.net/m2/client/profile/update`&lt;/li&gt;&lt;/ul&gt; |
|mboxpcID|  &lt;ul&gt;&lt;li&gt;mboxpcID または mbox3rdPartyId のいずれかが必要です。詳細については、[Adobe Target: プロファイルの更新](https://experienceleague.adobe.com/en/docs/target-dev/developer/api/profile-apis/profile-single-api) を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|mbox3rdPartyId|  &lt;ul&gt;&lt;li&gt;mboxpcID または mbox3rdPartyId のいずれかが必要です。詳細については、[Adobe Target: プロファイルの更新](https://experienceleague.adobe.com/en/docs/target-dev/developer/api/profile-apis/profile-single-api) を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|属性|  &lt;ul&gt;&lt;li&gt;パラメータ形式は `profile.paramName` です。&lt;/li&gt;&lt;li&gt;すべての pcIds または mbox3rdPartyId に対してすべてのパラメータ値が存在する必要はありません。&lt;/li&gt;&lt;li&gt;パラメータと値は大文字と小文字が区別されます。&lt;/li&gt;&lt;li&gt;GET の現在のサイズ制限は 8 KB です。&lt;/li&gt;&lt;li&gt;プロファイル更新 API への呼び出しは mbox の料金には含まれません。&lt;/li&gt;&lt;/ul&gt; |