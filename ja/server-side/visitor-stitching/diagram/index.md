---
title: 訪問のスティッチング例
description: この記事では、訪問がウェブサイトを訪れる際に異なるデバイスを使用すると発生する訪問のスティッチングプロセスの例を提供します。
url: https://docs.tealium.com/ja/server-side/visitor-stitching/diagram/
---
## 初回訪問

新しい訪問があなたのウェブサイトを自分のラップトップから訪れます。
1. 匿名IDが訪問に割り当てられ、プロファイルAが作成されます。匿名IDにより、複数の訪問に対して一つのプロファイルを維持することができます。
1. 訪問がこれまでに見たことのないメールアドレス、user@example.comで認証すると、そのメールアドレスがユーザー識別子に割り当てられます。
1. プロファイルAの訪問ID属性がユーザー識別子（メールアドレス）の値で豊かになります。
![](https://docs.tealium.com/images/server-side/visitor-stitching-example-first-visit.png)

## 二回目の訪問

翌日、同じ人が自分のタブレットからあなたのウェブサイトを訪れます。
1. 匿名IDが訪問に割り当てられ、プロファイルBが作成されます。
1. 訪問がプロファイルAに保存されている同じメールアドレス、user@example.comを使用してウェブサイトにログインします。
![](https://docs.tealium.com/images/server-side/visitor-stitching-example-second-visit.png)  
    プロファイルBの訪問ID属性がメールアドレス、user@example.comに構成されます。
1. AudienceStreamはメールアドレスに対して訪問IDのルックアップを実行します。プロファイルAとプロファイルBは同じメールアドレスに構成された訪問ID属性を持っており、プロファイルが関連していると判断されます。
1. AudienceStreamはプロファイルAとBをスティッチングし、プロファイルCを作成します。  
![](https://docs.tealium.com/images/server-side/visitor-stitching-profile-c-created.png)
    * プロファイルCはデスクトップとタブレットの両方で使用され、以下を含みます：
        * プロファイルAとBからのすべてのイベントと履歴データ。
        * プロファイルAとBへのリンクを含む`replaces`配列。
    * プロファイルAとBの`replaced by`属性にはプロファイルCへのリンクが含まれています。
    * プロファイルAとBの匿名IDに対するルックアップは引き続き実行できます。

## 三回目の訪問

数日後、ヌーチャーキャンペーンが`user@example.com`にメールを送ります。
1. ユーザーは自分の携帯電話でメールを開き、あなたのウェブサイトへのリンクをタップします。
1. メールアドレスがURLのクエリストリングパラメーターで渡され、AudienceStreamがページの読み込み時にユーザーを識別できるようになります。
1. メールアドレスが構成されたユーザー識別子でプロファイルDが作成されます。  
![](https://docs.tealium.com/images/server-side/visitor-stitching-third-visit-profile-d-created.png)  
    プロファイルDのメールアドレスはプロファイルCの訪問ID属性のメールアドレスと一致し、2つのプロファイルがスティッチングされ、プロファイルEが作成されます。
![](https://docs.tealium.com/images/server-side/visitor-stitching-profile-e-created.png)
    * プロファイルEはデスクトップ、タブレット、携帯電話のすべてで使用され、以下を含みます：
        * プロファイルCとDからのすべてのイベントと履歴データ。
        * プロファイルCとDへのリンクを含む`replaces`配列。
    * プロファイルCとDの`replaced by`属性にはプロファイルEへのリンクが含まれています。
    * プロファイルA、B、C、Dの匿名IDに対するルックアップは引き続き実行できます。
