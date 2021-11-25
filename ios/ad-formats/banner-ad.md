# Banner Ad

Follow these steps to build a banner ad layout and then requests it.

Step 1: [Create `TKAdSuprAd` Object](banner-ad.md#step-1-create-tkadsuprad-object)\
Step 2: [Register AdView and TKMediaView](banner-ad.md#step-2-register-adview-and-tkmediaview)\
Step 3: [Ad Loading Completion Callback](banner-ad.md#step-3-ad-loading-completion-callback)\
Step 4: [Error Callback](banner-ad.md#step-4-error-callback)\
Step 5: [Destroy Ad (Optional)](banner-ad.md#step-5-optional-destroy-ad)

### Functions

* **isExpired()**

You can use this method to check if the ad is expired or not.

```swift
[self.myAdNative isExpired]; // YES or NO
```

* **impression & click delegate**

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
// .m

#import <AotterTrek-iOS-SDK/AotterTrek-iOS-SDK.h>

@interface ViewController () <TKAdSuprAdDelegate>
{
    UIView *_suprAdView;
}
@property (nonatomic,strong) TKAdSuprAd *suprAd;
@end
.
.
.
@implementation ViewController
  
- (void)viewDidLoad {
    [super viewDidLoad];
    [self fetchSuprAd];
}

#pragma mark : fetch TKAdSuprAd

- (void)fetchSuprAd {
   //Replace the value in initWithPlace to your own UUID. Ex. "0000-12345-6789-000"
   //and category Ex. "News"
    if(!self.suprAd){
        self.suprAd = [[TKAdSuprAd alloc] initWithPlace:@"YOUR UUID" category:@"CATEGORIES"];
    }
    self.suprAd.delegate = self;
  
    //register view controller for presenting
    [self.suprAd registerPresentingViewController:self];
    
    // fetch ad
    [self.suprAd fetchAd];
}
@end
```

### Step 2: Register AdView and TKMediaView

It is recommended to create the view that its size is based on ad size.

```swift
-(void)TKAdSuprAd:(TKAdSuprAd *)suprAd didReceivedAdWithAdData:(NSDictionary *)adData preferedMediaViewSize:(CGSize)size isVideoAd{
  
    self.suprAd = suprAd;
    
    //size for the ad
    _suprAdView = [[UIView alloc]initWithFrame:CGRectMake(0, 0, size.width, size.height)];
    
    //AdView: the container view for ad
    [self.suprAd registerAdView:_suprAdView];
    [self.suprAd registerTKMediaView:_suprAdView];
    
    // AutoLayout
    [self.view addSubview:_suprAdView];
    
    [_suprAdView setTranslatesAutoresizingMaskIntoConstraints:NO];
    [_suprAdView.widthAnchor constraintEqualToConstant:size.width].active = YES;
    [_suprAdView.heightAnchor constraintEqualToConstant:size.height].active = YES;
    [_suprAdView.bottomAnchor constraintEqualToAnchor:self.view.safeAreaLayoutGuide.bottomAnchor].active = YES;
}
```

### Step 3: Ad Loading Completion Callback

```swift
- (void)TKAdSuprAdCompleted:(TKAdSuprAd *)suprAd{
    NSLog(@"TKAdSuprAd >> Completed");
}
```

### Step 4: Error Callback

```swift
- (void)TKAdSuprAd:(TKAdSuprAd *)suprAd adError:(TKAdError *)error{
    NSLog(@"TKAdSuprAd >> adError: %@", error.message);
}
```

### Step 5: (Optional) Destroy Ad

This function will destroy ads completely. In the condition that`TKAdSuprAd`manages itself, destroy() is not necessary to be invoked. However, it is still nice to have it when you are pretty sure that this view or view controller won't be used anymore.

```swift
-(void)viewDidDisappear:(BOOL)animated{
[super viewDidDisappear:animated];
[self.suprAd destroy];
}
```

###
