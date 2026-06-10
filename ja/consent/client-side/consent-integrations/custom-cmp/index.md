---
title: カスタムCMP統合
description: この記事では、クライアントサイドの同意統合でカスタム同意管理プラットフォームを構成する方法について説明します。
url: https://docs.tealium.com/ja/consent/client-side/consent-integrations/custom-cmp/
---
## 仕組み

クライアントサイドの同意統合は、以下の二部分から構成されます：

* Tealium iQの同意強制フレームワーク（`utcm_framework` テンプレート）。
* Tealium iQの同意強制フレームワークを活用するCMP特有の統合テンプレート。これらの統合テンプレートはできるだけ軽量に設計されています。

私たちの[事前構築された統合]()は、様々な同意管理プラットフォーム（CMP）との統合をサポートしています。しかし、以下のような場合にはカスタム統合が推奨されます：

* 事前に構築された統合がないCMPを使用する場合。
* 同意をキャプチャするための内部ツールを使用する場合。
* 標準の統合を破壊する広範なカスタマイズを伴うサポートされているCMPを使用する場合。

このような場合、カスタム統合を使用できます。JavaScript関数を使用することで、任意の同意キャプチャツールが強制フレームワークを活用できます。

新しいカスタム統合を追加するには、既存の統合と提供されたテンプレートをガイドとして使用してください。

以下は、カスタム統合を作成するための基本的なワークフローを説明しています：
1. Tealium iQの外部（CMPが実装されているウェブサイト）で統合を開発およびデバッグします。
1. Tealium iQで新しいカスタム同意統合と目的グループを追加します。詳細については、[同意統合と目的グループの管理]()を参照してください。
1. Tealium iQと適切なタグを目的グループ内の目的に割り当てます。
1. テンプレートを作成するために、プロファイルを保存します。
1. 新しく作成されたテンプレートを編集します。詳細については、を参照してください。
1. 開発環境またはテスト環境にテンプレートを公開して、すべてが期待通りに動作することを確認し、その後通常のテストおよび公開フローに従ってください。

## 統合機能

統合のCMP特有のコンポーネントは、`window.tealiumCmpIntegration` オブジェクトを使用して定義されます。

`window.tealiumCmpIntegration` オブジェクトは、名前 `.cmpName`、バージョン `.cmpIntegrationVersion`、および以下の関数で構成されます：

### 動作モードの決定

* `.cmpCheckIfOptInModel` - 統合が `opt-in` モデルまたは `opt-out` モデルで動作するかどうかを決定します。ブール値を返します。

### 決定の取得

* `.cmpFetchCurrentConsentDecision` - CMPからの同意決定の現在の生バージョンを取得します。結果はオブジェクトでなければならず、すべての後続の関数に引数として渡されます。

### 決定の検証と標準化

* `.cmpCheckForWellFormedDecision` - 同意決定の生バージョンが適切に形成され、理解可能であるかどうかをチェックします。ブール値を返します。

* `.cmpCheckForTiqConsent` - 生の同意決定にTealium iQによるデータ処理の許可が含まれているかどうかを決定します。falseの場合、何も実行されません。ブール値を返します。

* `.cmpCheckForExplicitConsentDecision` - 生の同意決定が `明示的` か `暗黙的` かを決定します。ブール値を返します。

* `.cmpConvertResponseToGroupList` - 生の決定を下流の強制のための許可された目的キーの単純な配列に変換します。同意された目的キーの配列を返します。

`cmpConvertResponseToGroupList` によって返される目的キーは、同意統合で構成された目的名と正確に一致する必要があります。**Vendor ID** フィールドは、Tealium iQ UIでテンプレートが関連するCMPクッキーまたは識別子を識別するために使用されます。この値はCMPの使用例でのクッキー名または識別子と一致する必要があります。大文字と小文字を区別します。

### 同意更新の監視とトリガー

