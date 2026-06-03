---
title: Charlesを使ってiOSデバイスのプロキシを構成する
description: このガイドでは、Charlesを使用してiOSデバイスからのHTTPトラフィックをプロキシするための構成手順を説明します。このガイドはCharlesのバージョン3.10以降に適用されます。
url: https://docs.tealium.com/ja/platforms/ios-swift/charles-proxy-iosdevice/
---
## Charlesの構成

Charlesを構成するには:

1. **Proxy &gt; Proxy Settings...** メニューを開きます。
2. **Proxies** タブをクリックし、**HTTP Proxy Port** フィールドに `8888` を入力します。  
![](/images/platforms/ios-swift/charles-proxy/charles-proxy-iosdevice1.jpeg)
3. **SSL Proxying Settings...** メニューを開きます。
4. **SSL Proxying** タブで、**Enable SSL Proxying** チェックボックスを選択します。  
![](/images/platforms/ios-swift/charles-proxy/charles-proxy-iosdevice2.jpeg)
    * デフォルトでは、Charlesはリストに含まれる特定のドメインのみでSSLプロキシを行います。
    * **Add** をクリックし、上記のロケーションリストに `*.*` を入力します。
    * アプリが正常に動作しなくなった場合、アプリがCharlesプロキシからの自己署名証明書を拒否している可能性があります。このような場合は、ワイルドカードマッチを無効にし、Tealiumのドメイン `*.tealiumiq.com` と `*.tiqcdn.com` のみをリストに記載します。
5. **Help &gt; SSL Proxying &gt; Install Charles Root Certification a Mobile Device or Remote Browser...** に移動します。  
![](/images/platforms/ios-swift/charles-proxy/charles-proxy-iosdevice3.jpeg)
6. 証明書を取得するためのIPアドレスとURLをメモします。例: `10.0.2.158` と `http://charlesproxy.com/getssl`

## iOSデバイスの構成

iOSデバイスを構成するには:

1. **Settings &gt; Wi-Fi** に移動し、コンピュータと同じWi-Fiネットワークに接続します。
2. アクティブなWi-Fiネットワークの詳細を選択し、**HTTP Proxy** セクションで **Manual** モードを選択します。
3. **Server** と **Port** フィールドに、上記の手順で取得したIPアドレスとポート番号（例: `8888`）を入力します。  
![](/images/platforms/ios-swift/charles-proxy/charles-proxy-iosdevice4.png)
4. iOSデバイスでプロキシ構成を保存すると、コンピュータ上のCharlesから接続を許可するように求めるアラートが表示されます。**Allow** をクリックします。  
![](/images/platforms/ios-swift/charles-proxy/charles-proxy-iosdevice5.jpeg)

## Charles SSL証明書のインストール

iOSデバイスにCharles SSL証明書をインストールするには:

1. iOSデバイス上でSafariを開き、[http://www.charlesproxy.com/getssl](http://www.charlesproxy.com/getssl)に移動します。
2. 証明書をインストールし、アクセスを許可するための指示に従います。  
![](/images/platforms/ios-swift/charles-proxy/charles-proxy-iosdevice6.png)

詳細については、[Using Charles SSL Certificates](http://www.charlesproxy.com/documentation/using-charles/ssl-certificates/)を参照してください。

 デバイスが証明書を信頼していることを確認するには、**Settings &gt; General &gt; About &gt; Certificate Trust Settings** に移動します。証明書が信頼されていない場合、プロキシ内のSSLリクエストは失敗します。  
