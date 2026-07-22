---
title: Track
description: Learn about the methods for tracking user activity.
url: https://docs.tealium.com/platforms/python/track/
---
## Track Views

The [`trackEvent()`](https://docs.tealium.com/platforms/python/api/#trackevent) method is used to track views, as shown in the following example:

```python
trackEvent("SCREEN_NAME", data, callback)
```

The parameters `data` and `callback` are optional.

## Track Events

The same [`trackEvent()`](https://docs.tealium.com/platforms/python/api/#trackevent) method is used to track events, as shown in the following example:

```python
trackEvent("EVENT_NAME", data, callback)
```

The parameters `data` and `callback` are optional. 

The following example demonstrates an event with the optional data and callback arguments provided:

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
