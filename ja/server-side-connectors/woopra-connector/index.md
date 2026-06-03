---
title: Woopraコネクタ構成ガイド
description: この記事では、Woopraコネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/woopra-connector/
---
## コネクタアクション

| アクション名 | AudienceStream | EventStream |
| --- | :---: | :---: |
|イベントを追跡| ✓| ✓|
|訪問を更新| ✓| ✓|

## 構成を構成する

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。コネクタを追加する一般的な手順については、[コネクタ概要](/ja/server-side/connectors/manage/)の記事を参照してください。

コネクタを追加した後、以下の構成を構成します：

## アクション構成 - パラメータとオプション

**次へ**をクリックするか、**アクション**タブに移動します。ここでコネクタアクションを構成します。

このセクションでは、各アクションのパラメータとオプションの構成方法について説明します。

### アクション - イベントを追跡

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|プロジェクト|  &lt;ul&gt;&lt;li&gt;Woopraでのプロジェクトの名前。&lt;/li&gt;&lt;li&gt;このエンドポイントに関する詳細情報は、[Woopraのドキュメンテーション](https://docs.woopra.com/reference#section-endpoint-http-s-www-woopra-com-track-ce-)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|クッキー|  &lt;ul&gt;&lt;li&gt;クッキーはデバイスIDと考えるべきです。&lt;/li&gt;&lt;li&gt;匿名IDとしても使用できます。&lt;/li&gt;&lt;li&gt;`cv_{訪問識別子}`がない場合は必須。&lt;/li&gt;&lt;/ul&gt; |
|イベント|  &lt;ul&gt;&lt;li&gt;追跡しているカスタムイベントの名前。&lt;/li&gt;&lt;/ul&gt; |
|タイムスタンプ|  &lt;ul&gt;&lt;li&gt;イベントが発生したUnixエポックからのミリ秒単位でフォーマットされたイベントタイムスタンプ。（これは過去に遡ることができますが、未来には遡ることはできません。）&lt;/li&gt;&lt;/ul&gt; |
|訪問識別子タイプ|  &lt;ul&gt;&lt;li&gt;メール、電話番号など。&lt;/li&gt;&lt;li&gt;訪問識別子を使用する場合は必須。&lt;/li&gt;&lt;/ul&gt; |
|訪問識別子|  &lt;ul&gt;&lt;li&gt;この訪問に関連付ける識別子または複数の識別子。&lt;/li&gt;&lt;li&gt;この形式に関する詳細情報は、[Woopraのドキュメンテーション](https://docs.woopra.com/reference#track-ce)を参照してください。&lt;/li&gt;&lt;li&gt;クッキーがない場合は必須。各キーは`cv_`で始まる必要があります。例：`cv_email`。 &lt;/li&gt;&lt;/ul&gt; |
|訪問のプロパティ|  &lt;ul&gt;&lt;li&gt;訪問のプロフィールに構成するプロパティ。&lt;/li&gt;&lt;li&gt;この形式に関する詳細情報は、[Woopraのドキュメンテーション](https://docs.woopra.com/reference#track-ce)を参照してください。&lt;/li&gt;&lt;li&gt;これらは文字列、数値、日付などになることがあります。各キーは`cv_`で始まる必要があります。例：`cv_first_name`または`cv_title`。 &lt;/li&gt;&lt;/ul&gt; |
|イベントプロパティ|  &lt;ul&gt;&lt;li&gt;カスタムイベントに構成するプロパティ。&lt;/li&gt;&lt;li&gt;この形式に関する詳細情報は、[Woopraのドキュメンテーション](https://docs.woopra.com/reference#track-ce)を参照してください。&lt;/li&gt;&lt;li&gt;これらは文字列、数値、日付などになることがあります。各キーは`ce_`で始まる必要があります。例：`ce_total_value`または`ce_purchase_date`。 &lt;/li&gt;&lt;/ul&gt; |
|訪問プロパティ|  &lt;ul&gt;&lt;li&gt;訪問またはセッションに構成するプロパティ。&lt;/li&gt;&lt;li&gt;この形式に関する詳細情報は、[Woopraのドキュメンテーション](https://docs.woopra.com/reference#track-ce)を参照してください。&lt;/li&gt;&lt;li&gt;これらは文字列、数値、日付などになることがあります。各キーは`cs_`で始まる必要があります。例：`cs_is_work_computer`または`cs_mobile_web`。 &lt;/li&gt;&lt;/ul&gt; |
|リファラー|  &lt;ul&gt;&lt;li&gt;訪問のリファラーURL。&lt;/li&gt;&lt;li&gt;WoopraサーバーはURLをリファラーのデータベースと照合し、該当する場合はリファラータイプと検索用語を生成します。&lt;/li&gt;&lt;li&gt;リファラーデータはWoopraインターフェースから自動的にアクセス可能になります。&lt;/li&gt;&lt;/ul&gt; |
|IPアドレス|  &lt;ul&gt;&lt;li&gt;訪問のIPアドレス。&lt;/li&gt;&lt;li&gt;定義されている場合、接続の物理的なIPアドレスを上書きします。&lt;/li&gt;&lt;/ul&gt; |
|タイムアウト|  &lt;ul&gt;&lt;li&gt;ミリ秒単位。&lt;/li&gt;&lt;li&gt;デフォルトは30000（30秒相当）で、この時間を過ぎるとイベントは期限切れとなり、訪問は終了し、訪問はオフラインとマークされます。&lt;/li&gt;&lt;/ul&gt; |
|ブラウザ|  &lt;ul&gt;&lt;li&gt;ユーザーのブラウザ。&lt;/li&gt;&lt;li&gt;定義されている場合、リクエストのユーザーエージェントから自動検出されたブラウザを上書きします。&lt;/li&gt;&lt;li&gt;カスタムユーザーエージェントを作成することもできます。&lt;/li&gt;&lt;/ul&gt; |
|オペレーティングシステム|  &lt;ul&gt;&lt;li&gt;ユーザーのオペレーティングシステム。&lt;/li&gt;&lt;li&gt;定義されている場合、リクエストのユーザーエージェントから自動検出されたブラウザを上書きします。&lt;/li&gt;&lt;li&gt;カスタムユーザーエージェントを作成することもできます。&lt;/li&gt;&lt;/ul&gt; |
|デバイス|  &lt;ul&gt;&lt;li&gt;ユーザーのデバイスタイプ。&lt;/li&gt;&lt;li&gt;定義されている場合、ユーザーエージェントから自動検出されたデバイスタイプを上書きします。一般的な値はモバイル、タブレット、デスクトップです。&lt;/li&gt;&lt;/ul&gt; |

### アクション - 訪問を更新

#### パラメータ

|**パラメータ**| **説明**|
|---| ---|
|プロジェクト|  &lt;ul&gt;&lt;li&gt;Woopraでのプロジェクトの名前。&lt;/li&gt;&lt;li&gt;このエンドポイントに関する詳細情報は、[Woopraのドキュメンテーション](https://docs.woopra.com/reference#track-identify)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
|クッキー|  &lt;ul&gt;&lt;li&gt;クッキーはデバイスIDと考えるべきです。&lt;/li&gt;&lt;li&gt;匿名IDとしても使用できます。&lt;/li&gt;&lt;li&gt;`cv_{訪問識別子}`がない場合は必須。&lt;/li&gt;&lt;/ul&gt; |
|訪問識別子タイプ|  &lt;ul&gt;&lt;li&gt;メール、電話番号など。&lt;/li&gt;&lt;li&gt;訪問識別子を使用する場合は必須。&lt;/li&gt;&lt;/ul&gt; |
|訪問識別子|  &lt;ul&gt;&lt;li&gt;この訪問に関連付ける識別子または複数の識別子。&lt;/li&gt;&lt;li&gt;この形式に関する詳細情報は、[Woopraのドキュメンテーション](https://docs.woopra.com/reference#-identify)を参照してください。&lt;/li&gt;&lt;li&gt;クッキーがない場合は必須。各キーは`cv_`で始まる必要があります。例：`cv_email`。 &lt;/li&gt;&lt;/ul&gt; |
|訪問のプロパティ|  &lt;ul&gt;&lt;li&gt;訪問のプロフィールに構成するプロパティ。&lt;/li&gt;&lt;li&gt;これらは文字列、数値、日付などになることがあります。各キーは`cv_`で始まる必要があります。例：`cv_first_name`または`cv_title`。&lt;/li&gt;&lt;li&gt;この形式に関する詳細情報は、[Woopraのドキュメンテーション](https://docs.woopra.com/reference#track-identify)を参照してください。&lt;/li&gt;&lt;/ul&gt; |
