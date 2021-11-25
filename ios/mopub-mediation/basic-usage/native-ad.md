# Native Ad

In this section we provide **native ad layout** for your reference.

## **Example Native Ad layout**

_- **MopubNativeAdRenderingView**_

{% tabs %}
{% tab title="MopubNativeAdRenderingView.h" %}
```objectivec
#import <Foundation/Foundation.h>
#import <UIKit/UIKit.h>

@interface MopubNativeAdRenderingView : UIView
- (void)layoutSubviews;
- (UILabel *)nativeMainTextLabel;
- (UILabel *)nativeTitleTextLabel;
- (UILabel *)nativeCallToActionTextLabel;
- (UIImageView *)nativeIconImageView;
- (UIImageView *)nativeMainImageView;
- (UIImageView *)nativePrivacyInformationIconImageView;
@end
```
{% endtab %}

{% tab title=".m" %}
```objectivec
#import "MPNativeAdRendering.h"
#import "MPNativeAdRenderingImageLoader.h"
  
@interface MopubNativeAdRenderingView()<MPNativeAdRendering>
@property (strong, nonatomic) UILabel *labelTitle;
@property (strong, nonatomic) UILabel *labelSummary;
@property (strong, nonatomic) UILabel *labelInfo;
@property (strong, nonatomic) UIImageView *iconImageView;
@property UIImageView *imageViewBackground;
@property UIView *seperator;
@end
  
@implementation MopubNativeAdRenderingView

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
    self.imageViewBackground = [[UIImageView alloc] init];
    self.seperator = [[UIView alloc] init];
    self.labelTitle = [[UILabel alloc] init];
    self.labelSummary = [[UILabel alloc] init];
    self.labelInfo = [[UILabel alloc] init];
    self.iconImageView = [[UIImageView alloc] init];
}

- (void)layoutSubviews
{
    [super layoutSubviews];
    
    [self.labelTitle setTranslatesAutoresizingMaskIntoConstraints:NO];
    [self.labelSummary setTranslatesAutoresizingMaskIntoConstraints:NO];
    [self.labelInfo setTranslatesAutoresizingMaskIntoConstraints:NO];
    [self.iconImageView setTranslatesAutoresizingMaskIntoConstraints:NO];
    [self.imageViewBackground setTranslatesAutoresizingMaskIntoConstraints:NO];
    [self.seperator setTranslatesAutoresizingMaskIntoConstraints:NO];
    
    [self.labelTitle setTextColor:[UIColor colorWithRed:63/255.0f
                                                  green:63/255.0f
                                                   blue:63/255.0f
                                                  alpha:1.0f]];
    [self.labelSummary setFont:[UIFont systemFontOfSize:12]];
    [self.labelSummary setTextColor:[UIColor colorWithRed:170/255.0f
                                                    green:170/255.0f
                                                     blue:170/255.0f
                                                    alpha:1.0f]];
    
    
    [self.labelInfo setTextColor:[UIColor colorWithRed:150/255.0f
                                                 green:150/255.0f
                                                  blue:150/255.0f
                                                 alpha:1.0f]];
    
    if(UI_USER_INTERFACE_IDIOM() == UIUserInterfaceIdiomPad) {
        [self.seperator setBackgroundColor:UIColor.whiteColor];
    }else {
        [self.seperator setBackgroundColor:[UIColor colorWithRed:171/255.0f
                                                           green:171/255.0f
                                                            blue:171/255.0f
                                                           alpha:0.4f]];
    }
    
    [self.labelTitle setNumberOfLines:2];
    [self.labelSummary setNumberOfLines:2];
    [self.imageViewBackground setBackgroundColor:UIColor.whiteColor];
        
    [self addSubview:self.imageViewBackground];
    [self addSubview:self.labelTitle];
    [self addSubview:self.labelSummary];
    [self addSubview:self.labelInfo];
    [self addSubview:self.iconImageView];
    [self addSubview:self.seperator];
    
    
    NSDictionary *views = @{@"labelTitle": self.labelTitle,
                            @"labelSummary": self.labelSummary,
                            @"labelInfo": self.labelInfo,
                            @"iconImageView": self.iconImageView,
                            @"imageViewBackground": self.imageViewBackground,
                            @"seperator": self.seperator};
    
    NSArray *constraits = @[];
    
    if(UI_USER_INTERFACE_IDIOM() == UIUserInterfaceIdiomPad) {
        constraits = [constraits arrayByAddingObjectsFromArray:[NSLayoutConstraint constraintsWithVisualFormat:@"H:|-0-[imageViewBackground]-0-|" options:0 metrics:nil views:views]];
        constraits = [constraits arrayByAddingObjectsFromArray:[NSLayoutConstraint constraintsWithVisualFormat:@"H:|-5-[iconImageView(100@500)]" options:0 metrics:nil views:views]];
    }else {
        constraits = [constraits arrayByAddingObjectsFromArray:[NSLayoutConstraint constraintsWithVisualFormat:@"H:|-3-[imageViewBackground]-3-|" options:0 metrics:nil views:views]];
        constraits = [constraits arrayByAddingObjectsFromArray:[NSLayoutConstraint constraintsWithVisualFormat:@"H:|-5-[iconImageView(100)]" options:0 metrics:nil views:views]];
    }
    
    constraits = [constraits arrayByAddingObjectsFromArray:[NSLayoutConstraint constraintsWithVisualFormat:@"V:|-0-[imageViewBackground]-0-|" options:0 metrics:nil views:views]];
    constraits = [constraits arrayByAddingObjectsFromArray:[NSLayoutConstraint constraintsWithVisualFormat:@"V:|-5-[iconImageView]-5-|" options:0 metrics:nil views:views]];
    constraits = [constraits arrayByAddingObjectsFromArray:[NSLayoutConstraint constraintsWithVisualFormat:@"H:[iconImageView]-6-[labelTitle]-11-|" options:0 metrics:nil views:views]];
    constraits = [constraits arrayByAddingObjectsFromArray:[NSLayoutConstraint constraintsWithVisualFormat:@"V:|-2-[labelTitle]" options:0 metrics:nil views:views]];
    constraits = [constraits arrayByAddingObjectsFromArray:[NSLayoutConstraint constraintsWithVisualFormat:@"V:[labelTitle]-4-[labelSummary]-(>=2)-[labelInfo]-2-[seperator(1)]-0-|" options:NSLayoutFormatAlignAllLeading | NSLayoutFormatAlignAllTrailing metrics:nil views:views]];
    constraits = [constraits arrayByAddingObjectsFromArray:[NSLayoutConstraint constraintsWithVisualFormat:@"H:[iconImageView]-(>=0)-[seperator]" options:0 metrics:nil views:views]];
    constraits = [constraits arrayByAddingObject:[NSLayoutConstraint constraintWithItem:self.iconImageView attribute:NSLayoutAttributeWidth relatedBy:NSLayoutRelationEqual toItem:self.iconImageView attribute:NSLayoutAttributeHeight multiplier:1.0f constant:0.0f]];
    
    [NSLayoutConstraint activateConstraints:constraits];
    
}

- (UILabel *)nativeMainTextLabel
{
    return self.labelSummary;
}

- (UILabel *)nativeTitleTextLabel
{
    return self.labelTitle;
}

- (UILabel *)nativeCallToActionTextLabel
{
    return nil;
}

- (UIImageView *)nativeIconImageView
{
    return self.iconImageView;
}

- (UIImageView *)nativeMainImageView
{
    return nil;
}

- (UIImageView *)nativePrivacyInformationIconImageView
{
    return nil;
}

-(void)layoutCustomAssetsWithProperties:(NSDictionary *)customProperties imageLoader:(MPNativeAdRenderingImageLoader *)imageLoader{
    
    NSLog(@"[RenderingView TableViewCell for MopubNativeAd] layoutCustomAssetsWithProperties: %@",         customProperties);
    
    //NSString *callToActionString = customProperties[@"ctatext"];    
    //NSString *iconImage = customProperties[@"img_icon"];        // 82x82
    //NSString *mainImage = customProperties[@"mainimage"];       // 1200x628
    NSString *titleString = customProperties[@"title"];
    NSString *textString = customProperties[@"text"];
    NSString *iconHDImage  = customProperties[@"iconimage"];      // 300x300
    NSString *advertiserName = customProperties[@"advertiserName"];
    NSString *sponsored = customProperties[@"sponser"];
    
    self.labelTitle.text = titleString;
    self.labelSummary.text = textString;
    if(advertiserName && [advertiserName length]>0){
        self.labelInfo.text = [NSString stringWithFormat:@"%@ | %@",sponsored,advertiserName];
    }
    else{
        self.labelInfo.text = [NSString stringWithFormat:@"%@",sponsored];
    }
    
    [imageLoader loadImageForURL:[NSURL URLWithString:iconHDImage] intoImageView:self.iconImageView];
    
}

@endo
```
{% endtab %}
{% endtabs %}

