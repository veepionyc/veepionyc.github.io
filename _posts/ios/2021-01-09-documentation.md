---
layout: post
title:  VPKit Documentation (iOS)
version: 2.9.x
category: ios
---

VPKit is an iOS SDK for generating interactive media which provides a seamless transition from a social feed to an e-commerce experience.

To use VPKit, we provide you with `VPKPreview`, a subclass of `UIImageView`. Your image is now interactive, and your team can manage the journey and gain analytical insight. If the image is a placeholder for a video, VPKit provides an interactive video player as a replacement for `AVPlayerViewController`

A VEEP is a metadata object providing interactive hotspots in images and video, with a built-in browser to follow those links whilst remaining inside the host app.

The SDK can be __[downloaded from our Github repository](http://www.github.com/veepionyc/VPKitDemo)__


A complete class reference is avaialble [here](https://veepionyc.github.io/reference/ios/2/9/)

For installation help: __sdk_support@veepio.com__



## About the SDK

VPKit is supplied as a pre-compiled static framework. It is ready for drag-and-drop use in your Swift or Objective-C iOS project or can be installed using Cocoapods. A demo app is provided in each language showing how to incorporate and use the SDK.

### Viewing a VEEP image
![](../assets/img/consume.jpg)

VEEPIO interactive media are identified by the Veep icon overlay in `VPKPreview` imageViews.

- Tapping the CONSUME image (a `VPKPreview`) launches the `VPKVeepViewer` view controller.
- Interactive areas of images are marked by veep track borders.
- Click on veep track to view linked web content below the media.
- Click the expand icon " ^ " to view the webview in full screen mode.
- Click "X" icon to exit full screen web view.
- Swipe the image to dismiss the `VPKVeepViewer` and return to your place in the hosting app.

### Viewing a VEEP video

VEEPIO interactive media are identified by the Veep icon overlay in `VPKPreview` imageViews.

- Tapping the CONSUME image (a `VPKPreview`) launches the `VPKVeepViewer` view controller.
- Interactive areas of videos are marked by veep track borders.
- Color bars on the video timeline indicate locations of veep tracks in the video.
- Click on veep track to view linked web content below the media.
- Click the expand icon " ^ " to view the webview in full screen mode.
- Click "X" icon to exit full screen web view.
- Swipe the image to dismiss the `VPKVeepViewer` and return to your place in the hosting app.


### Creating VEEP'd media

Refer to the __VPKitMaker SDK__  for creating VEEP meda meatadata.    
 (Forthcoming: contact us for more information and bespoke solutions)

## Integrating the framework

Integrate manually or using cocoapods. In both cases, add App Transport Security settings to your info.plist file.


### Manual integration

The pre-compiled binary with demo integrations is available [on github](http://www.github.com/veepionyc/VPKitDemo)

Drag and drop the `VPKit.framework` binary into your XCode project

**General Tab - XCode 10**  
Ensure the framework is included in _both_ "Embedded Binaries" and "Linked Frameworks and Libraries" in the general tab of your target settings.

![](../assets/img/project-general.png)

**General Tab - XCode 11+**  
Ensure the framework is included in "Frameworks, Libraries and Embedded Content" in the general tab of your target settings. Select `embed without signing`.	

![](../assets/img/xc11-project-general.png)

**Build Phases Tab**

Ensure the framework appears in both "Link Binary with Libraries" and "Embed Frameworks" sections. This should be correct if you have added the framework correctly in the General Tab. The `signing` box can be unchecked.

![](../assets/img/xc11-build-phases.png)


`VPKit.framework` is a __univerrsal static framework__ and will run in the simulator and on the device. Due to an [App Store submission bug](http://www.openradar.me/radar?id=6409498411401216), you must strip x86 (simulator) code before uploading to Apple. We provide two options to help with this exercise:

- __Device-only binary__  
The file `VPKit_framework_iphoneos.zip` is a device-only build of the framework. Replace the universal with this version before submitting to the app store.

- __Build script__   
VPKit.framework includes a script to strip non-valid binaries when building. Run it from a "Run Script" build phase, which should be positioned _after_ the "Embed Frameworks" phase.  
`bash "${BUILT_PRODUCTS_DIR}/${FRAMEWORKS_FOLDER_PATH}/VPKit.framework/strip-frameworks.sh"`  
The demo projects show the use of a build script phase.


### Cocoapods integration

Cocoapods manages builds of valid binaries for you so this is the preferred integration option.

Refer to [https://cocoapods.org/#getstarted](https://cocoapods.org/#getstarted) to get started with a Cocopods podfile.

Add this line to your podfile

`pod 'VPKit'`

Run `pod install` from the commandline



### Info.plist settings


- Add the ```App Transport Security Settings``` key to your project's info.plist, with  sub-keys:
    -   `Allow Arbitrary Loads : YES`
    -   `Allow Arbitrary Loads in Web Content : YES` 

`NSAllowsArbitraryLoadsInWebContent` is the correct key for iOS 10+; `NSAllowsArbitraryLoads` is the fallback setting for iOS 9 and is ignored if the former key is available for iOS 10.
		
	<key>NSAppTransportSecurity</key>
	<dict>
		<key>NSAllowsArbitraryLoads</key>
		<true/>
		<key>NSAllowsArbitraryLoadsInWebContent</key>
		<true/>
	</dict>
	
This will ensure the correct app permissions are set in order for the web view to appear. Apple have indicated that setting these to 'YES' will require justification when submitting to the app store - although this restriction has not been implemented yet.  

## VPKit demo apps


Demo apps are hosted on Github with pre-compiled binary VPKit Framework
__[github.com/veepionyc/VPKitDemo](http://www.github.com/veepionyc/VPKitDemo)__

You will find detailed usage and integration notes in the App Delegate and ViewController files:

### view veeps 

objective-c  
[AppDelegate.m](https://github.com/veepionyc/VPKitDemo/blob/master/demo_view_objc/VPKitDemo/AppDelegate.m)  
[ViewController.m](https://github.com/veepionyc/VPKitDemo/blob/master/demo_view_objc/VPKitDemo/ViewController.m)  

swift    
[AppDelegate.swift](https://github.com/veepionyc/VPKitDemo/blob/master/demo_view_swift/VPKitDemoSwift/AppDelegate.swift)  
[ViewController.swift](https://github.com/veepionyc/VPKitDemo/blob/master/demo_view_swift/VPKitDemoSwift/ViewController.swift)  


## Usage

### App registration

Your app will need to be registered with VEEPIO before you can create or consume VEEP metadata. This process can be completed on the [VEEPIO developer portal](https://developer.veep.io/). Each app that you create will be assigned an `appID` (name), `clientID`, `clientSecret`.


### Initialization in your App Delegate

You will need to identify your app to the VPKit SDK in order to successfully request VEEP metadata. The App Delegate is a good location for this. You will need to have first obtained your  `appID` (name), `clientID`, `clientSecret` from the the [VEEPIO developer portal](https://developer.veep.io/). For testing purposes you can use the identifiers for the Veepio test app:

```swift
//swift
let appID = "VEEPIO_test_app_id"
let clientID = "VsRIkxIfTtkFJhw1ABItnO50B6fSW23NhIRnST53"
let clientSecret = "OdWbCaP9i1I2AV2yZUzwfDFE4gU04RDX1HdubnTEg8oWw8F9yWQwjX179zHRXLUad5vrsOo5B7UtFq2utsrWbkjVus5aJKxW8wXTvDknqdgeowunL9yeEN8selNpTOJF"
        
VPKit.setApplicationId(appID,
             clientId: clientID,
         clientSecret: clientSecret)
```

```objc
//objective-c

NSString* appID = @"VEEPIO_test_app_id";
NSString* clientID = @"VsRIkxIfTtkFJhw1ABItnO50B6fSW23NhIRnST53";
NSString* clientSecret = @"OdWbCaP9i1I2AV2yZUzwfDFE4gU04RDX1HdubnTEg8oWw8F9yWQwjX179zHRXLUad5vrsOo5B7UtFq2utsrWbkjVus5aJKxW8wXTvDknqdgeowunL9yeEN8selNpTOJF";
	    
[VPKit setApplicationId:appID
               clientId:clientID
           clientSecret:clientSecret];
```

Other settings to consider at initialization:

#### Production status

```swift  
//swift  
VPKit.setProduction(_:Bool)  
```
```objc  
//objective-c
[VPKit setProduction:(BOOL)]  
```

Production ON - your live production database: use for publishing  
Production OFF - your sandbox database: use for testing and development without polluting your live data.

#### IDFA support - optional
     
(optional) send IDFA for Veep tracking
     
This requires host app linking to `AdSupport.framework` ("link binary with libarires" section of project Build Phases)
     
Setting this option to YES entails [additional reporting requirements when submitting to the app store](https://developer.apple.com/library/content/documentation/LanguagesUtilities/Conceptual/iTunesConnect_Guide/Chapters/SubmittingTheApp.html#//apple_ref/doc/uid/TP40011225-CH33-SW8)
     
     
```swift  
//swift  
VPKit.sendIDFA(_:Bool)  
```
```objc  
//objective-c
[VPKit sendIDFA:(BOOL)]  
```


#### UI styling - optional

This is also a good place to add any custom fonts and colours to the veep viewer. Examples in the demo apps:

```swift
//swift
VPKit.styles().margin = 12
VPKit.styles().color.navBar = UIColor.init(white: 0.1, alpha: 1.0)
VPKit.styles().font.navBarFont = UIFont .systemFont(ofSize: 18, weight: UIFontWeightHeavy);
VPKit.styles().font.cellNavBarFont = UIFont .systemFont(ofSize: 14, weight: UIFontWeightBold);
```

```objc
//objecive-C
[VPKit styles].margin = 12;
VPKit.styles.color.navBar = [UIColor colorWithWhite:0.1 alpha:1.0];
VPKit.styles.font.navBarFont = [UIFont systemFontOfSize:18 weight:UIFontWeightHeavy];
VPKit.styles.font.cellNavBarFont = [UIFont systemFontOfSize:14 weight:UIFontWeightBold];
```

See `VPKStyles` in our [SDK reference](https://veepionyc.github.io/reference/ios/2/8/) for all available properties

### Viewing

#### VPKPreview

The easiest way to use the VEEPIO functionality is to use a `VPKPreview` in your UI.  
- `VPKPreview` is a drop-in replacement subclass of `UIImageView`.  
- It is initialized with a `VPKImage` - which is a `UIImage` subclass with optional `Veep` identifier properties.  
- It provides a VEEP icon overlay to indicate that an image is interactive.


```objc
//objective-C
self.vpkPreview = [[VPKPreview alloc] init];
[self.view addSubview:self.vpkPreview];
UIImage* image = [UIImage imageNamed:@"KrispyGlas"];
image = [[VPKImage alloc] initWithImage:image veepID:@"658"];
self.vpkPreview.image = image;
```

```swift
//swift
let preview = VPKPreview()
guard let image = UIImage.init(named: "KrispyGlas") else {return}
let previewImage: VPKImage = VPKImage(image: image, veepID:"658")
self.preview.image = previewImage;
self.view.addSubview(self.preview)
```

#### VPKPreview pass-through delegate

VPKPreview handles presenting and dismissing of its viewer controllers, and it also has an optional **pass-through delegate** if your app needs user interaction feedback.

`id <VPKPreviewPassThroughDelegate> passThroughDelegate`

Set the `passThroughDelegate`:  
- if your host app needs to handle tap gestures on the VPKPreview when the preview object has nothing to do (when there is no associated veep content with the view).  
- if your host app needs to handle additional tap gesture behaviour when the preview object launches a `VeepViewer` in response to veep content.  

There are two `passThroughDelegate` methods. Their purpose is to forward the tapGestureRecognizer when taps are received.

```objc
//objective-C
-vpkPreview:(VPKPreview*)preview 
              passedThroughTap:(UITapGestureRecognizer*)tapGestureRecognizer
```

```swift
//swift
public func vpkPreview(_ preview: VPKPreview, 
              passedThroughTap tapGestureRecognizer: UITapGestureRecognizer)
```  
Sent if a users taps on a VPKPreview and there is no veep content associated with it. 


```objc
//objective-C
-vpkPreview:(VPKPreview*)preview 
              handledTap:(UITapGestureRecognizer*)tapGestureRecognizer
```

```swift
//swift
public func vpkPreview(_ preview: VPKPreview, 
              handledTap tapGestureRecognizer: UITapGestureRecognizer)
```  
Sent if the user taps on veep content, and the VPKPreview will launch a `VeepViewer`, but the host app needs to augment the tap behaviour.

The VPKPreview also exposes a `UITouchGestureRecognizer` as a read-only property for more fine-grained control


#### VPKPreviewDelegate (deprecated)

If the `delegate` property is set on `VPKPreview` the host app is responsible for presenting and dismissing the `VeepViewer`. This is not recommended and the property is deprecated. See earlier versions of this tutorial for more information.


### Creating veep content

Refer to the separate **VPKitMaker SDK** for creating Veep Content. The SDK will be available for public download soon. Please contact us for more information and bespoke solutions.
 
 
### Customization

All UI in VPKit is customizable to fit in with your app UI design.

The following example makes the navigation bar red:

```swift
//swift
VPKit.styles().color.navbar = UIColor.red()
```

```objc
//objective-c
VPKit.styles.color.navbar = [UIColor red]
```

See `VPKStyles` in our [SDK reference](https://veepionyc.github.io/reference/ios/2/8/) for all available properties


## Event notifications
A number of event messages are available to intercept as `NSNotification` objects. For details refer to:

[VPKPublicEventConstants](https://github.com/veepionyc/VPKitDemo/blob/2.8.1/VPKit.framework/Headers/VPKPublicEventConstants.h)  

The notification objects include a `userInfo` dictionary with a single `VPKIdentifierKey` entry. If a [`mediaIdentifier`](#vpkimage--uiimage) string is set on the `VPKPreview's` [`VPKImage`](#vpkimage--uiimage), this will be returned as the value. The identifier may aid in ensuring that the correct media events are handled.

## Reference

A complete class reference is avaialble [here](https://veepionyc.github.io/reference/ios/2/9/).


## Support


For installation help and more information: __sdk_support@veepio.com__ 




