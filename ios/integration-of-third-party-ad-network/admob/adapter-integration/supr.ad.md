# Supr.Ad

Follow these steps to build a Supr.Ad layout and then requests it.

Step 1: [Initialize AotterTrek SDK ](broken-reference)\
Step 2: [Customize _TableViewCell_ / _CollectionViewCell_ / _ViewController_](broken-reference)

{% hint style="info" %}
When executing Supr.Ad, a multimedia ad, you might receive video ads. You might not like the audio of the video ad to intervene in your user's background music. Moreover, If your app combines various audio playing conditions, it is recommended to choose [the category](https://developer.apple.com/documentation/avfaudio/avaudiosessioncategory) that most accurately describes the audio behavior you want.&#x20;

In the code snippet above, we choose `AVAudioSessionCategoryAmbient` which means audio from other apps mixes with audio from ads.
{% endhint %}

{% hint style="warning" %}
Notice: If your project is based on Swift, please import _Aotter-iOS-SDK.h_ in the bridge file.
{% endhint %}

```swift
#import <AotterTrek-iOS-SDK/AotterTrek-iOS-SDK.h>
```

### Step 1: Initialize AotterTrek SDK&#x20;

_File: AppDelegate.m_

{% tabs %}
{% tab title="Objective-C" %}
```objectivec
File:Appdelegate.m

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

### Step 2: Customize TableViewCell / CollectionViewCell / ViewController

Here we customize **TableViewCell** : `TrekNativeAdTableViewCell`

{% hint style="warning" %}
**Note:** **View Class** depends on the GoogleMobileAds SDK version\
GoogleMobileAds SDK version 8 and above: `GADNativeAdView`&#x20;
{% endhint %}

![](../../../../.gitbook/assets/109942288-03671200-7d0f-11eb-8606-f5689a98ecec.png)

**- TrekNativeAdTableViewCell**

{% tabs %}
{% tab title="TrekNativeAdTableViewCell.h" %}
\- **GoogleMobileAds SDK version 8 and above**

```swift
#import <UIKit/UIKit.h>
#import <AotterTrek-iOS-SDK/AotterTrek-iOS-SDK.h>
#import <GoogleMobileAds/GoogleMobileAds.h>
#import <SDWebImage/SDWebImage.h>

NS_ASSUME_NONNULL_BEGIN

@interface TrekNativeAdTableViewCell : UITableViewCell
@property(nonatomic, strong) GADNativeAdView *nativeAdView; 

- (void)setGADNativeAdData:(GADNativeAd *)nativeAd withViewSize:(CGSize)size;

@end

