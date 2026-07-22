---
title: Install
description: Learn to install Tealium for Ruby.
url: https://docs.tealium.com/platforms/ruby/install/
---
## Requirements

* [Tealium Customer Data Hub account](https://docs.tealium.com/introduction-to-customer-data-hub/)

## Install

To install Tealium library for Ruby, run the following command:

```bash
gem install tealium
```

## Initialize

To initialize Tealium:  

1. Import the Tealium package with the following command:  
      ```ruby
      require 'tealium'
      ```  
2. Initialize the Tealium object with the [`new()`](https://docs.tealium.com/platforms/ruby/api/#initialize) method, as shown in the following example:
      ```ruby
      teal = Tealium.new("ACCOUNT", "PROFILE", "DATASOURCE")
      ```
