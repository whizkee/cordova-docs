---
layout: post
author:
    name: Niklas Merz
    url: https://twitter.com/niklasmaerz
title:  "How to use the WKWebViewOnly compile flag to avoid the UIWebView deprecation warning"
categories: howto
tags: cordova-ios uiwebview wkwebview webview roadmap
---

As of August 2019, Apple is now showing a deprecation warning when uploading apps to the App Store that include UIWebView-related code. UIWebView has been unofficially deprecated in favour of the new WKWebView for a while, but Apple has now made it officially deprecated. As a result, all Cordova apps built for iOS will receive this deprecation warning on upload.

## Requirements

The goal of this post is explain how to use the `WKWebViewOnly` preference for apps that are **already using WKWebView** right now. Migrating from UIWebView to WKWebView requires some additional considerations.

The `WKWebViewOnly` preference was introduced with 5.1.0 and is supported by `cordova-plugin-inappbrowser` 3.2.0 and higher.

<!--more-->
## How it works

If you want to remove all UIWebView from your app bundle you submit to the App Store, you should set this preference to the config.xml file in the iOS part:

`<preference name="WKWebViewOnly" value="true" />`

After adding this preference you need to remove the iOS platform and add it again. With this setting enabled the compiler will not add any UIWebView code to your app and the warning after submitting to the App Store should disappear. The InAppBrowser plugin now will only use WKWebView as well, if it is installed in your app.

**Note**: Other plugins may still use UIWebView references. Please check all your plugins, if you still get the warning.