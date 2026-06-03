---
title: CookieConsent v3 ローダー
description: CookieConsent v3 ローダー拡張機能を使用して、オープンソースのCookieConsent同意管理ツールをサイトにロードおよび構成します。
url: https://docs.tealium.com/ja/iq-tag-management/extensions/extensions-list/cookieconsent-v3-loader-extension/
---
CookieConsent v3 ローダー拡張機能を使用すると、サイト上で直接行う代わりにTealium iQを通じて [CookieConsent: CookieConsent v3](https://cookieconsent.orestbida.com/) を実装でき、より良い制御とバージョニングが可能になります。必要なJavaScriptおよびCSSファイルをロードし、カスタム構成を実行して、同意バナーとモーダルを表示します。

## 要件

CookieConsent v3 ローダー拡張機能は、JavaScriptコード拡張機能の管理権限が必要です。

## 動作方法

この拡張機能はCookieConsentライブラリをロードし、`ccConfig`構成オブジェクトを使用して初期化します。拡張機能のJSON構成を通じてカテゴリ、サービス、スタイル、言語構成、および動作を定義できます。

このツールは、オプトインまたはオプトアウトモードで動作し、ページのインタラクションを無効にする、モーダルレイアウトをカスタマイズする、リンクされたカテゴリとクッキーテーブルの構成などの高度な機能をサポートしています。

ページがロードされると、拡張機能は以下を行います：

* CookieConsentライブラリをロードします。
* カスタマイズされた`ccConfig`構成を適用します。
* ユーザーの構成に基づいて同意モーダルを表示します。

## 構成方法

1. Tealium iQで**拡張機能**に移動し、**拡張機能を追加**をクリックします。
1. **プライバシー**タブをクリックします。
1. **CookieConsent v3 ローダー**拡張機能の隣にある**&#43; 追加**をクリックします。
1. 拡張機能の**タイトル**を入力します。
1. **スコープ**の下で、デフォルトオプション**DOM Ready**を使用します。これはロード条件をサポートしており、拡張機能の実行タイミングを制御できます。**プリローダー**スコープもサポートされていますが、ロード条件は許可されていません。
1. （オプション）この拡張機能にロード条件を適用するために**条件を追加**をクリックします。これは、特定のシナリオでのみバナーを実行する場合に便利です（例えば、地域固有のロードルールが真の場合）。条件が同意統合の施行ルールと一致することを確認して、施行の問題を避けてください。
1. **構成**コードで、`ccConfig` JSONオブジェクトを更新して構成を定義します。これには以下が含まれます：
   * `necessary`、`analytics`、`marketing`などのカテゴリ定義。
   * 同意および構成モーダルの言語と翻訳文字列。
   * 同意モード：`opt-in`または`opt-out`。
   * バナー/モーダルのレイアウトと位置を制御するGUIオプション。
   * 構成モーダルのセクションとクッキーテーブル。
   * ラベル、タイトル、ボタンテキストなどのアクセシビリティ関連のコンテンツ。

   構成オプションの完全なリストについては、[CookieConsent: Configuration Reference](https://cookieconsent.orestbida.com/reference/configuration-reference.html)を参照してください。