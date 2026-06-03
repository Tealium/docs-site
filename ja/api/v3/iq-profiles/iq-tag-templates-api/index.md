---
title: iQタグテンプレートAPI
description: iQタグテンプレートAPIはPATCHメソッドを使用してプロファイルタグテンプレートを更新します。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-tag-templates-api/
---
このAPIと利用可能なオブジェクトフィールドについて詳しくは、[iQプロファイルAPI]()および[iQプロファイルオブジェクト]()を参照してください。

## 動作方法

タグを作成した後、iQタグテンプレートAPIを使用してタグテンプレートを編集できます。

`PATCH`メソッドを使用してiQプロファイルオブジェクトのコンポーネントを更新します。

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}/templates/{TEMPLATE_ID}
```

PATCHメソッドを使用すると、保存または名前を付けて保存を使用してプログラム的にプロファイルタグテンプレートを変更します。APIで変更を加えた後、アプリケーションにログインして公開する必要があります。

### cURLリクエストの例

```bash
curl --location --request PATCH \
  --url https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}/templates/79 \
  --header &#39;Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9&#39; \
  --header &#39;Content-Type: application/json&#39; \
  --data &#39;
```

## 認証

Bearerトークンは、すべてのAPI呼び出しを認証するために使用され、APIキーは認証呼び出しでのみ使用されます。Bearerトークンに加えて、認証応答には、後続のサーバーサイドAPI呼び出しで使用する必要がある地域固有のホスト名が含まれています。

APIキーからBearerトークンを生成する方法については、[認証]()を参照してください。

## プロファイルフィールド

プロファイルタグテンプレートは、以下の可能なフィールドを含むJSONオブジェクトです：

| OBJECT | TYPE | REQUIRED | DESCRIPTION |
| --- | --- | --- | --- |
| `versionTitle` | String | Optional | 保存されたバージョンのタイトル。&lt;br&gt;`saveType`が`saveAs`に構成されている場合のデフォルト：`API \| {TIMESTAMP}`&lt;br&gt;`saveType`が`save`に構成されている場合のデフォルト：既存のバージョンタイトル |
| `saveType` | String | Optional| PATCHリクエストで実行する保存のタイプ：`save`または`saveAs`。デフォルトは`saveAs`です。 |
| `notes` | String | Required | 公開バージョンに関する追加の注記。 |
| `templateData.content` | Object | Required | 更新したいタグテンプレートの内容。|

### 応答の例

```json
{
  &#34;versionTitle&#34;: &#34;Version 2022.03.22.2108&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes&#34;,
  &#34;templateData&#34;: {
    &#34;content&#34;: &#34;testing a template update&#34;
  }
}
```

## PATCH操作パラメータ

タグテンプレートを追加または削除するには、タグを追加または削除する必要があります。

## タグテンプレートの更新

このPATCHメソッドは、プロファイルオブジェクトと追加のタグテンプレートフィールドを取ります。

### リクエストの例

```json
{
  &#34;versionTitle&#34;: &#34;test version&#34;,
  &#34;saveType&#34;: &#34;saveAs&#34;,
  &#34;notes&#34;: &#34;version notes&#34;,
  &#34;templateData&#34;: {
    &#34;content&#34;: &#34;testing a template update&#34;
  }
}
```

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| ERROR CODE | ERROR MESSAGE |
| --- | --- |
| 400 | `&#34;プロファイルライブラリが古くなっています。プロファイルをパッチする前に変更をマージしてください - {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;patchProfile.arg2.notes: 空であってはなりません&#34;`|
| 404 | `&#34;プロファイルが見つかりません - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;プロファイルライブラリが見つかりません - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;プロファイル（レガシー）が見つかりません - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;同じアカウントを現在閲覧しているユーザー: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;最新バージョンが見つかりません - {ACCOUNT} \| profile: {PROFILE}&#34;` |
| 409 | `&#34;プロファイルの保存エラー: {PROFILE} for account: {ACCOUNT}, 重複バージョン: {VERSION}&#34;` |
| 500 | `&#34;プロファイル: {PROFILE} はライブラリプロファイルから継承されています&#34;`&lt;br&gt;`&#34;プロファイルメタデータの保存エラー - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;プロファイルの保存エラー - account: {ACCOUNT} \| profile: {PROFILE}&#34;`&lt;br&gt;`&#34;プロファイル(レガシー)の保存エラー - {ACCOUNT} \| profile: {PROFILE}&#34;`|
