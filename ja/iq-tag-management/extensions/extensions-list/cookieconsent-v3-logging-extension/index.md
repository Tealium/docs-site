---
title: CookieConsent v3 ロギング
description: CookieConsent v3 ロギング拡張機能を使用して、ユーザーの同意決定をキャプチャし、構成可能なエンドポイントに送信します。
url: https://docs.tealium.com/ja/iq-tag-management/extensions/extensions-list/cookieconsent-v3-logging-extension/
---
この拡張機能を使用して、CookieConsent v3 インターフェースを通じて収集されたユーザーの同意決定をログに記録します。同意ID、承認されたカテゴリ、同意モデルなどの関連情報をキャプチャし、`fetch()` APIを使用してこのデータをJSONペイロードとしてエンドポイントに送信します。Tealium Collectエンドポイントに送信する場合でもカスタムの宛先に送信する場合でも、ペイロードをシステムの要件に合わせて構成できます。

## 要件

CookieConsent v3 ロギング拡張機能は、JavaScriptコード拡張機能の管理権限が必要です。

## 動作方法

この拡張機能は、CookieConsentインターフェースからの `consent_updated` イベントをリッスンします。ユーザーが同意決定を行うか更新すると、拡張機能は同意状態を取得し、`fetch()` メソッドを使用して指定されたエンドポイントに情報をJSONペイロードとして送信します。

ペイロードには通常、以下が含まれます：

* `tealium_event`: イベントタイプ、例えば `consent_decision`。
* `consent_id`: ユーザーの同意決定のユニークな識別子。
* `decision_type`: ユーザーがカテゴリを承認したか拒否したか。
* `accepted_purposes` と `rejected_purposes`: ユーザーが選択したカテゴリ。
* `consent_model`: `opt-in` または `opt-out`。
* `url`: クエリパラメーターを除いた現在のページURL。
* `decision_timestamp`: 同意が最後に更新された時間。
* `expiration_time`: 同意が有効である期間。
* `revision`: 同意構成の現在のバージョン。
* `tealium_account` と `tealium_profile`: イベントを送信する場所。
* `tealium_visitor_id`: （オプション）`utag_main` クッキーで既に利用可能な場合に含まれます。

このペイロードは、エンドポイントまたはデータモデルに合わせて調整できます。

## 構成方法

1. Tealium iQで、**Extensions** に移動し、**Add Extension** をクリックします。
1. **Privacy** タブをクリックします。
1. **CookieConsent v3 Logging** 拡張機能の隣にある **&#43; Add** をクリックします。
1. 拡張機能の **Title** を入力します。
1. **Scope** の下で、デフォルトオプション **DOM Ready** を使用します。これはロード条件をサポートしており、拡張機能が実行されるタイミングを制御できます。**Preloader** スコープもサポートされていますが、ロード条件は許可されません。
1. （オプション）この拡張機能にロード条件を適用するには **Add Condition** をクリックします。問題を避けるために、同意統合の施行ルールと条件が一致していることを確認してください。
1. **Configuration** コードで以下のいずれかを行います：
    * Tealium Collectにログを送信する場合は、`tealium_account` と `tealium_profile` のプレースホルダー値を実際の値に置き換えます。
    * 別のエンドポイントにログを送信する場合は、`fetch()` URLを同意ログを送信したい宛先に更新します。