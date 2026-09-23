---
title: Google AdsカスタマーマッチアクションをGoogle Data Manager APIに移行する
description: この記事では、新しいGoogle AdsカスタマーマッチアクションがGoogle Data Manager APIを使用する理由と、既存のGoogle Ads APIベースのアクションからの移行方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/google-ads-customer-match-data-manager-api-migration/
---
## 変更点

[Google Adsカスタマーマッチコネクター](https://docs.tealium.com/google-ads-customer-match-connector/)に、Google Data Manager APIを使用する2つの新しいアクションを導入します：

* リストへのユーザー追加（Data Manager API）
* リストからのユーザー削除（Data Manager API）

これらのアクションは、コネクターUIの既存のリストへのユーザー追加およびリストからのユーザー削除アクションを密接に反映して設計されており、レガシーのGoogle Ads APIではなくGoogleのData Manager APIを通じてオーディエンス更新を送信します。

さらに、コネクターの構成には、Google AdsアカウントとTealiumの間に製品リンクを確立するリンクステップが含まれるようになりました。このリンクは、新しいData Manager APIアクションを使用する前に必要です。

## Data Manager APIアクションを導入する理由

Google Data Manager APIは、カスタマーマッチデータの取り込みにおける戦略的な進路です。

このAPIにコネクターを移行することで、以下の利点があります：

* Google AdsカスタマーアカウントとTealiumの間に正式な製品リンクを使用するため、Tealiumがあなたの代理として承認されたデータパートナーとして機能できます。
* ユーザーレベルのOAuthトークンに依存しないで継続的なオーディエンス更新を可能にし、製品リンクが確立された後は、Tealiumがデータパートナー統合を使用して取り込みを管理できます。
* 同意、利用規約、データフォーマット（識別子の正規化およびハッシュ化を含む）に関するGoogleのカスタマーマッチ要件と一致します。
* GoogleがGoogle AdsおよびData Manager APIを進化させるにつれて、構成の長期的な安定性が向上します。

## 既存のGoogle Ads APIアクションの廃止

[Google Adsカスタマーマッチコネクター](https://docs.tealium.com/google-ads-customer-match-connector/)の既存のGoogle Ads APIカスタマーマッチアクションは、将来のリリースで廃止されます。

その時まで、以下の点に注意してください：

* 既存のアクションは引き続き機能します。
* 将来の変更を最小限に抑えるために、できるだけ早く新しいData Manager APIアクションに移行することを強くお勧めします。
* レガシーアクションを削除する前に、標準リリースチャンネルを通じてタイムラインと重大な変更を通知します。

## 新しいData Manager APIアクションについて

新しいアクションは、[Google Adsカスタマーマッチコネクター](https://docs.tealium.com/google-ads-customer-match-connector/)の既存のGoogle Adsカスタマーマッチアクションと一緒に表示されます：

* **リストへのユーザー追加（Data Manager API）**
* **リストからのユーザー削除（Data Manager API）**

主なポイント：

* **UIレイアウト**：これらのアクションの構成画面は、既存のGoogle Adsカスタマーマッチアクションに密接に従っているため、ほとんどのマッピングと構成が馴染み深いものになります。

* **同意と利用規約**：Data Managerは、各取り込みコールに明示的な同意とカスタマーマッチの利用規約を必要とします。コネクターは、ペイロードに必要な同意と利用規約のフィールドが含まれていることを確認します。

* **識別子のフォーマット**：プレーンテキストまたは事前にハッシュ化された識別子（メールアドレス、電話番号、郵便住所など）をマッピングします。

  * **SHA256ハッシュを適用**：TealiumはGoogleが要求する正規化（トリム、小文字化、ハッシュ）を実行します。
  * **すでにSHA256ハッシュ化されている**：コネクターは、値が有効なSHA-256 16進数文字列であり、正確に64個の16進数文字を含み、`0x`プレフィックスがないことを検証します。
  * **無効な識別子**：コネクターは、リクエストを送信する前に無効な値を削除します。レコードに有効な識別子と無効な識別子の両方が含まれている場合、有効な識別子が送信されます。検証後に有効な識別子が残っていない場合、アクションは検証エラーで失敗し、再試行されません。
  * **住所情報**：4つのフィールドすべてが必要です：国コード、名、姓、郵便番号。いずれかの住所フィールドが欠けている場合、コネクターはリクエストから住所オブジェクト全体を削除します。

* **リストキータイプ**：Data Manager APIを使用して作成および管理されるリストは、`CONTACT_ID`（メール、電話、または住所）、`USER_ID`（第一者ID）、または`MOBILE_ID`（デバイスID）などのリストキータイプを使用します。リストのキータイプと互換性のある識別子をマッピングします。

**Manager Customer ID**のオーバーライドやその他のGoogle Ads API固有のセクションは、Data Manager APIアクションでは使用されません。Data Managerの構成は、製品リンクと選択されたリストおよび識別子を通じて処理されます。


## 移行する前に

Google Data Manager APIアクションを使用する前に、Google AdsアカウントとTealiumの間に製品リンクを作成してください。

製品リンクはTealiumまたはGoogle Adsのいずれかで作成できます。

### Tealiumで製品リンクを作成する

Tealiumから製品リンクを作成する場合、コネクターを再認証して、Google OAuthトークンにData Manager APIスコープが含まれるようにします：

1. 既存の[Google Adsカスタマーマッチコネクター](https://docs.tealium.com/google-ads-customer-match-connector/)を開きます。
1. **Googleでサインイン**をクリックし、再度Googleアカウントでサインインします。
1. 認証中、コネクターは既存のGoogle Ads権限に加えて`https://www.googleapis.com/auth/datamanager`へのアクセスを要求します。
1. コネクター構成の**Link Customer ID to Tealium**セクションを使用して製品リンクを作成します。

### Google Adsで製品リンクを作成する

Google Ads Data Managerから製品リンクを作成することもできます。このオプションは、Tealiumで製品リンクを作成するためのGoogle OAuthフローを必要としません。

詳細については、[Google Adsカスタマーマッチコネクター](https://docs.tealium.com/google-ads-customer-match-connector/)を参照してください。

カスタマーマッチユーザーリストを所有するGoogle Adsアカウントの製品リンクを作成します。アクションが**Customer ID Override**を使用する場合、アクションによって使用される各リスト所有カスタマーアカウントが製品リンクによってカバーされていることを確認してください。

## 既存のGoogle Ads APIアクションからの移行方法

目標は、各既存のGoogle AdsカスタマーマッチアクションをそのGoogle Data Manager APIの同等物に行動の変更を最小限に抑えて移行することです。

### ステップ1: 既存のアクションを新しいGoogle Data Manager APIに移行する

既存のアクションに基づいて新しいアクションを作成する（テスト中に両方を並行して実行したい場合に推奨）、または既存のアクションをその場で切り替えます。

#### オプションA - 既存のアクションを新しいGoogle Data Manager APIアクションにコピーする

各既存のGoogle Ads APIアクションについて：

1. コネクターの**Actions**タブで、既存のGoogle Adsカスタマーマッチアクションを探します。
1. **Copy to new action**オプションを使用して構成を複製します。
1. 新しいコピーで、アクションタイプをData Manager APIアクションに変更します。たとえば、**Add User to List (Data Manager API)**または**Remove User from List (Data Manager API)**。
1. 次の点を確認します：
   * 同じユーザーリストが選択されているか、またはオーバーライドフィールドがData Managerの正しいリストIDフォーマットを使用するように更新されています。
   * 必要な識別子マッピングがすべて存在し、リストのキータイプと一致しています。たとえば、`CONTACT_ID`リストの場合は、ハッシュ化されたメール、ハッシュ化された電話、または住所フィールドの少なくとも1つ、`USER_ID`リストの場合は第一者ユーザーID、または`MOBILE_ID`リストの場合はモバイルデバイスIDなど。
1. 新しいData Manager APIアクションを保存します。

このアプローチでは、新しいAPIに切り替えながら、既存のトリガー条件とほとんどのフィールドマッピングを再利用できます。

#### オプションB - アクションを新しいData Manager APIアクションタイプに切り替える

コピーを作成せずにアクションを新しいAPIに切り替える場合：

1. コネクターアクションタブで、既存のGoogle Adsカスタマーマッチアクションを探します。
1. 上部右メニューから**Change Action Type**オプションを使用して、アクションのアクションタイプを切り替えます。
1. アクションのData Manager APIバリアントを選択します。
1. 選択されたユーザーリストとマッピングが保持されていることを確認します。
1. Data Manager APIアクションを保存します。
### ステップ2：テストと検証

アクションをコピーした場合（オプションA）もしくはその場で切り替えた場合（オプションB）に関わらず：

1. 新しいData Manager APIアクションを起動するイベントをトリガーします。
1. Google Adsで、ターゲットのCustomer Matchリストが予想通りにユーザーを受け取り始めているか（追加アクションの場合）、または予想通りにユーザーが削除されているか（削除アクションの場合）を確認します。
1. Data Managerに関連するエラー（例：無効な識別子、同意問題、リスト構成の問題など）がないかTealiumコネクタのログをチェックし、必要に応じてマッピングを調整します。

### ステップ3：レガシーアクションのクリーンアップ（該当する場合）

新しいData Manager APIアクションをコピーして検証した場合：

1. コネクタの**Actions**タブに戻ります。
1. 重複した更新を避けるため、古いGoogle Ads Customer Matchアクションを無効にするか削除します。

オプションBを使用してアクションをその場で切り替えた場合、そのアクションに対する追加のクリーンアップは必要ありません。

これらのステップを完了すると、Google Ads Customer Matchの構成はTealiumのGoogle Data Manager APIを使用するように完全に移行されます。

## FAQ

**Google Ads Customer Matchリストを再作成する必要がありますか？**  
いいえ。新しいアクションは、既存のGoogle Ads Customer Matchリストと互換性があり、リストのキータイプが送信する識別子と一致している限り、使用できます。また、コネクタのリスト管理操作（利用可能な場合）を使用して、Google Data Manager APIを通じて直接リストを作成または管理することもできます。

**移行しない場合、どうなりますか？**  
短期的には、既存のGoogle Ads APIベースのアクションは引き続き機能します。しかし、これらのアクションは廃止予定であるため、いずれ削除されるか、Googleが基盤となるAds APIを進化させるにつれて、Google Ads Customer Matchオーディエンスを管理する能力を失う可能性があります。今移行することで、将来の混乱を最小限に抑え、Google Data Managerを使用した推奨されるパスに構成を合わせることができます。

**同意とデータガバナンスの管理は引き続き行えますか？**  
はい。エンドユーザーの同意の収集と管理、適用される法律およびGoogleのポリシーに準じてGoogleとのデータ共有を確実に行う責任は引き続きあなたにあります。同意の観点から、新しいGoogle Data Manager APIアクションは既存のアクションと同じように動作します。コネクタはリクエストペイロードのGoogle同意フィールドに常に`GRANTED`を送信し、適切な同意を持つユーザーのみがGoogleに送信されるように、あなたの上流の同意およびオーディエンスロジックに依存します。