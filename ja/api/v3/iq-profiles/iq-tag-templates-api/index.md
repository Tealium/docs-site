---
title: iQタグテンプレートAPI
description: iQタグテンプレートAPIはPATCHメソッドを使用してプロファイルタグテンプレートを更新します。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-tag-templates-api/
---
このAPIと利用可能なオブジェクトフィールドについて詳しくは、[iQプロファイルAPI](https://docs.tealium.com/iq-profiles-v3-api/)および[iQプロファイルオブジェクト](https://docs.tealium.com/iq-profiles-api-objects/)を参照してください。

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
  --header 'Authorization: Bearer eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzUx...MiJ9' \
  --header 'Content-Type: application/json' \
  --data '
```

## 認証


<blockquote>
Bearerトークンは、すべてのAPI呼び出しを認証するために使用され、APIキーは認証呼び出しでのみ使用されます。Bearerトークンに加えて、認証応答には、後続のサーバーサイドAPI呼び出しで使用する必要がある地域固有のホスト名が含まれています。
</blockquote>


APIキーからBearerトークンを生成する方法については、[認証](https://docs.tealium.com/api/v3/getting-started/authentication/)を参照してください。

## プロファイルフィールド

プロファイルタグテンプレートは、以下の可能なフィールドを含むJSONオブジェクトです：

| OBJECT | TYPE | REQUIRED | DESCRIPTION |
| --- | --- | --- | --- |
| `versionTitle` | String | Optional | 保存されたバージョンのタイトル。<br>`saveType`が`saveAs`に構成されている場合のデフォルト：`API \| {TIMESTAMP}`<br>`saveType`が`save`に構成されている場合のデフォルト：既存のバージョンタイトル |
| `saveType` | String | Optional| PATCHリクエストで実行する保存のタイプ：`save`または`saveAs`。デフォルトは`saveAs`です。 |
| `notes` | String | Required | 公開バージョンに関する追加の注記。 |
| `templateData.content` | Object | Required | 更新したいタグテンプレートの内容。|

### 応答の例

```json
{
  "versionTitle": "Version 2022.03.22.2108",
  "saveType": "saveAs",
  "notes": "version notes",
  "templateData": {
    "content": "testing a template update"
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
  "versionTitle": "test version",
  "saveType": "saveAs",
  "notes": "version notes",
  "templateData": {
    "content": "testing a template update"
  }
}
```

## エラーメッセージ

このエンドポイントの潜在的なエラーメッセージ：

| ERROR CODE | ERROR MESSAGE |
| --- | --- |
| 400 | `"プロファイルライブラリが古くなっています。プロファイルをパッチする前に変更をマージしてください - {ACCOUNT} \| profile: {PROFILE}"`<br>`"patchProfile.arg2.notes: 空であってはなりません"`|
| 404 | `"プロファイルが見つかりません - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"プロファイルライブラリが見つかりません - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"プロファイル（レガシー）が見つかりません - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"同じアカウントを現在閲覧しているユーザー: {ACCOUNT} \| profile: {PROFILE}"`<br>`"最新バージョンが見つかりません - {ACCOUNT} \| profile: {PROFILE}"` |
| 409 | `"プロファイルの保存エラー: {PROFILE} for account: {ACCOUNT}, 重複バージョン: {VERSION}"` |
| 500 | `"プロファイル: {PROFILE} はライブラリプロファイルから継承されています"`<br>`"プロファイルメタデータの保存エラー - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"プロファイルの保存エラー - account: {ACCOUNT} \| profile: {PROFILE}"`<br>`"プロファイル(レガシー)の保存エラー - {ACCOUNT} \| profile: {PROFILE}"`|
