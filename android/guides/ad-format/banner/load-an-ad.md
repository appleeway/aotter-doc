# Load an ad

## Implementing banner ads in your app following steps:

#### **Step 1.**[**Add TrekBannerAdView to layout**](load-an-ad.md#add-trekbanneradview-to-layout)****

#### **Step 2.**[**Loading ads**](load-an-ad.md#loading-ads)****

#### **Step 3.**[**Destroy ad**](load-an-ad.md#destroy-ad)****

### [Add **`TrekBannerAdView`** to layout](load-an-ad.md#step-1.add-trekbanneradview-to-layout)

The first step toward displaying a banner is to place **`TrekBannerAdView`** in the layout for the **`Activity`** or **`Fragment`** in which you'd like to display it. &#x20;

Here's an example that shows an activity's **`TrekBannerAdView`**:

```xml
<com.aotter.net.trek.ads.TrekBannerAdView
    android:id="@+id/trekBannerAdView"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
/>
```

### ****[**Loading ads**](load-an-ad.md#step-2.loading-ads)****

{% hint style="info" %}
If request ad is  success , TrekBannerAdView is going to render view automatically.
{% endhint %}

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
viewBinding.trekBannerAdView.setPlaceUid("[Your Trek Banner PlaceUid]")

//preload's default value is false
viewBinding.trekBannerAdView.preload = true

//autoRefresh's default value is false
viewBinding.trekBannerAdView.autoRefresh = true

//refresh each every time 
//RefreshTime.REFRESH_TIME_15000_MS , 15 sec
//RefreshTime.REFRESH_TIME_30000_MS , 30 sec
//RefreshTime.REFRESH_TIME_60000_MS , 60 sec
viewBinding.trekBannerAdView.refreshTime = RefreshTime.REFRESH_TIME_30000_MS

viewBinding.trekBannerAdView.setAdListener(object : TrekAdListener {
    override fun onAdFailedToLoad(message: String) {
    
    }
    override fun onAdLoaded(trekNativeAd: TrekNativeAd) {
    
    }
    override fun onAdClicked() {
    
    }
    override fun onAdImpression() {
    
    }
})

val trekAdRequest = TrekAdRequest.Builder()
    .setCategory("[your category string]")//Ex."news"
    .setContentUrl("[your content url string]")//Ex."https://agirls.aotter.net/"
    .setContentTitle("[your content title string]")//Ex."電獺少女"
    .build()
    
viewBinding.trekBannerAdView.loadAd(trekAdRequest)
```
{% endtab %}

{% tab title="Java" %}
```java
viewBinding.trekBannerAdView.setPlaceUid("[Your Trek Banner PlaceUid]");

//preload's default value is false
viewBinding.trekBannerAdView.preload = true;

//autoRefresh's default value is false
viewBinding.trekBannerAdView.autoRefresh = true;

//refresh each every time 
//RefreshTime.REFRESH_TIME_15000_MS , 15 sec
//RefreshTime.REFRESH_TIME_30000_MS , 30 sec
//RefreshTime.REFRESH_TIME_60000_MS , 60 sec
viewBinding.trekBannerAdView.refreshTime = RefreshTime.REFRESH_TIME_30000_MS;

viewBinding.trekBannerAdView.setAdListener(new TrekAdListener(){
    @override
    public void onAdFailedToLoad(String message) {
    
    }
    @override
    public void onAdLoaded(TrekNativeAd trekNativeAd) {
    
    }
    @override
    public void onAdClicked() {
    
    }
    @override
    public void onAdImpression() {
    
    }
});

val trekAdRequest = TrekAdRequest.Builder()
    .setCategory("[your category string]")//Ex."news"
    .setContentUrl("[your content url string]")//Ex."https://agirls.aotter.net/"
    .setContentTitle("[your content title string]")//Ex."電獺少女"
    .build();
    
viewBinding.trekBannerAdView.loadAd(trekAdRequest);
```
{% endtab %}
{% endtabs %}

### [Destroy ad](load-an-ad.md#step-3.destroy-ad)

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
viewBinding.trekBannerAdView.destroy()
```
{% endtab %}

{% tab title="Java" %}
```java
viewBinding.trekBannerAdView.destroy();
```
{% endtab %}
{% endtabs %}