NS_ASSUME_NONNULL_END
```
{% endtab %}

{% tab title="TrekNativeAdTableViewCell.m" %}
### Declare data method

#### - **GoogleMobileAds SDK version 8 and above** <a href="#declare-a-gadunifiednativead-data-method" id="declare-a-gadunifiednativead-data-method"></a>

```swift
- (void)setGADNativeAdData:(GADNativeAd *)nativeAd withViewSize:(CGSize)size {
    
    for (UIView *subView in self.contentView.subviews) {
        [subView removeFromSuperview];
    }

    CGRect rect = CGRectMake(0, 0, size.width, size.height);
    GADMediaView *gADMediaView = [[GADMediaView alloc]initWithFrame:rect];
    gADMediaView.mediaContent = nativeAd.mediaContent;
    [self.contentView addSubview:gADMediaView];

    [gADMediaView setTranslatesAutoresizingMaskIntoConstraints:NO];

    [gADMediaView setTranslatesAutoresizingMaskIntoConstraints:NO];
    [gADMediaView.leadingAnchor constraintEqualToAnchor:self.contentView.leadingAnchor].active = YES;
    [gADMediaView.trailingAnchor constraintEqualToAnchor:self.contentView.trailingAnchor].active = YES;
    [gADMediaView.topAnchor constraintEqualToAnchor:self.contentView.topAnchor].active = YES;
    [gADMediaView.bottomAnchor constraintEqualToAnchor:self.contentView.bottomAnchor].active = YES;
}
```
{% endtab %}

{% tab title="TrekNativeAdTableViewCell.xib" %}
![TrekNativeAdTableViewCell](../../../../.gitbook/assets/109943071-c2233200-7d0f-11eb-894f-2ccd4ff701ee.png)
{% endtab %}

{% tab title="Swift" %}
```swift
func setGADNativeAdData(_ nativeAd: GADNativeAd){
        let nibObject = NSBundle.main.loadNibNamed("UniedNativeAdView", owner: nil)
        self.setAdView(nibObject?.first)
        
        self.nativeAdView?.iconView?.image = nativeAd.icon.image
        self.nativeAdView?.headlineView?.text = nativeAd.headline
        self.nativeAdView?.bodyView?.text = nativeAd.body
        self.nativeAdView?.advertiserView?.text = nativeAd.advertiser
        self.nativeAdView?.nativeAd = nativeAd
        
        self.addSubview(self.nativeAdView)
    }
    
    func setAdView(_ view:UIView){
        // Remove previous ad view.
        self.nativeAdView?.removeFromSuperview()
        self.nativeAdView = view;

        // Add new ad view and set constraints to fill its container.
        self.addSubview(view)
        self.nativeAdView?.translatesAutoresizingMaskIntoConstraints = false
        
        let viewDictionary = _NSDictionaryOfVariableBindings(self.nativeAdView)
        self.addConstraint(NSLayoutConstraint.constraints(withVisualFormat: "H:|[_nativeAdView]|", metrics: nil, views: viewDictionary))
        self.addConstraint(NSLayoutConstraint.constraints(withVisualFormat: "V:|[_nativeAdView]|", metrics: nil, views: viewDictionary))
    }
```
{% endtab %}
{% endtabs %}

\- **YourViewController**

{% tabs %}
{% tab title="YourViewController.m" %}
#### **- GoogleMobileAds SDK version 8 and above**

```swift
// Define the display position of the ad in the TableView
static NSInteger googleMediationSuprAdPosition = 8;
.
.
.
@interface SuprAdViewController ()<GADNativeAdLoaderDelegate, UITableViewDataSource, UITableViewDelegate> {
    
    GADNativeAd *_gADUnifiedSuprAd;
    UIView *_suprAdView;
}

@property UIRefreshControl *refreshControl;
@property (atomic, strong) GADAdLoader *adLoader;
@property (weak, nonatomic) IBOutlet UITableView *suprAdTableView;

@end

@implementation YourViewController

- (void)viewDidLoad {
    [super viewDidLoad];
  
    [self setupTableVie];
    [self setupRefreshControl];
    [self setupGADAdLoader];
}

#pragma mark : Setup TableView

- (void)setupTableVie {
    self.suprAdTableView.dataSource = self;
    self.suprAdTableView.delegate = self;
    
    
    [self.suprAdTableView registerClass:UITableViewCell.class forCellReuseIdentifier:@"Cell"];
    
    [self.suprAdTableView registerNib:[UINib nibWithNibName:@"TrekSuprAdTableViewCell" bundle:nil] forCellReuseIdentifier:@"TrekSuprAdTableViewCell"];
}

- (void)setupRefreshControl {
    self.refreshControl = [[UIRefreshControl alloc]init];
    
    [self.refreshControl addTarget:self action:@selector(onRefreshTable) forControlEvents:UIControlEventValueChanged];
    [self.suprAdTableView addSubview:self.refreshControl];
}

#pragma mark : Setup GADAdLoader

- (void)setupGADAdLoader {
    
    // GoogleMobileAds version 8 above
    self.adLoader = [[GADAdLoader alloc]initWithAdUnitID: @"<Your adUnit Id>"
                                      rootViewController: self
                                                 adTypes: @[kGADAdLoaderAdTypeNative]
                                                 options: @[]];
    
    self.adLoader.delegate = self;

    [self adLoaderLoadRequest];
}

