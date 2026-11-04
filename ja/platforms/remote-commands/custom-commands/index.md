---
title: カスタムコマンド
description: カスタムコマンドについて説明します。
url: https://docs.tealium.com/ja/platforms/remote-commands/custom-commands/
---
アプリでタグ管理を使用する場合、カスタムリモートコマンドを使用すると、非表示の Web ビューからネイティブコードブロックをトリガーできます。これは、非表示の Web ビュー内に保持されているデータを、さらに処理するためにネイティブコードへ渡す必要がある場合に使用します。

リモートコマンドでは、JavaScript タグからアプリ内のメソッドをトリガーする手段として、カスタム URL スキームを使用します。非表示の Web ビュー内のタグがアプリにリクエストを送信し、そのリクエストは、カスタムコードまたはベンダー SDK をトリガーするリモートコマンドハンドラーによって処理されます。

### コンポーネント

リモートコマンドには、コマンド名とデータのペイロードがあります。

- **コマンド**  
アプリのネイティブコードに登録されているコマンド名（コマンド ID）。
- **ペイロード**  
ネイティブアプリに渡されるデータ。ハンドラーのレスポンスコールバックでは、`requestPayload` という名前のオブジェクトとして受信されます。


<blockquote>
ビルド時にネイティブアプリ内でリモートコマンドを定義します。カスタムリモートコマンドタグは、デバイス上で事前定義されたコードのみを実行します。
</blockquote>


### ネイティブコード

ネイティブコードでは、`add()` 関数によってリモートコマンドハンドラーを登録します。コールバック関数 `response` は、`response.payload` を使用してペイロードにアクセスできます。次の例では、参照されているペイロード変数に対応するデータレイヤー変数がタグ管理で構成されています。



```swift
tealium = Tealium(config: config) { [weak self] _ in
	let remoteCommand = RemoteCommand(commandId: "myRemoteCommand", description: "") { response in
		guard let payload = response.payload,
	    let myVariable = payload["myVariable"] as? String else {
			return
		}
		print(myVariable)
	}
	self.tealium?.remoteCommands?.add(remoteCommand)
}
```


```kotlin
val remoteCommand = object : RemoteCommand("sample", "testing RCs") {
    override fun onInvoke(response: Response) {
        Logger.dev(BuildConfig.TAG, "ResponsePayload for webView RemoteCommand ${response.requestPayload}")
    }
}
val tealium = Tealium.create(instanceName, config) {
    remoteCommands?.add(webViewRemoteCommand)
}
```



プラットフォームのビルドスクリプトに、ベンダーインテグレーション用のモジュールを追加します。モジュール名は `TealiumVendorXYZ` という形式で、たとえば `TealiumBraze` です。

インストールするには、ベンダーの依存関係を Tealium リモートコマンドの依存関係に置き換えます。たとえば、次の行を削除します。  
```bash
pod "VendorXYZ-iOS-SDK"
```
次に、以下の行を追加します。
```bash
pod "TealiumVendorXYZ"
```


### ユースケース：購入後アンケート

以下の手順では、ユーザーが購入を完了した後に、リモートコマンドを使用してアプリ内のアンケートをトリガーする方法を説明します。

1. メッセージと URL（非表示の Web ビューから取得）をメソッドパラメータとして渡し、ユーザーにアンケートへの回答を促すネイティブコードを作成します。
2. そのコードブロックを、Tealium API を使用してリモートコマンドとして登録します。
3. タグ管理でカスタムリモートコマンドタグを追加し、コマンド ID をネイティブコードに登録したコマンドと同じ値に構成します。
4. `survey_title` や `survey_url` などの特定の変数をアプリに渡すためのデータマッピングを構成します。
5. ネイティブコードで、レスポンスペイロードとして返された変数を使用し、ユーザーにアンケートを表示します。

これらの手順を完了すると、アプリを再デプロイすることなく、タグ管理の拡張機能を使用してアンケートのタイトル、URL、およびロジックを構成できます。


### リモートコマンドタグ

タグ管理では、以下の構成を使用して、リモートコマンドをカスタムリモートコマンドタグのインスタンスとして構成します。

* **コマンド ID**  
コマンドの名前（ネイティブメソッド `addRemoteCommandID` で使用する名前と同じもの）。
* **ロードルール**  
リモートコマンドをトリガーするタイミングを決定するルール。
* **マッピングされた変数**  
リモートコマンドに含めるデータ。マッピングされたデータレイヤー変数は、ネイティブコードのコールバック内にある `response.requestPayload` オブジェクトで使用できます。

### リモートコマンドタグの例

以下は、Swift でトラッキングされるイベントの例です。

```swift
tealium?.track(
    title: "My Screen",
    data: ["tealium_event": "my_event", "my_variable": "my_value"]
);
```

タグは次のように構成します。

* **コマンド ID**  
`myRemoteCommand`
* **ロードルール**  
`IF tealium_event EQUALS my_event`
* **マッピングされた変数**  
`my_variable -> myVariable`

以下のスクリーンショットは、タグ管理で構成された例を示しています。

![](https://docs.tealium.com/images/platforms/remote-commands/tag-example.png)