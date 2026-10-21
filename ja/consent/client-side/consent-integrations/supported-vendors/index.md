---
title: サポートされているベンダー統合
description: この記事では、クライアントサイドの同意統合でサポートされているCMPについて説明し、同意統合の構成を完了するために必要なベンダー固有の情報を簡単に収集する方法について説明します。
url: https://docs.tealium.com/ja/consent/client-side/consent-integrations/supported-vendors/
---
## 仕組み

クライアントサイドの同意統合は、さまざまな同意管理プラットフォーム（CMP）との統合をサポートしています。サポートされている同意管理プラットフォーム（CMP）のユーザーインターフェースまたはウェブページから、関連するベンダー固有の情報にアクセスできます。このドキュメントを信頼性が高くユーザーフレンドリーに保つために、このセクションではウェブページからベンダー固有の情報を取得する手順のみをカバーしています。各パートナーCMPのユーザーインターフェースでベンダーIDと目的を取得する手順については、各CMPのドキュメントを参照してください。

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
    // GDPRスタイルの「オプトイン」モデルを実行しているかどうかを真偽値で返す必要があります
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
    // Tealium iQが正しいCMP構成を持っていることを確認するのに役立つ文字列を返す必要があります（他のページ/ CMPの顧客ではない）
    function cmpFetchCurrentLookupKey() {
        if (!window.Cookiebot || typeof window.Cookiebot.serial !== 'string') return false
        return Cookiebot.serial
    }
    // 生の決定がCMPの期待に合っているかどうかを真偽値で返す必要があります
    function cmpCheckForWellFormedDecision (cmpRawOutput) {
      return typeof cmpRawOutput === 'object' &&  typeof cmpRawOutput.stamp ==='string'
    }
    // 同意決定がユーザーによって明示的に行われたかどうかを真偽値で返す必要があります
    function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
      // この例で決定が明示的であるかどうかを判断する唯一の方法は、オプトアウトクッキーが構成されているかどうかを確認することです
      return cmpRawOutput.method === 'explicit'? true : false;
    }
    // 同意されたベンダー/目的の配列を返す必要があります - これらはTealium iQの目的と正確に一致する必要があります
    function cmpConvertResponseToGroupList(cmpRawOutput) {
        var consentDecision = []
        // データの販売/共有が許可されているかどうかを判断するために、空でないオプトアウトクッキーを非常に単純にチェックします
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

### Didomi（レガシー）

このスニペットを [didomi.io](https://didomi.io) または [上記の指示に従って](#how-it-works) あなたのウェブサイトでテストして、互換性を確認し、統合に必要な情報を取得してください。

Didomi（レガシー）統合は、**ベンダー**を**目的**として使用します。


<blockquote>
Didomi（レガシー）は、暗黙的に同意された目的やベンダーを返しません。暗黙的なトリガーを有効にするために、この統合は無条件に `always_consented` という目的キーをアウトバウンドの同意決定に追加します。新しい構成の場合は、[Didomi v2](#didomi-v2) を使用してください。v2 統合はこの回避策が必要ありません。
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


### Didomi v2

このスニペットを [didomi.io](https://didomi.io) または [上記の指示に従って](#how-it-works) あなたのウェブサイトでテストして、互換性を確認し、統合に必要な情報を取得してください。

Didomi v2 統合は、**ベンダー**を**目的**として使用します。

新しいDidomi構成にはDidomi v2を推奨します。Didomi v2を使用するには、新しい同意統合を作成し、ベンダーとして**Didomi v2**を選択してください。既存のDidomi（レガシー）統合は変更なしで引き続き機能します。

Didomi v2は、Didomi（レガシー）と以下の点で異なります：

* **ベンダーID**フィールドがありません。
* デフォルトの目的グループがありません。目的キーはベンダー固有であり、Didomiの構成によって異なります。
* コールバックサポート。統合はDidomiからの`consent.changed`イベントをリッスンし、自動的に同意を再確認します。詳細については、[同意更新の監視とトリガー](https://docs.tealium.com/custom-cmp-integrations/#monitor-and-trigger-consent-updates)を参照してください。


```js
;(function didomiIntegration (window) {
  // CMP specific functionality and labels
  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = 'Didomi'
  window.tealiumCmpIntegration.cmpIntegrationVersion = 'didomiv2-1.0.0'

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
  window.tealiumCmpIntegration.cmpConvertResponseToLookupObject = cmpConvertResponseToLookupObject
  window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck = cmpAddCallbackToTriggerRecheck

  // defaults to opt-in model to be safe if we can't determine the model, since opt-in works (less efficiently) for opt-out cases but not vice versa
  function cmpCheckIfOptInModel () {
      if (!window.Didomi || typeof window.Didomi.getConfig !== 'function') return true
      var config = window.Didomi.getConfig()
      if (typeof config !== "object" || config === null || !config.regulation || !config.regulation.group || !config.regulation.group.name) return true
      return config.regulation.group.name !== 'none' // even 'mixed' might need the opt-in type handling, see https://support.didomi.io/processing-rule-override
  }

  function cmpFetchCurrentConsentDecision () {
      if (!window.Didomi || typeof window.Didomi.getCurrentUserStatus !== 'function') return false
      if (typeof window.Didomi.getConfig !== 'function') return false
      var cmpRawOutput = {}
      cmpRawOutput.userStatus = window.Didomi.getCurrentUserStatus()
      cmpRawOutput.vendorInfo = window.Didomi.getRequiredVendors()
      cmpRawOutput.shouldUserStatusBeCollected = window.Didomi.shouldUserStatusBeCollected()
      return cmpRawOutput
  }

  // Didomi has chosen not to support this feature in their integration
  function cmpFetchCurrentLookupKey () {
    // return whatever Vendor ID is expected be active to short-circuit the ID-based double check
    return (window.tealiumCmpIntegration && window.tealiumCmpIntegration.map && Object.keys(window.tealiumCmpIntegration.map)[0]) || '(Vendor ID check disabled)'
  }

  function cmpCheckForWellFormedDecision (cmpRawOutput) {
      // treat things we don't understand as an opt-out
      if (typeof cmpRawOutput !== 'object') return false
      if (typeof cmpRawOutput.userStatus !== 'object') return false
      if (typeof cmpRawOutput.vendorInfo !== 'object') return false
      if (typeof cmpRawOutput.shouldUserStatusBeCollected !== 'boolean') return false
      return true
  }

  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
      // treat things we don't understand as an opt-out
      if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false
      return cmpRawOutput.shouldUserStatusBeCollected === false // false after an explicit decision is made
  }

  function cmpConvertResponseToGroupList (cmpRawOutput) {
      return Object.keys(cmpConvertResponseToLookupObject(cmpRawOutput))
  }

  function cmpConvertResponseToLookupObject (cmpRawOutput) {
    // Didomi handles checking each vendor's required purposes
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return {}

    // Since the friendly names are stored as part of a (long) array of objects, we want to avoid unneeded looping by converting it once
    var fullLookup = {}
    cmpRawOutput.vendorInfo.forEach(function (vendor) {
        fullLookup[vendor.didomiId] = { name: vendor.name || 'iab-vendor-' + vendor.id, id: String(vendor.id), didomiId: vendor.didomiId }
    })

    var consentedVendors = {}
    // enforce strings, even for IAB vendor ids
    Object.values(cmpRawOutput.userStatus.vendors || {}).forEach(function (vendor) {
        if (vendor.enabled === true) {
          var ref = fullLookup[vendor.id] || {}
          consentedVendors[ref.id] = ref.name || '(missing)'
        }
    })
    return consentedVendors
  }

  function cmpAddCallbackToTriggerRecheck (triggerRecheck) {
    if (typeof triggerRecheck !== 'function') return false; // don't do anything unless we have a function to call when it's time to trigger

    // Guard against duplicate registration
    if (window.tealiumCmpIntegration._callbacksRegistered) return false
    window.tealiumCmpIntegration._callbacksRegistered = true

    // Docs: https://developers.didomi.io/cmp/web-sdk/reference/events#event-types
    window.didomiEventListeners = window.didomiEventListeners || [];
    window.didomiEventListeners.push({
      event: 'consent.changed',
      listener: triggerRecheck
    });
    window.didomiOnReady = window.didomiOnReady || [];
    window.didomiOnReady.push(triggerRecheck);
  }

  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
      // treat things we don't understand as an opt-out
      if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false
      tiqGroupName = tiqGroupName || 'tiq-group-name-missing'
      var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput)
      return allowedGroups.indexOf(tiqGroupName) !== -1
  }
})(window)

/*
// DEBUG OUTPUT - uncomment this block, then paste/repaste this entire template on your test pages to get console output
// of the CMP decision and how it's being processed by our integration code. You can use this output to debug and adjust
// the cmp* functions above as needed during development of the integration

var setCallback = window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck(function () {
  setTimeout(consoleOut, 200)
})
if (!setCallback) consoleOut() // if we weren't able to set the callback, output the decision for the debugging user


function consoleOut () {
  // Debugging / development output - uncomment this block, then paste/repaste this entire template on your test pages
  var decision = window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision()
  var outputString = `\n${window.tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model

Checks:
  - well-formed: ${window.tealiumCmpIntegration.cmpCheckForWellFormedDecision(decision)}
  - explicit:    ${window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(decision)}
  - lookup:      ${JSON.stringify(window.tealiumCmpIntegration.cmpConvertResponseToLookupObject(decision), null, 8)}:
  - group list:  ${JSON.stringify(window.tealiumCmpIntegration.cmpConvertResponseToGroupList(decision), null, 8)}

`
  console.log(outputString);
}
*/
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

このスニペットを https://onetrust.com またはあなたのウェブサイトでテストして、[上記の指示に従って](#how-it-works)互換性を確認し、統合に必要な情報を取得してください。


<blockquote>
OneTrustは構成をプレビューするためのテストモードを提供しており、ベンダーIDに `-test` を追加することでアクティブ化できます。統合を簡素化するために、OneTrustの同意統合はベンダーIDから `-test` 接尾辞を削除します。ページ上で `-test` 接尾辞を使用している場合でも、統合構成時に同意統合UIに `-test` を含まないベンダーIDを入力してください。Tealium iQ UIとアクティブな統合間でベンダーIDが一致しないと、Tealium iQタグ管理がページ上でクッキーを構成したりタグをトリガーしたりするのを防ぎます。
</blockquote>


OneTrustは `cmpAddCallbackToTriggerRecheck` を通じてコールバック関数をサポートしています。このコールバックにより、Tealium iQはポーリングせずに同意状態の変更に関するリアルタイムの更新を受け取ることができます。詳細については、[同意更新の監視とトリガー](https://docs.tealium.com/custom-cmp-integrations/#monitor-and-trigger-consent-updates)を参照してください。


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
                var isOneTrustScript = re.test(allScripts[i].src); // can be null
                if (isOneTrustScript) {
                    var fullVendorId = allScripts[i].getAttribute("data-domain-script"); // parse it from the script
                    return fullVendorId.split("-test")[0];
                }
            }
            return "error-not-found";
        }
        if (disableVendorIdValidation) {
            // just return whatever Vendor ID is expected be active
            return (window.tealiumCmpIntegration && window.tealiumCmpIntegration.map && Object.keys(window.tealiumCmpIntegration.map)[0]) || "(Vendor ID check disabled)";
        }
        return scrapeOneTrustVendorId();
    }
    function cmpCheckForWellFormedDecision(cmpRawOutput) {
        // treat things we don't understand as an opt-out
        if (typeof cmpRawOutput !== "object") return false;
        if (toString.call(cmpRawOutput.Groups) !== "[object Array]") return false;
        if (toString.call(cmpRawOutput.dataLayer) !== "[object Array]") return false;
        return true;
    }
    function cmpCheckForExplicitConsentDecision(cmpRawOutput) {
        // treat things we don't understand as implicit
        if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false;
        return window.OneTrust && typeof window.OneTrust.IsAlertBoxClosed === "function" && window.OneTrust.IsAlertBoxClosed();
    }
    function cmpConvertResponseToLookupObject(cmpRawOutput) {
        // convert from array of objects to object for easier lookups
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
        // An official Google dataLayer listener, pulled from https://github.com/google/data-layer-helper/blob/master/dist/data-layer-helper.js, see https://github.com/google/data-layer-helper
        (function () {/*
         Copyright The Closure Library Authors.
         SPDX-License-Identifier: Apache-2.0
        */
            'use strict';/*
         jQuery v1.9.1 (c) 2005, 2012
         jQuery Foundation, Inc. jquery.org/license.
        */
```


### オプトアウトクッキー + GPC

この統合は、CCPA/CPRAなどのシンプルなオプトアウトモデルをサポートしています。**Vendor ID** フィールドはオプトアウトクッキーのクッキー名として解釈され、大文字と小文字が区別されます。このクッキーが任意の値で見つかった場合、または [グローバルプライバシーコントロール (GPC)](https://docs.tealium.com/about-global-privacy-control/) のオプトアウトシグナルが見つかった場合、ユーザーはオプトアウトしたと見なされます。

統合で使用される**目的キー**とデフォルトの**目的グループ**に含まれるものは以下の通りです：

* `no-selling` - ユーザーのオプトアウトシグナルに関係なく許可するタグ。これらのタグはデータを販売/共有しないか、法務チームなどによって厳密に必要とされています。
* `yes-selling` - オプトアウトしたユーザーに対してブロックするタグ。適用される規制やポリシーにより、ユーザーがオプトアウトした後の追跡が禁止されています。
### セキュリティ

このスニペットを[動作方法](#how-it-works)セクションの指示に従ってあなたのウェブサイトでテストし、互換性を確認し、統合に必要な情報を取得してください。

Securitiは`cmpAddCallbackToTriggerRecheck`を通じてコールバック関数をサポートしています。このコールバックにより、Tealium iQはポーリングせずに同意状態の変更に関するリアルタイムの更新を受け取ることができます。詳細については、[同意更新の監視とトリガー](https://docs.tealium.com/custom-cmp-integrations/#monitor-and-trigger-consent-updates)を参照してください。

デフォルトの**目的グループ**における**目的キー**は以下の通りです：

* `essential`: 必須
* `analytics_customization`: 分析とカスタマイズ
* `advertising`: 広告
* `performance_functionality`: パフォーマンスと機能性
* `unclassified`: 未分類


```js
;(function securitiIntegration (window) {
    // CMP特有の機能とラベル
    window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

    window.tealiumCmpIntegration.cmpName = 'Securiti'
    window.tealiumCmpIntegration.cmpIntegrationVersion = 'securiti-1.0.0'

    window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
    window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
    window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
    window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
    window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
    window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
    window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
    window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck = cmpAddCallbackToTriggerRecheck

    // コンソール出力用に公開されている
    window.tealiumCmpIntegration.cmpConvertResponseToLookupObject = cmpConvertResponseToLookupObject

    // CMPが「オプトイン」モデル（GDPRスタイル）を実行しているかどうかを返すべきです。真偽値を返すべきです。
    function cmpCheckIfOptInModel () {
      var isOptInModel = window.tealiumCmpIntegration && window.tealiumCmpIntegration.decisionCache && window.tealiumCmpIntegration.decisionCache.isOptInModel
      return !isOptInModel
    }

    // CMP特有の生のオブジェクト（オブジェクトでなければならない）を返すべきです。この出力は以下の関数でcmpRawOutput引数として使用されます。
    function cmpFetchCurrentConsentDecision () {
      window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}
      window.tealiumCmpIntegration.decisionCache = window.tealiumCmpIntegration.decisionCache || {}
      return window.tealiumCmpIntegration.decisionCache
    }

    // 今のところこの統合ではこの機能をサポートしていません
    function cmpFetchCurrentLookupKey () {
      // アクティブであると予想されるベンダーIDを返すことで、IDに基づくダブルチェックを短絡させる
      return (window.tealiumCmpIntegration && window.tealiumCmpIntegration.map && Object.keys(window.tealiumCmpIntegration.map)[0]) || '(ベンダーIDチェック無効)'
    }

    // 生の決定がこの特定のCMPからの決定に対する私たちの期待を満たしているかどうかを返すべきです。真偽値を返すべきです。
    function cmpCheckForWellFormedDecision (cmpRawOutput) {
      return typeof cmpRawOutput === 'object' &&
             typeof cmpRawOutput.category === 'object' &&
             typeof cmpRawOutput.isExplicit === 'boolean' &&
             typeof cmpRawOutput.isOptInModel === 'boolean'
    }

    // 同意決定がユーザーによって明示的に行われたかどうかを返すべきです。真偽値を返すべきです。
    function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
      if (typeof cmpRawOutput === 'object' && cmpRawOutput.isExplicit === true) return true
      return false
    }

    function cmpConvertResponseToGroupList (cmpRawOutput) {
      return Object.keys(cmpConvertResponseToLookupObject(cmpRawOutput))
    }

    function cmpConvertResponseToLookupObject (cmpRawOutput) {
        // 'Performance & Analytics'を'performance_analytics'に変換します
      var tokenizeName = function (name) {
        if (typeof name !== 'string') return name
        return name.toLowerCase().replace(https://docs.tealium.com/[^a-z0-9]+/g, '_')
      }
      if (!cmpCheckForWellFormedDecision(cmpRawOutput)) return []
      var consentedCategoryNames = Object.keys(cmpRawOutput.category).filter(function (categoryName) { return cmpRawOutput.category[categoryName] === "granted" });
      var lookupObject = {}
      consentedCategoryNames.forEach(function (name) {
        lookupObject[tokenizeName(name)] = name
      })
      return lookupObject
    }

    function cmpAddCallbackToTriggerRecheck (triggerRecheck) {
        if (typeof triggerRecheck !== 'function') return false; // トリガーするタイミングで呼び出す関数がない限り何もしない

        window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

        // 重複登録を防ぐ
        if (window.tealiumCmpIntegration._callbacksRegistered) return false
        window.tealiumCmpIntegration._callbacksRegistered = true

        // コールバックに呼び出すヘルパー
        var fetchAndCacheDecision = function (sdk) {
          var isExplicit = sdk.isConsentGiven()
          var defaultConsentState = sdk.getDefaultConsentState()
          var consentDecision = isExplicit ? sdk.getConsent() : defaultConsentState
          // 原子的な割り当て – 中間の空オブジェクトウィンドウはありません
          window.tealiumCmpIntegration.decisionCache = {
            category: (consentDecision && consentDecision.category) || {},
            isExplicit: !!isExplicit,
            isOptInModel: defaultConsentState && defaultConsentState.category ? (Object.keys(defaultConsentState.category).filter(function (categoryName) { return defaultConsentState.category[categoryName] === "granted" }).length === Object.keys(defaultConsentState.category).length) : undefined
          }
          setTimeout(triggerRecheck, 1) // 現在の処理が終了するのを待ってから再チェックをトリガーします
        }

        // すでにロードされている場合は、コールバックをすぐにアタッチして信頼性を確保します
        if (typeof window.SecuritiSDK !== 'undefined' && typeof window.SecuritiSDK.onReady === 'function') {
          window.SecuritiSDK.onReady(function (sdk) {
            fetchAndCacheDecision(sdk)
          })
        }

        window.SecuritiDataLayer = window.SecuritiDataLayer || [];
        SecuritiDataLayer.push(['onReady', fetchAndCacheDecision]);
        SecuritiDataLayer.push(['onConsentGiven', fetchAndCacheDecision]);
        return true
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
// デバッグ出力 - このブロックのコメントを外し、このテンプレート全体をテストページに貼り付けて/再貼り付けして、CMP決定と統合コードによる処理のコンソール出力を取得します。この出力を使用して、統合の開発中に必要に応じて上記のcmp*関数をデバッグおよび調整できます。

  var setCallback = window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck(function () {
    consoleOut()
  })
  if (!setCallback) consoleOut() // コールバックを構成できなかった場合は、デバッグユーザーのために決定を出力します


 function consoleOut () {
    // デバッグ/開発出力 - このブロックのコメントを外し、このテンプレート全体をテストページに貼り付けて/再貼り付けしてください
    var decision = window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision()
    var outputString = `\n${window.tealiumCmpIntegration.cmpCheckIfOptInModel() ? 'Opt-in' : 'Opt-out'} Model

  Checks:
    - well-formed: ${window.tealiumCmpIntegration.cmpCheckForWellFormedDecision(decision)}
    - explicit:    ${window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision(decision)}
    - lookup:      ${JSON.stringify(window.tealiumCmpIntegration.cmpConvertResponseToLookupObject(decision), null, 8)}
    - group list:  ${JSON.stringify(window.tealiumCmpIntegration.cmpConvertResponseToGroupList(decision), null, 8)}

  `
    console.log(outputString);
  }
  */

```


### TrustArc

このスニペットを [trustarc.com](https://trustarc.com/) またはあなたのウェブサイトでテストし、[操作方法セクション](#how-it-works) の指示に従って互換性を確認し、統合に必要な情報を取得してください。


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

  function cmpConvertResponse to GroupList (cmpRawOutput) {
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
```

### Usercentrics v2

[How it works](#how-it-works)セクションの指示に従って、このスニペットをあなたのウェブサイトでテストし、互換性を確認し、統合に必要な情報を取得してください。

Usercentrics v2統合は、Usercentrics Browser SDK v1およびv2用であり、**Vendors**を**Purposes**として使用します。

Usercentrics v2は、`cmpAddCallbackToTriggerRecheck`を通じてコールバック関数をサポートしています。このコールバックにより、Tealiumはポーリングせずに同意状態の変更に関するリアルタイムの更新を受け取ることができます。


```js
;(function usercentricsBrowserSdk (window) {
  // CMP specific functionality and labels
  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = 'Usercentrics Browser SDK (v2)'
  window.tealiumCmpIntegration.cmpIntegrationVersion = 'usercentrics-1.1.0'

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
  window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck = cmpAddCallbackToTriggerRecheck

  function cmpFetchCurrentConsentDecision () {
    if (!window.UC_UI || typeof window.UC_UI.getServicesBaseInfo !== 'function') return false
    const cmpRawOutput = window.UC_UI.getServicesBaseInfo()
    return cmpRawOutput
  }

  function cmpFetchCurrentLookupKey () {
    var v2 = window.UC_UI && typeof window.UC_UI.getSettingsCore === 'function' && window.UC_UI.getSettingsCore().id
    return v2
  }

  function cmpCheckIfOptInModel () {
    return true // only opt-in for now
  }

  function cmpCheckForWellFormedDecision (cmpRawOutput) {
    if (toString.call(cmpRawOutput) !== '[object Array]') return false
    if (cmpRawOutput && cmpRawOutput[0] && typeof cmpRawOutput[0].name === 'string' && cmpRawOutput[0].name.length > 0) {
      return true
    }
    return false
  }

  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
    if (toString.call(cmpRawOutput) !== '[object Array]') return false
    if (!Array.isArray(window.dataLayer)) return false;
    const latestConsentStatus = [...window.dataLayer]
      .reverse()
      .find(entry => entry.event === 'consent_status');
    return latestConsentStatus && latestConsentStatus.type ? latestConsentStatus.type.toLowerCase() === 'explicit' : false;
  }

  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
    let foundOptIn = false
    if (toString.call(cmpRawOutput) !== '[object Array]') return false
    tiqGroupName = tiqGroupName || 'tiq-group-name-missing'
    cmpRawOutput.forEach(function (tagInfo) {
      if ((tagInfo.consent && tagInfo.consent.status === true) && tagInfo.name === tiqGroupName) {
        foundOptIn = true
      }
    })
    return foundOptIn
  }

  function cmpConvertResponseToGroupList (cmpRawOutput) {
    const vendorArray = []
    cmpRawOutput && cmpRawOutput.forEach(function (tagConsent) {
      if (tagConsent.consent && tagConsent.consent.status === true) {
        vendorArray.push(tagConsent.name)
      }
    })
    return vendorArray
  }

  function cmpAddCallbackToTriggerRecheck (triggerRecheck) {
    if (typeof triggerRecheck !== 'function') return false;

    if (window.tealiumCmpIntegration._callbacksRegistered) return false
    window.tealiumCmpIntegration._callbacksRegistered = true

    window.addEventListener("ucEvent", function (e) {
      if( e.detail && e.detail.event && e.detail.event === "consent_status" ) {
        triggerRecheck()
      }
    })

    window.addEventListener('UC_UI_CMP_EVENT', function(e) {
      triggerRecheck()
    });

    window.addEventListener('UC_UI_INITIALIZED', function(e) {
      triggerRecheck()
    });
    return true;
  }
})(window)
```

### Usercentrics v3

[How it works](#how-it-works)セクションの指示に従って、このスニペットをあなたのウェブサイトでテストし、互換性を確認し、統合に必要な情報を取得してください。

Usercentrics v3統合は、Usercentrics Browser SDK V3用であり、**Vendors**を**Purposes**として使用します。


```js
// tv:1.0.0
// base:usercentricsv3
;(function usercentricsBrowserSdk (window) {
  // CMP specific functionality and labels
  window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}

  window.tealiumCmpIntegration.cmpName = 'Usercentrics Browser SDK (v3)'
  window.tealiumCmpIntegration.cmpIntegrationVersion = 'usercentricsv3-1.0.0'

  window.tealiumCmpIntegration.cmpFetchCurrentConsentDecision = cmpFetchCurrentConsentDecision
  window.tealiumCmpIntegration.cmpFetchCurrentLookupKey = cmpFetchCurrentLookupKey
  window.tealiumCmpIntegration.cmpCheckIfOptInModel = cmpCheckIfOptInModel
  window.tealiumCmpIntegration.cmpCheckForWellFormedDecision = cmpCheckForWellFormedDecision
  window.tealiumCmpIntegration.cmpCheckForExplicitConsentDecision = cmpCheckForExplicitConsentDecision
  window.tealiumCmpIntegration.cmpCheckForTiqConsent = cmpCheckForTiqConsent
  window.tealiumCmpIntegration.cmpConvertResponseToGroupList = cmpConvertResponseToGroupList
  // just for internal/debugging use
  window.tealiumCmpIntegration.cmpConvertResponseToLookupObject = cmpConvertResponseToLookupObject
  // callbacks supported!
  window.tealiumCmpIntegration.cmpAddCallbackToTriggerRecheck = cmpAddCallbackToTriggerRecheck


  // use the previously cached value, set by callbacks from the CMP
  function cmpFetchCurrentConsentDecision () {
    window.tealiumCmpIntegration = window.tealiumCmpIntegration || {}
    window.tealiumCmpIntegration.decisionCache = window.tealiumCmpIntegration.decisionCache || {}
    return window.tealiumCmpIntegration.decisionCache
  }

  function cmpFetchCurrentLookupKey () {
   return window.tealiumCmpIntegration.decisionCache && cmpCheckForWellFormedDecision(window.tealiumCmpIntegration.decisionCache) ? window.tealiumCmpIntegration.decisionCache.consent.setting.id : 'ERROR: Vendor ID not found!'
  }

  function cmpCheckIfOptInModel () {
    return true
  }

  function cmpCheckForWellFormedDecision (cmpRawOutput) {
    if (typeof cmpRawOutput !== 'object' || cmpRawOutput === null) return false
    if (typeof cmpRawOutput.services !== 'object' || cmpRawOutput.services === null) return false
    if (typeof cmpRawOutput.consent !== 'object' || cmpRawOutput.consent === null) return false
    if (typeof cmpRawOutput.consent.setting !== 'object' || cmpRawOutput.consent.setting === null) return false
    if (typeof cmpRawOutput.consent.setting.id !== 'string' || cmpRawOutput.consent.setting.id.length === 0) return false
    return true
  }

  function cmpCheckForExplicitConsentDecision (cmpRawOutput) {
    return cmpRawOutput && cmpRawOutput.consent && cmpRawOutput.consent.type && cmpRawOutput.consent.type.toLowerCase() === 'explicit' ? true : false;
  }

  function cmpAddCallbackToTriggerRecheck (triggerRecheck) {
    if (typeof triggerRecheck !== 'function') return false;

    // Guard against duplicate registration
    if (window.tealiumCmpIntegration._callbacksRegistered) return false;
    window.tealiumCmpIntegration._callbacksRegistered = true;

    // if the CMP has already loaded, get the current decision and cache it immediately
    window.__ucCmp && window.__ucCmp.getConsentDetails && window.__ucCmp.getConsentDetails().then(function (consentDetails) {
      if (consentDetails) {
        window.tealiumCmpIntegration.decisionCache = consentDetails
        triggerRecheck()
      }
    })

    // Docs: https://usercentrics.com/docs/web/features/events/uc-consent/
    window.addEventListener('UC_CONSENT', function (event) {
      if (event && event.detail && event.detail.services) {
        // Cache the decision details in a known location for later retrieval by cmpFetchCurrentConsentDecision
        window.tealiumCmpIntegration.decisionCache = event.detail
      }
      triggerRecheck()
    });
    return true;
  }

  function cmpConvertResponseToGroupList (cmpRawOutput) {
    if (!cmpCheckForWellFormedDecision(cmpRawOutput)) return []
    var consentedGroups = cmpConvertResponseToLookupObject(cmpRawOutput)
    return Object.keys(consentedGroups)
  }

  function cmpConvertResponseToLookupObject (cmpRawOutput) {
    if (!cmpCheckForWellFormedDecision(cmpRawOutput)) return []
    var consentedGroups = {}
    Object.keys(cmpRawOutput.services).forEach(function (key) {
      if (cmpRawOutput.services[key].consent.given === true) {
        consentedGroups[key] = cmpRawOutput.services[key].name
      }
    })
    return consentedGroups
  }

  // You shouldn't need to change this function, or anything below it
  function cmpCheckForTiqConsent (cmpRawOutput, tiqGroupName) {
    // treat things we don't understand as an opt-out
    if (cmpCheckForWellFormedDecision(cmpRawOutput) !== true) return false
    tiqGroupName = tiqGroupName || 'tiq-group-name-missing'
    var allowedGroups = cmpConvertResponseToGroupList(cmpRawOutput)
    return allowedGroups.indexOf(tiqGroupName) !== -1
  }

})(window)
```


### カスタム統合テンプレート

カスタム統合テンプレートについての詳細と使用方法については、[カスタム統合](https://docs.tealium.com/custom-cmp-integrations/)を参照してください。