- (void)adLoaderLoadRequest {
    GADRequest *request = [GADRequest request];
    GADCustomEventExtras *extra = [[GADCustomEventExtras alloc] init];
    // FIll in categories like "news"、"movie" at CATEGORIES
    [extra setExtras:@{@"category":@"CATEGORIES"} forLabel:@"AotterTrekGADCustomEventNativeAd"]; //label must be same as your mediation class name, AotterTrekGADMediaAdapter or AotterTrekGADCustomEventNativeAd.
    [request registerAdNetworkExtras:extra];
}

#pragma mark - UITableViewDataSource

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {
    return 30;
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {
    if (indexPath.row == googleMediationSuprAdPosition) {
        if(_gADUnifiedSuprAd != nil) {
            TrekSuprAdTableViewCell *trekSuprAdTableViewCell = [tableView dequeueReusableCellWithIdentifier:@"TrekSuprAdTableViewCell" forIndexPath:indexPath];
            
            if ([[_gADUnifiedSuprAd.extraAssets allKeys]containsObject:@"adSizeWidth"] &&
                [[_gADUnifiedSuprAd.extraAssets allKeys]containsObject:@"adSizeHeight"]) {
                
                // get ad prefered AdSize
                NSString *width = _gADUnifiedSuprAd.extraAssets[@"adSizeWidth"];
                NSString *height = _gADUnifiedSuprAd.extraAssets[@"adSizeHeight"];
                double adSizeWidth = [width doubleValue];
                double adSizeHeight = [height doubleValue];

                CGFloat viewWidth = UIScreen.mainScreen.bounds.size.width;
                CGFloat viewHeight = viewWidth * adSizeHeight/adSizeWidth;
                int adheight = (int)viewHeight;
                CGSize preferedMediaViewSize = CGSizeMake(viewWidth, adheight);
                
                [trekSuprAdTableViewCell setGADNativeAdData:_gADUnifiedSuprAd withViewSize:preferedMediaViewSize];
            }
            
            return trekSuprAdTableViewCell;
        }
    }
    
    
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"Cell" forIndexPath:indexPath];
    cell.textLabel.text = [[NSString alloc]initWithFormat:@"index:%ld",(long)indexPath.row];
    return  cell;
}

#pragma mark - UITableViewDelegate

- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath {

    if (indexPath.row == googleMediationSuprAdPosition) {
        if ([[_gADUnifiedSuprAd.extraAssets allKeys]containsObject:@"adSizeWidth"] &&
            [[_gADUnifiedSuprAd.extraAssets allKeys]containsObject:@"adSizeHeight"]) {
            
            // get ad prefered AdSize
            NSString *width = _gADUnifiedSuprAd.extraAssets[@"adSizeWidth"];
            NSString *height = _gADUnifiedSuprAd.extraAssets[@"adSizeHeight"];
            double adSizeWidth = [width doubleValue];
            double adSizeHeight = [height doubleValue];

            CGFloat viewWidth = UIScreen.mainScreen.bounds.size.width;
            CGFloat viewHeight = viewWidth * adSizeHeight/adSizeWidth;
            
            return _gADUnifiedSuprAd == nil ? 0:viewHeight;
        }
    }
    
    return 80;
}

// Supr.Ad need to be notified when the ad view is scrolled, 
// you should always add this method:
#pragma mark : ScrlloView delegate

- (void)scrollViewDidScroll:(UIScrollView *)scrollView {
    if (_gADUnifiedSuprAd != nil) {
        [[NSNotificationCenter defaultCenter]postNotificationName:@"SuprAdScrolled"
                                                           object:nil
                                                         userInfo:nil];
    }
}


#pragma mark - GADNativeAdLoaderDelegate

