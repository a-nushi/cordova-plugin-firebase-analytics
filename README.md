
# Cordova plugin for [Firebase Analytics](https://firebase.google.com/docs/analytics/)

[![NPM version][npm-version]][npm-url] [![NPM downloads][npm-downloads]][npm-url] [![NPM total downloads][npm-total-downloads]][npm-url] [![PayPal donate](https://img.shields.io/badge/paypal-donate-ff69b4?logo=paypal)][donate-url] [![Twitter][twitter-follow]][twitter-url]

| [![Donate](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)][donate-url] | Your help is appreciated. Create a PR, submit a bug or just grab me :beer: |
|-|-|

## Forked from the original [cordova-plugin-firebase-analytics](https://github.com/chemerisuk/cordova-plugin-firebase-analytics) to fix some issues on the logEvent method (incorrect quantity on items parameter for iOS platform and missing items handling on Android platform). All credit goes to the original author of this repo

## Index

<!-- MarkdownTOC levels="2" autolink="true" -->

- [Supported platforms](#supported-platforms)
- [Installation](#installation)
- [Methods](#methods)

<!-- /MarkdownTOC -->

## Supported platforms

- iOS
- Android

## Installation

    $ cordova plugin add cordova-plugin-firebase-analytics

If you get an error about CocoaPods being unable to find compatible versions, run
    
    $ pod repo update

Use variables `ANDROID_FIREBASE_ANALYTICS_VERSION` or `IOS_FIREBASE_ANALYTICS_VERSION` to override dependency versions for Firebase SDKs:
    
    $ cordova plugin add cordova-plugin-firebase-analytics --variable IOS_FIREBASE_POD_VERSION="~> 8.8.0" --variable ANDROID_FIREBASE_CRASHLYTICS_VERSION="19.0.+"

NOTE: on iOS in order to collect demographic, age, gender data etc. you should additionally [include `AdSupport.framework`](https://firebase.google.com/support/guides/analytics-adsupport) into your project.

### Disabling analytics data collection
In some cases, you may wish to temporarily or permanently disable collection of Analytics data. You can set the value of variable `ANALYTICS_COLLECTION_ENABLED` to `false` to prevent collecting any user data:

    $ cordova plugin add cordova-plugin-firebase-analytics --variable ANALYTICS_COLLECTION_ENABLED=false

Later you can re-enable analytics data collection (for instance after getting end-user consent) using method [setEnabled](#setenabledenabled).

### Disabling automatic screen collection
In order to [disable automatic collection of screen view events](https://firebase.googleblog.com/2020/08/google-analytics-manual-screen-view.html) set the value of variable `AUTOMATIC_SCREEN_REPORTING_ENABLED` to `false`:

    $ cordova plugin add cordova-plugin-firebase-analytics --variable AUTOMATIC_SCREEN_REPORTING_ENABLED=false

### Adding required configuration files

Cordova supports `resource-file` tag for easy copying resources files. Firebase SDK requires `google-services.json` on Android and `GoogleService-Info.plist` on iOS platforms.

1. Put `google-services.json` and/or `GoogleService-Info.plist` into the root directory of your Cordova project
2. Add new tag for Android platform

```xml
<platform name="android">
    ...
    <resource-file src="google-services.json" target="app/google-services.json" />
</platform>
...
<platform name="ios">
    ...
    <resource-file src="GoogleService-Info.plist" />
</platform>
```

This way config files will be copied on `cordova prepare` step.

## Methods
Every method returns a promise that fulfills when a call was successful.

### logEvent(_name_, _params_)
Logs an app event.
```js
cordova.plugins.firebase.analytics.logEvent("my_event", {param1: "value1"});
```

Be aware of [automatically collected events](https://support.google.com/firebase/answer/6317485).

### setUserId(_id_)
Sets the user ID property.
```js
cordova.plugins.firebase.analytics.setUserId("12345");
```
This feature must be used in accordance with [Google's Privacy Policy](https://www.google.com/policies/privacy).

### setUserProperty(_name_, _value_)
Sets a user property to a given value.
```js
cordova.plugins.firebase.analytics.setUserProperty("name1", "value1");
```

Be aware of [automatically collected user properties](https://support.google.com/firebase/answer/6317486?hl=en&ref_topic=6317484).

### setCurrentScreen(_name_)
Sets the current screen name, which specifies the current visual context in your app. This helps identify the areas in your app where users spend their time and how they interact with your app.
```js
cordova.plugins.firebase.analytics.setCurrentScreen("User profile");
```

### setEnabled(_enabled_)
Sets whether analytics collection is enabled for this app on this device.
```js
cordova.plugins.firebase.analytics.setEnabled(false);
```

### resetAnalyticsData()
Clears all analytics data for this instance from the device and resets the app instance ID.
```js
cordova.plugins.firebase.analytics.resetAnalyticsData();
```

### setDefaultEventParameters(_params_)
Adds parameters that will be set on every event logged from the SDK, including automatic ones.
```js
cordova.plugins.firebase.analytics.setDefaultEventParameters({foo: "bar"});
```

[npm-url]: https://www.npmjs.com/package/cordova-plugin-firebase-analytics
[npm-version]: https://img.shields.io/npm/v/cordova-plugin-firebase-analytics.svg
[npm-downloads]: https://img.shields.io/npm/dm/cordova-plugin-firebase-analytics.svg
[npm-total-downloads]: https://img.shields.io/npm/dt/cordova-plugin-firebase-analytics.svg?label=total+downloads
[twitter-url]: https://twitter.com/chemerisuk
[twitter-follow]: https://img.shields.io/twitter/follow/chemerisuk.svg?style=social&label=Follow%20me
[donate-url]: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=4SVTMPKTAD9QC&source=url
