---
title: Install
description: Learn to install Tealium for Ruby.
url: https://docs.tealium.com/platforms/ruby/install/
---
## Requirements

* [Tealium Customer Data Hub account]()

## Install

To install Tealium library for Ruby, run the following command:

```bash
gem install tealium
```

## Initialize

To initialize Tealium:  

1. Import the Tealium package with the following command:  
      ```ruby
      require &#39;tealium&#39;
      ```  
2. Initialize the Tealium object with the [`new()`](/platforms/ruby/api/#initialize) method, as shown in the following example:
      ```ruby
      teal = Tealium.new(&#34;ACCOUNT&#34;, &#34;PROFILE&#34;, &#34;DATASOURCE&#34;)
      ```