- (void)adLoader:(GADAdLoader *)adLoader didReceiveNativeAd:(GADNativeAd *)nativeAd {

    // Delegated nativeAd are able to receive its Custom Ad View，
    // This part can put nativeAd into CustomTableViewCell to get data.

    if (nativeAd != nil) {

        if ([[nativeAd.extraAssets allKeys]containsObject:@"trekAd"]) {
            NSString *adType = nativeAd.extraAssets[@"trekAd"];

            if ([adType isEqualToString:@"suprAd"]) {
                _gADUnifiedSuprAd = nativeAd;
            }
        }
    }

    [self.suprAdTableView reloadData];
}

- (void)adLoader:(GADAdLoader *)adLoader didFailToReceiveAdWithError:(NSError *)error {
    NSLog(@"Error Message:%@",error.description);
}


@end
```

{% hint style="warning" %}
Note: In`YourViewController.m` - `adLoaderLoadRequest`\
When requesting ads, the label parameter should be corresponding to the label set in the AdMob dashboard.
{% endhint %}

![](../../../../.gitbook/assets/132634590-ddef116f-0b74-4877-a218-f9c232a28045.png)

![](../../../../.gitbook/assets/132634585-ad98552e-3239-4f4d-abc4-842163179328.png)
{% endtab %}

{% tab title="Swift" %}
```swift
class YourViewController: UIViewController,GADNativeAdLoaderDelegate, UITableViewDataSource, UITableViewDelegate, UIScrollViewDelegate{
    var gADUnifiedNativeAd:GADNativeAd
    var refreshControl:UIRefreshControl
    var adLoader:GADAdLoader
    let nativeAdTableView:UITableView!
    
    override func viewDidLoad() {
        self.setupTableView()
        self.setupRefreshControl()
        self.setupGADAdLoader()
    }
    
    func setupTableView(){
        self.nativeAdTableView.dataSource = self
        self.nativeAdTableView.delegate = self
        self.nativeAdTableView.register(UITableViewCell.class, forCellReuseIdentifier: "Cell")
        self.nativeAdTableView.register(UINib.init(nibName: "TrekNativeAdTableViewCell", bundle: nil), forCellReuseIdentifier: "TreknativeAdTableViewCell")
    }
    
    func setupRefreshControl(){
        self.refreshControl = UIRefreshControl.init()
        self.refreshControl.addTarget(self, action: #selector(onRefreshTable), for: .touchUpInside)
        self.nativeAdTableView.addSubview(self.refreshControl)
    }
    
    func setupGADAdLoader(){
        self.adLoader = GADAdLoader.init(adUnitID: "your adUnitId id", rootViewController: self, adTypes: [GADAdLoaderAdType.native], options: [])
        self.adLoader.delegate = self
        
        var request = GADRequest.init()
        var extra = GADCustomEventExtras.init()
        extra.setExtras(["category":"CATEGORIES"], forLabel: "AotterTrekGADCustomEventNativeAd")
        //label must be same as your mediation class name, AotterTrekGADMediaAdapter or AotterTrekGADCustomEventNativeAd.
        request.register(extra)
        
        self.adLoader.load(request)
    }
    
    func adLoader(_ adLoader: GADAdLoader, didReceive nativeAd: GADNativeAd) {
        guard let adType = nativeAd.extraAssets?["trekAd"] else{
            return;
        }
        if(adType == "suprAd"){
            self.gADUnifiedNativeAd = nativeAd
        }

        self.nativeAdTableView.reloadData()
    }
    
    func scrollViewDidScroll(_ scrollView: UIScrollView) {
        if(self.gADUnifiedNativeAd){
            NotificationCenter.default.post(name: "SuprAdScrolled", object: nil)
        }
    }
}
```
{% endtab %}
{% endtabs %}

### Special Cases

There are some special cases when implementing Supr.Ad in your app. \
Please read the section [Special Cases](broken-reference)

