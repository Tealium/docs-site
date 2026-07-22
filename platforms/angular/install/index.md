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

2. Copy the file [utag.service.ts](https://github.com/Tealium/integration-angular/tree/master/example/src/app/tealium) into your application's path `./src/app/tealium/`.

3. Follow the example found in the sample app's [`app.compontent.ts`](https://github.com/Tealium/integration-angular/blob/master/example/src/app/app.component.ts) file to define and invoke the Tealium service in your app.

      ```ruby
      import { Component, OnInit } from '@angular/core';
      import { TealiumUtagService } from './tealium/utag.service';

      @Component({
            selector: 'app-root',
            providers: [TealiumUtagService],
            templateUrl: './app.component.html',
            styleUrls: ['./app.component.css']
      })
      ```

## Initialize

The [`setConfig()`](https://docs.tealium.com/platforms/angular/api/#setconfig) method initializes Tealium and builds the path to the `utag.js` file, as shown in the following example:

```ruby
constructor(private tealium: TealiumUtagService) {
    this.tealium.setConfig({
        "account"     : "ACCOUNT",
        "profile"     : "PROFILE",
        "environment" : "ENVIRONMENT"});
}
```
The installation adds a new class to your application called `TealiumUtagService` which available by registering it as a provider to a component.


## Example

The following is a full example of importing the Tealium service to your application, [`app.component.ts`](https://github.com/Tealium/integration-angular/blob/master/example/src/app/app.component.ts).

```ruby
import { Component, OnInit } from '@angular/core';
import { TealiumUtagService } from './tealium/utag.service';

@Component({
  selector: 'app-root',
  providers: [TealiumUtagService],
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']})

export class AppComponent implements OnInit {

  title = 'Testing App';

  constructor(private tealium: TealiumUtagService) {
    this.tealium.setConfig({ account: '##TEALIUM_ACCOUNT##', profile: '##TEALIUM_PROFILE##', environment: 'prod' });
  }

  ngOnInit(): void {
    // The tealium.view function will call the tealium.track function with 'view' as first param
    // Most tags support the 'view' event and many analytics tags also support the 'link' event
    this.tealium.view({event_name: 'init'});
    //this.tealium.track('view', {'event_name' : 'init'});
  }
}
```
