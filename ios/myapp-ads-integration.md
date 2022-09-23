# MyApp Ads Integration

## Prerequisites

* Minimum iOS version: 9.0
* MyApp ads support SDK 3.1 and later.

## Download AotterTrek SDK

**- Using Cocoapods**

&#x20;    1\. Add the following line to your project's Podfile:

```objectivec
//Podfile
pod 'AotterTrek-iOS-SDK', '~> 3.1'
```

&#x20;   2\. Run `pod install`

#### - Manually install

&#x20;   1\. Pull & drag AotterTrek-iOS-SDK to your project\
&#x20;   2\. Link AotterTrek-iOS-SDK (if it's not auto-linked)\
&#x20;   3\. Add linked frameworks and libraries to your target (See the table below)\
&#x20;   4\. Install [Google-IMA-iOS-SDK](https://developers.google.com/interactive-media-ads/docs/sdks/ios/)

|   | Frameworks and Libraries |                     |               |
| - | ------------------------ | ------------------- | ------------- |
|   | CoreMedia                | SystemConfiguration | CoreTelephony |
|   | WebKit                   | CoreTelephony       | AdSupport     |
|   | AVKit                    | AVFoundation        | Foundation    |
|   | UIKit                    |                     |               |

## Initiation & Settings <a href="#initial-sdk" id="initial-sdk"></a>

Initial MyApp Service in _AppDelegate.m_

{% tabs %}
{% tab title="ObjC" %}
```objectivec
// AppDelegate.m
#import <AotterTrek-iOS-SDK/AotterTrek-iOS-SDK.h>


//only initial MyApp service
[[AotterTrek sharedAPI] initMyAppServiceWithClientId:@""
                                              secret:@""]; 
 
//initial MyApp service and TrekService if needed
[[AotterTrek sharedAPI] initTrekServiceWithClientId:@""
                                              secret:@""
                                       myAppClientId:@""
                                   myAppClientSecret:@""];
```
{% endtab %}

{% tab title="Swift" %}
```swift

//add Header.h as Objective-C bridging Header
//reference: https://developer.apple.com/documentation/swift/importing-objective-c-into-swift
#import <AotterTrek-iOS-SDK/AotterTrek-iOS-SDK.h>
​
​
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

**#usage**

Native ad `TKMyAppAdNative` usage is the same as `TKAdNative`. See[ Native Ad](ad-formats/) for more information.

{% tabs %}
{% tab title="ObjC" %}
```objectivec
  self.nativeAd = [[TKMyAppAdNative alloc] initWithPlace:@"myPlace" category:@"testCategory"];
  [self.nativeAd registerPresentingViewController:self];
  self.nativeAd.delegate = self;
  [self.nativeAd fetchAd];
```
{% endtab %}

{% tab title="Swift" %}
```swift
self.nativeAd = TKMyAppAdNative.init(place: "myPlace", category: "testCategory")
self.nativeAd?.registerPresenting(self)
self.nativeAd?.delegate = self
self.nativeAd?.fetchAd()
```
{% endtab %}
{% endtabs %}

## Overwrite Click Event for MyApp Ads <a href="#overwrite-click-event-for-myapp-ads" id="overwrite-click-event-for-myapp-ads"></a>

Implement `TKAdNativeDelegate` ->`TKMyAppAdNativeOnClicked:(TKMyAppAdNative *)ad`

{% tabs %}
{% tab title="ObjC" %}
```objectivec
-(void)TKMyAppAdNativeOnClicked:(TKMyAppAdNative *)ad{
    NSLog(@"[Demo MyApp] >> onClick MyAppAdNative with adData: %@", ad.AdData);
    NSString *targetUrl = ad.AdData[@"url_original"];
}
```
{% endtab %}

{% tab title="Second Tab" %}
```swift
func tkMyAppAdNative(onClicked ad: TKMyAppAdNative!) {
    print("MyApp onClick MyAppAdNative")
    if let targetUrl = ad.adData["url_original"]{
        //do something
    }
}
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
**Notice**: This method is only available for MyApp's ads.&#x20;
{% endhint %}

{% hint style="warning" %}
**Notice:** When implementing this method, the default click event will be prevented. You should manually implement click action such as open URL or browser.
{% endhint %}
