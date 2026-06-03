---
title: カスタムCMP統合
description: この記事では、Tealium iQ Consent Integrationsでカスタム同意管理プラットフォームを構成する方法について説明します。
url: https://docs.tealium.com/ja/consent/client-side/consent-integrations/custom-cmp/
---
## 仕組み

Tealium Consent Integrationsは、以下の2つの部分で構成されています：

* Tealium iQ用の同意強制フレームワーク（`utcm_framework`テンプレート）。
* Tealium iQの同意強制フレームワークを活用するCMP特有の統合テンプレート。これらの統合テンプレートはできるだけ軽量に設計されています。

私たちの[事前構築された統合]()は、様々な同意管理プラットフォーム（CMP）との統合をサポートしています。しかし、以下のような場合にはカスタム統合が推奨されます：

* 事前に構築された統合がないCMPを使用する場合。
* 同意をキャプチャするための内部ツールを使用する場合。
* 標準の統合を破る広範なカスタマイズを伴うサポートされているCMPを使用する場合。

このような場合には、カスタム統合を使用できます。JavaScript関数を使用することで、任意の同意キャプチャツールが強制フレームワークを活用できます。

新しいカスタム統合を追加するには、既存の統合と提供されたテンプレートをガイドとして使用してください。

以下は、カスタム統合を作成するための基本的なワークフローを説明しています：
1. Tealium iQの外部（CMPが実装されているウェブサイト）で統合を開発およびデバッグします。
1. Tealium iQで新しいカスタム同意統合および目的グループを追加します。詳細については、[同意統合と目的グループの管理]()を参照してください。
1. 目的グループ内の目的にTealium iQおよび適切なタグを割り当てます。
1. テンプレートを作成するには、プロファイルを保存します。
1. 新しく作成されたテンプレートを編集します。詳細については、を参照してください。
1. 開発環境またはテスト環境にテンプレートを公開して、すべてが期待通りに動作することを確認し、その後通常のテストおよび公開フローに従ってください。

## カスタム統合の開発、デバッグ、および検証

