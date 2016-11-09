---
layout: post
title:  Styles at a glance
category: jekyll 
---
# VPKit documentation

VPKit is an iOS SDK for generating interactive media which provides a seamless transition from a social feed to an e-commerce experience.

To use VPKit, you might decide to replace an UIImage with a VPKPreview. Your image is now interactive, and your team can manage the journey and gain analytical insight.

A VEEP is a metadata object defining the transition from an image or video in a social feed to an e-commerce experience or a URL.


## Installation with Binary

1. Drag and drop the binary blob into your XCode project
2. Ensure that you have the ```App Transport Security Settings``` key your project's Custom iOS Target Properties. This should be a dictionary with a key: ```Allow Arbitrary Loads``` set to ```YES``` This will ensure the correct app permissions are set in order for the web view to appear.

```xml
 <key>NSAppTransportSecurity</key>
    <dict>
        <key>NSAllowsArbitraryLoads</key>
        <true/>
    </dict> 
```
3. Follow the usage instructions below

    
## Usage

### Initialization

Firstly, you'll need to introduce your application to VEEPIO

```swift
VPKit.setApplicationIdentifier("Veepio-iOS")
```

```objective-c
[VPKit setApplicationIdentifier appID:@"Veepio-iOS"]
```

Next, you'll need to assign a unique identifier for your users. This might be a random string, or an ???advertising id???, or a username or an email address.

### Viewing
The easiest way to use the VEEPIO functionality is to use a `VPKPreview` in your UI. `VPKPreview` is a drop-in replacement for an `UIImage` that accepts an extra argument `veepID` on initialization. The SDK provides functionality for creating a VEEP, but we've also created a test image and a test VEEP. The app developer may typically store the VEEP id in their database.

```swift
imageView.image = VPKImage(image: foo, veepID: 1234)
```

```objc
imageView.image = [VPKImage initWithImage image:foo image, veepID: 1234)
```

### Manual VEEP viewer instantiation
The `VPKImage` class is necessary to measure the proportion of users who view tap an image having seen it. However, if you don't need this important engagement metric, you can open the VEEP viewer manually.

```swift
VPKVeepViewer(image, view)
```

```objc
??? [VPKVeepViewer viewerWithImage image:image view:view]
```

###User generated content
If you want to allow your users to VEEP their own user generated content from within your app, you can open the VEEP editor:

```swift
VPKVeepEditor(image, view)
```

```objc
??? [VPKVeepEditor viewerWithImage image:image view:view]
```

###Customization

All UI in VPKit is customizable to fit in with your app UI design. The following example makes the navigation bar red:

```swift
    VPKColorStyles.navBar = UIColor.red()
```

```objc
    VPKColorStyles.navBar = [UIColor red]
```

## Reference

#### VPKImage

    @property (nonnull, nonatomic, strong, readonly) NSString* veepID;
 
    - (nonnull instancetype)initWithImage:(nonnull UIImage*)image   
                                   veepID:(nonnull NSString*)veepID;
`

#### VPKPublicVeep

    @property (nonnull, nonatomic, strong) NSString* veepID;
    @property (nullable, nonatomic, strong) NSString* title;
    @property (nullable, nonatomic, strong) NSString* descriptionString;
    @property (nullable, nonatomic, strong) NSURL* originalContentURI;
    
## VPKitClass methods

#### Initialising VPKit

    + (void)setApplicationIdentifier:(nonnull NSString*)appID;
    
#### User identification

    + (void)setEmail:(nullable NSString*)email;
	
#### Consume Veep'd content

    + (nullable VPKVeepViewer*)viewerWithImage:(VPKImage*)image 
                                      fromView:(UIView*)view

#### Create Veep'd content

    + (nullable VPKVeepEditor*)editorWithImage:(UIImage*)image 
                                      fromView:(UIView*)view`
                                      
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

	@property (nonatomic, strong) UIColor* navBar; //used
	@property (nonatomic, strong) UIColor* navBarText;
	
	@property (nonatomic, strong) UIColor* navBarLight; //used
	@property (nonatomic, strong) UIColor* navBarDark; //used
	@property (nonatomic, strong) UIColor* cellNavBar; //used
	@property (nonatomic, strong) UIColor* cellMidGrey; //used
	
	@property (nonatomic, strong) UIColor* searchBar;
	@property (nonatomic, strong) UIColor* alert;
	@property (nonatomic, strong) UIColor* on;
	@property (nonatomic, strong) UIColor* off;

          



### Common Problems

#### WebView not loading
Ensure that you have the ```App Transport Security Settings``` key your project's Custom iOS Target Properties. This should be a dictionary with a key: ```Allow Arbitrary Loads``` set to ```YES``` This will ensure the correct app permissions are set in order for the web view to appear.

```xml
 <key>NSAppTransportSecurity</key>
    <dict>
        <key>NSAllowsArbitraryLoads</key>
        <true/>
    </dict> 
```
                                  
   