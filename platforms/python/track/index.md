---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/python/track/
---
## Track Views

The [`trackEvent()`](/platforms/python/api/#trackevent) method is used to track views, as shown in the following example:

```python
trackEvent(&#34;SCREEN_NAME&#34;, data, callback)
```

The parameters `data` and `callback` are optional.

## Track Events

The same [`trackEvent()`](/platforms/python/api/#trackevent) method is used to track events, as shown in the following example:

```python
trackEvent(&#34;EVENT_NAME&#34;, data, callback)
```

The parameters `data` and `callback` are optional. 

The following example demonstrates an event with the optional data and callback arguments provided:

```python
def tealiumCallback(info, success, error=None):
    if error is not None:
        print (info, success, error)
        return
    print (info, success)

eventData = {&#39;KEY&#39;: &#39;VALUE&#39;}
teal.trackEvent(&#39;EVENT_NAME&#39;,
                data=eventData,
                callback=tealiumCallback) 
```
