# Banner Ad

Follow these steps to build a banner ad layout and then requests it.

Step 1: [Initialize AotterTrek SDK](banner-ad.md#step-1-initialize-aottertrek-sdk)\
Step 2: [Customize _ViewController_](banner-ad.md#step-2-customize-viewcontroller)__

### Step 1: Initialize AotterTrek SDK&#x20;

_File: AppDelegate.m_

```swift
/// Need to import Lib
#import <AotterTrek-iOS-SDK/AotterTrek-iOS-SDK.h>
#import <GoogleMobileAds/GoogleMobileAds.h>
.
.
.

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions {
    // Override point for customization after application launch.
    
    [[GADMobileAds sharedInstance] startWithCompletionHandler:nil];
    
    [[AotterTrek sharedAPI] initTrekServiceWithClientId:@"Your Client ID"
                                                   secret:@"Your Client Secret"];
    
    // Open Log
    //[[AotterTrek sharedAPI] performSelector:@selector(enableLoggerLevelDevDetail)];
    
    return YES;
}
```

### Step 2: Customize ViewController

\- **GoogleMobileAds SDK version 8 and above**

```swift
//Ex:BannerViewController
#import "BannerViewController.h"
#import <GoogleMobileAds/GoogleMobileAds.h>

static NSString *const BannerAdUnit = @"Your AdMob banner ad unit";

@interface BannerViewController ()<GADBannerViewDelegate> {
    GADBannerView *_gadBannerView;
}
@end

@implementation BannerViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do additional setup after loading the view from its nib.
    
    [self setupGADBannerView];
}

#pragma mark : Setup GADBanner

- (void)setupGADBannerView {
    _gadBannerView = [[GADBannerView alloc]initWithAdSize:kGADAdSizeBanner];
    _gadBannerView.delegate = self;
    _gadBannerView.rootViewController = self;
    _gadBannerView.adUnitID = BannerAdUnit;
        
    [self bannerLoadRequest];
}

-(void)bannerLoadRequest {
    GADRequest *request = [GADRequest request];
    GADCustomEventExtras *extra = [[GADCustomEventExtras alloc] init];
  
  	// FIll in categories like "news"、"movie" at CATEGORIES
    [extra setExtras:@{@"category":@"CATEGORIES"} forLabel:@"AotterTrekGADCustomEventBannerAd"]; //label must be same as your mediation class name, AotterTrekGADMediaAdapter or AotterTrekGADCustomEventBannerAd.
    [request registerAdNetworkExtras:extra];
    
    [_gadBannerView loadRequest:request];
}

- (void)setupBannerViewUI:(GADBannerView *)bannerView {
    
    [self.view addSubview:bannerView];

    [bannerView setTranslatesAutoresizingMaskIntoConstraints:NO];

    [bannerView.heightAnchor constraintEqualToConstant:bannerView.bounds.size.height].active = YES;
    [bannerView.bottomAnchor constraintEqualToAnchor:self.view.safeAreaLayoutGuide.bottomAnchor constant:0.0].active = YES;
    [bannerView.leftAnchor constraintEqualToAnchor:self.view.leftAnchor constant:0].active = YES;
    [bannerView.rightAnchor constraintEqualToAnchor:self.view.rightAnchor constant:0].active = YES;
}

#pragma mark :GADBannerViewDelegate
- (void)bannerViewDidReceiveAd:(GADBannerView *)bannerView {
    if (bannerView != nil) {
        [self setupBannerViewUI:bannerView];
    }
}

- (void)bannerView:(GADBannerView *)bannerView didFailToReceiveAdWithError:(NSError *)error {
    NSLog(@"error message: %@",error.localizedDescription);
}

@end
```
