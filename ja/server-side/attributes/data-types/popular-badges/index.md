---
title: 人気のバッジ
description: これらは他のクライアントに役立つことが証明された人気のバッジです。
url: https://docs.tealium.com/ja/server-side/attributes/data-types/popular-badges/
---
| バッジ | 説明 |
|:-----:| ----------- |
| ![](https://docs.tealium.com/images/server-side/whiteui-badge-browseabandoner.png)<br> ブラウズ放棄者 |  <ul><li>**ルール** – 商品を閲覧し、カートに商品を追加しなかった訪問。</li><li>**アクション** – 既知の訪問であり、Facebook IDが分かっている場合、データをFacebookに送信して、ブランドを訪問に再ターゲティングします。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges)business-family.png)<br> ビジネス/ホーム族旅行者 |  <ul><li>**ルール** – 訪問が旅行のタイプをマークしたときに割り当てます。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-cartabandoner.png)<br> カート放棄者 |  <ul><li>**ルール** – カートに商品を追加し、購入しなかった訪問。</li><li>**アクション** – メールアドレスが分かっている場合、放棄された商品を含むパーソナライズされたメールを送信します。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-couponcodeabuser.png)<br> クーポンコード乱用者 |  <ul><li>**ルール** – 訪問が一度の訪問で特定の数以上のクーポンまたはプロモーションコードを使用しようとする。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-bades-couponcodestuffer.png)<br> クーポンコード詰め込み者 |  <ul><li>**ルール** – 訪問がすべての訪問で特定の数以上のクーポンまたはプロモーションコードを成功裏に使用している。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-disappointedshopper.png)<br> がっかりしたショッパー |  <ul><li>**ルール** – 現在在庫切れの商品を閲覧した訪問に割り当てます。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-freetrialuser.png)<br> 無料トライアルユーザー |  <ul><li>**ルール** – 無料トライアルにサインアップした訪問に割り当てます。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-frequenttraveler.png)<br> 頻繁な旅行者 |  <ul><li>**ルール** – 訪問が特定の期間に特定の回数以上旅行したときに割り当てます。例：訪問が過去12週間で5回旅行した。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-knownvisitor.png)<br> 既知の訪問 |  <ul><li>**ルール** – 訪問の重要な識別子をキャプチャしたときに割り当てます。例：顧客ID（クライアントのID）、顧客のメール、Facebook ID。これらの訪問は通常、メールやソーシャルメディアを通じてターゲットにされます。</li><li>**アクション** – なし。ただし、選択したベンダーAPIで訪問がターゲットにできることを確認するために、オーディエンスで使用されます。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-loyalvisitor.png)<br> 忠実な訪問 |  <ul><li>**ルール** – サイトへの直接訪問が特定の回数に達した訪問に割り当てます。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-newvisitor.png)<br> 新規訪問 |  <ul><li>**ルール** – "ライフタイム訪問数"が1に等しいときに割り当てます。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-purchaser.png)<br> 購入者 |  <ul><li>**ルール** – コンバートした訪問。例：商品を購入した、またはサービスにサインアップした。</li><li>**アクション** – 2週間後にメールで別の購入を誘うオファー、または購入した商品に関連する商品を示すメールを送信します。例えば、訪問が野球のバットを買った場合、野球のバッグとバッティンググローブを提供します。</li><li>**アクション** – 訪問をリターゲティングキャンペーンから削除し、不必要に再マーケティングされないようにします。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-recentvipvisitor.png)<br> 最近のVIP訪問 |  <ul><li>**ルール** – その90日間の購入価値が特定のドル額を超えたときに割り当てます。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-salesearcher.png)<br> セール検索者 |  <ul><li>**ルール** – 訪問が特定の数以上のセールページを閲覧したときに割り当てます。それがセールスカテゴリーであるか、セール中の商品であるかは問いません。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badge-browseabandoner.png)<br> 検索放棄者 |  <ul><li>**ルール** – 検索エンジンからサイトにアクセスし、共通のアクションを完了していない訪問。例えば、訪問中に少なくとも3ページを閲覧するなど。</li><li>**アクション** – 検索したカテゴリーを特定し、ディスプレイ広告ベンダーで再ターゲティングします。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-siteresearcher.png)<br> サイトリサーチャー |  <ul><li>**ルール** – 訪問がサイトを特定の回数以上訪れ、平均訪問時間が特定の分数以上の場合に割り当てます。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-testuser.png)<br> テストユーザー |  <ul><li>**ルール** – "test"がURLに含まれている、またはデバッグクッキーが構成されている、またはテスト訪問を示す他の基準がある場合に割り当てます。</li><li>キャンペーンがライブになる前に、構成が正しいことを確認するために、オーディエンスとアクションを製品でテストできます。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-unknownvisitor.png)<br> 未知の訪問 |  <ul><li>**ルール** – 訪問がまだウェブサイトで認証していない場合に割り当てます。認証とは必ずしもログインを意味しません。訪問がメールからサイトに来て、URLにメールが含まれている場合、訪問が誰であるかを特定し、彼らが"認証"したと判断します。</li><li>**アクション** – 訪問に自分自身を特定するように促すモーダルを表示します。これらの訪問は、より一般的にディスプレイ広告を通じてターゲットにされます。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-recentvipvisitor.png)<br> VIP訪問 |  <ul><li>**ルール** – ライフタイムの購入価値が特定のドル額に達したときに割り当てます。</li></ul> |
| ![](https://docs.tealium.com/images/server-side/whiteui-badges-windowshopper.png)<br> ウィンドウショッパー |  <ul><li>**ルール** – サイトを頻繁に訪れるが購入しない訪問。例：過去7日間に3回サイトを訪れ、商品詳細ページを閲覧したり記事を読んだりしているが、商品を購入したりサービスにサインアップしたりしていない訪問。</li><li>**アクション** – カテゴリーへの親和性を特定し、次のセッションのランディングページを変更して体験をパーソナライズします。</li></ul> |
