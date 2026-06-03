---
title: カスタムコマンド
description: カスタムコマンドについて学びます。
url: https://docs.tealium.com/ja/platforms/remote-commands/custom-commands/
---
アプリでiQタグ管理を使用する際、カスタムリモートコマンドは、レンダリングされていないWebビューからネイティブコードブロックをトリガーする機能を提供します。これは、レンダリングされていないWebビュー内に保持されているデータをネイティブコードに戻してさらに処理する必要がある場合に使用されます。

リモートコマンドは、JavaScriptタグがアプリ内のメソッドをトリガーするためのカスタムURLスキームを使用します。レンダリングされていないWebビュー内のタグがアプリにリクエストを送信し、リモートコマンドハンドラがカスタムコードまたはベンダーSDKをトリガーしてリクエストを処理します。

### コンポーネント

リモートコマンドには、コマンド名とデータのペイロードがあります。

- **コマンド**  
アプリのネイティブコードに登録されたコマンド、またはコマンドIDの名前。
- **ペイロード**  
ネイティブアプリに渡され、ハンドラのレスポンスコールバックで`requestPayload`という名前のオブジェクトとして受け取られるデータ。

ビルド時にネイティブアプリでリモートコマンドを定義します。カスタムリモートコマンドタグは、デバイス上で事前に定義されたコードのみを実行します。

### ネイティブコード

ネイティブコードでは、`add()`関数がリモートコマンドハンドラを登録します。コールバック関数`response`は`response.payload`でペイロードにアクセスします。以下の例では、参照されているペイロード変数は、iQタグ管理で構成されたデータレイヤー変数と一致しています。



```swift
tealium = Tealium(config: config) { [weak self] _ in
	let remoteCommand = RemoteCommand(commandId: &#34;myRemoteCommand&#34;, description: &#34;&#34;) { response in
		guard let payload = response.payload,
	    let myVariable = payload[&#34;myVariable&#34;] as? String else {
			return
		}
		print(myVariable)
	}
	self.tealium?.remoteCommands?.add(remoteCommand)
}
```


```kotlin
val remoteCommand = object : RemoteCommand(&#34;sample&#34;, &#34;testing RCs&#34;) {
    override fun onInvoke(response: Response) {
        Logger.dev(BuildConfig.TAG, &#34;ResponsePayload for webView RemoteCommand ${response.requestPayload}&#34;)
    }
}
val tealium = Tealium.create(instanceName, config) {
    remoteCommands?.add(webViewRemoteCommand)
}
```



ベンダー統合のモジュールをプラットフォームのビルドスクリプトに追加します。モジュールは`TealiumVendorXYZ`の形式で名前が付けられています。例えば`TealiumBraze`などです。

インストールするには、ベンダーの依存関係をTealiumのリモートコマンド依存関係に置き換えます。例えば、以下の行を削除します：  
```bash
pod &#34;VendorXYZ-iOS-SDK&#34;
```
次に、以下の行を追加します：
```bash
pod &#34;TealiumVendorXYZ&#34;
```


### ユースケース：購入調査

以下の手順は、ユーザーが購入を完了した後にアプリで調査をトリガーするためのリモートコマンドの使用方法を示しています。

1. ユーザーに調査を促すネイティブコードを作成し、メッセージとURLをメソッドパラメータとして渡します（レンダリングされていないWebビューから）。
2. Tealium APIでコードブロックをリモートコマンドとして登録します。
3. iQタグ管理でカスタムリモートコマンドタグを追加し、コマンドIDをネイティブコードで登録した同じコマンドに構成します。
4. `survey_title`や`survey_url`などの特定の変数をアプリに戻すためのデータマッピングを構成します。
5. ネイティブコードで、レスポンスペイロードで戻された変数を使用してユーザーに調査を表示します。

これらの手順を完了すると、iQタグ管理の拡張機能を使用して調査のタイトル、URL、ロジックを構成できるようになり、アプリを再デプロイすることなく行うことができます。


### リモートコマンドタグ

iQタグ管理では、リモートコマンドがカスタムリモートコマンドタグのインスタンスとして構成され、以下の構成が行われます：

* **コマンドID**  
コマンドの名前（ネイティブメソッド`addRemoteCommandID`で使用される同じ名前）。
* **ロードルール**  
リモートコマンドをトリガーするタイミングを決定するルール。
* **マップされた変数**  
リモートコマンドに含めるデータ。マップされたデータレイヤー変数は、ネイティブコードコールバックの`response.requestPayload`オブジェクトで利用可能です。

### 例：リモートコマンドタグ

以下は、Swiftでのトラックされたイベントの例です。

```swift
tealium?.track(
    title: &#34;My Screen&#34;,
    data: [&#34;tealium_event&#34;: &#34;my_event&#34;, &#34;my_variable&#34;: &#34;my_value&#34;]
);
```

タグの構成は以下のように定義されます：

* **コマンドID**  
`myRemoteCommand`
* **ロードルール**  
`IF tealium_event EQUALS my_event`
* **マップされた変数**  
`my_variable -&gt; myVariable`

以下のスクリーンショットは、iQタグ管理で構成された例を示しています。

![](/images/platforms/remote-commands/tag-example.png)