カスタムCMP統合を作成するには、以下の[カスタムテンプレート](#custom-integration-template)を編集してCMPの要件に合わせます。カスタムテンプレートのコメントを参照して、動作例を確認してください。

### 公開前の開発とデバッグ

開発中にデバッグするために以下のステップを完了してください：
1. [カスタムテンプレート](#custom-integration-template)の最後にある**デバッグ**ブロックのコメントを外します。
1. サポートしたいCMPを実行しているウェブサイトのコンソールにテンプレートを貼り付けます。
1. デバッグコードブロックが同意決定を出力します。
1. 決定をカスタマイズしてテンプレートを再度貼り付け、新しく解釈された同意決定を確認します。
1. テンプレートに満足したら、Tealium iQに貼り付けて公開する前に再度デバッグブロックをコメントアウトします。

プロファイルを保存して[テンプレートを編集]()することで、デバッグスニペットも見つけることができます。

### 公開後の検証

公開後にテンプレートをデバッグおよび検証する方法は2つあります：デバッグモードを使用するか、`window.tealiumCmpOutput`オブジェクトを使用するかです。

#### デバッグモードの使用

[デバッグモード]()を使用するには：
* コンソールで`document.cookie = &#34;utagdb=true&#34;`を構成して`utagdb`クッキーを`true`に構成します。
* 関連する出力のみを表示するようにコンソールフィルターを構成します（デバッグ出力に推奨されるフィルターがあります）。
* 期待通りに動作するかどうか、異なるオプションをテストします。

#### `window.tealiumCmpOutput`オブジェクトの使用

`window.tealiumCmpOutput`オブジェクトを使用するには：
* テンプレートの下部にコメントアウトされたデバッグコードブロックをコンソールに貼り付けて、あなたの決定と関連する出力のみを出力します。
* 必要に応じて、テンプレート内の関数を個別に呼び出すか、このオブジェクトの他の便利なプロパティにアクセスすることもできます。

事前構築された統合およびカスタム統合の詳細なデバッグのヒントについては、[同意統合の検証とデバッグ]()を参照してください。

## 統合機能

統合のCMP特有のコンポーネントは、`window.tealiumCmpIntegration`オブジェクトを使用して定義されます。

`window.tealiumCmpIntegration`オブジェクトは、名前`.cmpName`、バージョン`.cmpIntegrationVersion`、および以下の関数で構成されています：

### 動作モードの決定

* `.cmpCheckIfOptInModel` - 統合が`opt-in`モデルまたは`opt-out`モデルのどちらで動作するかを決定します。ブール値を返します。

### 決定の取得

* `.cmpFetchCurrentConsentDecision` - 同意決定の現在の生バージョン（CMPからの生バージョン）を取得します。結果はオブジェクトでなければならず、すべての後続の関数に引数として渡されます。

### 決定の検証と標準化

* `.cmpCheckForWellFormedDecision` - 同意決定の生バージョンが適切に形成され、理解可能であるかどうかをチェックします。ブール値を返します。

* `.cmpCheckForTiqConsent` - 生の同意決定にTealium iQによるデータ処理の許可が含まれているかどうかを決定します。falseの場合、何も実行されません。ブール値を返します。

* `.cmpCheckForExplicitConsentDecision` - 生の同意決定が`明示的`か`暗黙的`かを決定します。ブール値を返します。

* `.cmpConvertResponseToGroupList` - 生の決定を下流の強制のための許可された目的キーの単純な配列に変換します。同意された目的キーの配列を返します。

### 同意更新の監視とトリガー

* `.cmpAddCallbackToTriggerRecheck` - CMPの同意ステータスが変更されるたびに呼び出されるコールバック関数を登録します。これにより、ポーリングに依存せずにTealium iQが最新の同意決定を迅速に更新できるようになります。

  `cmpAddCallbackToTriggerRecheck`は、CMPがコールバックまたは代替実装方法を通じて同意ステータスの変更を通知するたびに`triggerRecheck()`を呼び出すように構成されていることを確認してください。暗黙の同意のためにバナーが表示されるときやCMPのロード時の類似点で`triggerRecheck()`を呼び出します。詳細については、[カスタム統合テンプレート](#custom-integration-template)のコメントを参照してください。現在コールバックをサポートしている統合については、を参照してください。
## カスタム統合テンプレート

以下は、独自のカスタム統合を開始するための空白テンプレートです。このテンプレートには、テンプレートの最後にデバッグスニペットが含まれており、コンセント統合のデバッグと検証に使用できます。



```js
;(function myCustomConsentIntegration (window) {
  /**
    * このテンプレートは編集を目的としており、カスタムCMP/キャプチャツールのサポートを構築するために使用されます。
    *
    * 例示コード（コメントアウトされている）は、オプトアウトクッキーをチェックし、次の2つの決定のいずれかを返す統合から取得されています：
    *  - [&#39;no-selling&#39;]（任意の値が見つかったオプトアウトクッキー） - 常に明示的な決定（オプトアウトクッキーが構成されています）
    *  - [&#39;no-selling&#39;, &#39;yes-selling&#39;]（オプトアウトクッキーが見つからない） - 常に暗黙的な決定（クッキーが構成されていません）
    *
    * オプトアウトクッキーの（大文字と小文字を区別する）名前はUIの「Vendor ID」フィールドから取得されます。
    *
    * 詳細については、https://docs.tealium.com/iq-tag-management/consent-integrations/supported-vendors/#opt-out-cookie--gpc を参照してください。
    * 
    * （上記の統合はこの例のために簡略化されました - GPCロジックは削除されました）
    */

  // CMP特有の機能とラベル
  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = &#39;Custom Example&#39;
  window.tealiumCmpIntegration.cmpIntegrationVersion = &#39;v1.1.0&#39;

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList

  // 以下の行を削除（コメントアウト）してください。ポーリングを使用したい場合や、ソリューションがコールバックをサポートしていない場合です
  window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck = cmpAddCallbackToTriggerRecheck;

  /*
  // UIで入力されたVendor IDを単一の関連統合のために引っ張ってくる
  var optOutCookieName = (window.tealiumCmpIntegration &amp;&amp; window.tealiumCmpIntegration.map &amp;&amp; Object.keys(window.tealiumCmpIntegration.map)[0]) || &#39;error-no-map-found-so-no-cookie-name-available&#39;
  */

  // CMPが「オプトイン」モデル（GDPRスタイル）を実行している場合は真を返す必要があります
  // このオプトアウトクッキーの例はオプトアウトモデル（CCPA/CPRAスタイル）のみをサポートしているため、これはfalseを返すようにハードコードされています。
  function cmpCheckIfOptInModel () {
    /*
    return false
    */
  }

  // CMP特有の生のオブジェクト（オブジェクトでなければならない）を返す必要があります。これには、決定に関する必要な情報が含まれています。
  // この出力は、以下の関数でcmpRawOutput引数として使用されます。
  function cmpFetchCurrentConsentDecision () {
    /*
    // まだタグマネージャーの機能を使用できません。許可されていないためです
    var readCookie = function (name) {
      var reString = &#39;(?:(?:^|.*;\\s*)&#39; &#43; name &#43; &#39;\\s*\\=\\s*([^;]*).*$)|^.*$&#39;
      var re = new RegExp(reString)
      var cookieValue = document.cookie.replace(re, &#39;$1&#39;)
      if (!cookieValue) return undefined
      return cookieValue
    }
    var cookie = readCookie(optOutCookieName) || &#39;opt-out-cookie-not-found&#39;
    return { cookieState: cookie } // 統合を機能させるためにオブジェクトを返す必要があります - これにより、後で他のプロパティ（グローバルプライバシーコントロールなど）を追加できます
    */
  }

  // Tealium iQが正しいCMP構成を持っていることを確認するのに役立つ文字列を返す必要があります（他のページ/ CMPの他の顧客のものではありません）
  function cmpFetchCurrentLookupKey () {
    /*
    return optOutCookieName
    */
  }

  // 生の決定がCMPの期待に合っている場合は真を返す必要があります
  function cmpCheckForWellFormedDecision (cmpRawOutput) {
    /*
    return typeof cmpRawOutput === &#39;object&#39; &amp;&amp; typeof cmpRawOutput.cookieState === &#39;string&#39;
    */
  }

  // 同意決定がユーザーによって明示的に行われた場合は真を返す必要があります
  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
    /*
    // この例では、決定が明示的であるかどうかを判断する唯一の方法は、オプトアウトクッキーが構成されているかどうかを確認することです
    if ((typeof cmpRawOutput === &#39;object&#39; &amp;&amp; typeof cmpRawOutput.cookieState === &#39;string&#39; &amp;&amp; cmpRawOutput.cookieState !== &#39;opt-out-cookie-not-found&#39;)) return true
    return false
    */
  }

  // 同意されたベンダー/目的の配列を返す必要があります - これらはTealium iQの目的と正確に一致する必要があります
  function cmpConvertResponseToGroupList (cmpRawOutput) {
    /*
    var consentDecision = [&#39;no-selling&#39;] // データを売却/共有しないタグは常に許可されます
    // タグがデータを売却することが許可されているかどうかを判断するために、空でないオプトアウトクッキーを簡単にチェックします
    if (cmpRawOutput.cookieState === &#39;opt-out-cookie-not-found&#39;) {
      consentDecision.push(&#39;yes-selling&#39;) // クッキーが見つからないので、データの売却/共有が問題ないと仮定しなければなりません
    }
    return consentDecision
    */
  }

  // 基盤となるフレームワークがサポートしている場合、一部のポーリングを避けるために着信コールバック機能を使用します
  // トリガーチェック関数を頻繁に呼び出す方が良いです（ネガティブな影響はありません） - 同意の変更とそれに伴うデータを見逃すよりも少ないです（問題があります）。
  // CMPの同意ステータスに変更があるたびにトリガーチェックを呼び出す必要があります。例えば：
  //  - 初期同意ポップアップ（オプトインモデルでの暗黙の同意）
  //  - 明示的な同意の変更
  //  - 以前の決定が行われたときの初期CMPロード
  // この関数がウィンドウスコープオブジェクトに含まれていない場合、ポーリングが代わりに使用されます
  function cmpAddCallbackToTriggerRecheck (triggerRecheck) {
    // この例では、例と一致するようにクッキーの変更をリスンするリスナーを構成していますが、適切なものをリスンすることができます
    /*
    (function() {
        // 元のdocument.cookie記述子
        const originalCookieDescriptor = Object.getOwnPropertyDescriptor(Document.prototype, &#39;cookie&#39;);

        // カスタムイベントを作成
        function emitCookieChange(value) {
          const event = new CustomEvent(&#39;cookieUpdated&#39;, {
            detail: {
              cookies: value
            }
          });
          document.dispatchEvent(event);
        }

        // document.cookieプロパティをオーバーライド
        Object.defineProperty(document, &#39;cookie&#39;, {
          get: function() {
            return originalCookieDescriptor.get.call(document);
          },
          set: function(value) {
            originalCookieDescriptor.set.call(document, value);
            emitCookieChange(value);
          }
        });
      })();

      // 例のリスナー
      document.addEventListener(&#39;cookieUpdated&#39;, (e) =&gt; {
        // オプトアウトクッキーが更新されたときにコールバック関数をトリガーします（ここでのいくつかの偽陽性は問題ありません）
        if ((e.detail.cookies.indexOf(optOutCookieName)) !== -1) {
            triggerRecheck();
        }
      });
    */
  }

  // この関数やそれ以下のものを変更する必要はありません
  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
    // 理解できないものはオプトアウトとして扱います
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false

    tiqGroupName = tiqGroupName || &#39;tiq-group-name-missing&#39;
    var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput)
    return allowedGroups.indexOf(tiqGroupName) !== -1
  }
})(window)

/*
// デバッグ/開発出力 - このブロックのコメントを外し、このテンプレート全体をテストページに貼り付け/再貼り付けしてください
var outputString = `${tealiumCmpIntegration.cmpCheckIfOptInModel() ? &#39;Opt-in&#39; : &#39;Opt-out&#39;} Model

Checks:
  - id:          ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
  - well-formed: ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
  - explicit:    ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
  - group list:  ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()))}
`
console.log(outputString);
*/
```


