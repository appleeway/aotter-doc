# Installation

Follow these steps to download and include SDK in your project:

Step 1: [Download AotterTrek SDK](installation.md#step-1-download-aottertrek-sdk)\
Step 2: [Initiation & Settings](installation.md#step-2-initialzation-and-settings)

### Step 1: Download AotterTrek SDK

#### - Using Cocoapods

1\.  Add the following line to your project's Podfile:

```swift
pod 'AotterTrek-iOS-SDK', '3.7.7'
```

2\.  Run `pod install`&#x20;

#### - Manually Install

1\. Pull & drag AotterTrek-iOS-SDK to your project\
2\. Link AotterTrek-iOS-SDK (if it's not auto-linked)\
3\. Add linked frameworks and libraries to your target (See the table below)\
4\. Install [Google-IMA-iOS-SDK](https://developers.google.com/interactive-media-ads/docs/sdks/ios/)

| Frameworks and Libraries |                     |               |
| ------------------------ | ------------------- | ------------- |
| CoreMedia                | SystemConfiguration | CoreTelephony |
| WebKit                   | CoreTelephony       | AdSupport     |
| AVKit                    | AVFoundation        | Foundation    |
| UIKit                    |                     |               |

### Step 2: Initialzation & Settings

Please use **your client id** for initialization which can be found in the [application list](https://trek.aotter.net/publisher/list/app).&#x20;

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

### Test ad units

We also provide test client id and test place id for receiving test ads only.

{% hint style="info" %}
* Test Client ID **:**&#x20;
  * **21tgwWwuzFYiD4ko5Klr**
* Test Client Secret:
  * **fD8P20gzWYrlbuwWklRkicYcNwlWZSZwV+iHj3TzGSzzyfgTWmVR5trs5F1Dp+x9tX2jxq44**
* Test Place ID **:**&#x20;
  * Native Ad : **bc47b614-7b24-4eb1-aae2-65e8de8e96de**
  * Supr.Ad : **669bad6a-27ec-487a-a583-7b5305732ff7**
  * Banner Ad **: adcb5212-0453-4594-932a-104be11e521a**
{% endhint %}

### Optional

**- Logger**

Enable logger if you needed. There are three different levels of logger:

* `TKLoggerLevelNone`: No log will be shown.
* `TKLoggerLevelNormal`: Necessary logs or warning/error logs will be shown.
* `TKLoggerLevelDetail`: All logs will be shown. ( **include verbose logs** )

\- **Audio Session**

When executing Supr.Ad, a multimedia ad, you might receive video ads. You might not like the audio of the video ad to intervene in your user's background music. Moreover, If your app combines various audio playing conditions, it is recommended to choose [the category](https://developer.apple.com/documentation/avfaudio/avaudiosessioncategory) that most accurately describes the audio behavior you want.&#x20;

In the code snippet above, we choose `AVAudioSessionCategoryAmbient` which means audio from other apps mixes with audio from ads.

## Next Steps

* Follow our guides for integrating different Ad Formats in your app:
  * [Native Ad](../ad-formats/banner-ad.md)
  * [Supr.Ad](../ad-formats/supr.ad.md)
  * [Banner Ad](../ad-formats/banner-ad.md)
* Or you would like to check out the demo app:
  * [Demo](demo-working.md)
