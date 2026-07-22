---
title: Tealiumの同意概要
description: クライアントサイドおよびサーバーサイドのプラットフォームでユーザーの同意をどのようにTealiumが強制するかを学び、商用の同意管理プラットフォーム、カスタムツール、またはTealiumがサポートする同意キャプチャを使用する場合に適したソリューションを選択します。
url: https://docs.tealium.com/ja/consent/consent-overview/
---
Tealiumはさまざまなニーズに対応する柔軟な同意管理機能を提供し、ユーザーの同意をキャプチャ、解釈、および強制するのに役立ちます。このガイドでは、Tealiumの同意機能と、クライアントサイドおよびサーバーサイドの環境でそれらを使用する方法について説明します。

## 同意の強制がどのように機能するか

Tealiumには、クライアントサイドおよびサーバーサイドのイベントに対する同意決定を強制するための組み込みメカニズムが含まれています。同意ポリシーを定義し、それらがどのように適用されるかを構成すると、強制コンポーネントはそれらのポリシーに基づいてデータ収集および処理をブロックまたは許可します。

### クライアントサイドの強制

クライアントサイドの同意強制は、Consent Integrations Framework (UTCM) および同意登録を使用します：

* **Consent Integrations Framework (UTCM)**: ブラウザで同意決定を強制します。[consent integrations](https://docs.tealium.com/about-consent-integrations/)および[CookieConsent](https://docs.tealium.com/cookieconsent-consent-integration/)によって使用され、デフォルトで同意されていないタグをブロックし、同意を待っている間イベントをキューに入れ、同意された目的のみがタグをトリガーすることを保証します。

* [**Consent Register**](https://docs.tealium.com/consent-register/): ユーザーの同意決定とリアルタイムでの更新を保存する共有オンページ構造です。これにより、タグ、拡張機能、およびサードパーティツール（Google Consent Modeやオプトアウトタグなど）が現在の同意状態にアクセスして対応することができます。

### サーバーサイドの強制

サーバーサイドでは、[consent orchestration](https://docs.tealium.com/about-consent-orchestration/)がイベントレベルで同意ポリシーを強制し、イベントが処理またはアクティブ化される前に受信イベントを目的ベースのルールに対して評価し、同意条件を満たさないイベントをブロックします。

同意オーケストレーションは、以下を含むイベントレベルの強制を適用します：

* EventStreamコネクタアクション
* Functions（イベントレベルのアクティベーション）
* EventStore
* EventDB
* AudienceStreamプロファイル処理

AudienceStreamのアクティベーションにはまだ同意を強制していません。サポートが利用可能になるまで、AudienceStreamでは[manual enforcements](https://docs.tealium.com/manual-enforcement/)を使用してください。

これらのコンポーネントは、ビジネスロジックに強制を結びつけることなく、追加のカスタム開発を必要とせずに、データスタック全体でスケーラブルで一元化された一貫した同意強制を提供します。

## 同意機能についてとそれを使用するタイミング

![](https://docs.tealium.com/images/iq-tag-management/tealium-consent-levels.png)

|**機能**| **使用するタイミング**|
|---| ---|
| [Consent integrations](#consent-integrations) | <ul><li>OneTrust、TrustArc、Didomi、Usercentricsなどの商用同意管理プラットフォーム（CMP）を使用して同意をキャプチャし、Tealiumを通じてそれらの決定を信頼性を持って強制したい場合。</li><li>目的ベースの強制とタグマッピングを可能にしながら、CMPからの同意決定を尊重し、強制するためにTealiumが必要な場合。</li></ul> |
| [CookieConsent同意統合](#cookieconsent-consent-integration) | <ul><li>商用CMPに依存せずにユーザーの同意をキャプチャし、強制したい場合。</li><li>サイトのデザインおよびコンプライアンスニーズに合わせたカスタマイズ可能な同意バナーが必要な場合。</li><li>Tealiumの同意マネージャーから移行し、Tealium内で機能する現代的でスケーラブルな代替手段が必要な場合。</li></ul> |
| [カスタム同意統合](#custom-consent-integration) | <ul><li>事前に組み込まれた統合によってサポートされていないCMPまたは同意ツールを使用している場合。</li><li>独自の内部CMPまたはカスタム同意キャプチャソリューションを構築し、それをTealiumに接続する必要がある場合。</li><li>サポートされているCMPを使用しているが、標準の事前組み込み統合ではサポートされていない方法でカスタマイズしている場合。</li></ul> |
| [同意オーケストレーション](#consent-orchestration) | <ul><li>EventStream、EventStore、EventDB、AudienceStreamプロファイル処理、およびサーバーサイドコネクタ全体で、イベントレベルでのユーザー同意の中央集中型のサーバーサイド強制が必要な場合。</li><li>プライバシー法に準拠するために、目的ベースの同意ポリシーを中央で定義し、管理する必要がある場合。</li><li>同意が必要ない特定のデータソースや地域を除外し、他の場所で同意を強制する必要がある場合。</li></ul> |
| [同意マネージャー](#consent-manager) | <ul><li>同意マネージャーの構成を持っており、CookieConsent同意統合に移行する予定の場合。</li></ul> |
| [手動同意条件](#manual-consent-conditions) | <ul><li>AudienceStreamのオーディエンス内で訪問レベルの同意条件を強制する必要があり、まだ同意オーケストレーションによってサポートされていない場合。</li><li>EventStreamで手動条件を使用しており、まだ同意オーケストレーションに移行していない場合。</li></ul> |

### 同意統合

[クライアントサイドの同意統合](https://docs.tealium.com/about-consent-integrations/)は、サードパーティのCMPと統合します。統合は、CMPからの同意決定をキャプチャし、Tealiumの同意強制フレームワークを通じてそれらを強制するため、同意が与えられたときにのみタグが発火します。

#### 主な特徴

* OneTrust、TrustArc、Didomi、UsercentricsなどのCMPとの事前組み込み統合。
* 構成変更をサポートするために調整可能なテンプレート。
* 同意の目的ベースの強制。
* タグ再発火オプションと強制ルール。
* 強制条件の競合処理。

#### 同意統合を使用するタイミング

OneTrust、TrustArc、Didomi、UsercentricsなどのサードパーティCMPを使用している場合は、同意統合を使用してください。同意統合は[事前組み込み統合](https://docs.tealium.com/vendor-specific-configuration/)を提供し、同意統合フレームワークを使用して、同意されたデータのみがアクティブ化されることを保証します。

CMPが事前組み込み統合によってサポートされていない場合は、JavaScript関数を使用して同意決定をTealiumに渡す[カスタム同意統合](#custom-consent-integrations)を使用できます。

#### 推奨事項

* 新しい実装では、同意強制のためにロードルールを使用することは避けてください。代わりに同意統合を使用してください。
* CMPに対する事前組み込み統合が利用可能でない場合は、カスタム同意統合を使用してください。

### CookieConsent同意統合

CookieConsentは、Tealium iQと統合する柔軟でオープンソースのWCAG準拠の同意管理ツールです。同意決定をキャプチャするためのカスタマイズ可能なインターフェースを提供します。同意統合と組み合わせることで、同意が与えられたときにのみタグが発火するようにこれらの決定を強制します。[CookieConsent同意統合](https://docs.tealium.com/cookieconsent-consent-integration/)は、[クライアントサイドの同意マネージャー](https://docs.tealium.com/about-consent-management/)の推奨される代替品です。

#### 主な特徴

* 同意キャプチャのためのアクセス可能でカスタマイズ可能なインターフェース。
* 同意バナーのA/Bテストをサポート。
* イベントキューイングとリトライメカニズムで同意を強制。
* デフォルトでブロックするフレームワークを使用して、同意されていないトラッキングを防止。
* アクセシビリティ基準をサポート。
* CookieConsentはオープンソースでカスタマイズ可能であり、デザインとユーザーインタラクションの制御を提供しながら、Tealiumスタックとの完全なサポートと統合の利点を享受できます。

#### CookieConsent同意統合を使用するタイミング

[CookieConsent同意統合](https://docs.tealium.com/cookieconsent-consent-integration/)を使用する場合は、完全なTealium管理の同意ソリューションが必要なときです。このオプションは、次の場合に理想的です：

* 事前に組み込まれたポリシーや法的ガイダンスを提供する商用CMPが不要な場合。
* WCAG準拠でアクセス可能でカスタマイズ可能なインターフェースを使用して、サイト上で直接ユーザーの同意をキャプチャする必要がある場合。
* 最小限のエンジニアリング努力で同意決定を強制し、スケーラブルで信頼性の高い強制を実現するためにTealiumの同意強制フレームワークを使用する場合。

CookieConsentは、技術リソースが限られているチームや、キャプチャと強制の両方に対するターンキーソリューションを探しているチームに適しています。
#### 検討事項

* クライアント側の同意管理者の推奨代替品。
* IABの透明性と同意フレームワーク（TCF）をサポートしていません。
* Google認定のCMPではありません。

### カスタム同意統合

[カスタム同意統合](https://docs.tealium.com/custom-cmp-integrations/)を使用すると、TealiumでカスタムCMPまたは同意キャプチャツールを使用できます。同意決定をキャプチャするカスタム統合テンプレートを作成し、Tealium同意強制フレームワークを使用してそれらを強制します。

#### 主な機能

* 顧客が構築したまたは大幅にカスタマイズされたCMPをサポート。
* 強制フレームワークと統合するためのカスタマイズ可能なJavaScript関数を使用。
* 同意レジスターおよび強制レイヤーとの構造化された通信を可能にします。
* サポートされていないCMPやユニークな構成で動作します。
* 実装が簡単で、最小限のサポートが必要です。

#### カスタム同意統合を使用するタイミング

事前に組み込まれた統合に対応していないCMPや同意キャプチャソリューションを使用している場合は、カスタム同意統合を使用します。このアプローチは、以下の場合に理想的です：

* カスタムビルドのCMPを使用している。
* 標準外または高度にカスタマイズされた構成を使用する商用CMPを使用している。
* Tealium同意強制フレームワークに内部同意ツールを統合する必要がある。

#### 検討事項

* 構成、テスト、およびメンテナンスにはJavaScriptの知識が必要です。

### 同意オーケストレーション

[同意オーケストレーション](https://docs.tealium.com/about-consent-orchestration/)は、イベントレベルでユーザーの同意をサーバーサイドで強制します。これは、ビジネスロジックから同意強制を分離することにより、サーバーサイドでの同意管理をスケーラブルで集中的な方法で提供します。

#### 主な機能

* すべてのサーバーサイドイベントで一貫した強制を保証するために、一か所で同意ルールを定義および管理。
* 処理前にイベントレベルで同意決定を強制し、許可されていないデータ収集または処理を防ぎます。
* EventStreamコネクタアクション、イベント機能、EventStore、およびEventDBとシームレスに統合。
* AudienceStream処理でイベントが続行される場所を制御します（AudienceStreamのアクティベーションには適用されません）。
* データ処理活動を細かく制御するために定義されたカテゴリに基づいて同意を強制します。

#### 同意オーケストレーションを使用するタイミング

サーバーサイドのデータ収集および処理に対して集中的でルールベースの同意強制が必要な場合は、同意オーケストレーションを使用します。データプライバシー規制への準拠を保証するために、同意ポリシーに対する集中的な制御が必要な組織にとって理想的です。

#### 検討事項

* 同意オーケストレーションはまだAudienceStreamのアクティベーションを強制しておらず、Audiencesで訪問レベルの同意条件（同意ベースのバッジなど）をサポートしていません。サポートが追加されるまで、[サーバーサイド同意管理](https://docs.tealium.com/server-side-consent-management/)で説明されているように、AudienceStreamで手動の同意条件を使用してください。
* 同意オーケストレーションを使用するためには、サーバーサイドのプロファイルが正しく構成されていることを確認してください。
* 同意マネージャーを使用しているサーバーサイドの顧客は、同意オーケストレーションへの移行が可能になるまで、[手動強制](https://docs.tealium.com/manual-enforcement/)を実装する必要があります。
## 関連ドキュメント

* [同意統合](https://docs.tealium.com/about-consent-integrations/)
* [カスタム同意統合](https://docs.tealium.com/custom-cmp-integrations/)
* [CookieConsent同意統合](https://docs.tealium.com/cookieconsent-consent-integration/)
* [同意調整](https://docs.tealium.com/about-consent-orchestration/)
* [同意登録](https://docs.tealium.com/consent-register/)
* [クライアント側同意管理](https://docs.tealium.com/about-consent-management/)
* [サーバー側同意管理](https://docs.tealium.com/server-side-consent-management/)