---
description: Follow these steps to download and include SDK in your project
---

# Installation

**Step 1 :** [**Download & Install AotterTrek SDK**](installation.md#step-1-download-and-install-aottertrek-sdk)****

**Step 2 :** [**Import AotterTrek SDK**](installation.md#step-2-import-aottertrek-sdk)****

**Step 3 :** [**Initiation & Settings AotterTrek SDK**](installation.md#step-3-initialzation-and-settings-aottertrek-sdk)****

****

### [Step 1 : Download & Install AotterTrek SDK](../../sdk-integration/installation.md)

#### - Using Cocoapods

1\.  Add the following line to your project's Podfile:

```swift
pod 'AotterTrek-iOS-SDK', '3.8.5'
```

2\.  Run `pod install`&#x20;

#### - Manually Install

[Download the latest SDK](https://github.com/aotter/AotterTrek-iOS-SDK/releases)

1\. Pull & drag AotterTrek-iOS-SDK to your project\
2\. Link AotterTrek-iOS-SDK (if it's not auto-linked)\
3\. Add linked frameworks and libraries to your target (See the table below)

| Frameworks and Libraries |                     |               |
| ------------------------ | ------------------- | ------------- |
| CoreMedia                | SystemConfiguration | CoreTelephony |
| WebKit                   | CoreTelephony       | AdSupport     |
| AVKit                    | AVFoundation        | Foundation    |
| UIKit                    |                     |               |

### [Step 2 : **Import AotterTrek SDK**](../../sdk-integration/installation.md)****

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

### [Step 3 : Initialzation & Settings AotterTrek SDK](../../sdk-integration/installation.md)

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

## Next Steps

* Follow our guides for integrating different Ad Formats in your app:
  * [Native Ad](../../ad-formats/banner-ad.md)
  * [Supr.Ad](../../ad-formats/supr.ad.md)
  * [Banner Ad](../../ad-formats/banner-ad.md)
* Or you would like to check out the demo app:
  * [Demo](../../sdk-integration/demo-working.md)
