---
layout: post
title:  VPKit Documentation (iOS)
version: 2.6.0+
category: ios
---

VPKit is an iOS SDK for generating interactive media which provides a seamless transition from a social feed to an e-commerce experience.

To use VPKit, you might decide to replace a `UIImageView` with a `VPKPreview`. Your image is now interactive, and your team can manage the journey and gain analytical insight. If the image is a placeholder for a video, VPKit provides an interactive video player as a replacement for `AVPlayerViewController`

A VEEP is a metadata object defining the transition from an image or video in a social feed to an e-commerce experience or a URL.

The SDK can be __[downloaded from our Github repository](http://www.github.com/veepionyc/VPKitDemo)__

For installation help and more information: __sdk_support@veepio.com__ or use the __[VPKitDemo issue tracker](https://github.com/veepionyc/VPKitDemo/issues)__



## A little more about the SDK

VPKit is supplied as a pre-compiled dynamic framework ready for drag-and-drop use in your Swift or Objective-C iOS project. A demo app is provided in each language showing how to incorporate and use the SDK.

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


### Creating a VEEP image

<!--![](../assets/img/add_veep.png)-->
![](../assets/img/create.jpg)

The demo app includes a CREATE image to show how veep content is originated.

- Tapping the CREATE image launches the `VPKVeepEditor` view controller.
- The user may add veep tracks by tapping an area of interest in the image.
- Each track can be moved and reshaped by manipulating its bounding box.
- Each track can also be associated with a URL using the Google and Amazon search pages.
- After defining one or more  veep tracks, the user can publish the veep.
- This will send the Veep metadata to Veepio's hosting servers and return a VeepID for you to store in your app.

The VEEP metadata can in turn be consumed using a `VPKPreview` object as mentioned above.

### Creating a VEEP video
Video create is not yet avaialable via the VPKit public SDK but is on the roadmap for future release.

## Integrating the framework

Integrate manually or using cocoapods. In both cases, add App Transport Security settings to your info.plist file.


### Manual integration

The pre-compiled binary with demo integrations is available [on github](http://www.github.com/veepionyc/VPKitDemo)

Drag and drop the `VPKit.framework` binary into your XCode project

Ensure the framework is included in "Embedded Binaries" and "Linked Frameworks and Libraries" in the general tab of your target settings.

![](../assets/img/project-general.png)


`VPKit.framework` is a __univerrsal dynamic framework__ and will run in the simulator and on the device. Due to an [App Store submission bug](http://www.openradar.me/radar?id=6409498411401216), you must strip x86 (simulator) code before uploading to Apple. We provide two options to help with this exercise:

- __Device-only binary__  
The file `VPKit_framework_iphoneos.zip` is a device-only build of the framework. Replace the universal with this version before submitting to the app store.

- __Build script__   
VPKit.framework includes a script to strip non-valid binaries when building. Run it from a "Run Script" build phase, which should be positioned _after_ the "Embed Frameworks" phase.  
`bash "${BUILT_PRODUCTS_DIR}/${FRAMEWORKS_FOLDER_PATH}/VPKit.framework/strip-frameworks.sh"`


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

`NSAllowsArbitraryLoadsInWebContent` is the correct key for iOS 10; `NSAllowsArbitraryLoads` is the fallback setting for iOS 9 and is ignored if the former key is available for iOS 10.
		
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

### create veeps 

objective-c  
[AppDelegate.m](https://github.com/veepionyc/VPKitDemo/blob/master/demo_create_objc/VPKitDemo/AppDelegate.m)  
[ViewController.m](https://github.com/veepionyc/VPKitDemo/blob/master/demo_create_objc/VPKitDemo/ViewController.m)  

swift    
[AppDelegate.swift](https://github.com/veepionyc/VPKitDemo/blob/master/demo_create_swift/VPKitDemoSwift/AppDelegate.swift)  
[ViewController.swift](https://github.com/veepionyc/VPKitDemo/blob/master/demo_create_swift/VPKitDemoSwift/ViewController.swift)  


## Usage

### Initialization in your App Delegate

Firstly, you'll need to introduce your application to VEEPIO. The App Delegate is a good location for this. A triplet of unique strings identify your app to the Veepio SDK: appID, clientID and clientSecret. To obtain these identifiers, contact skd_support@veepio.com. 

For testing purposes you can use the identifiers for the Veepio test app:

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
           clientSecret:clientSecret];*------/
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
Production OFF - your sandbox database: use for development  

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

### Viewing

#### VPKPreview

The easiest way to use the VEEPIO functionality is to use a `VPKPreview` in your UI.
- `VPKPreview` is a drop-in replacement for a `UIImageView`.
- It is initialized with a `VPKImage` - which is a `UIImage` subclass with added `VeepID` property.
- It provides an animated VEEP icon to indicate that an image is interactive.


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

#### VPKPreview delegates

VPKPreview has two optional delegates. If neither of these delegates is set, the VPKPreview object will handle presenting and dismissing the SDK view controllers. _Only set these delegates if your host app requires more control_.

#### `id <VPKPreviewPassThroughDelegate> passThroughDelegate`

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


#### `id <VPKPreviewDelegate> delegate`

When this delegate is set, the host app is responsible for the entire process of presenting and dismissing the VPKVeepViewer and (or) VPKVeepEditor View Controllers as described below. __The host app only needs to implement `VPKVeepViewer` and `VPKVeepEditor` handling code if this delegate is set.__




#### VPKVeepViewer

The `VPKVeepViewer` view Controller is initialized with a `VPKImage` and its associated `VPKPreview`.
These methods are delegate callbacks from the VPKPreview on receiving a use touch event:

```swift
//swift
func vpkPreviewTouched(_ preview:VPKPreview, image:VPKImage){
	guard let viewer = VPKit.viewer(with: image, from: preview) else {return}
    viewer.delegate = self
    viewer.modalPresentationStyle = UIModalPresentationStyle.overFullScreen
    preview.hideIcon()
    self.present(viewer, animated: true, completion: nil)
}
```

```objc
//objective-c
- (void)vpkPreviewTouched:(VPKPreview *)preview image:(VPKImage*)image {
    self.vpViewer = [VPKit viewerWithImage:image
                                  fromView:preview];
    self.vpViewer.delegate = self;
    self.vpViewer.modalPresentationStyle = UIModalPresentationOverFullScreen;
    [preview hideIcon];
    [self presentViewController:self.vpViewer animated:YES completion:nil];
}
```

(NB: If you don't set a delegate on VPKPreview, these methods can be omitted and similar behaviour is provided by default from the VPKPreview object itself)



### Creating veep content

If you want to allow your users to VEEP their own user generated content from within your app, you can open the VEEP editor:

```swift
//swift
guard let vpEditor = VPKit.editor(with: image, from: self.imageButton) else {return}
vpEditor.useVeepLogo = false
vpEditor.delegate = self
vpEditor.modalPresentationStyle = UIModalPresentationStyle.overFullScreen
self.present(vpEditor, animated: true, completion: nil)
```
  
```objc
//objective-C
self.vpEditor = [VPKit editorWithImage:self.imageButton.image
                              fromView:self.imageButton];
self.vpEditor.useVeepLogo = NO;
if (self.vpEditor) {
    self.vpEditor.delegate = self;
    self.vpEditor.modalPresentationStyle = UIModalPresentationOverFullScreen;
    [self presentViewController:self.vpEditor animated:YES completion:nil];
}
```
 
 
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

##Event notifications
A number of event messages are available to intercept as `NSNotification` objects. For details refer to:

[VPKPublicEventConstants](https://github.com/veepionyc/VPKitDemo/blob/2.6.0/VPKit.framework/Headers/VPKPublicEventConstants.h)  

The notification objects include a `userInfo` dictionary with a single `VPKIdentifierKey` entry. If a [`mediaIdentifier`](#vpkimage--uiimage) string is set on the `VPKPreview's` [`VPKImage`](#vpkimage--uiimage), this will be returned as the value. The identifier may aid in ensuring that the correct media events are handled.

## Reference

#### VPKImage : UIImage

    @property (nonatomic, strong, nullable) NSString *mediaIdentifier
    
`mediaIdentifier` is a courtesy property that the host app can use for tracking purposes (see [Event Notifications](./documentation#event-notifications)).

    @property (nonnull, nonatomic, strong, readonly) NSString* veepId;

    - (nonnull instancetype)initWithImage:(nonnull UIImage*)image
                                   veepID:(nullable NSString*)veepId;
                                   
    - (nonnull instancetype)initWithImage:(nonnull UIImage*)image
                                   url:(nullable NSURL*)imageURL;
                                   

If `VPKImage` is initialised with null veepId or imageURL it will behave as a standard UIImage



#### VPKPreview : UIImage

#### VPKPublicVeep : NSObject

    @property (nonnull, nonatomic, strong) NSString* veepID;
    @property (nullable, nonatomic, strong) NSString* title;
    @property (nullable, nonatomic, strong) NSString* descriptionString;
    @property (nullable, nonatomic, strong) NSURL* originalContentURI;

## VPKitClass methods

#### Initializing VPKit

    + (void)setApplicationId:(nonnull NSString*)appId
                clientId:(nullable NSString*)clientId
                  clientSecret:(nullable NSString*)secret;

<!--#### User identification

    + (void)setEmail:(nullable NSString*)email;-->

#### Consume Veep'd content

    + (nullable VPKVeepViewer*)viewerWithImage:(VPKImage*)image
                                      fromView:(UIView*)fromView
   

#### Create Veep'd content

    + (nullable VPKVeepEditor*)editorWithImage:(UIImage*)image
                                      fromView:(UIView*)fromView`

#### Fetch a VPKPublicVeep

    + (void) requestVeep:(NSString*)veepID
        completionBlock:^(VPKPublicVeep* _Nullable veep,
                          NSError* _Nullable error) completion;

## Controlling appearance

#### VPKStyles

    @property (nonatomic, assign) CGFloat lineWidth;
    @property (nonatomic, assign) CGFloat margin;

#### VPKFontStyles

	@property (nonatomic, strong) UIFont* barButtonItemFontDisabled;
	@property (nonatomic, strong) UIFont* barButtonItemFontEnabled;
	@property (nonatomic, strong) UIFont* barButtonItemFont;
	@property (nonatomic, strong) UIFont* navBarFont;
	@property (nonatomic, strong) UIFont* cellNavBarFont;
	@property (nonatomic, strong) UIFont* cellLabelFont;
	@property (nonatomic, strong) UIFont* cellTextViewFont;
	@property (nonatomic, strong) UIFont* bigLabelFont;


#### VPKColorStyles

	@property (nonatomic, strong) UIColor* navBar;
	@property (nonatomic, strong) UIColor* navBarText;

	@property (nonatomic, strong) UIColor* navBarLight;
	@property (nonatomic, strong) UIColor* navBarDark;
	@property (nonatomic, strong) UIColor* cellNavBar;
	@property (nonatomic, strong) UIColor* cellMidGrey;


## Support


For installation help and more information: __sdk_support@veepio.com__ or use the __[VPKitDemo issue tracker](https://github.com/veepionyc/VPKitDemo/issues)__





