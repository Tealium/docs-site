---
title: Impact Page Loads コネクタ構成ガイド
description: この記事では、Impact Page Loads コネクタの構成方法について説明します。
url: https://docs.tealium.com/ja/server-side-connectors/impact-page-loads-connector/
---
## コネクタアクション

| アクション名 | 訪問プロファイル | イベントデータ |
| --- | :---: | :---: |
|ランディングページイベントを送信| ✓| ✓|

## 構成

コネクタマーケットプレイスに移動し、新しいコネクタを追加します。詳細については、[about-connectors](https://docs.tealium.com/about-connectors/)を参照してください。

コネクタを追加した後、以下の項目を構成します。

## アクションとパラメーター

**Continue**をクリックして、コネクタアクションを構成します。アクションの名前を入力し、リストからアクションタイプを選択します。

### ランディングページイベントを送信

| **パラメーター** | **説明** |
| --- | --- |
| Campaign ID | （必須）Impactから提供される一意の整数のキャンペーン識別子。 |
| Page URL | （必須）ランディングページの完全なURL。例：`https://www.example.com?utm_source=google&utm_medium=cpc`。 |
| Custom Profile ID | （必須）広告主独自のユーザー固有値。例：`cookie value`。 |
| User Agent | （必須）ブラウザーとオペレーティングシステムを識別する文字列。 |
| IP Address | （必須）顧客のIPアドレスを表す文字列。 |
| Referring URL | クリック元ページのURL。 |
| Customer ID | プラットフォームが顧客アカウントに割り当てる、一意の英数字の顧客識別子。個人を特定できる情報は使用しないでください。 |
| Customer Email | 顧客のメールアドレスをSHA1でハッシュ化した文字列。 |
| Event Date | 文字列値`NOW`、または<a href="https://en.wikipedia.org/wiki/ISO_8601" target="_blank">ISO 8601</a>形式か`dd-MMM-yyyy HH:mm:ss z`形式の日付を使用します。デフォルトでは`NOW`が使用されます。 |
| Customer Email Already Hashed | 顧客のメールアドレスがすでにハッシュ化されている場合は、このチェックボックスをオンにします。 |