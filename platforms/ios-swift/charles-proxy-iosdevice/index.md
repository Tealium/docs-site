---
title: Set up Charles to proxy an iOS device
description: This guide explains the steps to configure Charles to proxy HTTP traffic from your iOS device. This guide applies to version 3.10 and higher of Charles.
url: https://docs.tealium.com/platforms/ios-swift/charles-proxy-iosdevice/
---
## Configure Charles

To configure Charles:

1. Open the **Proxy &gt; Proxy Settings...** menu.
2. Click the **Proxies** tab, in the **HTTP Proxy Port** field and enter `8888`.  
![](/images/platforms/ios-swift/charles-proxy/charles-proxy-iosdevice1.jpeg)
3. Open the **SSL Proxying Settings...** menu.
4. On the **SSL Proxying** tab, select the **Enable SSL Proxying** checkbox.  
![](/images/platforms/ios-swift/charles-proxy/charles-proxy-iosdevice2.jpeg)
    * By default, Charles will only perform SSL proxying for specific domains you include in the list.
    * Click **Add**, and enter `*.*` in the location list above.
    * If your app ceases to function correctly, it&#39;s possible that the app is rejecting the self-signed certificate from Charles proxy. If this happens, disable the wildcard match, and list only the `*.tealiumiq.com` and `*.tiqcdn.com` Tealium domains.
5. Go to **Help &gt; SSL Proxying &gt; Install Charles Root Certification a Mobile Device or Remote Browser...**  
![](/images/platforms/ios-swift/charles-proxy/charles-proxy-iosdevice3.jpeg)
6. Make note of the instructions, specifically the IP address and URL to get the certificate, for example: `10.0.2.158` and `http://charlesproxy.com/getssl`

## Configure your iOS device

To configure your iOS device:

1. Go to **Settings &gt; Wi-Fi** and connect to the same Wi-Fi network as your computer.
2. Select the active Wi-Fi network details, and in the **HTTP Proxy** section select the **Manual** mode.
3. In the **Server** and **Port** fields, enter the IP address and the port number (for example, `8888`) from the steps above.  
![](/images/platforms/ios-swift/charles-proxy/charles-proxy-iosdevice4.png)
4. After you save your proxy settings on your iOS device, you will receive an alert from Charles on your computer asking you to allow the connection. Click **Allow**.  
![](/images/platforms/ios-swift/charles-proxy/charles-proxy-iosdevice5.jpeg)

## Install the Charles SSL certificate

To install the Charles SSL certificate on your iOS device:

1. On your iOS device, open Safari and navigate to [http://www.charlesproxy.com/getssl](http://www.charlesproxy.com/getssl).
2. Follow the instructions to install the certificate and allow the access.  
![](/images/platforms/ios-swift/charles-proxy/charles-proxy-iosdevice6.png)

For more information, see [Using Charles SSL Certificates](http://www.charlesproxy.com/documentation/using-charles/ssl-certificates/)

 Ensure the device trusts the certificate by going to **Settings &gt; General &gt; About &gt; Certificate Trust Settings**. If the certificate is not trusted, SSL requests will fail in the proxy.  
