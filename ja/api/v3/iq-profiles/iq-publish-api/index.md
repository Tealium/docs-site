---
title: iQ Publish API
description: iQ Publish APIを使用して、保存されたプロファイルバージョンを公開したり、公開ステータスを確認したり、保存と公開を一括で行うことができます。
url: https://docs.tealium.com/ja/api/v3/iq-profiles/iq-publish-api/
---
このAPIと利用可能なオブジェクトフィールドについて詳しくは、[iQ Profiles API](https://docs.tealium.com/iq-profiles-v3-api/) および [iQ Profiles Objects](https://docs.tealium.com/iq-profiles-api-objects/) を参照してください。

## 動作原理

iQ Publish APIは、`/v3/tiq` APIの範囲を拡張し、3つの公開機能を提供します。既存の保存されたバージョンを1つ以上の環境に公開したり、公開リクエストのステータスをポーリングしたり、プロファイルの保存と公開を1つのPATCH操作に組み合わせることができます。

## 認証


<blockquote>
すべてのAPI呼び出しにはベアラートークンが使用され、APIキーは認証呼び出しでのみ使用されます。ベアラートークンに加えて、認証応答には後続のサーバーサイドAPI呼び出しで使用する必要がある地域固有のホスト名が含まれています。
</blockquote>


APIキーからベアラートークンを生成する方法については、[Authentication](https://docs.tealium.com/api/v3/getting-started/authentication/)を参照してください。

## 既存のバージョンを公開する

保存されたプロファイルバージョンが既に存在し、プロファイルを変更せずに公開したい場合は、このエンドポイントを使用します。公開するためには、正確な`versionId`を提供する必要があります。APIは最新バージョンを暗黙的に公開しません。

```bash
POST /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}/publish
```

### リクエストパラメータ

| パラメータ | タイプ | 必須 | 説明 |
| --- | --- | --- | --- |
| `versionId` | 文字列 | はい | 公開する保存されたプロファイルのバージョンID。バージョンIDは`YYYYMMDDhhmm`の形式を使用します。例えば、`202608131215`。 |
| `operatorId` | 文字列 | はい | 監査目的で公開履歴に記録されるメールアドレス。このフィールドは自動的にベアラートークンから導出されません。 |
| `publishTargets` | 文字列の配列 | はい | 1つ以上のターゲット環境名。デフォルトのターゲットは`dev`、`qa`、`prod`です。プロファイルに構成されている場合、カスタム環境もターゲットとして使用できます。詳細については、[Custom publish environments](https://docs.tealium.com/custom-publish-environments/)を参照してください。ターゲット名には、文字、数字、およびダッシュのみを含めることができます。 |
| `title` | 文字列 | はい | 公開タイトル。128文字を超えるタイトルは拒否されます。 |
| `notes` | 文字列 | はい | 公開リクエストに記録されるメモ。 |

リクエストに複数のターゲットが含まれている場合、すべてのターゲットが権限チェックに合格する必要があります。リクエストされたターゲットのいずれかに対する権限が不足している場合、APIはリクエスト全体を拒否します。

### 例のリクエスト

```bash
curl --request POST \
  --url "https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}/publish" \
  --header "Authorization: Bearer {TOKEN}" \
  --header "Content-Type: application/json" \
  --header "Accept: application/json" \
  --data '{
    "versionId": "202608131215",
    "operatorId": "user@example.com",
    "publishTargets": ["qa"],
    "title": "API publish",
    "notes": "Publishing version 202608131215 to QA"
  }'
```

### レスポンス

成功したレスポンスは、公開リクエストが受け入れられ、キューに入れられたことを意味しますが、公開が完了したわけではありません。[status endpoint](#check-publish-status)をポーリングするためにレスポンスから`publishId`を使用してください。

```json
{
  "publishId": "212ab1da-7503-4691-bf87-f892b450ed5a",
  "account": "my_account",
  "profile": "main",
  "versionId": "202608131215",
  "operatorId": "user@example.com",
  "createdDate": "2026-08-13T20:16:01 UTC",
  "publishTargets": [
    {
      "target": "qa",
      "publishTargetId": "83ff6319-de94-4ac0-b05a-7f19bfb8e34f",
      "distroDate": null
    }
  ],
  "title": "API publish",
  "revisionId": "202608131215",
  "notes": "Publishing version 202608131215 to QA"
}
```

| フィールド | 説明 |
| --- | --- |
| `publishId` | 公開リクエストのUUID。この値を使用してステータスエンドポイントをポーリングします。 |
| `account` | Tealiumのアカウント名。 |
| `profile` | Tealiumのプロファイル名。 |
| `versionId` | 公開のために提出されたプロファイルバージョン。 |
| `operatorId` | リクエストで提供され、公開履歴に記録されたメールアドレス。 |
| `createdDate` | UTCでの公開リクエスト作成時間。 |
| `publishTargets` | 公開リクエストのために作成されたターゲットレコード。各エントリには`target`、`publishTargetId`、および`distroDate`が含まれます。 |
| `title` | リクエストで提供された公開タイトル。 |
| `notes` | リクエストで提供された公開メモ。 |
| `revisionId` | 公開されたプロファイルデータに関連する改訂識別子。 |

### エラーコード

| エラーコード | 説明 |
| --- | --- |
| 400 | 必須フィールドが欠けている、ターゲット名が不正、またはタイトルが128文字を超えています。 |
| 401 | ベアラートークンが欠けているか不正です。 |
| 403 | アカウント、プロファイル、またはリクエストされたターゲットのいずれかに対する公開権限が不足しています。 |
| 404 | アカウント、プロファイル、またはバージョン識別子が見つかりません。 |
| 409 | 同時ユーザーまたは公開の競合。 |
| 422 | 公開ターゲットの検証に失敗したか、プロファイルの参照整合性エラーです。 |

## 公開ステータスを確認する

POST公開またはPATCH保存および公開コールの後、公開リクエストのステータスをポーリングするためにこのエンドポイントを使用します。

```bash
GET /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}/publish/{PUBLISH_ID}/status
```

### パスパラメータ

| パラメータ | 説明 |
| --- | --- |
| `ACCOUNT` | Tealiumのアカウント名。 |
| `PROFILE` | Tealiumのプロファイル名。 |
| `PUBLISH_ID` | POST公開エンドポイントによって返された`publishId`、またはPATCH保存および公開応答の`publish.data.publishId`値。 |

### 例のリクエスト

```bash
curl --request GET \
  --url "https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}/publish/{PUBLISH_ID}/status" \
  --header "Authorization: Bearer {TOKEN}" \
  --header "Accept: application/json"
```

### レスポンス

```json
{
  "publishId": "212ab1da-7503-4691-bf87-f892b450ed5a",
  "publishTargetEventResponses": [
    {
      "publishTargetEventId": "02b71e23-8927-4156-9df0-1f9a87125a44",
      "publishTargetId": "83ff6319-de94-4ac0-b05a-7f19bfb8e34f",
      "publishTargetEventType": "tag_generation_queued",
      "publishTargetState": "queued",
      "detail": null,
      "createdDate": "2026-08-13T20:16:01 UTC"
    }
  ]
}
```

| フィールド | 説明 |
| --- | --- |
| `publishId` | 全体の公開リクエストを識別するUUID。 |
| `publishTargetEventResponses` | 各ターゲットイベントレコードの1つのステータスエントリ。各ターゲットの最新の状態を確認します。 |
| `publishTargetEventId` | ステータスイベントレコードを識別するUUID。この値はターゲットが進行するにつれて変化します。 |
| `publishTargetId` | 公開リクエスト内のターゲット提出を識別するUUID。 |
| `publishTargetEventType` | 公開サービスによって発行されるライフサイクルイベントタイプ。 |
| `publishTargetState` | イベントタイプから導出される粗い状態。 |
| `detail` | オプションの診断詳細。この値は`null`になることがあります。 |
| `createdDate` | イベントのUTCタイムスタンプ。 |

### 公開状態

| イベントタイプ | 状態 | 意味 |
| --- | --- | --- |
| `initialising_publish` | `queued` | リクエストが初期化されています。 |
| `tag_generation_queued` | `queued` | ターゲットはタグ生成を待っています。 |
| `tag_generation_started` | `processing` | タグ生成が開始されました。 |
| `publish_distro_queued` | `processing` | 配布がキューに入れられています。 |
| `publish_distro_starting` | `processing` | 配布が開始されています。 |
| `publish_success` | `published` | ターゲットが正常に完了しました。 |
| `publish_fail` | `stopped` | ターゲットが失敗したか停止しました。 |

複数のターゲットがあるリクエストの場合、すべてのターゲットの状態を確認してください。公開は、すべてのターゲットが`published`に達したときにのみ完了します。いずれかのターゲットが`stopped`に達した場合、公開は失敗しています。

ステータスエンドポイントは、公開IDごとに秒間1リクエストに制限されています。公開ステータスは急速に変化しないため、より頻繁にポーリングする必要はなく、`429`エラーが返されます。
### エラーコード

| エラーコード | 説明 |
| --- | --- |
| 401 | ベアラートークンが不足しているか、形式が正しくありません。 |
| 403 | アカウントまたはプロファイルに対する十分な公開権限がありません。 |
| 404 | アカウント、プロファイル、または公開識別子が見つかりません。 |
| 429 | リクエストレートが超過しました。1秒に1回以上ポーリングしないでください。 |

## 保存と公開

このエンドポイントを使用して、プロファイルの変更を保存し、その結果のバージョンを一度に公開します。サービスは保存によって作成されたバージョンを使用します。公開部分には `versionId` を提供しないでください。

```bash
PATCH /v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}
```

タグ、変数、ロードルール、イベント、拡張機能の既存のPATCH操作と同じ `operationList` 本文を使用します。保存と公開を有効にするために以下のフィールドを追加します。

### 公開フィールド

次の表のすべてのフィールドは、`publish` が `true` の場合に必要です。

| フィールド | タイプ | 説明 |
| --- | --- | --- |
| `publish` | Boolean | 保存と公開を有効にするために `true` に構成します。存在しないか `false` の場合、既存のPATCH保存動作が使用されます。 |
| `publishTargets` | 文字列の配列 | 保存後に公開する対象環境の名前。デフォルトのターゲットは `dev`、`qa`、`prod` です。プロファイルに構成されている場合、カスタム環境も使用できます。詳細については、[カスタム公開環境](https://docs.tealium.com/custom-publish-environments/)を参照してください。 |
| `publishTitle` | 文字列 | 公開タイトル。これを `title` と同じ値に構成します。128文字を超えるタイトルは拒否されます。 |
| `publishNote` | 文字列 | 公開リクエストで記録されたメモ。これを `notes` と同じ値に構成します。 |
| `operatorId` | 文字列 | 監査目的で公開履歴に記録されるメールアドレス。このフィールドは自動的にベアラートークンから導出されません。 |


<blockquote>
`notes` と `versionTitle` フィールドは、プロファイルが保存されたときに記録される保存メモとバージョンタイトルです。`publishNote` と `publishTitle` フィールドは、公開操作が実行されるときに別々に記録されます。保存と公開操作を実行するときは、これら4つのフィールドをすべて提供してください。
</blockquote>


### 例のリクエスト

```bash
curl --request PATCH \
  --url "https://platform.tealiumapis.com/v3/tiq/accounts/{ACCOUNT}/profiles/{PROFILE}" \
  --header "Authorization: Bearer {TOKEN}" \
  --header "Content-Type: application/json" \
  --header "Accept: application/json" \
  --data '{
    "versionTitle": "API patch publish",
    "saveType": "saveAs",
    "parentVersion": "202608131150",
    "notes": "Added page_type variable",
    "operationList": [
      {
        "op": "add",
        "path": "/variables",
        "value": {
          "object": "variable",
          "name": "page_type",
          "alias": "Page Type",
          "type": "udo",
          "notes": "UDO variable"
        }
      }
    ],
    "publish": true,
    "publishTargets": ["qa"],
    "publishTitle": "API patch publish",
    "publishNote": "Added page_type variable",
    "operatorId": "user@example.com"
  }'
```

### レスポンス

`publish` が `true` の場合、レスポンスには `profile` と `publish` の2つのトップレベルセクションが含まれます。

**成功レスポンス**

```json
{
  "profile": {
    "account": "my_account",
    "profile": "main",
    "version": "202608131215",
    "minorVersion": "202608131215"
  },
  "publish": {
    "status": "success",
    "data": {
      "publishId": "212ab1da-7503-4691-bf87-f892b450ed5a",
      "account": "my_account",
      "profile": "main",
      "versionId": "202608131215",
      "operatorId": "user@example.com",
      "createdDate": "2026-08-13T20:16:01 UTC",
      "publishTargets": [
        {
          "target": "qa",
          "publishTargetId": "83ff6319-de94-4ac0-b05a-7f19bfb8e34f",
          "distroDate": null
        }
      ],
      "title": "API patch publish",
      "revisionId": "202608131215",
      "notes": "Added page_type variable"
    }
  }
}
```

**失敗レスポンス** (保存は成功したが、公開は失敗した)

```json
{
  "profile": {
    "account": "my_account",
    "profile": "main",
    "version": "202608131215",
    "minorVersion": "202608131215"
  },
  "publish": {
    "status": "failed",
    "data": {
      "message": "Publish permission denied for target: prod",
      "account": "my_account",
      "profile": "main",
      "versionId": "202608131215"
    }
  }
}
```

| フィールド | 説明 |
| --- | --- |
| `profile` | 保存されたプロファイルのレスポンス。`version` フィールドには公開に使用されるバージョンIDが含まれます。 |
| `publish.status` | 公開が正常に提出された場合は `success`。権限、検証、または公開ステージのエラーが発生した場合は `failed`。 |
| `publish.data` | 公開レスポンスデータ。成功時には `publishId` とターゲットレコードが含まれます。失敗時にはエラーの詳細が含まれます。 |


<blockquote>
保存と公開のステップはアトミックではありません。保存が完了し、公開が失敗した場合、APIはプロファイルの保存を元に戻しません。再試行する前に GET リクエストでプロファイルの状態を確認してください。
</blockquote>


### エラーコード

HTTP 200レスポンスは公開が成功したことを確認しません。常に `publish.status` を確認してください。`publish.status` が `failed` の場合、プロファイルは正常に保存されましたが、公開は行われませんでした。`publish.status` が `success` の場合のみ、ステータスエンドポイントをポーリングするために `publish.data.publishId` を使用してください。

| エラーコード | 説明 |
| --- | --- |
| 400 | 必須フィールドが不足している、ターゲット名が不正、PATCH本文が無効、またはタイトルが128文字を超えています。 |
| 401 | ベアラートークンが不足しているか、形式が正しくありません。 |
| 403 | アカウント、プロファイル、または要求されたターゲットのいずれかに対する十分な公開権限がありません。 |
| 404 | アカウント、プロファイル、またはバージョン識別子が見つかりません。 |
| 409 | 同時ユーザーまたは公開の競合。 |
| 422 | 公開ターゲットの検証が失敗したか、プロファイルの参照整合性エラー。 |
| 429 | リクエストレートが超過しました。 |