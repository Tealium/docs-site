---
title: 同意連携の検証とデバッグ
description: この記事では、クライアント側の同意連携を検証およびデバッグする方法について説明します。
url: https://docs.tealium.com/ja/consent/client-side/consent-integrations/validate-and-debug/
---
## 公開前に同意連携を検証する

他の依存関係を含めずに、連携テンプレートをサイトのJavaScriptコンソールへ貼り付けて、同意連携を検証およびデバッグします。同意連携テンプレートは編集可能で、スタンドアロンで動作するように設計されているため、Webサイトのコンソールからデバッグできます。

テンプレートを使用して[カスタム連携を作成](https://docs.tealium.com/custom-cmp-integrations/)したり、ベンダーIDや目的キーを取得したり、構成前にデフォルトのテンプレートがカスタマイズなしで使用中のCMPインスタンスに対して機能することを確認したりできます。検証用スニペットを含む現在のテンプレートについて詳しくは、[サポートされているベンダー連携](https://docs.tealium.com/vendor-specific-configuration/)を参照してください。


## 公開後にデバッグモードを有効にする

Tealium iQの[デバッグモード](https://docs.tealium.com/platforms/javascript/debugging/)には、機能が有効な場合、免除が適用されない限り、同意連携からの詳細なステータスおよびエラーメッセージが表示されます。免除されている場合は、`window.tealiumCmpIntegration`が定義され、`window.tealiumCmpIntegration.exemptionMap`に有効な免除が表示されます。


<blockquote>
コンソール出力で関連するデバッグメッセージのみを表示するには、フィルターとして`/SENDING|\\\\*/`を使用します。
</blockquote>


## 公開後に同意連携を検証する

クライアント側の同意連携では、デバッグに役立つ多数のプロパティを持つ`window.tealiumCmpIntegration`というグローバルオブジェクトがDOMに作成されます。また、各コンポーネント関数を個別に呼び出して、デバッグと検証を容易にすることもできます。コンポーネント関数について詳しくは、[カスタムCMP連携](https://docs.tealium.com/custom-cmp-integrations/)を参照してください。

### 例

この例では、CMP連携に関する重要な情報を取得する方法について説明します。

CMP連携に関する重要な情報を確認し、顧客の選択が正しく取得されていることを確認するには、次の手順を実行します。

1. この[デモサイト](https://www.otprivacy.com/user/jmyles/TagManagerDemo/OTKicks_Tealium/index.html?otreset=false&otpreview=true&otgeo=IE)、または同意連携が有効な任意のサイトにアクセスし、次のスニペットをブラウザーコンソールに貼り付けます。
    ```js
    var outputString = `${tealiumCmpIntegration.cmpName} - ${tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model

    Checks:
      - vendor id:            ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
      - well-formed decision: ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
      - explicit decision:    ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
      - consented purposes:   ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()).sort(),null, 8)}
    `
    console.log(outputString)

    ```
1. 上記のスニペットをデモサイトのコンソールに貼り付けると、次の結果が返されます。
    ```
    OneTrust - Opt-in Model

    Checks:
      - vendor id:            b38364e4-b2c4-4349-8e4e-48cf28a35db8
      - well-formed decision: true
      - explicit decision:    false
      - consented purposes:   [
            "C0001"
    ]
    ```
1. Webページで**すべてのCookieを許可**をクリックし、同じスニペットを再度貼り付けます。次の出力は、連携が選択内容を正しく解釈して取得したことを示します。
    ```
    OneTrust - Opt-in Model

    Checks:
      - vendor id:            b38364e4-b2c4-4349-8e4e-48cf28a35db8
      - well-formed decision: true
      - explicit decision:    true
      - consented purposes:   [
            "C0001",
            "C0002",
            "C0003",
            "C0004"
    ]

    ```


## 公開後に競合と適用ルールをデバッグする

公開後に`window.tealiumCmpIntegration`を使用して同意の適用状況を調査し、競合を特定して、ブロックされたタグの問題をトラブルシューティングします。

このオブジェクトには、次のプロパティが含まれています。

* `loadRules`：どの同意連携が適用されているか、および競合が発生したかどうかを特定するプロパティが含まれます。競合が発生すると、タグ管理とすべてのタグがブロックされます。
* `map`および`tagBasedMap`：タグUIDと目的キーの間の異なるマッピングを示します。
* `tiqGroupName`：目的キーをタグ管理にマッピングします。
* `cmpName`：連携テンプレートによって判定された、有効な同意管理プラットフォーム（CMP）を識別します。
* `cmpIntegrationVersion`：ベンダー固有の連携テンプレートのバージョンを識別します。
* `version`：基盤となる同意適用フレームワークのバージョンを識別します。
* `originalEvents`：適用をトリガーする各イベントの元のイベントペイロードを、イベントID（`tci.event_id`）をキーとして保存します。イベントIDは自動的に割り当てられ、データレイヤーの後続処理に渡されます。
* `blockedTagsByEvent`：同意の選択によってブロックされたタグを、イベント別に記録します。各キーでは`<tci.event_id>||<consent-type>`という形式を使用します（例：`1234567890||implicit`）。各値は、ブロックされたタグUIDを`1`に構成したオブジェクトです。

  ブロックされたタグに関連付けられたイベントペイロードを調査するには、イベントIDを使用して`originalEvents`内の対応するエントリを見つけます。

  ブロックが発生するたびに、ブロックされたタグがブラウザーコンソールに記録されます。バージョン1.4.0以降、`blockedTagsByEvent`には、同意の選択によってブロックされたタグのみが含まれます。ロードルールの条件を満たさないタグは除外されます。

連携固有のプロパティについて詳しくは、[カスタムCMP連携](https://docs.tealium.com/custom-cmp-integrations/)を参照してください。