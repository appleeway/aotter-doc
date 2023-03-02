# Native Ad

## Add Native Ads to an iOS APP

The Native Ad API allows you to build a customized experience for the ads you show in your app. When using Native Ad API, instead of receiving an ad ready to be displayed, you will receive a group of **ad parameters** such as a title, an image, a call to action, and you are able to use them to construct a custom view where the ad is shown.

Follow these steps to build a native ad layout that fits your application and then requests it.

#### Step 1: [Create `TKAdNative` Object](native-ad.md#step-1-create-tkadnative-object-1)

#### Step 2: [Render `TKAdNatvie` UI Object](native-ad.md#step-2-render-tkadnatvie-ui-object-1)

#### Step 3: [Ad Fail Delegates](native-ad.md#step-3-ad-fail-delegates-1)

#### **Step 4:** [**Remove and Release**](native-ad.md#step-4-remove-and-release)

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

![](<../../../.gitbook/assets/截圖 2021-09-10 下午5.36.49.png>)

### Functions

* **isExpired()**

You can use this method to check if the ad is expired or not.

{% tabs %}
{% tab title="Objective-C" %}
```objectivec
[self.myAdNative isExpired]; // YES or NO
```
{% endtab %}

{% tab title="Swift" %}
```
self.myAdNative?.isExpired()
```
{% endtab %}
{% endtabs %}

* **impression & click delegate**

{% tabs %}
{% tab title="Objective-C" %}
```objectivec
-(void)TKAdNativeWillLogClicked:(TKAdNative *)ad{
    //will log when click occur
}

-(void)TKAdNativeWillLogImpression:(TKAdNative *)ad{
    //will log when impression occur
```
{% endtab %}

{% tab title="Swift" %}
```swift
func tkAdNativeWillLogClicked(_ ad: TKAdNative!) {
    //will log when click occur
}

func tkAdNativeWillLogImpression(_ ad: TKAdNative!) {
    //will log when impression occur
}
```
{% endtab %}
{% endtabs %}

### [Step 1: Create `TKAdNative` Object](native-ad.md#step-1-create-tkadnative-object)

In the following code snippet, replace the value in `initWithPlace` to your **UUID**.\
Setting category is optional. You can fill in `nil` if you don't want to set it.

{% tabs %}
{% tab title="Objective-C" %}
```objectivec
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
{% endtab %}

{% tab title="Swift" %}
```swift
//initial ad with place and category
//Replace the value in initWithPlace to your own UUID. Ex. "0000-12345-6789-000"
//and category Ex. "News"
self.myAdNative = TKAdNative.init(place: "YOUR UUID", category: "CATEGORIES")

//register current presenting view controller
self.myAdNative?.registerPresenting(self)

//set delegate if needed
self.myAdNative?.delegate = self

//fetch Ad data from API
self.myAdNative?.fetchAd()
```
{% endtab %}
{% endtabs %}

### [Step 2: Render `TKAdNatvie` UI Object](native-ad.md#step-2-render-tkadnatvie-ui-object)

{% tabs %}
{% tab title="Objective-C" %}
```objectivec
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
}jj
```
{% endtab %}

{% tab title="Swift" %}
```swift
 func tkAdNative(_ ad: TKAdNative!, didReceivedAdWithData adData: [AnyHashable : Any]!) {
        // Get ad data parameter
        let advertiserName = adData["advertiserName"]
        let title = adData["title"]
        let text = adData["text"]
        let imgMain = adData["img_main"]
        let imageIcon = adData["img_icon"]
        let imageIconHd = adData["img_icon_hd"]
        let callToAction = adData["callToAction"]
        let sponsor = adData["sponser"]
        
        //register ad view.
        self.myAdNative?.registerAdView(self.myAdView)
    
        //render ad data
        let adData = ad.adData
    
        //{render views...}

        //set Action button
        self.myAdNative?.registerCall(toActionButton: self.myButton)
    }
```
{% endtab %}
{% endtabs %}

### [Step 3: Ad Fail Delegates](native-ad.md#step-3-ad-fail-delegates)

{% tabs %}
{% tab title="Objective-C" %}
```objectivec
-(void)TKAdNative:(TKAdNative *)ad fetchError:(TKAdError *)error{
NSLog(@"TKAdNative fetch error: %@", error.message);
}
```
{% endtab %}

{% tab title="Swift" %}
```swift
func tkAdNative(_ ad: TKAdNative!, fetchError error: TKAdError!) {
        print("TKAdNative fetch error" + error.message)
}
```
{% endtab %}
{% endtabs %}

### [Step 4: Remove and Release](native-ad.md#step-4-remove-and-release)

{% tabs %}
{% tab title="Objective-C" %}
```objectivec
//remove and release data
[self.myAdNative destroy];
```
{% endtab %}

{% tab title="Swift" %}
```swift
//remove and release data
self.myAdNative?.destroy()
```
{% endtab %}
{% endtabs %}
