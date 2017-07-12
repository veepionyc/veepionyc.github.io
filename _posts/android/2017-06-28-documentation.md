---
layout: post
title:  VPKit_library Documentation (Android)
version: 1.2.1
category: android
---

VPKit_library is an Android SDK for generating interactive media which provides a seamless transition from a social feed to an e-commerce experience.

VPKit_library provides a VPKPreview to use in place of an ImageView. Your image is now interactive, and your team can manage the journey and gain analytical insight.

A VEEP is a metadata object defining the transition from an image or video in a social feed to an e-commerce experience or a URL.

The SDK is hosted on JCenter and MavenCentraL for installation using Gradle.

For installation help and more information: __sdk_support@veepio.com__ or use the __[VPKitDemo issue tracker](https://github.com/veepionyc/VPKitDemo_Android/issues)__



## A little more about the SDK

VPKit_library is supplied as a pre-compiled library ready for Gradle integration into your Android project. A demo app is provided  showing how to incorporate and use the SDK.

### Viewing a VEEP image
![](../assets/img/consume.jpg)

VEEPIO interactive media are identified by the Veep icon overlay in `VPKPreview` imageViews.

- Tapping the CONSUME image (a `VPKPreview`) launches the `VPKVeepViewerActivity`.
- Interactive areas of images are marked by veep track borders.
- Click on veep track to view linked web content below the media.
- Click the expand icon " ^ " to view the webview in full screen mode.
- Click "X" icon to exit full screen web view.
- Swipe the image to dismiss the `VPKVeepViewerActivy` and return to your place in the hosting app.


### Creating a VEEP image

Under development. Veep Create functions are only available on iOS at this time. 



## Integrating the framework

Integrate using Gradle. 

Add Internet permissions to your app's Manifset.xml file

     <uses-permission android:name="android.permission.INTERNET" />     


Add this line to your app's Gradle file

`compile ‘io.veep.android:vpkit_library:0.0.1’`



## VPKit demo apps


Demo apps are hosted on Github
__[github.com/veepionyc/VPKitDemo](http://www.github.com/veepionyc/VPKitDemo_Android)__

You will find detailed usage and integration notes in the [VPKDemoActivity file](https://github.com/veepionyc/VPKitDemo_Android/blob/master/VPKitDemo/vpkit_demo_view/src/main/java/io/veep/android/vpkitdemo/VPKitDemoActivity.java):



## Usage

### Initialising VPKit_library

Firstly, you'll need to introduce your application to VEEPIO. The first Activity of your app is a good location for this. A triplet of unique strings identify your app to the Veepio SDK: appID, clientID and clientSecret. To obtain these identifiers, visit the [Veepio Developer Portal](https://developer.veep.io), register an account and create an app. 

For testing purposes you can use the identifiers for the Veepio test app:

```     
        \\java
        String appId = "VEEPIO_by_url_test_app_id";
        String clientId = "1zArpBErovQ1MjVHvigJqXwE8qt47U2Yy5XzG3CP";
        String clientSecret = "VpLIvEetceUnHBEIf6fLUwLxELBh2QesZ6iLLiPHCesRLXfOLLJNcFfmp03wJfGaJquO3V8KqHjtvzlufuXfWWgcpWVw9wxfBJNYdZh96JHV5hk44dJbqiCqplrKcSml";
        VPKitApplication.setAppId(appId, clientId, clientSecret);
```



### Viewing

#### VPKPreview

The easiest way to use the VEEPIO functionality is to use a `VPKPreview` in your UI.  
- `VPKPreview` can be used in place of an ImageView, wherever you might display images with optional veep metadata.  
- It is initialized with an `imageUrl` or `veepId` string, along with the `Drawable` image.  
- It provides an animated VEEP icon to indicate that an image is interactive. The VEEP icon is only displayed if the image is initialised with a veepId, or with a URL that is associated with a veepId. Otherwise it behaves as an GroupView with contained ImageView.


```
        \\java
        VPKPreview preview = (VPKPreview)findViewById(R.id.vpk_preview2);
        String veepId= "1787";  
        preview.setVeepId(veepId);
        preview.mImageView.setImageDrawable([drawableImage]);
              
```

NB - setting the drawable content on VPKPreviews's imageView should happen _after_ setting the veepId or imageUrl - otherwise the object may not recognise it's image as containing veep'd content.



### Creating veep content

For Veep content creation, please refer to the [iOS documentation](https://veepionyc.github.io)
 
 

## Support

Veepio Developer Portal - [developer.veep.io](https://developer.veep.io)  

For installation help and more information: __sdk_support@veepio.com__   
or use the __[VPKitDemo_Android issue tracker](https://github.com/veepionyc/VPKitDemo_Android/issues)__





