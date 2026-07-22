---
title: サポートされているベンダー統合
description: この記事では、クライアントサイドの同意統合でサポートされているCMPについて説明し、同意統合の構成を完了するために必要なベンダー固有の情報を簡単に収集する方法について説明します。
url: https://docs.tealium.com/ja/consent/client-side/consent-integrations/supported-vendors/
---
## 仕組み

クライアントサイドの同意統合は、さまざまな同意管理プラットフォーム（CMP）との統合をサポートしています。サポートされている同意管理プラットフォーム（CMP）のユーザーインターフェースまたはウェブページから、関連するベンダー固有の情報にアクセスできます。このドキュメントを信頼性が高くユーザーフレンドリーに保つため、このセクションではウェブページからベンダー固有の情報を取得する手順のみをカバーしています。各パートナーCMPのユーザーインターフェースでベンダーIDと目的を取得する手順については、各CMPのドキュメントを参照してください。

ウェブページから関連情報を取得するには、次の手順に従ってください：

1. CMPが実装されているウェブサイトを訪問します。
1. すべてのトラッキングを受け入れます。
1. 開発者ツールのJavaScriptコンソールを開きます。
1. 下記のコードスニペットからCMP固有のコードを開発者ツールのJavaScriptコンソールに貼り付けます。
1. 表示された**ベンダーID**、**目的キー**、および**目的名**をあなたの同意統合に入力します。


<blockquote>
同意決定を更新した後、最新の解釈を確認するためにコードを再度貼り付けてください。
</blockquote>


## 統合固有の指示とコードスニペット

### Cookiebot

[cookiebot.com](https://www.cookiebot.com/) またはあなたのウェブサイトでこのスニペットをテストし、[仕組みセクション](#how-it-works)の指示に従って互換性を確認し、統合に必要な情報を取得します。


```js

;(function cookiebotIntegration (window) {
    window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}
    window.tealiumCmpIntegration.cmpName = 'Cookiebot'
    window.tealiumCmpIntegration.cmpIntegrationVersion = 'v1.0.0'
    window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
    window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
    window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
    window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
    window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
    window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
    window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
    // GDPRスタイルの「オプトイン」モデルを実行しているかどうかを返す必要があります。ブール値を返す必要があります。
    function cmpCheckIfOptInModel () {
      if (!window.Cookiebot || !window.Cookiebot.regulations || typeof window.Cookiebot.regulations.gdprApplies !== 'boolean') return false
      return Cookiebot.regulations.gdprApplies
    }
    // 必要な情報についての決定を含むCMP固有の生のオブジェクト（オブジェクトでなければならない）を返す必要があります。
    // この出力は、以下の関数でcmpRawOutput引数として使用されます。
    function cmpFetchCurrentConsentDecision () {
      if (!window.Cookiebot || typeof window.Cookiebot.hasResponse !== 'boolean') return false
      return cmpRawOutput = window.Cookiebot.consent;
    }
    // Tealium iQが正しいCMP構成を持っていることを確認するのに役立つ文字列を返す必要があります（他のページ/ CMPの顧客ではない）。
    function cmpFetchCurrentLookupKey() {
        if (!window.Cookiebot || typeof window.Cookiebot.serial !== 'string') return false
        return Cookiebot.serial
    }
    // 生の決定がCMPの期待に合っているかどうかを返す必要があります。ブール値を返す必要があります。
    function cmpCheckForWellFormedDecision (cmpRawOutput) {
      return typeof cmpRawOutput === 'object' &&  typeof cmpRawOutput.stamp ==='string'
    }
    // 同意決定がユーザーによって明示的に行われたかどうかを返す必要があります。ブール値を返す必要があります。
    function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
      // この例では、決定が明示的であるかどうかを判断する唯一の方法は、オプトアウトクッキーが構成されているかどうかを確認することです
      return cmpRawOutput.method === 'explicit'? true : false;
    }
    // 同意されたベンダー/目的の配列を返す必要があります。これらはTealium iQの目的と正確に一致する必要があります。
    function cmpConvertResponseToGroupList(cmpRawOutput) {
        var consentDecision = []
        // データを販売/共有するタグが許可されているかどうかを判断するために、空でないオプトアウトクッキーを非常に単純にチェックします
        if (cmpRawOutput.necessary) {
            consentDecision.push('necessary') // クッキーが見えないので、データの販売/共有が問題ないと仮定しなければなりません
        }
        if (cmpRawOutput.preferences) {
            consentDecision.push('preferences') // クッキーが見えないので、データの販売/共有が問題ないと仮定しなければなりません
        }
        if (cmpRawOutput.marketing) {
            consentDecision.push('marketing') // クッキーが見えないので、データの販売/共有が問題ないと仮定しなければなりません
        }
        if (cmpRawOutput.statistics) {
            consentDecision.push('statistics') // クッキーが見えないので、データの販売/共有が問題ないと仮定しなければなりません
        }
        return consentDecision
    }
    // この関数やそれ以下のものを変更する必要はありません
    function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
      // 理解できないものはオプトアウトとして扱います
      if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false
      tiqGroupName = tiqGroupName || 'tiq-group-name-missing'
      var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput)
      return allowedGroups.indexOf(tiqGroupName) !== -1
    }
  })(window)
  /*
    // デバッグ/開発出力 - このブロックのコメントを外し、このテンプレート全体をテストページに貼り付け/再貼り付けしてください
    var outputString = `${tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model
    Checks:
      - id:          ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
      - well-formed: ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
      - explicit:    ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
      - group list:  ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()))}
    `
    console.log(outputString);
  */
 ```

