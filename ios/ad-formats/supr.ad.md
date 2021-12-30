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

```swift
[self.myAdNative isExpired]; // YES or NO
```

* **isVideoAd()**

You can use this method to check the ad is a video ad or not.

```objectivec
[self.suprAd isVideoAd]; //YES or NO
```

* **impression & click delegate**

Notice that this function is unavailable for the video type of Supr.Ad.

```objectivec
-(void)TKAdSuprAdWillLogImpression:(TKAdSuprAd *)ad{
    NSLog(@"TKSuprAd log when impression occur");
}

-(void)TKAdSuprAdWillLogClick:(TKAdSuprAd *)ad{
    NSLog(@"TKSuprAd log when click occur");
}
```

### Step 1: Create `TKAdSuprAd` Object

In the following code snippet, replace the value in `initWithPlace` to your **UUID**.\
Setting category is optional. You can fill in `nil` if you don't want to set it.

```swift
//Replace the value in initWithPlace to your own UUID. Ex. "0000-12345-6789-000"
//and category Ex. "News"
self.suprAd = [TKAdSuprAd alloc] initWithPlace:@"YOUR UUID" category:@"CATEGORIES"];
self.suprAd.delegate = self;

// Register view controller for presenting
[self.suprAd registerPresentingViewController:self];
```

### Step 2: Fetch Ad

```swift
[self.suprAd fetchAd];
```

### Step 3: Register AdView and TKMediaView

If you'd like to use **screen width** as ad-view width, we recommend using `preferedMediaViewSize` for calculating the corresponding ad-view height.

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
    
    [self.suprAd registerTKMediaView:self.adCell.contentView];

    //AdView: the container view for ad
    [self.suprAd registerAdView:self.adCell.contentView];

    //prefered size for the ad
    self.myAdSize = size;
}
```

### Step 4: Ad Loading Completion Callback

```swift
-(void)TKAdSuprAdCompleted:(TKAdSuprAd *)suprAd{
        [self.adCell setNeedsLayout];
        [self.mainTableView reloadData];
}
```

### Step 5: Error Callback

```swift
-(void)TKAdSuprAd:(TKAdSuprAd *)suprAd adError:(TKAdError *)error{
        NSLog(@"Supr.Ad error: %@", error.description);
}
```

### Step 6: (Optional) Notify Ad Scroll Event&#x20;

When rendering ads in your **ScrollView / TableView / CollectionView** or any other that might have vertical scroll behavior, you should call this function when the scroll behavior takes place.

```objectivec
-(void)scrollViewDidScroll:(UIScrollView *)scrollView{
    if(self.suprAd){
        [self.suprAd notifyAdScrolled];
    }
}
```

### Step 7: (Optional) Destroy Ad

This function will destroy ads completely. In the condition that`TKAdSuprAd`manages itself, destroy() is not necessary to be invoked. However, it is still nice to have it when you are pretty sure that this view or view controller won't be used anymore.

```objectivec
-(void)viewDidDisappear:(BOOL)animated{
        [super viewDidDisappear:animated];
        [self.suprAd destroy];
}
```

### Special Cases

* Top View & IMA SDK

Supr.Ad including video ad advertising, which uses VAST technology provided by the Google IMA SDK. In the implementation of VAST, AotterTrek iOS SDK needs to register _ViewController_ when requesting VAST ads from Google IMA. In the meantime, Google IMA SDK will compare _**TopViewController**_ with _**the ViewController shows ads**_. _This_ _ViewController_ should be ** **_**the same** ViewController that displays the video ads!_ If it's not the same one, might lead to a **CRASH** in your app but cause by Google IMA SDK.

![](<../../.gitbook/assets/截圖 2021-09-23 下午12.18.13.png>)

| Request Ads        | Display Ads        | Position                             | Functional |
| ------------------ | ------------------ | ------------------------------------ | ---------- |
| "A" ViewController | "A" ViewController | "A" ViewController on the very top   | **Yes**    |
| "A" ViewController | "A" ViewController | other ViewController on the very top | **No**     |
| "A" ViewController | "B" ViewController |                                      | **No**     |

That is to say,  _**the ViewController**_** must be on the very top of the view**. Also, please make sure there is no _other ViewController_ such as `UIAlertController` / `CustomViewController` layover it.
