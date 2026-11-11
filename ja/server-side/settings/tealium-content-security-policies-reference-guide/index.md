---
title: コンテンツセキュリティポリシー
description: この記事では、コンテンツセキュリティポリシー（CSP）に追加する必要があるドメインを示します。
url: https://docs.tealium.com/ja/server-side/settings/tealium-content-security-policies-reference-guide/
---
## 仕組み

CSP（コンテンツセキュリティポリシー）は、クロスサイトスクリプティング（XSS）などの悪意のある攻撃を防止するためのセキュリティ機能です。Webページ上で読み込みおよび実行できるスクリプトや画像などのリソースを制御します。これらの制限を適用するため、CSPではHTTPヘッダーまたはメタタグにルールを定義し、コンテンツの提供元を制限してセキュリティをエンリッチメントします。

たとえば、次のCSPディレクティブについて考えてみます。

```
Content-Security-Policy: default-src 'self'; script-src 'self' tealium.com;
```

* `default-src`は、特定のリソースタイプに対して追加のディレクティブで異なるポリシーが構成されていない限り、ドキュメントと同一のオリジンからのみリソースを読み込むよう訪問のブラウザに指示します。
* `script-src`は、ドキュメントと同一のオリジンからのみスクリプトを読み込むよう訪問のブラウザに指示します。また、`tealium.com`からのスクリプトも許可します。

使用するTealium製品またはサービスごとに、そのデータセンターのドメインをCSPに追加してください。これにより、サイト訪問が必要なスクリプトを読み込めるようになります。また、タグ管理を通じて読み込まれるベンダーのドメインも追加してください。


<blockquote>
各リストには、将来使用される可能性のあるすべてのデータセンタードメインが含まれています。
</blockquote>


CSPの詳細については、[MDN：コンテンツセキュリティポリシー](https://developer.mozilla.org/en-US/docs/Web/HTTP/CSP)を参照してください。

## タグ管理

次のタグ管理データセンタードメインをCSPに追加してください。

```
tags.tiqcdn.com
tags.tiqcdn.cn
tags-eu.tiqcdn.com
```

## Tealium Collectタグ、顧客データプラットフォーム（CDP）、イベントストリーミング

次のTealium Collectタグ、顧客データプラットフォーム（CDP）、およびイベントストリーミングのデータセンタードメインをCSPに追加してください。

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

プライベートクラウド環境を使用している場合は、そのサイトをCSPに追加してください。たとえば、PC HMT Collect環境を追加するには、次のドメインをCSPに追加します。

```
pc-hmt-collect.tealiumiq.com
```

## データレイヤーエンリッチメント

次のTealiumデータレイヤーエンリッチメントのデータセンタードメインをCSPに追加してください。

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

次のTealium APIデータセンタードメインをCSPに追加してください。

```
api.tealiumiq.com
```