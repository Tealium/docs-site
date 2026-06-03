---
title: コンテンツセキュリティポリシー
description: この記事では、コンテンツセキュリティポリシー（CSP）に追加する必要があるドメインをリストアップしています。
url: https://docs.tealium.com/ja/server-side/administration/tealium-content-security-policies-reference-guide/
---
## 仕組み

CSP（コンテンツセキュリティポリシー）は、クロスサイトスクリプティング（XSS）などの悪意のある攻撃を防ぐためのセキュリティ機能です。これは、ウェブページ上でロードおよび実行できるリソース（スクリプトや画像など）を制御することによって実現されます。これらの制限を強制するために、CSPはHTTPヘッダーやメタタグでルールを定義し、コンテンツソースを制限してセキュリティをエンリッチメントします。

例えば、以下のCSPディレクティブを考えてみましょう：

```
Content-Security-Policy: default-src &#39;self&#39;; script-src &#39;self&#39; tealium.com;
```

* `default-src` は、追加のディレクティブが特定のリソースタイプに対して異なるポリシーを構成していない限り、ドキュメントと同じオリジンからのリソースのみをロードするように訪問のブラウザに指示します。
* `script-src` は、ドキュメントと同じオリジンからのスクリプトのみをロードするように訪問のブラウザに指示します。また、`tealium.com` からのスクリプトも許可します。

Tealiumの製品やサービスを使用する場合は、そのデータセンターのドメインをCSPに追加してください。これにより、サイト訪問が必要なスクリプトをロードできるようになります。また、Tealium iQタグ管理を通じてロードされるベンダーのドメインも追加してください。

各リストには、将来使用される可能性のあるすべてのデータセンタードメインが含まれています。

CSPについての詳細は、[MDN: コンテンツセキュリティポリシー](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)を参照してください。

## Tealium iQタグ管理

以下のiQタグ管理データセンタードメインをCSPに追加してください：

```
tags.tiqcdn.com
tags.tiqcdn.cn
tags-eu.tiqcdn.com
```

## Tealium Collectタグ、AudienceStream、EventStream

以下のTealium Collectタグ、Tealium AudienceStream、Tealium EventStreamデータセンタードメインをCSPに追加してください：

```
collect-ap-east-1.tealiumiq.com 
collect-ap-northeast-1.tealiumiq.com 
collect-ap-northeast-2.tealiumiq.com 
collect-ap-northeast-3.tealiumiq.com 
collect-ap-southeast-1.tealiumiq.com 
collect-ap-southeast-2.tealiumiq.com 
collect-ap-south-1.tealiumiq.com 
collect-ca-central-1.tealiumiq.com 
collect-eu-central-1.tealiumiq.com 
collect-eu-west-1.tealiumiq.com 
collect-eu-west-2.tealiumiq.com 
collect-eu-west-3.tealiumiq.com 
collect-sa-east-1.tealiumiq.com 
collect-us-east-1.tealiumiq.com 
collect-us-east-2.tealiumiq.com 
collect-us-west-1.tealiumiq.com 
collect-us-west-2.tealiumiq.com
collect.tealiumiq.com
```

### プライベートクラウド環境

プライベートクラウド環境を使用している場合は、そのサイトをCSPに追加してください。たとえば、PC HMT Collect環境を追加するには、以下のドメインをCSPに追加します：

```
pc-hmt-collect.tealiumiq.com
```

## データレイヤーのエンリッチメント

以下のTealiumデータレイヤーエンリッチメントデータセンタードメインをCSPに追加してください：

```
visitor-service-ap-east-1.tealiumiq.com
visitor-service-ap-northeast-1.tealiumiq.com 
visitor-service-ap-northeast-2.tealiumiq.com 
visitor-service-ap-northeast-3.tealiumiq.com 
visitor-service-ap-southeast-1.tealiumiq.com 
visitor-service-ap-southeast-2.tealiumiq.com 
visitor-service-ap-south-1.tealiumiq.com 
visitor-service-ca-central-1.tealiumiq.com 
visitor-service-eu-central-1.tealiumiq.com 
visitor-service-eu-west-1.tealiumiq.com 
visitor-service-eu-west-2.tealiumiq.com 
visitor-service-eu-west-3.tealiumiq.com 
visitor-service-sa-east-1.tealiumiq.com
visitor-service-us-east-1.tealiumiq.com 
visitor-service-us-east-2.tealiumiq.com 
visitor-service-us-west-1.tealiumiq.com 
visitor-service-us-west-2.tealiumiq.com
visitor-service.tealiumiq.com
```

## Tealium API

以下のTealium APIデータセンタードメインをCSPに追加してください：

```
api.tealiumiq.com
```