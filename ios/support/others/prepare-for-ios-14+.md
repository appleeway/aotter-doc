# Prepare for iOS 14+

Starting from iOS 14, it will be giving users the choice to block the IDFA identifier at the app level. Among other changes, what this means is the iOS 14 update will require apps to ask users for permission to collect and share data, which is called the [App Tracking Transparency](https://developer.apple.com/documentation/apptrackingtransparency) framework. It aims to present the app-tracking authorization request to the end-user. If an app does not present this request, the IDFA will automatically be zeroed out which may lead to a significant loss in ad revenue.

## Request AppTrackingTransparency for IDFA <a href="#request-apptrackingtransparency-for-idfa" id="request-apptrackingtransparency-for-idfa"></a>

**Step 1 :** [**Link AppTrackingTransparency.framework in your project**](prepare-for-ios-14+.md#step-1-link-apptrackingtransparencyframework-in-your-project)****

**Step 2 :** [**Add User Tracking Usage Description in **_**info.plist**_](prepare-for-ios-14+.md#step-2-add-user-tracking-usage-description-in-infoplist)_****_

_**Step 3 :**_ [**Request permission before request ads.**](prepare-for-ios-14+.md#step-3-request-permission-before-request-ads)****

****

### [Step 1. Link AppTrackingTransparency.framework in your project.](prepare-for-ios-14+.md#request-apptrackingtransparency-for-idfa) <a href="#step-1-link-apptrackingtransparencyframework-in-your-project" id="step-1-link-apptrackingtransparencyframework-in-your-project"></a>

As the framework is iOS14+, you need to link this feature with the framework at beta Xcode (12+)

### [Step 2. Add User Tracking Usage Description in _info.plist_](prepare-for-ios-14+.md#request-apptrackingtransparency-for-idfa)__ <a href="#step-2-add-user-tracking-usage-description-in-infoplist" id="step-2-add-user-tracking-usage-description-in-infoplist"></a>

Just like the usage of Camera / Album / Location, you need to provide a message telling users that why your app needs permission.

```
<key>NSUserTrackingUsageDescription</key>
<string>This identifier will be used to deliver personalized ads to you.</string>
```

### [Step 3. Request permission before request ads.](prepare-for-ios-14+.md#request-apptrackingtransparency-for-idfa) <a href="#step-3-request-permission-before-request-ads" id="step-3-request-permission-before-request-ads"></a>

To present the authorization request, call [`requestTrackingAuthorizationWithCompletionHandler:`](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/3547037-requesttrackingauthorization). We recommend waiting for the completion callback prior to loading ads so that if the user grants the App Tracking Transparency permission, the Interactive Media Ads SDK can use the IDFA in ad requests.

{% tabs %}
{% tab title="Objective-C" %}
```objectivec
#import <AppTrackingTransparency/AppTrackingTransparency.h>
#import <AdSupport/AdSupport.h>

- (void)requestIDFA {
  [ATTrackingManager requestTrackingAuthorizationWithCompletionHandler:^(ATTrackingManagerAuthorizationStatus status) {
    // Tracking authorization completed. Start loading ads here.
    // [self.myTKAdNative loadAd];
  }];
}
```
{% endtab %}

{% tab title="Swift" %}
```swift
import AdSupport
import AppTrackingTransparency

func requestIDFA(){
    ATTrackingManager.requestTrackingAuthorization { status in
        if status == .authorized {
            //Authorized.
            self.myTKAdNative.load()
        }
    }
}
```
{% endtab %}
{% endtabs %}

For more information about the possible status values, see [`ATTrackingManager.AuthorizationStatus`](https://developer.apple.com/documentation/apptrackingtransparency/attrackingmanager/authorizationstatus).