### Didomi

[didomi.io](https://didomi.io)または[上記の手順に従って](#how-it-works)あなたのウェブサイトでこのスニペットをテストして、互換性を確認し、統合に必要な情報を取得してください。

Didomi統合は、**Vendors**を**Purposes**として使用します。


<blockquote>
現在のDidomiとの統合では、暗黙の同意された目的やベンダーは返されません。これは当時利用可能な唯一のオプションでした。古いバージョンを使用している顧客をサポートし、新しいアプローチを可能にするアップデートが行われるまで、この統合は無条件に出力同意決定に目的キー`always_consented`を追加します。これは暗黙のトリガリングを可能にするための回避策として機能します。
</blockquote>



```js
;(function didomiIntegration (window) {
  // CMP specific functionality and labels
  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = 'Didomi'
  window.tealiumCmpIntegration.cmpIntegrationVersion = 'didomi-1.0.1'

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
  window.tealiumCmpIntegration.cmpConvertResponseToLookupObject = cmpConvertResponseToLookupObject

  function cmpCheckIfOptInModel () {
    if (!window.Didomi || typeof window.Didomi.getConfig !== 'function') return false
    return window.Didomi.getConfig().notice.type === 'optin'
  }

  function cmpFetchCurrentConsentDecision () {
    if (!window.Didomi || typeof window.Didomi.getUserStatus !== 'function') return false
    if (typeof window.Didomi.getConfig !== 'function') return false
    var cmpRawOutput = {}
    cmpRawOutput.userStatus = window.Didomi.getUserStatus()
    cmpRawOutput.vendorInfo = window.Didomi.getVendors()
    cmpRawOutput.shouldConsentBeCollected = window.Didomi.shouldConsentBeCollected()
    return cmpRawOutput
  }

  function cmpFetchCurrentLookupKey () {
    if (!window.Didomi || typeof window.Didomi.getConfig !== 'function') return ''
    var id = window.Didomi.getConfig().app.deploymentId
    return id || ''
  }

  function cmpCheckForWellFormedDecision (cmpRawOutput) {
    // treat things we don't understand as an opt-out
    if (typeof cmpRawOutput !== 'object') return false
    if (typeof cmpRawOutput.userStatus !== 'object') return false
    // do more checks than strictly necessary to confirm expectations
    if (typeof cmpRawOutput.userStatus.purposes !== 'object') return false
    if (typeof cmpRawOutput.userStatus.vendors !== 'object') return false
    if (typeof cmpRawOutput.userStatus.purposes.global !== 'object') return false
    if (typeof cmpRawOutput.userStatus.vendors.global !== 'object') return false
    if (toString.call(cmpRawOutput.userStatus.purposes.global.enabled) !== '[object Array]') return false
    if (toString.call(cmpRawOutput.userStatus.vendors.global.enabled) !== '[object Array]') return false

    if (typeof cmpRawOutput.vendorInfo !== 'object') return false

    if (typeof cmpRawOutput.shouldConsentBeCollected !== 'boolean') return false
    return true
  }

  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
    // treat things we don't understand as an opt-out
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false
    return cmpRawOutput.shouldConsentBeCollected === false // false after an explicit decision is made
  }

  function cmpConvertResponseToGroupList (cmpRawOutput) {
    // Didomi handles checking each vendor's required purposes
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return []
    // enforce strings, even for IAB vendor ids

    const decision = cmpRawOutput.userStatus.vendors.global.enabled.map(function (vendorId) {
      return String(vendorId)
    })

    decision.push('always_consented')
    return decision
  }

  function cmpConvertResponseToLookupObject (cmpRawOutput) {
    var allowedVendors = cmpConvertResponseToGroupList(cmpRawOutput)
    var allVendors = cmpRawOutput.vendorInfo
    var lookupObject = {}
    // WORKAROUND to allow implicit triggering until the Didomi bug is fixed
    lookupObject.always_consented = 'Always consented (to allow strictly needed triggering)'
    allVendors.forEach(function (vendorObject) {
      if (allowedVendors.indexOf(String(vendorObject.id)) === -1) return
      lookupObject[vendorObject.id] = vendorObject.name || 'iab-vendor-' + vendorObject.id
    })
    return lookupObject
  }

  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
    // treat things we don't understand as an opt-out
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false
    tiqGroupName = tiqGroupName || 'tiq-group-name-missing'
    var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput)
    return allowedGroups.indexOf(tiqGroupName) !== -1
  }
})(window)

// Debugging / development output - repaste the integration on your test pages each time you make a change to your consent state
var outputString = `CMP Found: ${window.tealiumCmpIntegration.cmpName} (${window.tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model)

Checks:
  - id:          ${window.tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
  - well-formed: ${window.tealiumCmpIntegration.cmpCheckForWellFormedDecision(window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
  - explicit:    ${window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
  - group list:  ${JSON.stringify(window.tealiumCmpIntegration.cmpConvertResponseToGroupList(window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision()))}

  - name lookup: ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToLookupObject(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()), null, 6)}
`
console.log(outputString)
```

### デジタルコントロールルーム

このスニペットを [digitalcontrolroom.com](https://www.digitalcontrolroom.com/) またはお使いのウェブサイトでテストし、[操作方法セクション](#how-it-works) の指示に従って互換性を確認し、統合に必要な情報を取得してください。


```js
;(function digitalControlRoom(window) {
  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {};
  window.tealiumCmpIntegration.cmpName = 'Digital Control Room';
  window.tealiumCmpIntegration.cmpIntegrationVersion = 'v1.0.0';
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel;
  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision;
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey;
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision;
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision;
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent;
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList;
  function cmpCheckIfOptInModel() {
    return (
      window._cookiereports &&
      window._cookiereports.panels &&
      window._cookiereports.panels[0].consent &&
      window._cookiereports.panels[0].consentExplicit
    );
  }
  // This output is used as the cmpRawOutput argument in functions below.
  function cmpFetchCurrentConsentDecision() {
    if (!window._cookiereports) {
      return {};
    }
    var levels = window._cookiereports.loadConsent();
    levels[1] = true;
    var output = { "levels": levels };
    output.panels = window._cookiereports.panels;
    return output;
  }
  // Should return a string that helps Tealium iQ confirm that it's got the right CMP configuration (and not one from some other page / customer of the CMP)
  function cmpFetchCurrentLookupKey() {
    if (window._cookiereports && window._cookiereports.panels && window._cookiereports.panels.length > 0)
      return window._cookiereports.panels[0].storagekey;
    return "";
  }
  function cmpCheckForWellFormedDecision(cmpRawOutput) {
    if (typeof cmpRawOutput.levels !== "object" || cmpRawOutput.levels === null || typeof cmpRawOutput.panels !== "object" || cmpRawOutput.panels === null) {
      return false;
    }
    return true;
  }
  // Should return a boolean - true if the consent decision was explicitly made by the user
  function cmpCheckForExplicitConsentDecision(cmpRawOutput) {
    if (cmpRawOutput && cmpRawOutput.panels)
      return cmpRawOutput.panels[0].consentDecisionIsExplicit();
    return false;
  }
  function cmpConvertResponseToGroupList(cmpRawOutput) {
    if (!cmpCheckForWellFormedDecision(cmpRawOutput)) {
      return ["1"];
    }
    var levels = cmpRawOutput.levels;
    var consentDecision = [];
    for (var key in levels) {
      if (levels.hasOwnProperty(key)) {
        if (levels[key] === true) {
          consentDecision.push(key);
        }
      }
    }
    return consentDecision;
  }
  // You shouldn't need to change this function, or anything below it
  function cmpCheckForTiqConsent(cmpRawOutput, tiqGroupName) {
    // treat things we don't understand as an opt-out
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false;
    tiqGroupName = tiqGroupName || "tiq-group-name-missing";
    var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput);
    return allowedGroups.indexOf(tiqGroupName) !== -1;
  }
})(window);
// Debugging / development output - uncomment this block, then paste/repaste this entire template on your test pages
/*
var outputString = `${tealiumCmpIntegration.cmpCheckIfOptInModel() ? "Opt-in" : "Opt-out"} Model
  Checks:
    - id:          ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
    - well-formed: ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
    - explicit:    ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
    - group list:  ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()))}
  `;
console.log(outputString);
*/
```

### OneTrust

このスニペットを https://onetrust.com またはあなたのウェブサイトでテストし、[上記の指示に従って](#how-it-works)互換性を確認し、統合に必要な情報を取得してください。


<blockquote>
OneTrustは構成をプレビューするためのテストモードを提供しており、ベンダーIDに `-test` を追加することで活性化されます。統合を簡素化するために、OneTrustの同意統合はベンダーIDから `-test` 接尾辞を削除します。シームレスな統合のために、ページで `-test` 接尾辞を使用している場合でも、統合構成時に同意統合UIにベンダーIDを `-test` なしで入力してください。Tealium iQ UIとアクティブな統合間でベンダーIDが一致しないと、Tealium iQタグ管理がページ上でクッキーを構成したりタグをトリガーしたりするのを防ぎます。
</blockquote>


OneTrustは `cmpAddCallbackToTriggerRecheck` を通じてコールバック関数をサポートしています。これにより、Tealium iQはポーリングなしで同意状態の変更に関するリアルタイムの更新を受け取ることができます。詳細については、を参照してください。


```js
;(function oneTrust(window) {
    // 名前/IDの動作を簡単に調整する
    var useNamesInsteadOfKeys = false;
    // 構成の簡素化のために予想されるベンダーIDの安全チェックを回避することを許可するが、リスクが増加する
    var disableVendorIdValidation = false;
    // CMP特有の機能とラベル
    window.tealiumCmpIntegration = window.tealiumCmpIntegration || {};
    window.tealiumCmpIntegration.cmpName = "OneTrust";
    window.tealiumCmpIntegration.cmpIntegrationVersion = "onetrust-2.1.0";
    window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision;
    window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey;
    window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel;
    window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision;
    window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision;
    window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent;
    window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList;
    window.tealiumCmpIntegration.cmpConvertResponseToLookupObject = cmpConvertResponseToLookupObject;
    window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck = cmpAddCallbackToTriggerRecheck;
    function cmpCheckIfOptInModel() {
        var decision = cmpFetchCurrentConsentDecision();
        if (decision && decision.ConsentModel && decision.ConsentModel.Name === "opt-out") {
            return false;
        }
        return true;
    }
    function cmpFetchCurrentConsentDecision() {
        if (!window.OneTrust || typeof window.OneTrust.GetDomainData !== "function") return false;
        var cmpRawOutput = window.OneTrust.GetDomainData();
        cmpRawOutput.dataLayer = window.dataLayer;
        return cmpRawOutput;
    }
    function cmpFetchCurrentLookupKey() {
        // 2022年末からの新しいバージョンのOneTrustでは、cctIdが定義されていない
        // しかし、このHTML属性はOneTrustが識別する方法です
        var scrapeOneTrustVendorId = function () {
            var allScripts = document.getElementsByTagName("script");
            var re = /\/otSDKStub\.js(\?.*)*$/;
            for (var i = 0; i < allScripts.length; i++) {
                var isOneTrustScript = re.test(allScripts[i].src); // nullの可能性あり
                if (isOneTrustScript) {
                    var fullVendorId = allScripts[i].getAttribute("data-domain-script"); // スクリプトから解析する
                    return fullVendorId.split("-test")[0];
                }
            }
            return "error-not-found";
        }
        if (disableVendorIdValidation) {
            // 予想されるアクティブなベンダーIDをそのまま返す
            return (window.tealiumCmpIntegration && window.tealiumCmpIntegration.map && Object.keys(window.tealiumCmpIntegration.map)[0]) || "(ベンダーIDチェック無効)";
        }
        return scrapeOneTrustVendorId();
    }
    function cmpCheckForWellFormedDecision(cmpRawOutput) {
        // 理解できないものはオプトアウトとして扱う
        if (typeof cmpRawOutput !== "object") return false;
        if (toString.call(cmpRawOutput.Groups) !== "[object Array]") return false;
        if (toString.call(cmpRawOutput.dataLayer) !== "[object Array]") return false;
        return true;
    }
    function cmpCheckForExplicitConsentDecision(cmpRawOutput) {
        // 理解できないものは暗黙的として扱う
        if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false;
        return window.OneTrust && typeof window.OneTrust.IsAlertBoxClosed === "function" && window.OneTrust.IsAlertBoxClosed();
    }
    function cmpConvertResponseToLookupObject(cmpRawOutput) {
        // オブジェクトの配列から簡単な検索のためのオブジェクトに変換する
        var decisionString = "";
        var foundOneTrustEntry = false;
        if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return {};
        for (var i = cmpRawOutput.dataLayer.length - 1; i >= 0; i--) {
            if (["OneTrustGroupsUpdated", "OneTrustLoaded"].indexOf(cmpRawOutput.dataLayer[i].event) !== -1) {
                decisionString = cmpRawOutput.dataLayer[i].OnetrustActiveGroups;
                foundOneTrustEntry = true;
                break;
            }
        }
        var permittedPurposeIds = decisionString.split(",").filter(function (group) {
            return group !== "";
        });
        if (decisionString === "" && cmpRawOutput.dataLayer.length === 1000 && foundOneTrustEntry === false) {
            permittedPurposeIds = window.tealiumConsentRegister && window.tealiumConsentRegister.getCurrentDecision();
        }
        var permittedPurposesWithNames = {};
        cmpRawOutput.Groups.forEach(function (groupInfo) {
            if (permittedPurposeIds.indexOf(groupInfo.OptanonGroupId) !== -1) {
                permittedPurposesWithNames[groupInfo.OptanonGroupId] = groupInfo.GroupName || "ERROR-MISSING";
            }
        })
        return permittedPurposesWithNames; // keys are IDs, values are names
    }
    function cmpConvertResponseToGroupList(cmpRawOutput) {
        var permittedPurposesWithNames = cmpConvertResponseToLookupObject(cmpRawOutput);
        var keysOrValues = useNamesInsteadOfKeys ? "values" : "keys";
        return Object[keysOrValues](permittedPurposesWithNames); // keys are IDs, values are names
    }
    function cmpAddCallbackToTriggerRecheck(triggerRecheck) {
        if (typeof triggerRecheck !== 'function') return false;
        // 公式のGoogle dataLayerリスナー、https://github.com/google/data-layer-helper/blob/master/dist/data-layer-helper.js から引用、詳細は https://github.com/google/data-layer-helper を参照
        (function () {/*
         Copyright The Closure Library Authors.
         SPDX-License-Identifier: Apache-2.0
        */
            'use strict';/*
         jQuery v1.9.1 (c) 2005, 2012
         jQuery Foundation, Inc. jquery.org/license.
        */

var f = /\[object (Boolean|Number|String|Function|Array|Date|RegExp|Arguments)\]/; function g(a) { return null == a ? String(a) : (a = f.exec(Object.prototype.toString.call(Object(a)))) ? a[1].toLowerCase() : "object" } function m(a, b) { return Object.prototype.hasOwnProperty.call(Object(a), b) } function n(a) { if (!a || "object" != g(a) || a.nodeType || a == a.window) return !1; try { if (a.constructor && !m(a, "constructor") && !m(a.constructor.prototype, "isPrototypeOf")) return !1 } catch (c) { return !1 } for (var b in a); return void 0 === b || m(a, b) }; function p(a, b) { var c = {}, d = c; a = a.split("."); for (var e = 0; e < a.length - 1; e++)d = d[a[e]] = {}; d[a[a.length - 1]] = b; return c } function q(a, b) { var c = !a._clear, d; for (d in a) if (m(a, d)) { var e = a[d]; "array" === g(e) && c ? ("array" === g(b[d]) || (b[d] = []), q(e, b[d])) : n(e) && c ? (n(b[d]) || (b[d] = {}), q(e, b[d])) : b[d] = e } delete b._clear };/* Copyright 2012 Google Inc. All rights reserved. */
function r(a, b, c) {
    b = void 0 === b ? {} : b; "function" === typeof b ? b = { listener: b, listenToPast: void 0 === c ? !1 : c, processNow: !0, commandProcessors: {} } : b = { listener: b.listener || function () { }, listenToPast: b.listenToPast || !1, processNow: void 0 === b.processNow ? !0 : b.processNow, commandProcessors: b.commandProcessors || {} }; this.a = a; this.l = b.listener; this.j = b.listenToPast; this.g = this.i = !1; this.c = {}; this.f = []; this.b = b.commandProcessors; this.h = u(this); var d = this.a.push, e = this; this.a.push = function () {
        var k = [].slice.call(arguments,
            0), l = d.apply(e.a, k); v(e, k); return l
    }; b.processNow && this.process()
} r.prototype.process = function () { this.registerProcessor("set", function () { var c = {}; 1 === arguments.length && "object" === g(arguments[0]) ? c = arguments[0] : 2 === arguments.length && "string" === g(arguments[0]) && (c = p(arguments[0], arguments[1])); return c }); this.i = !0; for (var a = this.a.length, b = 0; b < a; b++)v(this, [this.a[b]], !this.j) }; r.prototype.get = function (a) { var b = this.c; a = a.split("."); for (var c = 0; c < a.length; c++) { if (void 0 === b[a[c]]) return; b = b[a[c]] } return b };
r.prototype.flatten = function () { this.a.splice(0, this.a.length); this.a[0] = {}; q(this.c, this.a[0]) }; r.prototype.registerProcessor = function (a, b) { a in this.b || (this.b[a] = []); this.b[a].push(b) };
function v(a, b, c) {
    c = void 0 === c ? !1 : c; if (a.i && (a.f.push.apply(a.f, b), !a.g)) for (; 0 < a.f.length;) {
        b = a.f.shift(); if ("array" === g(b)) a: { var d = a.c; g(b[0]); for (var e = b[0].split("."), k = e.pop(), l = b.slice(1), h = 0; h < e.length; h++) { if (void 0 === d[e[h]]) break a; d = d[e[h]] } try { d[k].apply(d, l) } catch (w) { } } else if ("arguments" === g(b)) { e = a; k = []; l = b[0]; if (e.b[l]) for (d = e.b[l].length, h = 0; h < d; h++)k.push(e.b[l][h].apply(e.h, [].slice.call(b, 1))); a.f.push.apply(a.f, k) } else if ("function" == typeof b) try { b.call(a.h) } catch (w) { } else if (n(b)) for (var t in b) q(p(t,
        b[t]), a.c); else continue; c || (a.g = !0, a.l(a.c, b), a.g = !1)
    }
} r.prototype.registerProcessor = r.prototype.registerProcessor; r.prototype.flatten = r.prototype.flatten; r.prototype.get = r.prototype.get; r.prototype.process = r.prototype.process; window.DataLayerHelper = r; function u(a) { return { set: function (b, c) { q(p(b, c), a.c) }, get: function (b) { return a.get(b) } } };
})();
function listener(model, message) {
    // メッセージがプッシュされました。
    // ヘルパーがモデルにマージしました。
    // これでメッセージと更新されたモデルを使用して何かを行います。
    if (["OneTrustGroupsUpdated", "OneTrustLoaded"].indexOf(message.event) !== -1) {
        triggerRecheck()
    }
}
window.dataLayer = window.dataLayer || [];
const helper = new DataLayerHelper(window.dataLayer, { listener: listener });
var oldWrapper = window.OptanonWrapper || function () { }
window.OptanonWrapper = function () {
    oldWrapper();
    triggerRecheck();
}
return true;
}
function cmpCheckForTiqConsent(cmpRawOutput, tiqGroupName) {
    // 理解できないものはオプトアウトとして扱います
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false;
    tiqGroupName = tiqGroupName || "tiq-group-name-missing";
    var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput);
    return allowedGroups.indexOf(tiqGroupName) !== -1;
}
})(window);


/*
// デバッグ/開発出力 - コンソールに貼り付けるか、カスタム統合の開発中に全体のテンプレートをアンコメントして貼り付けます
function outputDebuggingInfo () {
  var outputString = `${tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model
  Checks:
    - id:                 ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
    - well-formed:        ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
    - explicit:           ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
    - using callback:     ${typeof tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck === 'function'}
    - consented purposes: ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()))}
  `
  console.log(outputString);
}
// コールバック関数を使用してデバッグ中にコンソールへの投稿を避け、コールバック関数自体のテストを可能にします
if (typeof tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck === 'function') {
    tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck(outputDebuggingInfo)
}
outputDebuggingInfo();
*/




### Opt-out Cookie + GPC

この統合は、CCPA/CPRAなどの非常にシンプルなオプトアウトモデルをサポートすることを目的としています。**Vendor ID** フィールドは、オプトアウトクッキーのクッキー名として解釈され、大文字と小文字が区別されます。このクッキーが任意の値で見つかった場合、または [Global Privacy Control (GPC)](https://docs.tealium.com/about-global-privacy-control/) のオプトアウトシグナルが見つかった場合、ユーザーはオプトアウトしたと見なされます。

統合で使用される**Purpose Keys**とデフォルトの**Purpose Group**に含まれるものは次のとおりです：

* `no-selling` - ユーザーのオプトアウトシグナルに関係なく許可するタグ。これらのタグはデータを販売/共有しないか、法務チームなどによって厳密に必要とされています。
* `yes-selling` - 適用される規制やポリシーがユーザーがオプトアウトした後の追跡を禁止しているため、オプトアウトユーザーに対してブロックするタグ。
### TrustArc

[trustarc.com](https://trustarc.com/)またはあなたのウェブサイトでこのスニペットをテストし、[操作方法セクション](#how-it-works)の指示に従って互換性を確認し、統合に必要な情報を取得してください。


```js
;(function trustarcIntegration (window) {

  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = 'TrustArc'
  window.tealiumCmpIntegration.cmpIntegrationVersion = 'trustarc-1.0.4'

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
  window.tealiumCmpIntegration.cmpConvertResponseToLookupObject = cmpConvertResponseToLookupObject

  function cmpCheckIfOptInModel () {
    var preferredButNewMethod = window.truste && window.truste.eu && window.truste.eu.bindMap && window.truste.eu.bindMap.consentModel;
    if (typeof preferredButNewMethod === 'string' && preferredButNewMethod !== 'none') return preferredButNewMethod !== 'opt-out'; 
    var modeCookieValue = ((window.truste && window.truste.util && typeof window.truste.util.readCookie === 'function' && window.truste.util.readCookie('notice_behavior')) || 'expressed|eu')
    return modeCookieValue.indexOf('expressed') === 0
  }

  var trustArcMap = {
      0: 'Required',
      1: 'Functional',
      2: 'Personalization/Advertising'
  }

  function cmpFetchCurrentConsentDecision () {
    if (!window.truste || !window.truste.util || typeof window.truste.util.readCookie !== 'function') return false;

    var cookieValue =  window.truste.util.readCookie(truste.eu.COOKIE_GDPR_PREF_NAME) || '0,'

    if (cmpCheckIfOptInModel() === false && cmpCheckForExplicitConsentDecision() === false) {
      cookieValue = Object.keys(trustArcMap).join(',') 
    }

    return {
      cookie: cookieValue
    }
  }

  function cmpFetchCurrentLookupKey () {
    return (window.tealiumCmpIntegration && window.tealiumCmpIntegration.map && Object.keys(window.tealiumCmpIntegration.map)[0]) || '(Vendor ID check disabled for this integration)'
  }

  function cmpCheckForWellFormedDecision (cmpRawOutput) {
    if (typeof cmpRawOutput !== 'object') return false
    if (typeof cmpRawOutput.cookie !== 'string') return false
    return true
  }

  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
    if (!window.truste || !window.truste.util || typeof window.truste.util.readCookie !== 'function') return false
    return typeof window.truste.util.readCookie(truste.eu.COOKIE_GDPR_PREF_NAME) === 'string'
  }

  function cmpConvertResponseToLookupObject (cmpRawOutput) {
    if (!cmpCheckForWellFormedDecision(cmpRawOutput)) return []
    const cookieConsentValues = cmpRawOutput.cookie.split(':')[0].split(',')
    const extraSplit = []
    cookieConsentValues.forEach((el) => {
      if (!el) return
      extraSplit.push.apply(extraSplit, el.split('|'))
    })

    const output = {}

    extraSplit.forEach((key) => {
      if (key !== '') {
        output[key] = trustArcMap[key] || 'Category name unknown'
      }
    })

    return output
  }

  function cmpConvertResponseToGroupList (cmpRawOutput) {
    var permittedPurposesWithNames = cmpConvertResponseToLookupObject(cmpRawOutput)
    var keysOrValues = 'keys'
    return Object[keysOrValues](permittedPurposesWithNames) 
  }

  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false

    tiqGroupName = tiqGroupName || 'tiq-group-name-missing'
    var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput)
    return allowedGroups.indexOf(tiqGroupName) !== -1
  }
})(window)

