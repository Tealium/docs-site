---
title: Tealium同意登録
description: この記事ではTealium同意登録についての概要を提供します。
url: https://docs.tealium.com/ja/consent/client-side/consent-register/
---
Tealium同意登録は、[Tealium iQ Consent Integrations](https://docs.tealium.com/about-consent-integrations/)および[Consent Manager](https://docs.tealium.com/about-consent-management/)によって使用され、ウェブサイトのコード全体に同意信号を公開します。また、Google同意モードタグがこれらの信号に直接アクセスし、適切な反応を可能にします。

## 主な機能

* **ユニバーサル同意イベント**: 最新のConsent Manager（`cmGeneral`テンプレートv3.1.0から）とConsent Integrations（フレームワークテンプレートv1.2.0から）は、同意構成が読み込まれたり更新されたりするときにイベントを発生させるために同意登録を使用します。これらの変更はページ上の`window.tealiumConsentRegister`オブジェクトで全世界的にアクセス可能です。詳細については、[MDN Web Docs: イベントの紹介](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events)を参照してください。
* **すべての同意信号のサポート**: `implicit`および`explicit`の両方の同意信号を発行および保持します。
* **イベントリスニング**: ページ上の任意のタグまたはスクリプトが`consent_loaded`および`consent_changed`イベントをリッスンできます。これにより、同意ステータスの変更に基づいて反応的なアクションが可能になります。詳細については、[MDN Web Docs: EventTarget addEventListener() メソッド](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener)を参照してください。
* **拡張のための堅固な基盤**: Tealium同意登録は、高度なカスタマイズオプションを提供し、将来の新機能の追加を容易にする堅牢な新システムを導入します。

## 動作原理

Tealium同意登録は、同意決定をウェブサイトのコード全体で共有することにより、同意管理を改善します。これにより、Google同意モードなどの機能がこれらの決定にアクセスして適切なアクションを取ることが可能になります。これは同意信号の標準化レイヤーとして機能し、それらの標準化された同意信号をウェブページ上で簡単に利用できるようにします。

## Google同意モード

基本的な背景とコンテキストについては、[Google同意モード](https://docs.tealium.com/google-consent-mode/)を参照してください。ページにGoogleタグを統合する適切なタイミングと方法については、リーダーシップおよび法務チームに相談することが重要です。

### 前提条件

* CMPから既存の同意モード機能を無効にして、競合を防ぎます。
* 使用ケースに基づいて、Consent IntegrationsフレームワークまたはConsent Managerの`cmGeneral`テンプレートの最新バージョンに更新します。
* 同意モードマッピングのためのJavaScript拡張を追加します。詳細については、[同意目的マッピング](https://docs.tealium.com/google-consent-mode/#consent-purpose-mapping)を参照してください。
* [Google同意モードタグ](https://docs.tealium.com/google-consent-mode-tag/)をインストールします。同意目的マッピング拡張からの変数名を使用する場合、追加のマッピングは必要ありません。
* 同意モードタグ（および関連するすべてのGoogleタグ）を適切に分類します。高度な同意モードを実装している場合は常に発火を許可し、適切な同意がある場合のみ発火を許可するようにします。

## 高度な使用例

### 同意決定へのアクセス

`window.tealiumConsentRegister.currentDecision`オブジェクトを使用すると、ウェブページ上の現在の同意決定に直接アクセスできます。これにより、次のようなカスタムアクションの実装が簡素化されます：

* ベンダーへのオプトアウトイベントの送信により、オーディエンスからの削除と完全な下流での非アクティブ化を可能にします。
* CMPが提供するものに加えて、Tealium iQ拡張を使用した同意ログの追加レイヤー。
* 同意変更の追跡、JavaScript APIコールを通じて現在の決定にアクセスを可能にします。

Consent IntegrationsとConsent Managerの場合、配列内の目的IDは特定の構成ごとに異なります。

```
// 現在の決定を取得
var currentDecision = window.tealiumConsentRegister.currentDecision

// 現在のページが読み込まれてから登録されたすべての決定を取得
var allDecisionsOnThisPage = window.tealiumConsentRegister.decisions
```

**OneTrustを使用したConsent Integrationsの例**

この例では、オプトインモデル（暗黙の決定）で開始し、説明のためにオプトインおよびオプトアウトを行います。

![](https://docs.tealium.com/images/iq-tag-management/consent-register-and-consent-integrations.png)

### 同意変更の監視

同意登録は、ページ上で`implicit`または`explicit`同意信号が最初に検出されたとき、または同意決定が更新されたときにイベントを発生させます。

```
// 同意変更を表面化するためのイベントリスナーの例を構成

// ページコードごとに一度実行できるように実装 - 使用ケースに応じてPre LoaderまたはDOM Readyを使用できます
window.addEventListener('consent_loaded', (event) => {
  console.log('Consent loaded:', event.detail.decision);
});

window.addEventListener('consent_updated', (event) => {
  console.log('Consent updated:', event.detail.decision);
});
```

**初回訪問時にオプトインするヨーロッパのユーザーのConsent Manager例**

![](https://docs.tealium.com/images/iq-tag-management/consent-register-and-consent-manager.png)


<blockquote>
透明性のため、これらの決定には常に`always_on`カテゴリが含まれます。これは、`omitted`タグが常に許可されるためです。
</blockquote>


### タグが発火を許可されているかどうかを確認

`isTagAllowed`メソッドを使用すると、現在の同意構成とユーザー決定に基づいて特定のTealium iQタグが発火を許可されているかどうかを確認できます。このメソッドの主な使用例は、以前に許可されていたタグの同意が取り消された場合のフォールバック動作です。

```javascript
window.tealiumConsentRegister.isTagAllowed(tagId);
```

* `tagId`（整数または文字列）: チェックするタグのUIDで、Tealium iQのタグに表示されます。このメソッドは、数値または数値に変換可能な文字列（例えば、「7」）を受け入れます。
* 戻り値はブール値: タグが必要な同意を持っている場合は`true`、タグが許可されていない、存在しない、または同意が与えられていない場合は`false`です。

どちらの条件も当てはまらない場合、または`tagId`が存在しない場合、メソッドは`false`を返します。

#### オプトアウト処理

`isTagAllowed`メソッドをTealium iQタグテンプレートに統合するには、テンプレートを編集するか、タグスコープの拡張を使用します。同意が取り消されたときにベンダー固有のオプトアウトアクションを処理するコールバックを構成します。以前に許可されていたタグが後でブロックされた場合、コールバックは次のことができます：

* ベンダーへのオプトアウトリクエストをトリガーします。
* ページからベンダーのオブジェクトを削除して、さらなるデータ送信を停止します。
* ベンダー固有のクッキーを削除します。
* その他の関連するクリーンアップアクションを実行します。

これらのコールバックをタグスコープの拡張または直接タグテンプレートに追加します。

#### タグ内での統合例（タグスコープの拡張、ハードコードされたUID）

```javascript
// コールバックを一度だけ追加することを確認してください（新しいタグスコープのブール値を使用）
if (!u.consent_callback_initialized) {
  u.consent_callback_initialized = true;
  window.addEventListener('consent_updated', (event) => {
    var exists = window.tealiumConsentRegister &&
                 typeof window.tealiumConsentRegister.isTagAllowed === "function";
    if (exists && !window.tealiumConsentRegister.isTagAllowed(7)) {
      console.log("Opt-out signal triggered for tag 7.");
      // ここで適切な、ベンダー固有のオプトアウトロジックを実装します。
      // 必要に応じて重複を排除します
    }
  });
}
```
#### タグ内の例示的な統合（テンプレートコード、動的UID）


<blockquote>
文字列 `##UTID##` はタグの一意のIDを表す動的なプレースホルダーです。この値は実行時にTealiumによって自動的に実際のタグIDに置き換えられます。手動で `##UTID##` を自分の値に置き換える必要はありません。
</blockquote>


```javascript
// コールバックを一度だけ追加するようにしてください（新しいタグスコープのブール値を使用）
if (!u.consent_callback_initialized) {
  u.consent_callback_initialized = true;
  window.addEventListener('consent_updated', (event) => {
    var exists = window.tealiumConsentRegister &&
                 typeof window.tealiumConsentRegister.isTagAllowed === "function";
    if (exists && !window.tealiumConsentRegister.isTagAllowed("##UTID##")) {
      console.log("タグ " + "##UTID##" + " に対するオプトアウト信号がトリガーされました");
      // ここで適切なベンダー固有のオプトアウトロジックを実装し、
      // 必要に応じて重複を排除します
    }
  });
}
```

## 同意イベントとリスナーのフローダイアグラム

新しいイベントとリスナーを説明するためのフローの簡略化された概要です。

![](https://docs.tealium.com/images/iq-tag-management/consent-register-flow.png)

## Tealium 同意レジスタの抑制

プリローダー拡張機能で `suppressConsentRegister` フラグを構成することにより、同意レジスタを抑制できます。

同意レジスタを抑制するには、プリローダースコープのJavaScriptコード拡張機能に次のコードを追加します：

```javascript
window.tealiumCmpIntegration = window.tealiumCmpIntegration || {};
window.tealiumCmpIntegration.suppressConsentRegister = true;
```


<blockquote>
この構成は慎重に使用してください。これにより、**すべての**同意レジスタ機能が抑制されます。
</blockquote>

