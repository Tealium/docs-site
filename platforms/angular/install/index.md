---
title: Install
description: Learn to install the Tealium SDK for Angular.
url: https://docs.tealium.com/platforms/angular/install/
---This sample is based on the [Angular CLI Quickstart](https://angular.io/docs/ts/latest/cli-quickstart.html).

## Requirements

*   Tealium iQ Tag Management account
*   Angular application

## Sample app

To help familiarize yourself with the Tealium library, tracking methods, and best practice implementation, explore the Tealium for Angular [sample app](https://github.com/Tealium/integration-angular).


## Install

The installation only requires one file to be added to your application. This service takes care of loading the Tealium `utag.js` library for your account and handling the tracking calls.

To install the Tealium library for Angular:

1. Create the directory `./src/app/tealium` in your Angular application.

2. Copy the file [utag.service.ts](https://github.com/Tealium/integration-angular/tree/master/example/src/app/tealium) into your application&#39;s path `./src/app/tealium/`.

3. Follow the example found in the sample app&#39;s [`app.compontent.ts`](https://github.com/Tealium/integration-angular/blob/master/example/src/app/app.component.ts) file to define and invoke the Tealium service in your app.

      ```ruby
      import { Component, OnInit } from &#39;@angular/core&#39;;
      import { TealiumUtagService } from &#39;./tealium/utag.service&#39;;

      @Component({
            selector: &#39;app-root&#39;,
            providers: [TealiumUtagService],
            templateUrl: &#39;./app.component.html&#39;,
            styleUrls: [&#39;./app.component.css&#39;]
      })
      ```

## Initialize

The [`setConfig()`](/platforms/angular/api/#setconfig) method initializes Tealium and builds the path to the `utag.js` file, as shown in the following example:

```ruby
constructor(private tealium: TealiumUtagService) {
    this.tealium.setConfig({
        &#34;account&#34;     : &#34;ACCOUNT&#34;,
        &#34;profile&#34;     : &#34;PROFILE&#34;,
        &#34;environment&#34; : &#34;ENVIRONMENT&#34;});
}
```
The installation adds a new class to your application called `TealiumUtagService` which available by registering it as a provider to a component.


## Example

The following is a full example of importing the Tealium service to your application, [`app.component.ts`](https://github.com/Tealium/integration-angular/blob/master/example/src/app/app.component.ts).

```ruby
import { Component, OnInit } from &#39;@angular/core&#39;;
import { TealiumUtagService } from &#39;./tealium/utag.service&#39;;

@Component({
  selector: &#39;app-root&#39;,
  providers: [TealiumUtagService],
  templateUrl: &#39;./app.component.html&#39;,
  styleUrls: [&#39;./app.component.css&#39;]})

export class AppComponent implements OnInit {

  title = &#39;Testing App&#39;;

  constructor(private tealium: TealiumUtagService) {
    this.tealium.setConfig({ account: &#39;##TEALIUM_ACCOUNT##&#39;, profile: &#39;##TEALIUM_PROFILE##&#39;, environment: &#39;prod&#39; });
  }

  ngOnInit(): void {
    // The tealium.view function will call the tealium.track function with &#39;view&#39; as first param
    // Most tags support the &#39;view&#39; event and many analytics tags also support the &#39;link&#39; event
    this.tealium.view({event_name: &#39;init&#39;});
    //this.tealium.track(&#39;view&#39;, {&#39;event_name&#39; : &#39;init&#39;});
  }
}
```
