---
title: AndroidデバイスにCharlesをプロキシ構成する方法
description: この記事では、AndroidデバイスでネットワークリクエストをCharlesを通じてプロキシする構成方法について説明します。Charlesは、Android用Tealiumの実装をトラブルシューティングおよびデバッグする際に役立ちます。
url: https://docs.tealium.com/ja/platforms/android-kotlin/charles-proxy-android/
---
## Charlesプロキシの構成

以下の手順に従ってCharlesプロキシを構成してください：

1. **Proxy > Proxy Settings**に移動します。
2. **Proxies**タブをクリックし、HTTP Proxy Portフィールドに`8888`を入力します。
3. **Proxy > SSL Proxying Settings**に移動します
![](https://docs.tealium.com/images/platforms/android/charles-proxy/android-charles-proxy1.jpeg)
4. **SSL Proxying**タブをクリックし、**Enable SSL Proxying**チェックボックスを選択して場所を構成します。
![](https://docs.tealium.com/images/platforms/android/charles-proxy/android-charles-proxy2.jpeg)
    * デフォルトでは、リストに含まれる特定のドメインに対してのみSSLプロキシングを行います。
    * **Add**をクリックし、上記の場所リストに`*.*`を入力します。
    * アプリが正常に機能しなくなった場合、アプリがCharlesプロキシの自己署名証明書を拒否している可能性があります。この場合、ワイルドカードマッチを無効にし、`*.tealiumiq.com`および`*.tiqcdn.com`のTealiumドメインのみをリストに追加してください。
5. ポートのデフォルト値は`443`です。このフィールドは空白のままにしておくことができます。Charlesが自動的に構成します。

### IPアドレスの特定

コンピュータのIPアドレスを特定するには：

1. **System Preferences > Network > Wifi > Advanced > TCP/IP**に移動します。
![](https://docs.tealium.com/images/platforms/android/charles-proxy/android-charles-proxy3.jpeg)  

<blockquote>
Macでは、システムトレイのネットワークアイコンをクリックする際に**Option**キーを押し続けることができます。
</blockquote>

2. IPV4アドレスをメモしておき、後の手順で使用します。

### AndroidデバイスをCharlesプロキシで使用するように構成

以下の手順に従って、AndroidデバイスをCharlesプロキシで使用するように構成してください：

1. **Settings > Wifi**に移動します。
2. 現在接続しているWifiネットワークデバイスの電源キーを長押しします。
3. モーダルが表示されたら、**Modify Network**を選択します。
4. **Show Advanced Options**を選択してプロキシオプションを表示します。
5. **Proxy**の下で**Manual**を選択します。
6. **Proxy Host Name**フィールドに、以前に開発マシンから保存したIPV4アドレスを入力します。
7. **Proxy Port**フィールドに、Charlesの構成時に使用した`8888`を入力します。
![](https://docs.tealium.com/images/platforms/android/charles-proxy/android-charles-proxy4.jpeg)
8. **Save**をクリックして構成を保存し、終了します。
9. デバイス上のブラウザを開いてテストします。CharlesはSSLプロキシングを許可するか拒否するかを尋ねるダイアログを表示します。
10. **Allow**をクリックします。SSLプロキシングを許可するように求められない場合は、Charlesを再起動して再試行してください。
11. デバイスから[http://charlesproxy.com/getssl](http://charlesproxy.com/getssl)にアクセスし、Charles SSL証明書をダウンロードします。  
新しいバージョンのAndroidでは、`download unsuccessful`のようなエラーが発生する場合があります。その場合は、以下の指示に従ってください：
    * **Help > SSL Proxying > Save Charles Root Certificate**に移動します。
  ![](https://docs.tealium.com/images/platforms/android/charles-proxy/android-charles-proxy5.jpeg)
    * ファイルタイプをデフォルトの`.pem`から`.cer`に変更し、後で覚えている場所に保存します。
    * SDカード、USBケーブル、またはGoogle Driveのようなリモート転送を使用して、`.cer`ファイルをデバイスに転送します。
    * AndroidファイルマネージャーやFile Commanderのようなサードパーティのファイルマネージャーを使用してファイルを開きます。
    * 証明書を保存するように求められます。残りの手順を続けてください。
12. 証明書に名前を付け、信頼された証明書として確認します。完了したら無効にするか削除してください。
13. 証明書がインストールされた後、PINを構成します。

### Android N以降の追加構成手順

Android N以降では、アプリケーションがCharles SSLプロキシングによって生成されたSSL証明書を信頼するように構成を追加する必要があります。これは、制御するアプリケーションでのみSSLプロキシングを使用できることを意味します。

アプリをCharlesを信頼するように構成するには、まず[Network Security Configuration File](https://developer.android.com/training/articles/security-config.html)をアプリに追加する必要があります。このファイルはシステムのデフォルトをオーバーライドし、アプリがユーザーがインストールしたCA証明書、例えばCharles Root Certificateを信頼するようにします。


<blockquote>
構成ファイルで、これがデバッグビルドのアプリケーションでのみ適用されるように指定することもできます。これにより、本番ビルドはデフォルトの信頼プロファイルを使用します。
</blockquote>


Network Security Configuration Fileを追加し、アプリのマニフェストにファイルへの参照を追加する手順は次のとおりです：

1. 次の例を使用してSecurity Network Configurationファイルを作成します。  
    ```xml
    <network-security-config> 
       <debug-overrides> 
         <trust-anchors> 
           <!-- Trust user added CAs while debuggable only -->
           <certificates src="user" /> 
         </trust-anchors> 
       </debug-overrides> 
    </network-security-config>
    ```
2. ファイルに`network_security_config.xml`という名前を付けます。
3. ファイルを`res/xml/network_security_config.xml`にコピーします。
4. 次の例を使用して、アプリのマニフェストに`network_security_config.xml`ファイルへの参照を追加します：  
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <manifest ... >
       <application android:networkSecurityConfig="@xml/network_security_config" ... >
           ...
       </application>
    </manifest>
    ```

詳細については、[Charles proxy SSL Certificates](https://www.charlesproxy.com/documentation/using-charles/ssl-certificates/)のドキュメントの**Android**セクションを参照してください。

## ネットワークトラフィックのビューをフィルタリングするためのヒント

次の表は、ネットワークトラフィックのビューをフィルタリングするために使用されるヒントを提供します：

| フィルタ | アクション |
| ----   | ----   | 
| デバイス別フィルタ | <ul><li>ローカルマシンではなく、Androidデバイスからのトラフィックのみを表示するようにするには、**Proxy**メニューに移動し、**macOS/Windows proxy**のチェックを外します。</li><li>この手順により、マシンからのローカルトラフィックに対するCharlesプロキシが無効になり、Charlesはリモート接続されたデバイスからのトラフィックのみを表示します。</li></ul>
| ドメイン別フィルタ | <ul><li>興味のあるトラフィックのみを表示するために、Charlesの**Sequence**タブに移動し、ドメイン別にフィルタフィールドを使用します。例えば、`collect.tealiumiq.com`。</li><li>検索構成でRegexを有効にすると、Regexもオプションとして使用できます。Regexを有効にすると、Tealiumサーバーに向かうすべてのヒットを表示するために`*.tealiumiq.com`フィルタを使用できます。</li></ul> |

## 証明書をクリアし、デバイスからPINを削除する

Androidデバイスから証明書をクリアし、PINを削除することはオプションです。

証明書をクリアし、PINを削除する、またはその両方を行うための手順は次のとおりです：

1. Androidデバイス上の**Settings**アプリケーションを開きます。
1. オプションのリストの最後にある**Security > Clear Credentials**に移動します。
1. **Clear Credentials**をクリックします。
1. 資格情報をクリアすることを確認します。
1. PINを削除するには、**Settings > Lock Screen > Screen Lock**に移動し、PINを削除します。

詳細については、[Charles SSL Proxying](http://www.charlesproxy.com/documentation/proxying/ssl-proxying/)および[iOSデバイスのCharlesプロキシ構成](https://docs.tealium.com/ja/platforms/ios-swift/charles-proxy-iosdevice)を参照してください。
