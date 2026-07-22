---
title: ビジタースティッチングのガイドライン
description: この記事では、ビジタースティッチングのガイドラインについて説明します。
url: https://docs.tealium.com/ja/server-side/visitor-stitching/guidelines/
---
以下は、ビジターID属性とビジタースティッチングに関する重要なガイドラインです：

* **一意性**  
ビジターID属性は、少なくとも3つの一意の文字を持ち、少なくとも6文字の長さが必要です。  
[ビジターID属性の要件]()について詳しくはこちらをご覧ください。
* **大文字と小文字の区別**<br>
ビジターID属性の値は大文字と小文字を区別するため、`UserName@example.com`は`username@example.com`とは異なります。属性値にこれらのバリエーションが含まれている場合は、[小文字化エンリッチメント]()を使用して正規化します。
* **複数のID**  
複数のビジターID属性は、属性IDの順序（最古から最新）でOR条件として評価されます。
* **堅牢性**  
ビジターID属性には、デバイス間でビジターと一致することが保証されている[ユーザー識別子]()のみを使用する必要があります。
* **ステッチされたビジタープロファイル**  
複数のビジタープロファイルがステッチされると、元のプロファイルは残り、ステッチされたプロファイルを保存する新しいビジタープロファイルが作成されます。
* **テストデータの回避**  
ユーザー識別子にデフォルト値やテスト値（`undefined`、`unknown`、`not set`など）を取り込まないよう注意してください。
* **共有ID**  
スティッチングが有効になる前に、図書館や大学で使用されるような共有IDをどのように処理するかを決定し、複数のビジターが誤ってステッチされないようにします。
* **サイズ制限**  
暗号化と圧縮後のビジタープロファイルの最大サイズは400 KBです。
* **共有デバイス**  
2人のユーザーがデバイスを共有する場合、両方のユーザーは同じ匿名IDを持ちます。彼らが同じウェブサイトを訪れるが、異なるユーザー識別子（メールアドレスや顧客IDなど）を使用する場合、これをビジタースイッチングと呼びます。Tealiumサポートまたはプロフェッショナルサービスがビジタースイッチングを処理するソリューションの実装を支援できます。詳細については、以下のTealiumのナレッジベース記事を参照してください：  
    * [AudienceStreamでのITP下の匿名ユーザートラッキングとビジタースイッチング](https://support.tealiumiq.com/en/support/solutions/articles/36000441645-anonymous-user-tracking-under-itp-with-visitor-switching-in-audiencestream)
    * [iQでのビジタースイッチング](https://support.tealiumiq.com/en/support/solutions/articles/36000419055-visitor-switching-in-iq)
    * [Tealium Mobile SDKsでのビジタースイッチング](https://support.tealiumiq.com/en/support/solutions/articles/36000493080-visitor-switching-in-tealium-mobile-sdks)