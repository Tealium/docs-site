---
title: Crypto Extension
description: The Crypto extension adds support for cryptographic hash functions to convert or generate data layer values.
url: https://docs.tealium.com/iq-tag-management/extensions/extensions-list/crypto-extension/
---
## Prerequisites

* utag v4.38 or later. For more information about updating the `utag.js` template, see our knowledge base article [Best Practices for Updating to the Latest Version of utag.js](https://support.tealiumiq.com/en/support/solutions/articles/36000363470).
* See [About Extensions]() to become familiar with how extension work.

### How it works

A cryptographic hash function is used to convert a text value containing sensitive information into an anonymous and unique, fixed-length string of characters. For example, hashing is commonly applied to a user&#39;s email address to anonymize the value while retaining its uniqueness. This extension offers a variety of commonly used hashing function algorithms, such as MD5 and SHA-1.

A data layer variable set in the extension is overwritten with the new hashed value. To generate a hashed value and preserve the original variable, use a second variable for the hashed value.

The term hashing is not synonomous with encryption.

## Using the extension

Once the Crypto extension is added, configure the following fields:

* **Hash Method**  
Select one of the available hashing functions:
    * **MD5**  
    The MD5 message-digest algorithm is a widely used hash function producing a 128-bit hash value.
    * **SHA-1**  
    The SHA-1 (Secure Hash Algorithm 1) is a hash function that takes an input and produces a 160-bit (20-byte) hash value known as a message digest – often rendered as a hexadecimal number, 40 digits long.
    * **SHA256**  
    The SHA256 hash function generates an almost-unique 256-bit (32-byte) signature for a text. SHA256 is a variant of the SHA-2 (Secure Hash Algorithm 2) set of cryptographic hash functions.
    * **SHA512**  
    A hash function that, when applied to the provided input, results in a 128-digit hexadecimal number that is highly unlikely to match the value produced for a different input. SHA512 is a variant of the SHA-2 (Secure Hash Algorithm 2) set of cryptographic hash functions.
    * **Variable**  
    Click **&#43; Add Variable** to add a variable value using the selected cryptographic function. Repeat this step to hash additional variables.

![](/images/iq-tag-management/cryptoextension-1.png)

### Example

The following example hashes a data layer variable named `customer_email`:

```
&gt; utag_data.customer_email
&lt; &#34;test@tealium.com&#34;
```

With the Crypto extension configured to convert `customer_email` using the SHA-1 cryptographic hash function, the new value becomes:

```
&gt; utag_data.customer_email
&lt; &#34;05fcf31275aa13408ace62e84dac60ae4b805a65&#34;
```

To preserve `customer_email` and create a hashed value, use a second variable named `customer_email_hash`. First, use the [Set Data Values extension]() to initialize the hash variable `customer_email_hash` to the value in `customer_email`, and then convert it in the Crypto extension. This ensures you preserve the original value after creating the new hash value:

```
&gt; utag_data.customer_email
&lt; &#34;test@tealium.com&#34;
&gt; utag_data.customer_email_hash
&lt; &#34;05fcf31275aa13408ace62e84dac60ae4b805a65&#34;
```

Another option is to scope the Crypto extension only to the tags that use the hashed value. This preserves the original variable for all other tags.
