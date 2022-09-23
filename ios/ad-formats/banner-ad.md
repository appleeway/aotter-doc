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

{% tabs %}
{% tab title="ObjC" %}
```objectivec
[self.myAdNative isExpired]; // YES or NO
```
{% endtab %}

{% tab title="Swift" %}
```swift
 self.myAdNative?.isExpired()
```
{% endtab %}
{% endtabs %}

* **impression & click delegate**

{% tabs %}
{% tab title="ObjC" %}
```objectivec
-(void)TKAdSuprAdWillLogImpression:(TKAdSuprAd *)ad{
    NSLog(@"TKSuprAd log when impression occur");
}

-(void)TKAdSuprAdWillLogClick:(TKAdSuprAd *)ad{
    NSLog(@"TKSuprAd log when click occur");
}
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
{% endtab %}

{% tab title="Swift" %}
```swift
class myViewController:UIViewController{
    var suprAdView:UIView?
    var suprAd:TKAdSuprAd?
    
    override func viewDidLoad() {
        self.fetchSuprAd()
    }
    
    func fetchSuprAd(){
        self.suprAd = TKAdSuprAd(place: "YOUR UUID", category: "CATEGORIES")
        self.suprAd?.delegate = self
        
        //register view controller for presenting
        self.suprAd?.registerPresenting(self)
        
        // fetch ad
        self.suprAd?.fetch()
    }
}
```
{% endtab %}
{% endtabs %}

### Step 2: Register AdView and TKMediaView

It is recommended to create the view that its size is based on ad size.

{% tabs %}
{% tab title="ObjC" %}
```objectivec
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
{% endtab %}

{% tab title="Swift" %}
```swift
func tkAdSuprAd(_ suprAd: TKAdSuprAd!, didReceivedAdWithAdData adData: [AnyHashable : Any]!, preferedMediaViewSize size: CGSize, isVideoAd: Bool) {
 
 self.suprAd = suprAd
 
 //size for the ad
 self.suprAdView = UIView.init(frame: CGRectMake(0, 0, size.width, size.height))
 
 //AdView: the container view for ad
 self.suprAd.register(self.suprAdView)
 self.suprAd.registerTKMediaView(self.suprAdView)
 
 //AutoLayout
 self.view.addSubview(self.suprAdView)
 
 self.suprAdView?.translatesAutoresizingMaskIntoConstraints = false
 self.suprAdView?.widthAnchor.constraint(equalToConstant: size.width).isActive = true
 self.suprAdView?.heightAnchor.constraint(equalToConstant: size.width).isActive = true
 self.suprAdView?.bottomAnchor.constraint(equalTo: self.view.safeAreaLayoutGuide.bottomAnchor).isActive = true
}
```
{% endtab %}
{% endtabs %}

### Step 3: Ad Loading Completion Callback

{% tabs %}
{% tab title="ObjC" %}
```objectivec
- (void)TKAdSuprAdCompleted:(TKAdSuprAd *)suprAd{
    NSLog(@"TKAdSuprAd >> Completed");
}
```
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

### Step 4: Error Callback

{% tabs %}
{% tab title="ObjC" %}
```swift
- (void)TKAdSuprAd:(TKAdSuprAd *)suprAd adError:(TKAdError *)error{
    NSLog(@"TKAdSuprAd >> adError: %@", error.message);
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

### Step 5: (Optional) Destroy Ad

This function will destroy ads completely. In the condition that`TKAdSuprAd`manages itself, destroy() is not necessary to be invoked. However, it is still nice to have it when you are pretty sure that this view or view controller won't be used anymore.

{% tabs %}
{% tab title="ObjC" %}
<pre class="language-objectivec"><code class="lang-objectivec">-(void)viewDidDisappear:(BOOL)animated{
<strong>  [super viewDidDisappear:animated];
</strong>  [self.suprAd destroy];
}</code></pre>
{% endtab %}

{% tab title="Swift" %}
<pre class="language-swift"><code class="lang-swift">override func viewDidDisappear(_ animated: Bool) {
<strong>    super.viewDidDisappear(animated)
</strong>    self.suprAd.destroy()
}</code></pre>
{% endtab %}
{% endtabs %}

###
