---
title: 同意統合の検証とデバッグ
description: この記事では、クライアントサイドの同意統合を検証およびデバッグする方法について説明します。
url: https://docs.tealium.com/ja/consent/client-side/consent-integrations/validate-and-debug/
---
## 公開前の同意統合を検証する

同意統合テンプレートをサイトのJavaScriptコンソールに貼り付けて、他の依存関係なしで同意統合を検証およびデバッグします。同意統合テンプレートは編集可能であり、ウェブサイトのコンソールからデバッグを行うために独立して設計されています。

テンプレートは[カスタム統合を作成する](https://docs.tealium.com/custom-cmp-integrations/)ために使用でき、ベンダーID、目的キーを取得するか、またはデフォルトテンプレートがカスタマイズなしでCMPのインスタンスに適合するかを確認する前に構成します。現在のテンプレートと検証スニペットについての詳細は、[サポートされているベンダー統合](https://docs.tealium.com/vendor-specific-configuration/)を参照してください。


## 公開後のデバッグモードをアクティブにする

Tealium iQの[デバッグモード](https://docs.tealium.com/platforms/javascript/debugging/)は、機能がアクティブな場合に同意統合からの詳細なステータスとエラーメッセージを含みます。免除が適用される場合、`window.tealiumCmpIntegration`が定義され、`window.tealiumCmpIntegration.exemptionMap`でアクティブな免除を表示します。


<blockquote>
コンソール出力で関連するデバッグメッセージのみを表示するために、`/SENDING|\\\\*/`をフィルターとして使用します。
</blockquote>


## 公開後の同意統合を検証する

クライアントサイドの同意統合はDOMに`window.tealiumCmpIntegration`というグローバルオブジェクトを作成し、デバッグに役立つ多くのプロパティを持っています。また、デバッグと検証を容易にするためにコンポーネント関数を個別に呼び出すこともできます。コンポーネント関数の詳細については、[カスタムCMP統合](https://docs.tealium.com/custom-cmp-integrations/)を参照してください。

### 例

この例では、CMP統合に関する重要な情報を取得する方法について説明します。

CMP統合に関する重要な情報を確認し、顧客の決定が正しくキャプチャされていることを確認するために、次の手順を完了します：

1. この[デモサイト](https://www.otprivacy.com/user/jmyles/TagManagerDemo/OTKicks_Tealium/index.html?otreset=false&otpreview=true&otgeo=IE)またはアクティブな同意統合がある任意のサイトを訪れ、次のスニペットをブラウザのコンソールに貼り付けます：
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
1. 上記のスニペットをデモサイトのコンソールに貼り付けると、次のように返されます：
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
1. ウェブページで**Accept All Cookies**をクリックし、同じスニペットをもう一度貼り付けます。次の出力は、決定が正しく理解され、統合によってキャプチャされたことを示します：
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


## 公開後の衝突と執行ルールのデバッグ

`window.tealiumCmpIntegrations`には、ページ上でどの統合が強制されているかを理解するのに役立つ多くの便利なプロパティがあります。たとえば、`loadRules`には、どの同意統合が強制され、Tealium iQとすべてのタグがブロックされたかどうかを示す衝突があったかどうかを示す子プロパティがあります。
 - `map`と`tagBasedMap`は、タグUIDとPurpose Keysの関係を異なる視点で示します。
 - `tiqGroupName`はPurpose KeyをTealium iQ自体にマッピングします。
 - `cmpName`は現在アクティブなCMPを示します（テンプレートによる）。
 - `cmpIntegrationVersion`は使用しているベンダー固有の統合テンプレートの現在のバージョンを示します。
 - `version`は使用している基礎となる同意執行フレームワークのバージョンを示します。

このオブジェクトにも含まれている特定の統合機能の詳細については、カスタム統合の作成に関する関連する[ドキュメント](https://docs.tealium.com/custom-cmp-integrations/)を参照してください。