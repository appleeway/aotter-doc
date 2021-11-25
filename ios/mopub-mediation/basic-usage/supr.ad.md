# Supr.Ad

In this section we provide Supr.Ad layout for your reference.

## E**xample Supr.Ad layout**

_**- MopubSuprAdRenderingView**_

{% tabs %}
{% tab title="MopubSuprAdRenderingView.h" %}
```objectivec
#import <UIKit/UIKit.h>

NS_ASSUME_NONNULL_BEGIN

@interface MopubSuprAdRenderingView : UIView

- (UIImageView *)nativeMainImageView;

@end

NS_ASSUME_NONNULL_END

```
{% endtab %}

{% tab title=".m" %}
```objectivec
#import "MopubSuprAdRenderingView.h"
#import "MPNativeAdRendering.h"
#import "MPNativeAdRenderingImageLoader.h"

@interface MopubSuprAdRenderingView()<MPNativeAdRendering>
@property (strong, nonatomic) UIImageView *mainImageView;
@end

@implementation MopubSuprAdRenderingView

-(instancetype)initWithFrame:(CGRect)frame{
    self = [super initWithFrame:frame];
    if(self){
        [self initialUI];
    }
    
    return self;
}

-(instancetype)initWithCoder:(NSCoder *)aDecoder{
    self = [super initWithCoder:aDecoder];
    if(self){
        [self initialUI];
    }
    
    return self;
}

-(void)initialUI{
    self.mainImageView = [[UIImageView alloc] init];
}

- (UIImageView *)nativeMainImageView {
    return self.mainImageView;
}

-(void)layoutSubviews {
    [super layoutSubviews];
    
    [self addSubview:self.mainImageView];
    
    [self.mainImageView setTranslatesAutoresizingMaskIntoConstraints:NO];
    [self.mainImageView.leadingAnchor constraintEqualToAnchor:self.leadingAnchor].active = YES;
    [self.mainImageView.trailingAnchor constraintEqualToAnchor:self.trailingAnchor].active = YES;
    [self.mainImageView.topAnchor constraintEqualToAnchor:self.topAnchor].active = YES;
    [self.mainImageView.bottomAnchor constraintEqualToAnchor:self.bottomAnchor].active = YES;
}

@end

```
{% endtab %}
{% endtabs %}

_**- MopubSuprAdTableViewCell**_

{% tabs %}
{% tab title="MopubSuprAdTableViewCell.h" %}
```objectivec
#import <UIKit/UIKit.h>

NS_ASSUME_NONNULL_BEGIN

@interface MopubSuprAdTableViewCell : UITableViewCell
- (void)setupSuprAdView:(UIView *)suprAdView;
@end

NS_ASSUME_NONNULL_END
```
{% endtab %}

{% tab title=".m" %}
```objectivec
#import "MopubSuprAdTableViewCell.h"

@implementation MopubSuprAdTableViewCell

- (void)awakeFromNib {
    [super awakeFromNib];
    // Initialization code
}

- (void)setSelected:(BOOL)selected animated:(BOOL)animated {
    [super setSelected:selected animated:animated];

    // Configure the view for the selected state
}

- (void)setupSuprAdView:(UIView *)suprAdView {
    [self.contentView addSubview:suprAdView];
    
    [suprAdView setTranslatesAutoresizingMaskIntoConstraints:NO];
    
    [suprAdView setTranslatesAutoresizingMaskIntoConstraints:NO];
    [suprAdView.leadingAnchor constraintEqualToAnchor:self.contentView.leadingAnchor].active = YES;
    [suprAdView.trailingAnchor constraintEqualToAnchor:self.contentView.trailingAnchor].active = YES;
    [suprAdView.topAnchor constraintEqualToAnchor:self.contentView.topAnchor].active = YES;
    [suprAdView.bottomAnchor constraintEqualToAnchor:self.contentView.bottomAnchor].active = YES;
}

@end
```
{% endtab %}

{% tab title=".xib" %}
![](<../../../.gitbook/assets/截圖 2021-09-01 上午10.39.29.png>)
{% endtab %}
{% endtabs %}

_**- YourViewController**_