_**- MopubNativeAdTableViewCell**_

{% tabs %}
{% tab title="MopubNativeAdTableViewCell.h" %}
```objectivec
#import <UIKit/UIKit.h>

NS_ASSUME_NONNULL_BEGIN

@interface MopubNativeAdTableViewCell : UITableViewCell
- (void)setupNativeAdView:(UIView *)nativeAdView;
@end

NS_ASSUME_NONNULL_END
```
{% endtab %}

{% tab title=".m" %}
```objectivec
#import "MopubNativeAdTableViewCell.h"

@implementation MopubNativeAdTableViewCell

- (void)awakeFromNib {
    [super awakeFromNib];
    // Initialization code
}

- (void)setSelected:(BOOL)selected animated:(BOOL)animated {
    [super setSelected:selected animated:animated];

    // Configure the view for the selected state
}

- (void)setupNativeAdView:(UIView *)nativeAdView {
    [self.contentView addSubview:nativeAdView];
    
    [nativeAdView setTranslatesAutoresizingMaskIntoConstraints:NO];
    
    [nativeAdView setTranslatesAutoresizingMaskIntoConstraints:NO];
    [nativeAdView.leadingAnchor constraintEqualToAnchor:self.contentView.leadingAnchor].active = YES;
    [nativeAdView.trailingAnchor constraintEqualToAnchor:self.contentView.trailingAnchor].active = YES;
    [nativeAdView.topAnchor constraintEqualToAnchor:self.contentView.topAnchor].active = YES;
    [nativeAdView.bottomAnchor constraintEqualToAnchor:self.contentView.bottomAnchor].active = YES;
}

@end
```
{% endtab %}

