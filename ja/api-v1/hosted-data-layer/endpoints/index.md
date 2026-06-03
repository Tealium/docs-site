---
title: ホストされたデータレイヤーAPIエンドポイント
description: ホストされたデータレイヤーオブジェクトまたはJSONファイルを使用して、ホストされたデータレイヤーを管理します。
url: https://docs.tealium.com/ja/api-v1/hosted-data-layer/endpoints/
---これは、[現行のTealiumホストデータレイヤーAPI]()の古いバージョンです。

## アップロード

ホストされたデータレイヤーオブジェクトをアップロードします。

`POST /v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}`

POSTの代わりにPUTを使用すると、405 Method Not Allowedエラーが発生します。

### cURLリクエスト

```bash
cURL -i -b JSESSIONID={session_id} -X POST -H &#34;Content-Type: application/json&#34; \
  https://api.tealiumiq.com/v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token} \
  -d @{dl_id}.json
```

cURLコマンドを使用して`-d`パラメータにファイルを渡すとき、ファイル名は`@`文字で始まる必要があります。

### 例のレスポンス

#### ステータス201 OK

```
{
   &#34;status&#34;: &#34;pending&#34;
}
```

変更がTealiumのサーバーに反映されるまでに5から10分かかる場合があります。ステータスが完了と表示されるまで、同じ`dl_id`に対して別の呼び出しを試みるのを待ちます。

### エラーメッセージ

#### 405 Method not allowed

このエラーは、アップロードを実行するためにPOSTの代わりにPUTを使用したときに発生します。

```
{
   &#34;returnCode&#34; : 1464,
   &#34;message&#34; : &#34;Resource already exists. Updates are not permitted via this type of request.&#34;
}

```

#### 400 Bad request

以下のいずれかが真の場合、このエラーが発生します：

* JSONキーにピリオドが含まれている
* アカウント、プロファイル、および`dl_id`の組み合わせが250文字を超えている
* `dl_id`に制限された文字が含まれている
* ユーザーが適切な権限を持っていない
* アカウント/プロファイル名に誤字がある
* リクエストボディが空である
* 不正または無効なJSON
* JSONデータが1メビバイト（MiB）を超えている

```
{
   &#34;returnCode&#34; : 1400,
   &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34;
}
```

#### 401 Unauthorized

このエラーは、ユーザーが適切な権限を持っていないか、アカウント/プロファイル名に誤字がある場合に発生します。

```
{
   &#34;returnCode&#34; : 1469,
   &#34;message&#34; : &#34;although the user is authenticated, the request is denied because of a lack of proper permissions&#34;
}
```

## 更新

` PUT /v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}`

POSTの代わりにPUTを使用すると、405 Method Not Allowedエラーが発生します。

### cURLリクエスト

```bash
cURL -i -b JSESSIONID={session_id} -X PUT -H &#34;Content-Type: application/json&#34; \
  https://api.tealiumiq.com/v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token} \
  -d @{dl_id}.json
```

### 例のレスポンス

#### ステータス200 OK

```
{
   &#34;status&#34;: &#34;pending&#34;
}

```

変更がTealiumのサーバーに反映されるまでに最大1時間かかる場合があります。ステータスが完了と表示されるまで、同じ`dl_id`に対して別の呼び出しを試みるのを待ちます。

### エラーメッセージ

#### 400 Bad request

以下のいずれかが真の場合、このエラーが発生します：

* JSONキーにピリオドが含まれている
* アカウント、プロファイル、および`dl_id`の組み合わせが250文字を超えている
* `dl_id`に制限された文字が含まれている
* ユーザーが適切な権限を持っていない
* アカウント/プロファイル名に誤字がある
* リクエストボディが空である
* 不正または無効なJSON
* JSONデータが1メビバイト（MiB）を超えている

```
{
   &#34;returnCode&#34; : 1400,
   &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34;
}
```

#### 404 Not Found

提供された`dl_id`が存在しない場合、このエラーが発生します。

```
{
   &#34;returnCode&#34; : 1404,
   &#34;message&#34; : &#34;Could not locate data layer for supplied params ([account]/[profile]/[dl_id]).&#34;
}
```

## 削除

`DELETE/v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}`

### cURLリクエスト

```bash
cURL -i -b JSESSIONID={session_id} -X DELETE -H &#34;Content-Type: application/json&#34; \
  https://api.tealiumiq.com/v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}
```

