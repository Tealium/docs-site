---
title: Apple ConfiguratorとCharlesを構成してApple TVをプロキシする
description: この記事では、Configuratorを使用してApple TVからのHTTPトラフィックをプロキシする手順を説明します。
url: https://docs.tealium.com/ja/platforms/ios-swift/proxy-appletv/
---
[Configurator](https://support.apple.com/en-us/HT202577)は、Appleデバイスに構成プロファイルを追加するためのツールです。

## 前提条件

* プロファイルを構成するためのApple Configurator。
* Charles Proxyバージョン3.10以降。

## Charles Proxyの構成

### Charles Proxyの構成

1. **Proxy > Proxy Settings...** メニューに移動します。
2. **Proxies**タブの**HTTP Proxy Port**フィールドに`8888`を入力します。  
![](https://docs.tealium.com/images/platforms/ios-swift/charles-proxy/charles-proxy-iosdevice1.jpeg)
3. **Proxy > SSL Proxying Settings...** メニューに移動します。
4. **SSL Proxying**タブで、**Enable SSL Proxying**チェックボックスを選択します。  
![](https://docs.tealium.com/images/platforms/ios-swift/charles-proxy/charles-proxy-iosdevice2.jpeg)
5. **Help > SSL Proxying > Install Charles Root Certification a Mobile Device or Remote Browser...**に移動します。  

<blockquote>
ダイアログに表示されるIPアドレスは、後で**Apple Configuratorの構成**で使用します。
</blockquote>
  
![](https://docs.tealium.com/images/platforms/ios-swift/charles-proxy/charles-proxy-iosdevice3.jpeg)
6. [https://charlesproxy.com/getssl](https://charlesproxy.com/getssl)に移動してSSL証明書をダウンロードします。


<blockquote>
証明書のダウンロード場所をメモしておいてください。
</blockquote>


### Charlesの証明書をエクスポートする

Charlesの証明書をエクスポートするには：

1. **Keychain Access**を開きます。
1. **File > Add Keychain**に移動し、上記のステップ6でダウンロードした証明書を選択します。
1. **Charles Proxy Custom Root Certificate**チェックボックスを選択します。
1. **File > Export Items**に移動し、証明書を`.cer`ファイルとしてローカルドライブの場所にエクスポートします。その場所をメモしておいてください。

## Apple Configuratorの構成

### Apple Configuratorを使用して構成プロファイルを作成する

Apple Configuratorを使用して構成プロファイルを作成するには：

1. **Open > New Profile**に移動します。
2. このプロファイルの名前と一意の識別子を入力します。
3. 左側のメニューから**Global HTTP Proxy**をクリックします。
4. **Proxy Server and Port**の下に、上記のCharles Proxyの構成ステップ5からのIPアドレスとポートを入力します。

![](https://docs.tealium.com/images/platforms/ios-swift/appleconfigurator1.jpeg)

5. 左側のメニューから**Certificates**を選択し、**Keychain Access**を通じて以前にエクスポートした`.cer`ファイルを選択します。
6. **File > Save**を選択してプロファイルをMacに保存します。ファイルの場所をメモしておいてください。

## Apple TVの構成

### Apple TVに構成プロファイルをインストールする

1. Apple TVをUSB経由でMacに接続します。Apple TVはConfiguratorの**All Devices**の下に表示されます。
1. Apple TVを選択し、上部メニューの**Add**をクリックします。
1. **Profiles**をクリックし、上記のCharles Proxyの構成ステップ6でダウンロードしたSSL証明書を選択します。これにより、構成プロファイルがApple TVにコピーされます。
1. Apple TVからのトラフィックは、これでCharlesを経由してプロキシされます。

### Apple TVから構成プロファイルを削除する

デバッグが終了したら、プロキシを停止するためにApple TVからプロファイルを削除する必要があります。そのためには：

1. Configuratorでデバイスをダブルクリックします。
1. 左側のメニューから**Profiles**をクリックします。
1. 構成プロファイルを選択し、**Edit > Delete**を選択します。

