# Banner Ad

Follow these steps to build a banner ad layout and then requests it.

Step 1: [Initialize AotterTrek SDK](broken-reference)\
Step 2: [Customize _ViewController_](broken-reference)__

### Step 1: Initialize AotterTrek SDK&#x20;

{% tabs %}
{% tab title="Objective-C" %}
_File: AppDelegate.m_

```objectivec
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
{% endtab %}

{% tab title="Swift" %}
```swift
func application(_ application: UIApplication, didFinishLaunchingWithOptions launchOptions: [UIApplication.LaunchOptionsKey: Any]?) -> Bool {
    GADMobileAds.sharedInstance().start()
    AotterTrek.sharedAPI().initTrekService(withClientId: "<client id", secret: "<client secret>")
 
 return true
}
```
{% endtab %}
{% endtabs %}

### Step 2: Customize ViewController

\- **GoogleMobileAds SDK version 8 and above**

{% tabs %}
{% tab title="Objective-C" %}
```objectivec
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
{% endtab %}

{% tab title="Swift" %}
```swift
class BannerViewController:UIViewController, GADBannerViewDelegate{
    var gadBannerView:GADBannerView
    let bannerAdUnit = "XXXX-XX-XXXXXXXX"
    
    override func viewDidLoad() {
        self.setupGADBannerView()
        self.bannerLoadRequest()
    }
    
    func setupGADBannerView(){
        self.gadBannerView = GADBannerView.init(adSize: GADAdSizeBanner)
        self.gadBannerView.delegate = self
        self.gadBannerView.rootViewController = self
        self.gadBannerView.adUnitID = bannerAdUnit
    }
    
    func bannerLoadRequest(){
        var request = GADRequest.init()
        var extras = GADCustomEventExtras.init()
        extras.setExtras(["category":"CATEGORIES"], forLabel: "AotterTrekGADCustomEventBannerAd")
        //label must be same as your mediation class name, AotterTrekGADMediaAdapter or AotterTrekGADCustomEventBannerAd
        request.register(extras)
        self.gadBannerView.load(request)
    }
    
    func setupBannerViewUI(_ bannerView:GADBannerView){
        self.view.addSubview(bannerView)
        bannerView.translatesAutoresizingMaskIntoConstraints = false
        bannerView.heightAnchor.constraint(equalToConstant: bannerView.bounds.size.height).isActive = true
        bannerView.bottomAnchor.constraint(equalTo: self.view.safeAreaLayoutGuide.bottomAnchor).isActive = true
        bannerView.leftAnchor.constraint(equalTo: self.view.leftAnchor).isActive = true
        bannerView.rightAnchor.constraint(equalTo: self.view.rightAnchor).isActive = true
    }
    
    func bannerViewDidReceiveAd(_ bannerView: GADBannerView) {
        self.setupBannerViewUI(bannerView)
    }
    
    func bannerView(_ bannerView: GADBannerView, didFailToReceiveAdWithError error: Error) {
        print("error message: " + error.localizedDescription)
    }
}
```
{% endtab %}
{% endtabs %}
