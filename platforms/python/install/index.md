---
title: Install
description: Learn to install Tealium for Python.
url: https://docs.tealium.com/platforms/python/install/
---## Requirements

* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)
* Python 2.7+ 

## Sample Script

To help familiarize yourself with the Tealium library, the tracking methods, and best practice implementation, see the [Python sample script](https://github.com/Tealium/tealium-python/blob/master/sample.py).


## Install

To install the Tealium library for Python:

1. Determine which version of Python you are using with the following command:

    ```python
    python -V
    ```

2. Run the following [pip](https://pip.pypa.io/en/stable/installing/) command:  

    **Python 2**  
    ```python
    pip install tealium
    ```
    **Python 3**  
    ```python
    pip3 install tealium
    ```


## Initialize

Import the module and initialize the `Tealium` instance with the [`Tealium()`](https://docs.tealium.com/platforms/python/api/#tealium) constructor, as shown in the following example:

```python
from tealium import Tealium
teal = Tealium("ACCOUNT", "PROFILE", "ENVIRONMENT", "DATASOURCE")
```


<blockquote>
As of version 2.0.0, visitorId, sessionId, local storage and `vdata` dispatcher has been removed. All Collect module requests are now sent as POST requests to the `/event` endpoint. The Tealium initializer no longer has a PATH parameter.
</blockquote>

