# Supr.Ad

Follow these steps to build a Supr.Ad layout and then requests it.

Step 1: [Create `TKAdSuprAd` Object](supr.ad.md#step-1-create-tkadsuprad-object)\
Step 2: [Fetch Ad](supr.ad.md#step-2-fetch-ad)\
Step 3: [Register AdView and TKMediaView](supr.ad.md#step-3-register-adview-and-tkmediaview)\
Step 4: [Ad Loading Completion Callback](supr.ad.md#step-4-ad-loading-completed)\
Step 5: [Error Callback](supr.ad.md#step-5-error-callback)\
Step 6: [Notify Ad Scroll Event (Optional)](supr.ad.md#step-6-optional-notify-ad-scroll-event)\
Step 7: [Destroy Ad (Optional)](supr.ad.md#step-7-optional-destroy-ad)\
[Special Cases](supr.ad.md#special-cases)

### AdData Parameter

| Variable         | Type   | Description     | **Always have value** | Required to be displayed |
| ---------------- | ------ | --------------- | --------------------- | ------------------------ |
| `advertiserName` | String | Advertiser Name | Yes                   | Recommended              |
| `title`          | String | Ad Headline     | Yes                   | Recommended              |
| `text`           | String | Ad Text         | No, could be empty    | Recommended              |
| `callToAction`   | String | Ex: "瞭解詳情"      | Yes                   | Recommended              |

### Functions

* **isExpired()**

You can use this method to check if the ad is expired or not.

{% tabs %}
{% tab title="ObjC" %}
```swift
[self.myAdNative isExpired]; // YES or NO
```
{% endtab %}

{% tab title="Swift" %}
```
 self.myAdNative?.isExpired()
```
{% endtab %}
{% endtabs %}

* **isVideoAd()**

You can use this method to check the ad is a video ad or not.

{% tabs %}
{% tab title="ObjC" %}
```objectivec
[self.suprAd isVideoAd]; //YES or NO
```
{% endtab %}

{% tab title="Swift" %}
```
self.myAdNative.isVideoAd()
```
{% endtab %}
{% endtabs %}

* **impression & click delegate**

{% hint style="warning" %}
Please noticed that Supr.ad includes video ad. **In the circumstance of video ad display, it will not trigger the `TKAdSuprAdWillLogImpression` and `TKAdSuprAdWillLogClick` event.**&#x20;
{% endhint %}

{% tabs %}
{% tab title="ObjC" %}
```objectivec
-(void)TKAdSuprAdWillLogImpression:(TKAdSuprAd *)ad{
    NSLog(@"TKSuprAd log when impression occur");
}

-(void)TKAdSuprAdWillLogClick:(TKAdSuprAd *)ad{
    NSLog(@"TKSuprAd log when click occur");
}  func tkAdSuprAdWillLogClick(_ ad: TKAdSuprAd!) {
```
{% endtab %}

{% tab title="Swift" %}
```swift
func tkAdSuprAdWillLogClick(_ ad: TKAdSuprAd!) {
    //will log when click occur
}

func tkAdSuprAdWillLogImpression(_ ad: TKAdSuprAd!) {
    //will log when impression occur
}
```
{% endtab %}
{% endtabs %}

### Step 1: Create `TKAdSuprAd` Object

In the following code snippet, replace the value in `initWithPlace` to your **UUID**.\
Setting category is optional. You can fill in `nil` if you don't want to set it.

{% tabs %}
{% tab title="ObjC" %}
```objectivec
//Replace the value in initWithPlace to your own UUID. Ex. "0000-12345-6789-000"
//and category Ex. "News"
self.suprAd = [TKAdSuprAd alloc] initWithPlace:@"YOUR UUID" category:@"CATEGORIES"];
self.suprAd.delegate = self;

// Register view controller for presenting
[self.suprAd registerPresentingViewController:self];
```
{% endtab %}

{% tab title="Swift" %}
```swift
//Replace the value in initWithPlace to your own UUID. Ex. "0000-12345-6789-000"
//and category Ex. "News"
self.suprAd = TKAdSuprAd.init(place: "YOUR UUID", category: "CATEGORIES")
self.suprAd.delegate = self;

// Register view controller for presenting
self.suprAd.registerPresenting(self)
```
{% endtab %}
{% endtabs %}

### Step 2: Fetch Ad

{% tabs %}
{% tab title="ObjC" %}
```objectivec
[self.suprAd fetchAd];
```
{% endtab %}

{% tab title="Swift" %}
```swift
self.suprAd.fetchAd()
```
{% endtab %}
{% endtabs %}

### Step 3: Register AdView and TKMediaView

If you'd like to use **screen width** as ad-view width, we recommend using `preferedMediaViewSize` for calculating the corresponding ad-view height.

{% tabs %}
{% tab title="ObjC" %}
```objectivec
-(void)TKAdSuprAd:(TKAdSuprAd *)suprAd didReceivedAdWithAdData:(NSDictionary *)adData preferedMediaViewSize:(CGSize)size isVideoAd{
    if(isVideoAd){
     // When you get video ad from Supr.Ad
    } 
  
    // Get ad data parameter
    NSString *advertiserName = adData[@"advertiserName"];
    NSString *title = adData[@"title"];
    NSString *text = adData[@"text"];
    NSString *callToAction = adData[@"callToAction"];

    // TKMediaView: the view for showing SuprAd content
    double adSizeWidth = size.width;
    double adSizeHeight = size.height;
    CGFloat viewWidth = UIScreen.mainScreen.bounds.size.width;
    CGFloat viewHeight = viewWidth * adSizeHeight/adSizeWidth;
    int adheight = (int)viewHeight; // Convert to integer
    
    UIView *mediaView = [[UIView alloc]initWithFrame:CGRectMake(0, 0, viewWidth, adheight)];
    [self.suprAd registerTKMediaView:mediaView];

    //AdView: the container view for ad
    [self.suprAd registerAdView:self.adCell.contentView];

    //prefered size for the ad
    self.myAdSize = size;
}
```
{% endtab %}

{% tab title="Swift" %}
```swift
func tkAdSuprAd(_ suprAd: TKAdSuprAd!, didReceivedAdWithAdData adData: [AnyHashable : Any]!, preferedMediaViewSize size: CGSize, isVideoAd: Bool) {
    if(isVideoAd){
        // When you get video ad from Supr.Ad
    }
    
    // Get ad data parameter
    let advertiserName = adData["advertiserName"]
    let title = adData["title"]
    let text = adData["text"]
    let callToAction = adData["callToAction"]
    
    // TKMediaView: the view for showing SuprAd content
    let adSizeWidth = size.width
    let adSizeHeight = size.height
    let viewWidth = UIScreen.main.bounds.size.width
    let viewHeight = viewWidth * adSizeHeight/adSizeWidth
    let adHeight = viewHeight;
    
    let mediaView:UIView?
    mediaView = UIView.init(frame: CGRectMake(0, 0, viewWidth, viewHeight))
    self.suprAd.registerTKMediaView(mediaView)
    
    //AdView: the container view for ad
    self.suprAd.register(self.adCell.contentView)
    
    self.myAdSize = size
}
```
{% endtab %}
{% endtabs %}

### Step 4: Ad Loading Completion Callback

{% tabs %}
{% tab title="ObjC" %}
<pre class="language-objectivec"><code class="lang-objectivec">-(void)TKAdSuprAdCompleted:(TKAdSuprAd *)suprAd{
<strong>    [self.adCell setNeedsLayout];
</strong>    [self.mainTableView reloadData];
}</code></pre>
{% endtab %}

{% tab title="Swift" %}
```swift
func tkAdSuprAdCompleted(_ suprAd: TKAdSuprAd!) {
  self.adCell?.setNeedsLayout()
  self.mainTableView?.reloadData()
}
```
{% endtab %}
{% endtabs %}

### Step 5: Error Callback

{% tabs %}
{% tab title="ObjC" %}
```objectivec
-(void)TKAdSuprAd:(TKAdSuprAd *)suprAd adError:(TKAdError *)error{
        NSLog(@"Supr.Ad error: %@", error.description);
}
```
{% endtab %}

{% tab title="Swift" %}
```swift
func tkAdSuprAd(_ suprAd: TKAdSuprAd!, adError error: TKAdError!) {
       print("TKAdSuprAd error" + error.description)
}
```
{% endtab %}
{% endtabs %}

### Step 6: (Optional) Notify Ad Scroll Event&#x20;

When rendering ads in your **ScrollView / TableView / CollectionView** or any other that might have vertical scroll behavior, you should call this function when the scroll behavior takes place.

{% tabs %}
{% tab title="ObjC" %}
```objectivec
-(void)scrollViewDidScroll:(UIScrollView *)scrollView{
    if(self.suprAd){
        [self.suprAd notifyAdScrolled];
    }
}
```
{% endtab %}

{% tab title="Swift" %}
```swift
func scrollViewDidScroll(_ scrollView: UIScrollView) {
    if(self.suprAd){
        self.suprAd.notifyScrolled()
    }
}
```
{% endtab %}
{% endtabs %}

### Step 7: (Optional) Destroy Ad

This function will destroy ads completely. In the condition that`TKAdSuprAd`manages itself, destroy() is not necessary to be invoked. However, it is still nice to have it when you are pretty sure that this view or view controller won't be used anymore.

{% tabs %}
{% tab title="ObjC" %}
```objectivec
-(void)viewDidDisappear:(BOOL)animated{
    [super viewDidDisappear:animated];
    [self.suprAd destroy];
}
```
{% endtab %}

{% tab title="Swift" %}
<pre class="language-swift"><code class="lang-swift">override func viewDidDisappear(_ animated: Bool) {
<strong>    super.viewDidDisappear(animated)
</strong>    self.suprAd.destroy()
}</code></pre>
{% endtab %}
{% endtabs %}

### Special Cases

* Top View & IMA SDK

Supr.Ad includes video ad advertising, which uses VAST technology provided by the Google IMA SDK. In the implementation of VAST, AotterTrek iOS SDK needs to register _ViewController_ when requesting VAST ads from Google IMA. In the meantime, Google IMA SDK will compare _**TopViewController**_ with _**the ViewController shows ads**_. _This_ _ViewController_ should be ** **_**the same** ViewController that displays the video ads!_ If it's not the same one, might lead to a **CRASH** in your app but caused by Google IMA SDK.

![](<../../.gitbook/assets/截圖 2021-09-23 下午12.18.13.png>)

| Request Ads        | Display Ads        | Position                             | Functional |
| ------------------ | ------------------ | ------------------------------------ | ---------- |
| "A" ViewController | "A" ViewController | "A" ViewController on the very top   | **Yes**    |
| "A" ViewController | "A" ViewController | other ViewController on the very top | **No**     |
| "A" ViewController | "B" ViewController |                                      | **No**     |

That is to say,  _**the ViewController**_** must be on the very top of the view**. Also, please make sure there is no _other ViewController_ such as `UIAlertController` / `CustomViewController` layover it.