/*
// Debugging - uncomment this code and paste the integration into the console on your test pages each time you make a change to your consent state to test without publishing
var outputString = `CMP Found: ${window.tealiumCmpIntegration.cmpName} (${window.tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model)

    Checks:
      - id:          ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
      - well-formed: ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
      - explicit:    ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
      - group list:  ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()))}

      - name lookup: ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToLookupObject(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()), null, 6)}
    `
console.log(outputString)
*/
```

### Usercentrics

このスニペットをあなたのウェブサイトでテストするには、互換性を確認し統合に必要な情報を得るために、[How it works](#how-it-works) セクションの指示に従ってください。
Usercentricsの統合では、**Vendors** を **Purposes** として使用します。


```js
;(function usercentricsBrowserSdkV2 (window) {
  // CMP specific functionality and labels
  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = 'Usercentrics Browser SDK'
  window.tealiumCmpIntegration.cmpIntegrationVersion = 'usercentrics-1.0.3'

  function cmpFetchCurrentConsentDecision () {
    if (!window.UC_UI || typeof window.UC_UI.getServicesBaseInfo !== 'function') return false
    var cmpRawOutput = window.UC_UI.getServicesBaseInfo()
    return cmpRawOutput
  }

  function cmpFetchCurrentLookupKey () {
    return (window.UC_UI && typeof window.UC_UI.getSettingsCore === 'function' && window.UC_UI.getSettingsCore().id) || ''
  }

  // only support opt-In model for Usercentrics for now, can be added if needed
  function cmpCheckIfOptInModel () {
    return window.UC_UI && typeof window.UC_UI.isConsentRequired === 'function' && window.UC_UI.isConsentRequired() === true
  }

  function cmpCheckForWellFormedDecision (cmpRawOutput) {
    // treat things we don't understand as an opt-out
    if (toString.call(cmpRawOutput) !== '[object Array]') return false
    // use the first entry as a proxy for all
    if (cmpRawOutput && cmpRawOutput[0] && typeof cmpRawOutput[0].name === 'string') {
      return true
    }
    return false
  }

  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
    // treat things we don't understand as an opt-out
    if (toString.call(cmpRawOutput) !== '[object Array]') return false
    // use the first entry as a proxy for all
    var consentHistory = (cmpRawOutput && cmpRawOutput[0] && cmpRawOutput[0].consent && cmpRawOutput[0].consent.history) || []
    var lastHistoryEntryType = (consentHistory && consentHistory.length && consentHistory[consentHistory.length - 1].type) || ''
    if (lastHistoryEntryType === 'explicit') {
      return true
    }
    return false
  }

  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
    var foundOptIn = false
    // treat things we don't understand as an opt-out
    if (toString.call(cmpRawOutput) !== '[object Array]') return false
    // use the mapping if found, with a fallback (Usercentrics default value) if not specified in the mapping

    tiqGroupName = tiqGroupName || 'tiq-group-name-missing'
    // check vendors if there's an object, look for at least one
    cmpRawOutput.forEach(function (tagInfo) {
      if ((tagInfo.consent && tagInfo.consent.status === true) && tagInfo.name === tiqGroupName) {
        foundOptIn = true
      }
    })
    return foundOptIn
  }

  function cmpConvertResponseToGroupList (cmpRawOutput) {
    var vendorArray = []
    cmpRawOutput && cmpRawOutput.forEach(function (tagConsent) {
      if (tagConsent.consent && tagConsent.consent.status === true) {
        vendorArray.push(tagConsent.name)
      }
    })
    return vendorArray
  }

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
})(window)

var outputString = `${tealiumCmpIntegration.cmpName} - ${tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model

Checks:
  - vendor id:            ${tealiumCmpIntegration.cmpFetchCurrentLookupKey()}
  - well-formed decision: ${tealiumCmpIntegration.cmpCheckForWellFormedDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
  - explicit decision:    ${tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(tealiumCmpIntegration.cmpFetchCurrentConsentDecision())}
  - consented purposes:   ${JSON.stringify(tealiumCmpIntegration.cmpConvertResponseToGroupList(tealiumCmpIntegration.cmpFetchCurrentConsentDecision()).sort(),null, 8)}
`
console.log(outputString)
```


### カスタム統合テンプレート

カスタム統合テンプレートについての詳細とその使用方法については、[Custom integration](https://docs.tealium.com/custom-cmp-integrations/)を参照してください。