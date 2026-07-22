---
title: インストール
description: Python用Tealiumのインストール方法を学びます。
url: https://docs.tealium.com/ja/platforms/python/install/
---## 必要条件

* [Tealium Customer Data Hubアカウント](https://docs.tealium.com/introduction-to-customer-data-hub/)
* Python 2.7+ 

## サンプルスクリプト

Tealiumライブラリ、トラッキング方法、およびベストプラクティスの実装に慣れるために、[Pythonサンプルスクリプト](https://github.com/Tealium/tealium-python/blob/master/sample.py)を参照してください。


## インストール

Python用のTealiumライブラリをインストールするには：

1. 次のコマンドで使用しているPythonのバージョンを確認します：

    ```python
    python -V
    ```

2. 次の[pip](https://pip.pypa.io/en/stable/installing/)コマンドを実行します：  

    **Python 2**  
    ```python
    pip install tealium
    ```
    **Python 3**  
    ```python
    pip3 install tealium
    ```


## 初期化

モジュールをインポートし、以下の例に示すように[`Tealium()`](https://docs.tealium.com/ja/platforms/python/api/#tealium)コンストラクタで`Tealium`インスタンスを初期化します：

```python
from tealium import Tealium
teal = Tealium("ACCOUNT", "PROFILE", "ENVIRONMENT", "DATASOURCE")
```


<blockquote>
バージョン2.0.0以降、visitorId、sessionId、ローカル保存、および`vdata`ディスパッチャーは削除されました。すべてのCollectモジュールリクエストは現在、`/event`エンドポイントにPOSTリクエストとして送信されます。Tealium初期化子にはもはやPATHパラメーターはありません。
</blockquote>

