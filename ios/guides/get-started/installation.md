---
description: Follow these steps to download and include SDK in your project
---

# Installation

#### **Step 1 :** [**Download & Install AotterTrek SDK**](installation.md#step-1-download-and-install-aottertrek-sdk)

#### **Step 2 :** [**Import AotterTrek SDK**](installation.md#step-2-import-aottertrek-sdk)

#### **Step 3 :** [**Initiation & Settings AotterTrek SDK**](installation.md#step-3-initialzation-and-settings-aottertrek-sdk)



### [Step 1 : Download & Install AotterTrek SDK](installation.md#step-1-download-and-install-aottertrek-sdk)

#### - Using Cocoapods

1\.  Add the following line to your project's Podfile:

```swift
pod 'AotterTrek-iOS-SDK', '3.9.0'
```

2\.  Run `pod install`&#x20;

#### - Manually Install

[Download the latest SDK](https://github.com/aotter/AotterTrek-iOS-SDK/releases)

1\. Pull & drag AotterTrek-iOS-SDK to your project\
2\. Link AotterTrek-iOS-SDK (if it's not auto-linked)\
3\. Add linked frameworks and libraries to your target (See the table below)

<table data-header-hidden><thead><tr><th width="261">Frameworks and Libraries</th><th></th><th></th></tr></thead><tbody><tr><td>Frameworks and Libraries</td><td></td><td></td></tr><tr><td>CoreMedia</td><td>SystemConfiguration</td><td>CoreTelephony</td></tr><tr><td>WebKit</td><td>CoreTelephony</td><td>AdSupport</td></tr><tr><td>AVKit</td><td>AVFoundation</td><td>Foundation</td></tr><tr><td>UIKit</td><td></td><td></td></tr></tbody></table>

### [Step 2 : **Import AotterTrek SDK**](installation.md#step-2-import-aottertrek-sdk)

* **Objective-C :**&#x20;

```
// import header
#import <AotterTrek-iOS-SDK/AotterTrek-iOS-SDK.h>
```

* **Swift :**&#x20;

Add header.h as [Objective-C bridging header](https://developer.apple.com/documentation/swift/importing-objective-c-into-swift)

```
// import header in "YourTargetName-Bridging-Header.h"
#import <AotterTrek-iOS-SDK/AotterTrek-iOS-SDK.h>
```

### [Step 3 : Initialzation & Settings AotterTrek SDK](installation.md#step-3-initiation-and-settings-aottertrek-sdk)

Please use **your client id** for initialization which can be found in the [application list](https://trek.aotter.net/publisher/list/app).&#x20;

{% tabs %}
{% tab title="Objective-C " %}
```objectivec
// AppDelegate.m
#import <AotterTrek-iOS-SDK/AotterTrek-iOS-SDK.h>

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
  //required
  [[AotterTrek sharedAPI] initTrekServiceWithClientId:@"<client id>"
                                               secret:@"<client secret>"];
  
  //optional (Logger)
  [[AotterTrek sharedAPI] enableLoggerWithLevel:TKLoggerLevelDetail];

  
  //Optional (Audio Session)
   [[AVAudioSession sharedInstance]setCategory:AVAudioSessionCategoryAmbient error:nil];
  
  
  return YES;
}
```
{% endtab %}

{% tab title="Swift" %}
```swift
//add Header.h as Objective-C bridging Header
//reference: https://developer.apple.com/documentation/swift/importing-objective-c-into-swift
#import <AotterTrek-iOS-SDK/AotterTrek-iOS-SDK.h>


//AppDelegate
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    //Required
    AotterTrek.sharedAPI().initTrekService(withClientId: "<client id", secret: "<client secret>")
    
    //Optional
    AotterTrek.sharedAPI().enableLogger(with: TKLoggerLevelDetail)
    
    //Optional
    AVAudioSession.sharedInstance().setCategory(.ambient)
    
    return true
}
```
{% endtab %}
{% endtabs %}
