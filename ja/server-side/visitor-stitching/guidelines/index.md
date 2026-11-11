---
title: ビジタースティッチングのガイドライン
description: この記事では、ビジタースティッチングに関するガイドラインについて説明します。
url: https://docs.tealium.com/ja/server-side/visitor-stitching/guidelines/
---
ビジターID属性とビジタースティッチングに関する重要なガイドラインを以下に示します。

* **一意性**  
ビジターID属性には、3文字以上の一意の文字が含まれ、全体で6文字以上である必要があります。  
詳しくは、[ビジターID属性の要件]()を参照してください。
* **大文字と小文字の区別**<br>
ビジターID属性の値では大文字と小文字が区別されるため、`UserName@example.com`と`username@example.com`は異なる値として扱われます。属性値にこのような表記の違いが含まれる場合は、[小文字変換エンリッチメント]()を使用して正規化してください。
* **複数のID**  
複数のビジターID属性は、属性IDが小さいものから大きいもの（古いものから新しいもの）の順に、OR条件として評価されます。
* **堅牢性**  
ビジターID属性には、デバイスが異なっても同じビジターに確実に一致する[ユーザー識別子]()のみを使用してください。
* **スティッチされたビジタープロファイル**  
複数のビジタープロファイルがスティッチされる場合、元のプロファイルは保持され、スティッチされたプロファイルを格納するための新しいビジタープロファイルが作成されます。
* **テストデータの回避**  
ユーザー識別子に、`undefined`、`unknown`、`not set`などのデフォルト値やテスト値が取り込まれないように注意してください。
* **共有ID**  
スティッチングを有効にする前に、図書館や大学などで使用される共有IDの取り扱い方法を決定し、複数のビジターが誤ってスティッチされないようにしてください。
* **サイズ制限**  
暗号化および圧縮後のビジタープロファイルの最大サイズは400 KBです。
* **共有デバイス**  
2人のユーザーが1台のデバイスを共有すると、両方のユーザーに同じ匿名IDが割り当てられます。同じWebサイトにアクセスしながら、それぞれ異なるユーザー識別子（メールアドレスや顧客IDなど）を使用する場合、これはビジタースイッチングと呼ばれます。Tealium SupportまたはProfessional Servicesでは、ビジタースイッチングに対応するソリューションの実装を支援できます。詳しくは、以下のTealiumナレッジベース記事を参照してください。  
    * [Customer Data Platform（CDP）におけるビジタースイッチングを使用したITP環境下での匿名ユーザートラッキング](https://support.tealiumiq.com/en/support/solutions/articles/36000441645-anonymous-user-tracking-under-itp-with-visitor-switching-in-audiencestream)
    * [iQでのビジタースイッチング](https://support.tealiumiq.com/en/support/solutions/articles/36000419055-visitor-switching-in-iq)
    * [Tealium Mobile SDKでのビジタースイッチング](https://support.tealiumiq.com/en/support/solutions/articles/36000493080-visitor-switching-in-tealium-mobile-sdks)