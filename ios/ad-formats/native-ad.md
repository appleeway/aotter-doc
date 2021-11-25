# Native Ad

## Add Native Ads to an iOS APP

The Native Ad API allows you to build a customized experience for the ads you show in your app. When using Native Ad API, instead of receiving an ad ready to be displayed, you will receive a group of **ad parameters** such as a title, an image, a call to action, and you are able to use them to construct a custom view where the ad is shown.

Follow these steps to build a native ad layout that fits your application and then requests it.

Step 1: [Create `TKAdNative` Object](native-ad.md#step-1-create-adnative-object)\
Step 2: [Render `TKAdNatvie` UI Object](native-ad.md#step-2-render-adnatvie-ui-object)\
Step 3: [Ad Fail Delegates](native-ad.md#step-3-ad-fail-delegates)\
Step 4: [Remove and Release](native-ad.md#step-4-remove-and-release)

### **AdData Parameter**

| Variable         | Type   | Description     | **Always have value** | Required to be displayed |
| ---------------- | ------ | --------------- | --------------------- | ------------------------ |
| `advertiserName` | String | Advertiser Name | Yes                   | Recommended              |
| `title`          | String | Ad Headline     | Yes                   | Required                 |
| `text`           | String | Ad Text         | No, could be empty    | Recommended              |
| `img_main`       | String | Size: 1200x628  | Yes                   | Recommended              |
| `img_icon`       | String | Size: 82x82     | Yes                   | Recommended              |
| `img_icon_hd`    | String | Size: 300x300   | Yes                   | Recommended              |
| `callToAction`   | String | Ex: "瞭解詳情"      | Yes                   | Recommended              |
| `sponser`        | String | Sponsored       | Yes                   | Required                 |

![](<../../.gitbook/assets/截圖 2021-09-10 下午5.36.49.png>)

### Functions

* **isExpired()**

You can use this method to check if the ad is expired or not.

```swift
[self.myAdNative isExpired]; // YES or NO
```

* **impression & click delegate**

```objectivec
-(void)TKAdNativeWillLogClicked:(TKAdNative *)ad{
    //will log when click occur
}

-(void)TKAdNativeWillLogImpression:(TKAdNative *)ad{
    //will log when impression occur
```

### Step 1: Create `TKAdNative` Object

In the following code snippet, replace the value in `initWithPlace` to your **UUID**.\
Setting category is optional. You can fill in `nil` if you don't want to set it.

```swift
   //initial ad with place and category
   //Replace the value in initWithPlace to your own UUID. Ex. "0000-12345-6789-000"
   //and category Ex. "News"
   self.myAdNative = [TKAdNative alloc] initWithPlace:@"YOUR UUID" category:@"CATEGORIES"];

   //register current presenting view controller
   [self.myAdNative registerPresentingViewController:self];
   
   //set delegate if needed
   self.myAdNative.delegate = self;
   
   //fetch Ad data from API
   [self.myAdNative fetchAd];
```

### Step 2: Render `TKAdNatvie` UI Object

```swift
-(void)TKAdNative:(TKAdNative *)ad didReceivedAdWithData:(NSDictionary *)adData{
  
    // Get ad data parameter
    NSString *advertiserName = adData[@"advertiserName"];
    NSString *title = adData[@"title"];
    NSString *text = adData[@"text"];
    NSString *imgMain = adData[@"img_main"];         //1200x628
    NSString *imageIcon = adData[@"img_icon"];       //82x82
    NSString *imageIconHd = adData[@"img_icon_hd"];  //300x300
    NSString *callToAction = adData[@"callToAction"];
    NSString *sponsor = adData[@"sponser"];
  
    //register ad view.
    [self.myAdView registerAdView:self.myAdView];

    //render ad data
    NSDictionary *adData = ad.AdData;
       //{render views...}

   //set Action button
   [self.myAdNative registerCallToActionButton:self.myButton];
}
```

### Step 3: Ad Fail Delegates

```swift
-(void)TKAdNative:(TKAdNative *)ad fetchError:(TKAdError *)error{
    NSLog(@"TKAdNative fetch error: %@", error.message);
}
```

### Step 4: Remove and Release

```swift
//remove and release data
[self.myAdNative destroy];
```