{% tabs %}
{% tab title="ViewController.m" %}
```objectivec
#import "ViewController.h"
#import <MoPubSDK/MoPub.h>
#import "AotterTrekNativeAdRenderer.h"
#import "MopubSuprAdRenderingView.h"
#import "MopubSuprAdTableViewCell.h"

static NSInteger suprAdPosition = 7;

@interface ViewController () <UITableViewDataSource, UITableViewDelegate> {
    CGFloat _viewWidth;
    CGFloat _viewHeight;
}

@property (weak, nonatomic) IBOutlet UITableView *adTableView;
@property (strong, nonatomic) UIRefreshControl *refreshControl;
@property (strong, nonatomic) MPNativeAd *suprAd;
@property (strong, nonatomic) UIView *suprAdView;
@property (strong, nonatomic) MPNativeAdRequest *suprAdRequest;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view.
    
    _viewWidth = UIScreen.mainScreen.bounds.size.width;
    _viewHeight = _viewWidth * 9/16;
    
    
    [self setupTableVie];
    [self setupRefreshControl];
}

- (void)viewDidAppear:(BOOL)animated {
    [super viewDidAppear:animated];
    
    [self configuareMoPubSuprAd];
}

#pragma mark : Setup TableView

- (void)setupTableVie {
    
    self.adTableView.dataSource = self;
    self.adTableView.delegate = self;
    
    [self.adTableView registerClass:UITableViewCell.class forCellReuseIdentifier:@"Cell"];
    
    [self.adTableView registerNib:[UINib nibWithNibName:@"MopubSuprAdTableViewCell" bundle:nil] forCellReuseIdentifier:@"MopubSuprAdTableViewCell"];
}

- (void)setupRefreshControl {
    self.refreshControl = [[UIRefreshControl alloc]init];
    
    [self.refreshControl addTarget:self action:@selector(onRefreshTable) forControlEvents:UIControlEventValueChanged];
    [self.adTableView addSubview:self.refreshControl];
}

#pragma mark : Configuare MoPub SuprAd

-(void) configuareMoPubSuprAd {
    
    // Supr Ad Test adUnit: 5e585f39d79942f88f58519070db28bf
    
    NSString *suprAdUnitId = @"You MoPub SuprAd Ad Unit";
    
    MPStaticNativeAdRendererSettings *settings = [[MPStaticNativeAdRendererSettings alloc] init];
    settings.renderingViewClass = [MopubSuprAdRenderingView class];
    
    settings.viewSizeHandler = ^(CGFloat maximumWidth) {
        return CGSizeMake(maximumWidth, CGFLOAT_MAX);
    };
    
    MPNativeAdRendererConfiguration *config_trek = [AotterTrekNativeAdRenderer rendererConfigurationWithRendererSettings:settings];
    
    
    _suprAdRequest = [MPNativeAdRequest requestWithAdUnitIdentifier:suprAdUnitId
                                                           rendererConfigurations:@[config_trek]];
    

    MPNativeAdRequestTargeting *targeting = [MPNativeAdRequestTargeting targeting];
    targeting.desiredAssets = [NSSet setWithObjects:kAdTitleKey, kAdTextKey, kAdMainImageKey, kAdIconImageKey, kAdCTATextKey, nil];
    // FIll in categories like "news"、"movie" at CATEGORIES
    targeting.localExtras = @{@"category": @"CATEGORIES"}; //@{@"category": self.category.name};
    
    _suprAdRequest.targeting = targeting;
    
    [_suprAdRequest startWithCompletionHandler:^(MPNativeAdRequest *request, MPNativeAd *response, NSError *error) {
        
        self->_suprAd = response;
        self->_suprAdView = [response retrieveAdViewWithError:nil];
        
        self->_suprAdView.frame = CGRectMake(0,self.view.center.y, UIScreen.mainScreen.bounds.size.width,UIScreen.mainScreen.bounds.size.width * 9/16);
        
        NSLog(@"start Load MPadReuest finished, retrieved View class: %@", [self->_suprAdView class]);
        NSLog(@"response.properties: %@", response.properties);
        NSLog(@"error: %@", error.description);
        
        [self.adTableView reloadData];

    }];
}


#pragma mark - Action

- (void)onRefreshTable {
    [self.refreshControl beginRefreshing];
    
    if (_suprAd != nil) {
        _suprAd = nil;
    }
    
    [self configuareMoPubSuprAd];

    [self.refreshControl endRefreshing];
}


// Supr.Ad need to be notified when the ad view is scrolled, 
// you should always add this method:
#pragma mark : ScrlloView delegate

- (void)scrollViewDidScroll:(UIScrollView *)scrollView {
    if (_suprAd != nil) {
        // The postNotificationName please fill in "SuprAdScrolled"
        [[NSNotificationCenter defaultCenter]postNotificationName:@"SuprAdScrolled"
                                                           object:self
                                                         userInfo:nil];
    }
}


#pragma mark - UITableViewDataSource

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {
    return 30;
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {

    if (indexPath.row == suprAdPosition) {
        if(_suprAd != nil && _suprAdView != nil) {
            MopubSuprAdTableViewCell *mopubSuprAdTableViewCell = [tableView dequeueReusableCellWithIdentifier:@"MopubSuprAdTableViewCell" forIndexPath:indexPath];
            [mopubSuprAdTableViewCell setupSuprAdView:_suprAdView];
            return mopubSuprAdTableViewCell;
        }
    }
    
    
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"Cell" forIndexPath:indexPath];
    cell.textLabel.text = [[NSString alloc]initWithFormat:@"index:%ld",(long)indexPath.row];
    return  cell;
}


#pragma mark - UITableViewDelegate

- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath {
    
    if (indexPath.row == suprAdPosition) {
        return _suprAd == nil ? 0:_viewHeight;
    }
    
    return 80;
}



@end
```
{% endtab %}
{% endtabs %}
