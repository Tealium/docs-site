---
title: サーバーサイド同意管理
description: 同意構成マネージャーを使用すると、ウェブサイトにトラッキング構成のオプションを展開できます。同意マネージャーによって提供される同意決定は、選択されたサーバーサイド製品によって自動的に施行されます。
url: https://docs.tealium.com/ja/consent/server-side/consent-management/
---

<blockquote>
イベントレベルのアクティベーションのためのサーバーサイド同意管理は、同意オーケストレーションに置き換えられました。詳細については、[同意オーケストレーションについて](https://docs.tealium.com/about-consent-orchestration/)をご覧ください。<br><br>同意管理の自動施行はすべてのプロファイルに対してオプションであり、新しいプロファイルではデフォルトで無効になっています。詳細については、[自動施行の無効化](#disabling-automatic-enforcement)をご覧ください。
</blockquote>


サーバーサイド同意管理の自動施行にはいくつかの制限があります。この記事では、製品ごとの現在の挙動と制限、および自動施行を効果的に無効化する方法について説明します。

## 仕組み

同意構成マネージャーは、タグを機能と目的に基づいてカテゴリにグループ化します。これらのカテゴリは訪問に提示され、トラッキングの許可または禁止を切り替えるためのトグルボタンとして表示されます。

現在利用可能な同意カテゴリは以下の通りです：

* アナリティクス
* アフィリエイト
* ディスプレイ広告
* 検索
* メール
* パーソナライゼーション
* ソーシャル
* ビッグデータ
* その他
* クッキーマッチ
* CDP
* モバイル
* エンゲージメント
* モニタリング
* CRM

Tealium Collectタグは、イベントに`consent_categories`配列を構成します。イベントに`consent_categories`配列が定義されている場合、配列内のカテゴリは以下に詳述するように施行されます。その配列が構成されていない場合、同意ポリシーは施行されず、すべてのサーバーサイド製品が有効になります。

### EventStreamコネクタアクション

同意構成はTealium EventStreamコネクタによって施行されます。コネクタアクションの同意カテゴリは、アクション構成画面の**詳細**に表示されます：

![](https://docs.tealium.com/images/server-side/6f9b6ee0-8de8-4bc9-84cf-6afed53b5679-1-201-a.jpeg)

#### EventStreamコネクタアクションの同意カテゴリ

EventStreamの各コネクタアクションには少なくとも1つの同意カテゴリが割り当てられています。この同意カテゴリは変更できません。`consent_categories`配列が定義されている場合、関連するすべてのカテゴリが存在するときのみアクションが発火します。ただし、[同意変更イベント](https://docs.tealium.com/consent-change-event-specifications/#consent-change-events)は例外です。これらのイベント（`decline_consent`、`grant_full_consent`、および`grant_partial_consent`）は、`consent_categories`配列の内容に関わらず送信/保存されます。

**例 1**

Facebookコネクタは、**アナリティクス**、**ディスプレイ広告**、および**ソーシャル**の同意カテゴリによって管理されます。訪問がこれらの三つのカテゴリすべてに同意した場合にのみ、Facebookコネクタアクションが発火します。

**例 2**

**アナリティクス**と**パーソナライゼーション**のために2つのコネクタが構成されています。訪問が構成フォームで**アナリティクス**のトラッキングを許可し、**パーソナライゼーション**を許可しない部分的な同意を与えます。

![](https://docs.tealium.com/images/iq-tag-management/consent-server-side-categories-example.png)

**アナリティクス**カテゴリのコネクタアクションのみがトリガーされます。**パーソナライゼーション**カテゴリの任意のコネクタアクションは抑制されます。

### AudienceStream処理

Tealium AudienceStreamは、**CDP**同意カテゴリに分類されます。訪問が**CDP**カテゴリに同意することで、AudienceStreamでの属性とコネクタの処理が可能になります。ただし、`decline_consent`、`grant_full_consent`、および`grant_partial_consent`のようなイベントについては、**CDP**の同意が与えられていなくてもAudienceStreamはデータを処理します。**CDP**同意を迂回することで、リマーケティングリストや他の第三者システムから訪問を削除するためのLeave Audienceコネクタアクションなどの特定のアクションをトリガーすることができます。詳細については、[同意イベント仕様](https://docs.tealium.com/consent-change-event-specifications/)をご覧ください。


<blockquote>
AudienceStreamに割り当てられた同意カテゴリは変更できません。
</blockquote>


### AudienceStreamコネクタアクション

Audienceコネクタは、コネクタアクションレベルでの同意カテゴリ施行をサポートしていません。AudienceStreamコネクタの同意施行をカスタマイズするには、オーディエンスルールに同意条件を追加する必要があります。

### DataAccess

DataAccess製品は、`consent_categories`配列に**ビッグデータ**同意が含まれている場合にのみイベントとプロファイルを記録します。Tealium EventStoreとTealium EventDBは、**ビッグデータ**同意カテゴリに分類されます。訪問が**ビッグデータ**カテゴリに同意することで、EventStoreおよびEventDBにイベントデータが保存されることが許可されます。

ただし、イベント記録には例外があります：

* [同意変更イベント](https://docs.tealium.com/consent-change-event-specifications/#consent-change-events)。
* **データガバナンスパッケージ**によって使用されるイベント
* Tealium AudienceStoreおよびTealium AudienceDB  
訪問が**CDP**カテゴリに同意することで、AudienceStoreおよびAudienceDBに訪問プロファイルが保存されることが許可されます。


<blockquote>
すべてのDataAccess製品（EventStore、AudienceStore、EventDB、およびAudienceDB）において、[同意変更イベント](https://docs.tealium.com/consent-change-event-specifications/#consent-change-events)は、同意記録をサポートするために`consent_categories`配列の内容に関わらず送信/保存されます。
</blockquote>


## 自動施行の無効化


<blockquote>
自動施行は新しいプロファイルではデフォルトで無効です。同意オーケストレーションを有効にすると、レガシーのイベントレベルのサーバーサイド施行が無効化され、置き換えられます。既存のプロファイルで自動施行を無効にする方法については、[サーバーサイドアカウント構成](https://docs.tealium.com/server-side-account-settings/#consent-enforcement)をご覧ください。詳細については、[同意オーケストレーションについて](https://docs.tealium.com/about-consent-orchestration/)をご覧ください。
</blockquote>


`consent_categories`に基づく組み込みの施行は、時に同意されたデータのブロッキングを引き起こすことがあります。そのロジックをオーバーライドするには、次の手順に従ってください：

1. Tealium CollectタグにスコープされたJavaScript Code拡張を使用して、オプトインカテゴリを新しい配列（例：`consent_categories_granted`）にコピーします：
      ```javascript
      b.consent_categories_granted = b.consent_categories
      delete b.consent_categories
      ```
1. `consent_categories`配列を削除して、サーバーサイド製品が制限なく動作するようにします。
1. 各イベントフィードとオーディエンスに`consent_categories_granted`に基づく条件を手動で追加します。


<blockquote>
これにより、すべての自動施行と同意に基づくブロッキングが無効になります。このワークアラウンドを使用する際は、エンドユーザーの許可なしにトラッキングを避けるために、構成に非常に注意してください。
</blockquote>


自動施行を無効にした後、[手動サーバーサイド同意施行](https://docs.tealium.com/manual-enforcement/)の手順に従って、手動で同意条件を構成してください。
