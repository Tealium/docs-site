---
title: iQリビジョンAPIについて
description: この記事では、iQリビジョンAPIの使用方法について説明します。
url: https://docs.tealium.com/ja/api/v2/iq-revisions/about/
---
## 仕組み

新しいリビジョンは、_Save as_アクションが実行されるたびに作成されます。各バージョンが更新または公開されると、その状態がリビジョンに反映されます。

## 前提条件

iQリビジョンAPIは、リビジョン情報を返す前に、あなたのアカウントで有効化されている必要があります。[サポートデスクに連絡](https://support.tealiumiq.com/)して、有効化をリクエストしてください。

## 認証


<blockquote>
ベアラートークンは、すべてのAPI呼び出しを認証するために使用され、APIキーではありません。APIキーは認証呼び出しでのみ使用されます。
</blockquote>


APIキーからベアラートークンを生成する方法については、[Getting Started](https://docs.tealium.com/api-authentication/)ガイドを参照してください。
