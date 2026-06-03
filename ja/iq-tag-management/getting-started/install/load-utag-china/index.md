---
title: 中国のネットワークからユニバーサルタグをロードする
description: この記事では、中国のネットワークからユニバーサルタグをロードする際のパフォーマンス向上について説明します。
url: https://docs.tealium.com/ja/iq-tag-management/getting-started/install/load-utag-china/
---
tags.tiqcdn.cnを使用して、中国本土内部だけでなく、世界中でコンテンツ配信を迅速化します。ドメイン`tags.tiqcdn.cn`は、ユーザーに最も近いノードを通じてAkamaiから配信され、そのノードはネットワークセキュリティ内部または外部にあることがあります。

## 考慮事項

* **ユニバーサルタグのロードに以下の方法のいずれかを選択します**:
    * **ウェブサイトのコードを更新します**: サイトのソースコードを変更でき、大量のトラフィックが中国から来ている場合は、ウェブサイトに追加するコードで`tags.tiqcdn.cn`を使用することをお勧めします。
    * **中国CDNデプロイメントエクステンションを使用します**: サイトのソースコードを変更できない、または少量のトラフィックが中国から来ている場合は、[中国CDNデプロイメントエクステンション]()を使用します。 一つの方法だけを使用してください。両方を使用しないでください。 
* **ユニークなプロファイルを使用します**  
各ウェブサイトに対してユニークなプロファイルを使用します。複数のプロファイルを使用することで、各ウェブサイトにタグを付け、そのウェブサイトのすべてのTealiumベースのコンテンツの配信をカスタマイズできます。
* **tags.tiqcdn.cn**  
`tags.tiqcdn.cn`は、ユーザーに最も近いノードを通じてAkamaiから利用できます。これは、中国のファイアウォール外のユーザーに対して`.cn`ドメインを使用しても、それらのユーザーのパフォーマンスに影響を与えないことを意味します。

* **インターネットコンテンツプロバイダー（ICP）ライセンス**  
中国本土で配信されるすべてのウェブコンテンツには、有効なICPライセンスが必要です。

## ウェブサイトのコードを更新する

ウェブサイトのコードを更新するには:

1. `.cn`ドメインのプロファイルを作成します。詳細については、[プロファイルの管理]()を参照してください。
    * 新しい専用の`.cn`ドメインプロファイルの構成を容易にするために、[プロファイルライブラリ]()を使用してプロファイル間で構成を共有することを検討してください。
2. **公開構成**の公開URLを更新して、`.cn`CDNパスを指定します。例えば:  
    ```bash
    https://tags.tiqcdn.cn/utag/ACCOUNT/PROFILE/dev/
    https://tags.tiqcdn.cn/utag/ACCOUNT/PROFILE/qa/
    https://tags.tiqcdn.cn/utag/ACCOUNT/PROFILE/prod/
    ```
    詳細については、[公開構成]()を参照してください。
3. HTMLソースに、`tags.tiqcdn.cn`を使用する以下のJavaScriptを追加します。
    ```javascript
    &lt;script type=&#34;text/javascript&#34;&gt;
      (function(a,b,c,d){
        a=&#39;https://tags.tiqcdn.cn/utag/ACCOUNT/PROFILE/prod/utag.js&#39;;
        b=document;c=&#39;script&#39;;d=b.createElement(c);d.src=a;d.type=&#39;text/java&#39;&#43;c;d.async=true;
        a=b.getElementsByTagName(c)[0];a.parentNode.insertBefore(d,a);
      })();
    &lt;/script&gt;
    ```

## 中国CDNデプロイメントエクステンションを使用する

ユーザーの位置を決定し、適切なCDNから`utag.js`を提供するために、中国CDNデプロイメントエクステンションを作成し、構成します。エクステンションの作成についての詳細は、[中国CDNデプロイメントエクステンション]()を参照してください。