{% tab title=".xib" %}
![](<../../../.gitbook/assets/截圖 2021-09-01 上午10.39.05.png>)
{% endtab %}
{% endtabs %}

#### &#x20;- _ViewController_

{% tabs %}
{% tab title="ViewController.m" %}
```objectivec
#import "ViewController.h"
#import <MoPubSDK/MoPub.h>
#import "AotterTrekNativeAdRenderer.h"
#import "MopubNativeAdRenderingView.h"
#import "MopubNativeAdTableViewCell.h"

static NSInteger nativeAdPosition = 5;

@interface ViewController () <UITableViewDataSource, UITableViewDelegate>

@property (weak, nonatomic) IBOutlet UITableView *adTableView;
@property (strong, nonatomic) UIRefreshControl *refreshControl;
@property (strong, nonatomic) MPNativeAd *nativeAd;
@property (strong, nonatomic) UIView *nativeAdView;
@property (strong, nonatomic) MPNativeAdRequest *nativeAdRequest;

@end

@implementation ViewController

- (void)viewDidLoad {
    [super viewDidLoad];
    // Do any additional setup after loading the view.

    [self setupTableVie];
    [self setupRefreshControl];
}

- (void)viewDidAppear:(BOOL)animated {
    [super viewDidAppear:animated];
    
    [self configuareMoPubNativeAd];
}

#pragma mark : Setup TableView

- (void)setupTableVie {
    
    self.adTableView.dataSource = self;
    self.adTableView.delegate = self;
    
    [self.adTableView registerClass:UITableViewCell.class forCellReuseIdentifier:@"Cell"];
    
    [self.adTableView registerNib:[UINib nibWithNibName:@"MopubNativeAdTableViewCell" bundle:nil] forCellReuseIdentifier:@"MopubNativeAdTableViewCell"];
}

- (void)setupRefreshControl {
    self.refreshControl = [[UIRefreshControl alloc]init];
    
    [self.refreshControl addTarget:self action:@selector(onRefreshTable) forControlEvents:UIControlEventValueChanged];
    [self.adTableView addSubview:self.refreshControl];
}

#pragma mark : Configuare MoPub Native Ad

-(void) configuareMoPubNativeAd {
    
    NSString *nativeAdUnitId = @"You MoPub NativeAd Ad Unit";
    
    MPStaticNativeAdRendererSettings *settings = [[MPStaticNativeAdRendererSettings alloc] init];
    settings.renderingViewClass = [MopubNativeAdRenderingView class];
    
    settings.viewSizeHandler = ^(CGFloat maximumWidth) {
        return CGSizeMake(maximumWidth, 120.0f);
    };
    
    //MPNativeAdRendererConfiguration *config_mpNative = [MPStaticNativeAdRenderer rendererConfigurationWithRendererSettings:settings];
    //config_mpNative.supportedCustomEvents = @[@"MPMoPubNativeCustomEvent"]
    
    MPNativeAdRendererConfiguration *config_trek = [AotterTrekNativeAdRenderer rendererConfigurationWithRendererSettings:settings];
    
    
    _nativeAdRequest = [MPNativeAdRequest requestWithAdUnitIdentifier:nativeAdUnitId
                                                           rendererConfigurations:@[config_trek]];
    

    MPNativeAdRequestTargeting *targeting = [MPNativeAdRequestTargeting targeting];
    targeting.desiredAssets = [NSSet setWithObjects:kAdTitleKey, kAdTextKey, kAdMainImageKey, kAdIconImageKey, kAdCTATextKey, nil];
    // FIll in categories like "news"、"movie" at CATEGORIES
    targeting.localExtras = @{@"category": @"CATEGORIES"};
    
    _nativeAdRequest.targeting = targeting;
    
    [_nativeAdRequest startWithCompletionHandler:^(MPNativeAdRequest *request, MPNativeAd *response, NSError *error) {
        
        self->_nativeAd = response;
        self->_nativeAdView = [response retrieveAdViewWithError:nil];
        self.nativeAd = response;
        self->_nativeAdView.frame = CGRectMake(0,self.view.center.y, UIScreen.mainScreen.bounds.size.width,120);
        
        NSLog(@"start Load MPadReuest finished, retrieved View class: %@", [self->_nativeAdView class]);
        NSLog(@"response.properties: %@", response.properties);
        NSLog(@"error: %@", error.description);
        
        [self.adTableView reloadData];

    }];
}


#pragma mark - Action

- (void)onRefreshTable {
    [self.refreshControl beginRefreshing];
    
    if (_nativeAd != nil) {
        _nativeAd = nil;
    }
    
    [self configuareMoPubNativeAd];

    [self.refreshControl endRefreshing];
}

#pragma mark - UITableViewDataSource

- (NSInteger)numberOfSectionsInTableView:(UITableView *)tableView {
    return 1;
}

- (NSInteger)tableView:(UITableView *)tableView numberOfRowsInSection:(NSInteger)section {
    return 30;
}

- (UITableViewCell *)tableView:(UITableView *)tableView cellForRowAtIndexPath:(NSIndexPath *)indexPath {
    
    if (indexPath.row == nativeAdPosition) {
        if (_nativeAd != nil && _nativeAdView != nil) {
            MopubNativeAdTableViewCell *mopubNativeAdTableViewCell = [tableView dequeueReusableCellWithIdentifier:@"MopubNativeAdTableViewCell" forIndexPath:indexPath];
            [mopubNativeAdTableViewCell setupNativeAdView:_nativeAdView];
            return mopubNativeAdTableViewCell;
        }
    }
    
    UITableViewCell *cell = [tableView dequeueReusableCellWithIdentifier:@"Cell" forIndexPath:indexPath];
    cell.textLabel.text = [[NSString alloc]initWithFormat:@"index:%ld",(long)indexPath.row];
    return  cell;
}


#pragma mark - UITableViewDelegate

- (CGFloat)tableView:(UITableView *)tableView heightForRowAtIndexPath:(NSIndexPath *)indexPath {
    
    if (indexPath.row == nativeAdPosition) {
        return _nativeAd == nil ? 0:120;
    }
    
    return 80;
}



@end
```
{% endtab %}
{% endtabs %}
