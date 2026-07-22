---
title: インストール
description: Ruby用のTealiumのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/ruby/install/
---
## 要件

* [Tealium Customer Data Hubアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)

## インストール

Ruby用のTealiumライブラリをインストールするには、次のコマンドを実行します：

```bash
gem install tealium
```

## 初期化

Tealiumを初期化するには：  

1. 次のコマンドでTealiumパッケージをインポートします：  
      ```ruby
      require 'tealium'
      ```  
2. 次の例に示すように、[`new()`](https://docs.tealium.com/ja/platforms/ruby/api/#initialize)メソッドを使用してTealiumオブジェクトを初期化します：
      ```ruby
      teal = Tealium.new("ACCOUNT", "PROFILE", "DATASOURCE")
      ```
