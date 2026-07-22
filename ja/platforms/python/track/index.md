---
title: トラック
description: ユーザー活動の追跡方法について学びます。
url: https://docs.tealium.com/ja/platforms/python/track/
---
## ビューの追跡

[`trackEvent()`](https://docs.tealium.com/ja/platforms/python/api/#trackevent) メソッドは、以下の例に示すように、ビューの追跡に使用されます：

```python
trackEvent("SCREEN_NAME", data, callback)
```

パラメータ `data` と `callback` はオプションです。

## イベントの追跡

同じ [`trackEvent()`](https://docs.tealium.com/ja/platforms/python/api/#trackevent) メソッドは、以下の例に示すように、イベントの追跡にも使用されます：

```python
trackEvent("EVENT_NAME", data, callback)
```

パラメータ `data` と `callback` はオプションです。

以下の例は、オプションのデータとコールバック引数が提供されたイベントを示しています：

```python
def tealiumCallback(info, success, error=None):
    if error is not None:
        print (info, success, error)
        return
    print (info, success)

eventData = {'KEY': 'VALUE'}
teal.trackEvent('EVENT_NAME',
                data=eventData,
                callback=tealiumCallback) 
```