### 例のレスポンス

#### ステータス200 OK

```
{
   &#34;status&#34;: &#34;pending&#34;
}

```

変更がTealiumのサーバーに反映されるまでに最大1時間かかる場合があります。ステータスが完了と表示されるまで、同じ`dl_id`に対して別の呼び出しを試みるのを待ちます。

### エラーメッセージ

#### 404 Not Found

提供された`dl_id`が存在しない場合、このエラーが発生します。

```
{
   &#34;returnCode&#34; : 1404,
   &#34;message&#34; : &#34;Could not locate data layer for supplied params ([account]/[profile]/[dl_id]).&#34;
}

```

#### 400 Bad request

以下のいずれかが真の場合、このエラーが発生します：

* アカウント、プロファイル、および`dl_id`の組み合わせが250文字を超えている
* `dl_id`に制限された文字が含まれている
* ユーザーが適切な権限を持っていない
* アカウント/プロファイル名に誤字がある

```
{
   &#34;returnCode&#34; : 1400,
   &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34;
}
```

#### 401 Unauthorized

このエラーは、適切な権限がないか、アカウント/プロファイル名に誤字がある場合に発生します。

```
{
   &#34;returnCode&#34; : 1469,
   &#34;message&#34; : &#34;although the user is authenticated, the request is denied because of a lack of proper permissions&#34;
}
```

## ステータスの取得

アップロード、更新、削除のアクションのステータスを取得します。ステータスは30日間だけ保持されます。

予想されるステータス値は次のとおりです：

* Pending
* Completed
* Failed

` GET /v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}`

### cURLリクエスト

```bash
cURL -i -b JSESSIONID={session_id} \
    https://api.tealiumiq.com/v1/dle/accounts/{account}/profiles/{profile}/datalayers/{dl_id}?utk={token}
```

### 例のレスポンス

```
{
   &#34;status&#34;: &#34;completed&#34;
}

```

### エラーメッセージ

#### 404 Not Found

提供された`dl_id`が存在しないか、提供された`dl_id`のステータスが期限切れであるため、30日間の保持期間を超えている場合、このエラーが発生します。

```
{
   &#34;returnCode&#34; : 1404,
   &#34;message&#34; : &#34;Status unavailable. Please refer to documentation for request status retention period.&#34;
}
```

#### 400 Bad request

以下のいずれかが真の場合、このエラーが発生します：

* アカウント、プロファイル、および`dl_id`の組み合わせが250文字を超えている
* `dl_id`に制限された文字が含まれている
* ユーザーが適切な権限を持っていない
* アカウント/プロファイル名に誤字がある

```
{
   &#34;returnCode&#34; : 1400,
   &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34;
}
```

#### 401 Unauthorized

このエラーは、適切な権限がないか、アカウント/プロファイル名に誤字がある場合に発生します。

```
{
   &#34;returnCode&#34; : 1469,
   &#34;message&#34; : &#34;although the user is authenticated, the request is denied because of a lack of proper permissions&#34;
}
```

## リスト

最大1,000のホストデータレイヤー名のリストを返します。

` GET /v1/dle/accounts/{account}/profiles/{profile}/datalayers?utk={token}`

### cURLリクエスト

```bash
cURL -i -b JSESSIONID={session_id} \
  https://api.tealiumiq.com/v1/dle/accounts/{account}/profiles/{profile}/datalayers?utk={token}

```

### 例のレスポンス

#### ステータス200 OK

```
{
   [&#34;demo_1&#34;,&#34;demo_2&#34;,&#34;demo_3&#34;]
}
```

### エラーメッセージ

#### 400 Bad request

このエラーは、適切な権限がないか、アカウント/プロファイル名に誤字がある場合に発生します。

```
{
   &#34;returnCode&#34; : 1400,
   &#34;message&#34; : &#34;Invalid request submission. Please check supplied parameters or request body.&#34;
}

```

#### 400 Bad Request

アカウント/プロファイルに対して1,000以上のホストデータレイヤーが見つかりました。

```
{
   &#34;returnCode&#34; : 1400,
   &#34;message&#34; : &#34;Invalid request submission. Data layer list size exceeds maximum permissible (1000).&#34;
}

```

#### 401 Unauthorized

```
{
   &#34;returnCode&#34; : 1469,
   &#34;message&#34; : &#34;although the user is authenticated, the request is denied because of a lack of proper permissions&#34;
}

```
