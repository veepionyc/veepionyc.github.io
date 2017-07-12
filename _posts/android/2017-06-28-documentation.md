---
layout: post
title:  VPKit Documentation (Android)
version: 1.2.+
category: android
---

VPKit_library is an Android SDK for generating interactive media which provides a seamless transition from a social feed to an e-commerce experience.

VPKit_library provides a VPKPreview to use in place of an ImageView. Your image is now interactive, and your team can manage the journey and gain analytical insight.

A VEEP is a metadata object defining the transition from an image or video in a social feed to an e-commerce experience or a URL.

The SDK is hosted on JCenter and MavenCentraL for installation using Gradle.

For installation help and more information: __sdk_support@veepio.com__ or use the __[VPKitDemo issue tracker](https://github.com/veepionyc/VPKitDemo_Android/issues)__



## A little more about the SDK

VPKit_library is supplied as a pre-compiled library ready for Gradle integration into your Android project. A [demo app](https://github.com/veepionyc/VPKitDemo_Android) is provided  showing how to incorporate and use the SDK.

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



# Quick-start 15 minute integration guide
reading time: 5 minutes  
integration time: 15 minutes  


## Integrating the framework using Gradle

### Project Gradle file

Enable jCenter in the `allprojects` section of the project Gradle file

    allprojects {
	    repositories {
	        jcenter()
    }



### App Gradle file

Add the vpkit_library to the `dependencies` section of the app Gradle file

    dependencies {  
        compile ‘io.veep.android:vpkit_library:1.2.+’
    }

### App Manifest file

Add Internet permissions to the top level `<manifest>` section of the app manifest file

    <manifest ...>  
         <uses-permission android:name="android.permission.INTERNET" />  
         
     </manifest   


## VPKit demo apps


Demo apps are hosted on Github  
__[github.com/veepionyc/VPKitDemo](http://www.github.com/veepionyc/VPKitDemo_Android)__

You will find detailed usage and integration notes in the [VPKDemoActivity file](https://github.com/veepionyc/VPKitDemo_Android/blob/master/VPKitDemo/vpkit_demo_view/src/main/java/io/veep/android/vpkitdemo/VPKitDemoActivity.java):



## Usage

### Initialising: VPKitApplication

    import io.veep.android.vpkit_library.VPKitApplication;


Firstly, you'll need to introduce your application to VEEPIO. The first Activity of your app is a good location for this. A triplet of unique strings identify your app to the Veepio SDK: appID, clientID and clientSecret. To obtain these identifiers, visit the [Veepio Developer Portal](https://developer.veep.io), register an account and create an app. 

For testing purposes you can use the identifiers for the Veepio test app:

```     
        //java
        String appId = "VEEPIO_by_url_test_app_id";
        String clientId = "1zArpBErovQ1MjVHvigJqXwE8qt47U2Yy5XzG3CP";
        String clientSecret = "VpLIvEetceUnHBEIf6fLUwLxELBh2QesZ6iLLiPHCesRLXfOLLJNcFfmp03wJfGaJquO3V8KqHjtvzlufuXfWWgcpWVw9wxfBJNYdZh96JHV5hk44dJbqiCqplrKcSml";
        VPKitApplication.setAppId(appId, clientId, clientSecret);
```

The credentials must be set before initialising an instance of `VPKPreview`


### Viewing: VPKPreview

    import io.veep.android.vpkit_library.CustomViews.VPKPreview;


The easiest way to use the VEEPIO functionality is to use a `VPKPreview` in your UI.  

- `VPKPreview` can be used in place of an ImageView, wherever you might display images with optional veep metadata. 

- Create a layout file with a VPKPreview. Follow a similar format to that of an ImageView, but change the type


        //xml
        
         //if this is your ImageView layout ...
         
         <ImageView
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:adjustViewBounds="true"
            android:scaleType="centerCrop"
            android:id="@+id/image_id_1"
            />
        
        //change the type to VPKPreview ...
        
         <io.veep.android.vpkit_library.CustomViews.VPKPreview
           ...
            />
            
 
- In the associated Activity or Fragment, include requisite vpkit_library objects:    
 
			import io.veep.android.vpkit_library.CustomViews.VPKPreview;


the VPKPreview is initialized with an `imageUrl` or `veepId` string, along with the `Drawable` image.  

   
If you are accessing and using an ImageView thus:
        
        //java
        
         Drawable image =  getResources().getDrawable(R.drawable.viewwithurl);
         ImageView imageView = (ImageView) findViewById(R.id.image_id_1);
         imageView.setImageDrawable(image); 
         
You would use a replacement VPKPreview in this way:

        //java
        
        VPKPreview preview = (VPKPreview)findViewById(R.id.image_id_1);
        String veepId= "1787";  
        preview.setVeepId(veepId);
        preview.mImageView.setImageDrawable(image);
        
Or, using a URL instead of a veepId:

        VPKPreview preview = (VPKPreview)findViewById(R.id.image_id_1);
        String imageUrl= <ImageUrl>;  
        preview.setVImageUrl(imageUrl);
        preview.mImageView.setImageDrawable(image);
              

- If an image is shown which has veep metadata a VEEP icon is displayed. The VEEP icon is only displayed if the image is initialised with a veepId, or with a URL that is associated with a veepId. Otherwise it behaves as a regular GroupView with contained ImageView.

- A veep-enabled VPKPreview will launch the Veep Viewer in response to a user touch event.


NB - setting the drawable content on VPKPreviews's imageView should happen _after_ setting the veepId or imageUrl - otherwise the object may not recognise it's image as containing veep'd content.



### Creating veep content

For Veep content creation, please refer to the [iOS documentation](https://veepionyc.github.io)
 
 

## Support

Veepio Developer Portal - [developer.veep.io](https://developer.veep.io)  

For installation help and more information: __sdk_support@veepio.com__   
or use the __[VPKitDemo_Android issue tracker](https://github.com/veepionyc/VPKitDemo_Android/issues)__





