---
title: Google Ads Customer Match アクションを Google Data Manager API に移行する
description: この記事では、新しい Google Ads Customer Match アクションが Google Data Manager API を使用する理由と、既存の Google Ads API ベースのアクションからの移行方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/google-ads-customer-match-data-manager-api-migration/
---
## 変更点

[Google Ads Customer Match コネクタ](https://docs.tealium.com/google-ads-customer-match-connector/)に、Google Data Manager API を使用する2つの新しいアクションが導入されます：

* リストにユーザーを追加（Data Manager API）
* リストからユーザーを削除（Data Manager API）

これらのアクションは、コネクタUIの既存のリストにユーザーを追加およびリストからユーザーを削除するアクションを密接に模倣して設計されており、GoogleのData Manager APIを通じてオーディエンスの更新を送信します。

さらに、コネクタの構成には、Google Ads アカウントと Tealium 間の製品リンクを確立するリンクステップが含まれるようになりました。このリンクは、新しい Data Manager API アクションを使用する前に必要です。

## Data Manager API アクションを導入する理由

Google Data Manager API は、Customer Match データの取り込みにおける戦略的な進路です。

このAPIにコネクタを移行することで、以下の利点があります：

* Google Ads 顧客アカウントと Tealium 間の正式な製品リンクを使用するため、Tealium があなたの代理として承認されたデータパートナーとして機能できます。
* ユーザーレベルの OAuth トークンに依存しないため、製品リンクが確立された後、Tealium がデータパートナー統合を使用して取り込みを管理できます。
* 同意、利用規約、データのフォーマット（識別子の正規化およびハッシュ化を含む）に関する Google の Customer Match 要件と一致します。
* Google が Google Ads および Data Manager API を進化させるにつれて、構成の長期的な安定性が向上します。

## 既存の Google Ads API アクションの廃止

[Google Ads Customer Match コネクタ](https://docs.tealium.com/google-ads-customer-match-connector/)の既存の Google Ads API Customer Match アクションは、将来のリリースで廃止される予定です。

それまでの間、以下の点に注意してください：

* 既存のアクションは引き続き機能します。
* 将来の変更を最小限に抑えるために、できるだけ早く新しい Data Manager API アクションに移行することを強くお勧めします。
* レガシーアクションを削除する前に、標準リリースチャネルを通じてタイムラインと重大な変更を通知します。

## 新しい Data Manager API アクションについて

新しいアクションは、[Google Ads Customer Match コネクタ](https://docs.tealium.com/google-ads-customer-match-connector/)の既存の Google Ads Customer Match アクションと一緒に表示されます：

* リストにユーザーを追加（Data Manager API）
* リストからユーザーを削除（Data Manager API）

主なポイント：

* **UI レイアウト**：これらのアクションの構成画面は、既存の Google Ads Customer Match アクションに密接に従っているため、ほとんどのマッピングと構成が馴染みのあるものになります。
* **同意と利用規約**：Data Manager は、各取り込みコールに明示的な同意と Customer Match の利用規約を要求します。コネクタは、ペイロードに必要な同意と利用規約のフィールドが含まれていることを保証します。
* **識別子のフォーマット**：プレーンテキストまたは事前にハッシュ化された識別子（メール、電話、郵便住所など）をマッピングします。**SHA256 ハッシュを適用**とラベル付けされたフィールドを選択すると、Tealium は Google が要求する正規化（トリム、小文字化、ハッシュ化）を実行します。**既に SHA256 ハッシュ化されている**とラベル付けされたフィールドを選択する場合、Google のフォーマット要件をすでに満たしているデータを提供する責任があります。
* **リストキータイプ**：Data Manager API を使用して作成および管理されるリストは、`CONTACT_ID`（メール/電話/住所）、`USER_ID`（ファーストパーティID）、または `MOBILE_ID`（デバイスID）などのリストキータイプを使用します。アクション構成では、リストのキータイプに対応する識別子をマッピングする必要があります。

**Manager Customer ID** オーバーライドおよびその他の Ads API 固有のセクションは、Data Manager API アクションでは使用されません。Data Manager 関連の構成は、製品リンクおよび選択されたリストと識別子を通じて処理されます。

## 移行する前に

アクションを切り替える前に、これらの前提条件を確認して完了してください。

### ステップ 1: Data Manager API アクセスを含めてコネクタを再認証する

すでに Tealium に Google Ads Customer Match コネクタを構成している場合、Google OAuth トークンに Data Manager API スコープが含まれるようにコネクタを再認証する必要があります。

再認証するには：

1. 既存の [Google Ads Customer Match コネクタ](https://docs.tealium.com/google-ads-customer-match-connector/) を開きます。
1. 認証コントロール（**Google でサインイン** ボタン）を使用して、Google アカウントで再度サインインします。
1. このプロセス中に、コネクタは既存の Google Ads 権限に加えて `https://www.googleapis.com/auth/datamanager` を含むアクセスを要求します。

このステップは、製品リンクを作成し、Google Data Manager API アクションを使用する前に必要です。

### ステップ 2: Google Ads 顧客IDを Tealium にリンクする（製品リンク）

再認証後、Google Ads 顧客アカウントと Tealium 間に製品リンクを作成する必要があります。

製品リンクは、Google Ads 顧客アカウントレベル（ユーザーリストの所有アカウント）で作成され、すべての Google Data Manager API アクションを使用するための前提条件です。

製品リンクの作成に失敗した場合（たとえば、リンクがすでに存在するか、ユーザーに権限がない場合）、UIのエラーメッセージを確認し、Google Ads の権限またはアカウント選択を適切に調整してください。

Google Ads 顧客IDを Tealium にリンクするには：

1. コネクタ構成で、**Link Customer ID to Tealium** とラベル付けされたセクションを探します。
1. このコネクタで Customer Match に使用される Google Ads 顧客IDを入力します。
1. **Create Product Link**（または同等のもの）とラベル付けされたボタンをクリックします。
1. Tealium UI でリンクが正常に作成されたことを示す確認メッセージが表示されるのを待ちます。

リンクが成功した後、Tealium は承認されたデータパートナーとして Google Data Manager API を使用して Google Ads アカウントに更新を送信できます。

## 既存の Google Ads API アクションからの移行方法

目標は、各既存の Google Ads Customer Match アクションをその Google Data Manager API の同等物に最小限の変更で移行することです。

### ステップ 1: 再認証およびリンク

[Google Ads Customer Match コネクタ](https://docs.tealium.com/google-ads-customer-match-connector/)を使用する各アカウントプロファイルについて：

1. Google Data Manager API スコープを含むようにコネクタを再認証します。
1. **Link Customer ID to Tealium** セクションを使用して、各コネクタアクションに使用される Google Ads 顧客IDの製品リンクを作成します。アクションで顧客IDオーバーライド機能を使用している場合は、ここで各リスト所有顧客アカウントIDのリンクプロセスを繰り返します。

### ステップ 2: 既存のアクションを新しい Google Data Manager API に移動する

既存のアクションに基づいて新しいアクションを作成する（テスト中に両方を並行して実行したい場合に推奨）、または既存のアクションをその場で切り替えます。
#### オプションA - 既存のアクションを新しいGoogle Data Manager APIアクションにコピー

各既存のGoogle Ads APIアクションについて:

1. コネクタの**アクション**タブで、既存のGoogle Ads Customer Matchアクションを見つけます。
1. **新しいアクションにコピー**オプションを使用して、構成を複製します。
1. 新しいコピーで、アクションタイプをData Manager APIアクションに変更します。例えば、**リストにユーザーを追加（Data Manager API）**または**リストからユーザーを削除（Data Manager API）**。
1. 次の点を確認します：
   * 同じユーザーリストが選択されているか、またはオーバーライドフィールドがData Manager用の正しいリストID形式を使用するように更新されている。
   * 必要な識別子マッピングが存在し、リストのキータイプと一致している。例えば、`CONTACT_ID`リストの場合はハッシュ化されたメール、ハッシュ化された電話、または住所フィールドの少なくとも1つ；`USER_ID`リストの場合は第一者ユーザーID；または`MOBILE_ID`リストの場合はモバイルデバイスID。
1. 新しいData Manager APIアクションを保存します。

このアプローチにより、既存のトリガー条件とほとんどのフィールドマッピングを再利用しながら新しいAPIに切り替えることができます。

#### オプションB - アクションを新しいData Manager APIアクションタイプに切り替え

コピーを作成するのではなく、アクションを新しいAPIに切り替えたい場合:

1. コネクタアクションタブで、既存のGoogle Ads Customer Matchアクションを見つけます。
1. 右上のメニューから**アクションタイプを変更**オプションを使用して、アクションのタイプを切り替えます。
1. アクションのData Manager APIバリアントを選択します。
1. 選択されたユーザーリストとマッピングが保持されていることを確認します。
1. Data Manager APIアクションを保存します。

### ステップ3: テストと検証

アクションをコピーした場合（オプションA）でも、その場で切り替えた場合（オプションB）でも：

1. 新しいData Manager APIアクションを発火させるイベントをトリガーします。
1. Google AdsでターゲットのCustomer Matchリストが期待通りにユーザーを受け取り始めていること（追加アクションの場合）、またはユーザーが期待通りに削除されていること（削除アクションの場合）を確認します。
1. Data Managerに関連するエラー（例えば、無効な識別子、同意問題、リスト構成の問題など）がないかTealiumコネクタのログを確認し、必要に応じてマッピングを調整します。

### ステップ4: レガシーアクションのクリーンアップ（該当する場合）

アクションのコピーを作成し、新しいData Manager APIアクションを検証した場合：

1. コネクタの**アクション**タブに戻ります。
1. 重複した更新を避けるために、古いGoogle Ads Customer Matchアクションを無効にするか削除します。

オプションBを使用してその場でアクションを切り替えた場合、そのアクションに対して追加のクリーンアップは必要ありません。

これらのステップを完了すると、Google Ads Customer Matchの構成はTealiumでGoogle Data Manager APIを使用するように完全に移行されます。

## FAQ

**Google Ads Customer Matchリストを再作成する必要がありますか？**  
いいえ。新しいアクションは、既存のGoogle Ads Customer Matchリストと互換性があり、リストのキータイプが送信する識別子と一致している場合に使用できます。また、コネクタのリスト管理操作（利用可能な場合）を使用して、Google Data Manager APIを通じて直接リストを作成または管理することもできます。

**移行しない場合はどうなりますか？**  
短期的には、既存のGoogle Ads APIベースのアクションは引き続き機能します。しかし、これらのアクションは廃止予定であるため、いずれそれらが削除されるか、Googleが基盤となるAds APIを進化させるにつれて、Google Ads Customer Matchオーディエンスの管理ができなくなる可能性があります。今すぐ移行することで、将来の混乱を最小限に抑え、Google Data Managerを使用する推奨されるパスに構成を合わせることができます。

**同意とデータガバナンスはまだ管理できますか？**  
はい。エンドユーザーの同意の収集と管理、適用される法律およびGoogleのポリシーに準じてGoogleとのデータ共有を確実に行う責任は引き続きあなたにあります。同意の観点から、新しいGoogle Data Manager APIアクションは既存のアクションと同じように動作します：コネクタは常にリクエストペイロードのGoogle同意フィールドに`GRANTED`を送信し、適切な同意を持つユーザーのみがGoogleに送信されるように、上流の同意およびオーディエンスロジックに依存します。