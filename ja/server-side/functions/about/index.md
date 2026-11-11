---
title: 関数について
description: 関数は、Tealium の機能を拡張するために使用できる小さな JavaScript コードブロックです。この記事では、関数の種類と主な利点について説明します。
url: https://docs.tealium.com/ja/server-side/functions/about/
---
## 関数の種類

Tealium は現在、以下の関数タイプをサポートしています。

* **データ変換関数**：Tealium Collect がイベントを受信し、関数のトリガー条件が満たされた後に実行される関数です。
詳細については、[データ変換関数について]()を参照してください。
* **イベント関数**：イベントの処理後に実行される関数です。詳細については、[イベント関数と訪問関数について]()を参照してください。
処理済みイベントによって実行される関数を使用するには、Event Streaming API Hub が有効になっている必要があります。詳細については、[Event Streaming の概要](https://docs.tealium.com/server-side/getting-started/tutorials/event-data-activation/introduction/)を参照してください。
* **訪問関数**：訪問の処理後に実行される関数です。詳細については、[イベント関数と訪問関数について]()を参照してください。処理済み訪問によって実行される関数を使用するには、Customer Data Platform（CDP）が有効になっている必要があります。詳細については、[CDP の概要](https://docs.tealium.com/server-side/getting-started/tutorials/visitor-profile-management/introduction/)を参照してください。
<!-- * **データレコード関数**：データレコードの処理後に実行される関数です。処理済みデータレコードによって実行される関数を使用するには、Data Cloud Activation プロファイルが必要です。詳細については、[Data Cloud Activation について]()を参照してください。 -->

## 主な利点

Functions は、お客様のニーズに合わせて Customer Data Hub の機能を拡張できるサーバーレス環境を提供します。

### サーバーレス環境

サーバーレス関数環境では、関数は Tealium Platform 上でホストされます。Tealium がサーバーとプラットフォームソフトウェアを管理するため、独自のデータ要件に対応する関数の実装に集中できます。メモリなどのリソースは、関数が呼び出されるたびに自動的に割り当てられます。詳細については、[実行環境とレート制限]()を参照してください。

### Customer Data Hub の拡張

データ変換関数を使用して、受信したイベントデータを変更できます。たとえば、データ変換関数を使用して、ネストされたオブジェクトのフラット化、機密データの削除、イベントオブジェクト内の変数への値の構成を行うことができます。

イベント関数と訪問関数を使用して、他のシステムからのデータの取得、Tealium データの拡充、または他のエンドポイントへのデータ送信を行うことができます。関数が訪問データまたはイベントデータを変更した場合、その変更は関数内に限定され、Tealium データには影響しません。関数は変更したデータを Tealium Collect に送信できます。そこでデータが再処理され、変更が Tealium データに反映されます。


<blockquote>
イベントデータまたは訪問データを Tealium Collect エンドポイントに送信すると、データが送信されるたびにイベント数が増加するため、コストが発生します。詳細については、[請求額の見積もり](https://docs.tealium.com/understanding-the-usage-report/#billing-estimation)を参照してください。
</blockquote>