* `.cmpAddCallbackToTriggerRecheck` - CMPの同意ステータスが変更されるたびに呼び出されるコールバック関数を登録します。これにより、Tealium iQはポーリングに頼ることなく最新の同意決定を迅速に更新できます。

  `cmpAddCallbackToTriggerRecheck` は、CMPがコールバックまたは代替実装方法を通じて同意ステータスの変更を通知するたびに `triggerRecheck()` を呼び出すように構成されていることを確認してください。バナーが暗黙的同意のために表示されるときやCMPの読み込み時の類似点で `triggerRecheck()` を呼び出します。詳細は、[カスタム統合テンプレート](#custom-integration-template) のコメントを参照してください。現在コールバックをサポートしている統合については、を参照してください。

## カスタム統合テンプレート

カスタムCMP統合を作成するには、以下の空白テンプレートを編集してCMPの要件に合わせます。テンプレートにはコメントが含まれており、動作例を参照してください。テンプレートの最後には、コンセント統合をデバッグおよび検証するために使用できるデバッグスニペットが含まれています。



```js
;(function myCustomConsentIntegration (window) {
  /**
    * このテンプレートは編集を意図しており、カスタムCMP/キャプチャツールのサポートを構築するために使用します。
    *
    * 例として挙げられているコード（コメントアウトされています）は、オプトアウトクッキーをチェックし、以下の二つの決定のいずれかを返す統合から取られています：
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

  // ポーリングを使用したい場合は以下の行を削除（コメントアウト）してください / あなたのソリューションがコールバックをサポートしていない場合
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

  // CMP特有の生のオブジェクト（オブジェクトでなければならない）を返す必要があります。これには決定に関する必要な情報が含まれています。
  // この出力は、以下の関数でcmpRawOutput引数として使用されます。
  function cmpFetchCurrentConsentDecision () {
    /*
    // ここではタグマネージャーの機能を使用できません。なぜならそれがまだ許可されていないからです
    var readCookie = function (name) {
      var reString = &#39;(?:(?:^|.*;\\s*)&#39; &#43; name &#43; &#39;\\s*\\=\\s*([^;]*).*$)|^.*$&#39;
      var re = new RegExp(reString)
      var cookieValue = document.cookie.replace(re, &#39;$1&#39;)
      if (!cookieValue) return undefined
      return cookieValue
    }
    var cookie = readCookie(optOutCookieName) || &#39;opt-out-cookie-not-found&#39;
    return { cookieState: cookie } // 統合が機能するためにはオブジェクトを返す必要があります - これにより、後で他のプロパティ（グローバルプライバシーコントロールなど）を追加することができます
    */
  }

  // Tealium iQが正しいCMP構成を持っていることを確認するのに役立つ文字列を返す必要があります（他のページ/ CMPの他の顧客からではない）
  function cmpFetchCurrentLookupKey () {
    /*
    return optOutCookieName
    */
  }

  // 生の決定がCMPの期待に合致している場合は真を返す必要があります
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
    // タグがデータを売却/共有してもよいかどうかを判断するために、空でないオプトアウトクッキーを非常に単純にチェックします
    if (cmpRawOutput.cookieState === &#39;opt-out-cookie-not-found&#39;) {
      consentDecision.push(&#39;yes-selling&#39;) // クッキーが見つからないので、データの売却/共有が問題ないと仮定しなければなりません
    }
    return consentDecision
    */
  }

  // 基盤となるフレームワークがサポートしている場合、ポーリングを避けるために着信コールバック機能を使用します
  // トリガーリチェック関数を頻繁に呼び出す方が良いです（ネガティブな影響はありません） - 同意の変更とそれに伴うデータを見逃すよりも少ないです（少なすぎると問題が発生します）。
  // CMPの同意ステータスに変更があるたびにトリガーリチェックを呼び出す必要があります。たとえば：
  //  - 初期同意ポップアップ（オプトインモデルの暗黙の同意）
  //  - 明示的な同意の変更
  //  - 以前の決定が行われたときの初期CMPロード
  // この関数がウィンドウスコープのオブジェクトに含まれていない場合、代わりにポーリングが使用されます
  function cmpAddCallbackToTriggerRecheck (triggerRecheck) {
    // この例では、例と一致するようにクッキーの変更をリスンするリスナーを構成していますが、適切なものをリスンすることができます
    /*
    (function() {
        // 元のdocument.cookieディスクリプタ
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
        // オプトアウトクッキーが更新されたときにコールバック関数をトリガーします（ここではいくつかの誤検知があります）
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
  // Debugging / development output - uncomment this block, then paste/repaste this entire template on your test pages
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


## 開発とデバッグを行ってから公開する

カスタムCMPインテグレーションを作成するには、[カスタムインテグレーションテンプレート](#custom-integration-template)を編集してCMPの要件に合わせます。カスタムテンプレートのコメントを参照して、動作例を確認してください。

開発中にデバッグを行うための次のステップを完了してください：
1. [カスタムインテグレーションテンプレート](#custom-integration-template)の最後にある**デバッグ**ブロックのコメントを外します。
1. テンプレートをサポートしたいCMPを実行しているウェブサイトのコンソールに貼り付けます。
1. デバッグコードブロックが同意決定を出力します。
1. あなたの決定をカスタマイズし、新しく解釈された同意決定を見るためにテンプレートを再度貼り付けます。
1. テンプレートに満足したら、Tealium iQに貼り付けて公開する前に再びデバッグブロックをコメントアウトします。

デバッグスニペットは、プロファイルを保存して[テンプレートを編集]()することで見つけることができます。

## 公開後の検証

公開後にテンプレートをデバッグして検証する方法は2つあります：デバッグモードを使用するか、`window.tealiumCmpOutput`オブジェクトを使用するかです。

### デバッグモードを使用する

[デバッグモード]()を使用するには：
* コンソールで`document.cookie = &#34;utagdb=true&#34;`を構成して`utagdb`クッキーを`true`に構成します。
* 関連する出力のみを表示するようにコンソールフィルターを構成します（デバッグ出力で提案されているフィルターを使用します）。
* 期待通りに動作するかどうか、異なるオプションをテストします。

### `window.tealiumCmpOutput`オブジェクトを使用する

`window.tealiumCmpOutput`オブジェクトを使用するには：
* テンプレートの最下部にコメントアウトされているデバッグコードブロックをコンソールに貼り付けて、あなたの決定と関連する出力のみを出力します。
* 必要に応じて、テンプレート内の関数を個別に呼び出すか、このオブジェクトの他の便利なプロパティにアクセスすることもできます。

プリビルトおよびカスタムインテグレーションのより詳細なデバッグのヒントについては、[同意インテグレーションの検証とデバッグ]()を参照してください。