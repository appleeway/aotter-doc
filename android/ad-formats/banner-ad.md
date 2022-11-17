# Banner Ad

Follow these steps to build a banner ad layout and then requests it.

Step 1: [Create TrekBannerAdView](banner-ad.md#step-1-create-banner-ad-layout)\
Step 2: [How to build and request ad](banner-ad.md#step-2-how-to-build-and-request-ad)&#x20;

### Step 1: Create TrekBannerAdView

```xml
<com.aotter.net.trek.ads.TrekBannerAdView
        android:id="@+id/trekBannerAdView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent">
</com.aotter.net.trek.ads.TrekBannerAdView>
```

### Step 2: How to build and request ad&#x20;

**Set PlaceUid**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
viewBinding.trekBannerAdView.setPlaceUid("YOUR_UUID")//Ex."0000-12345-6789-000"
```
{% endtab %}

{% tab title="Java" %}
```java
viewBinding.trekBannerAdView.setPlaceUid("YOUR_UUID");//Ex."0000-12345-6789-000"
```
{% endtab %}
{% endtabs %}

**Create TrekAdListener**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
private val trekAdListener = object : TrekAdListener {
        override fun onAdFailedToLoad(message: String) {
            super.onAdFailedToLoad(message)
            //ad error
        }

        override fun onAdLoaded(trekNativeAd: TrekNativeAd) {
            super.onAdLoaded(trekNativeAd)
            //sueecss get an ad data
            //trekNativeAd is an ad data.
        }

        override fun onAdClicked() {
            super.onAdClicked()

            //ad was clicked.
            
        }

        override fun onAdImpression() {
            super.onAdImpression()
            
            //ad has been displayed.

        }
    }
```
{% endtab %}

{% tab title="Java" %}
```java
private TrekAdListener trekAdListener = new TrekAdListener(){

        @Override
        public void onAdImpression() {
                //ad has been displayed.
        }

        @Override
        public void onAdClicked() {
                //ad was clicked.
        }

        @Override
        public void onAdLoaded(@NonNull TrekNativeAd trekNativeAd) {
             //sueecss get an ad data
            //trekNativeAd is an ad data.
        }

        @Override
        public void onAdFailedToLoad(@NonNull String message) {
              //ad error  
        }
    };
```
{% endtab %}
{% endtabs %}

**Create TrekAdRequest**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val trekAdRequest = TrekAdRequest
            .Builder()
            //The setCategory()、setContentUrl()、setContentTitle() method is optional. You can skip it if you don't want to set it.
            .setCategory("YOUR_CATEGORY_STRING_WHICH_YOU_WANT")//Ex."news"
            .setContentUrl("YOUR_CONTENT_URL_STRING_WHICH_YOU_WANT")//Ex."https://agirls.aotter.net/"
            .setContentTitle("YOUR_CONTENT_TITLE_WHICH_YOU_WANT")//Ex."電獺少女"
            .build()
```
{% endtab %}

{% tab title="Java" %}
```java
TrekAdRequest trekAdRequest = new TrekAdRequest
            .Builder()
            //The setCategory()、setContentUrl()、setContentTitle() method is optional. You can skip it if you don't want to set it.
            .setCategory("YOUR_CATEGORY_STRING_WHICH_YOU_WANT")//Ex."news"
            .setContentUrl("YOUR_CONTENT_URL_STRING_WHICH_YOU_WANT")//Ex."https://agirls.aotter.net/"
            .setContentTitle("YOUR_CONTENT_TITLE_WHICH_YOU_WANT")//Ex."電獺少女"
            .build();
```
{% endtab %}
{% endtabs %}

**Load ad**

{% hint style="info" %}
If request ad is  success , TrekBannerAdView is going to render view automatically.
{% endhint %}

{% tabs %}
{% tab title="Kotlin" %}
```kotlin

//autoRefresh's default value is false
viewBinding.trekBannerAdView.autoRefresh = true

//refresh each every time 
//RefreshTime.REFRESH_TIME_15000_MS , 15 sec
//RefreshTime.REFRESH_TIME_30000_MS , 30 sec
//RefreshTime.REFRESH_TIME_60000_MS , 60 sec
viewBinding.trekBannerAdView.refreshTime = RefreshTime.REFRESH_TIME_15000_MS

viewBinding.trekBannerAdView.loadAd(trekAdRequest)
```
{% endtab %}

{% tab title="Java" %}
```java
//autoRefresh's default value is false
viewBinding.trekBannerAdView.autoRefresh = true;

//refresh each every time 
//RefreshTime.REFRESH_TIME_15000_MS , 15 sec
//RefreshTime.REFRESH_TIME_30000_MS , 30 sec
//RefreshTime.REFRESH_TIME_60000_MS , 60 sec
viewBinding.trekBannerAdView.refreshTime = RefreshTime.REFRESH_TIME_15000_MS;

viewBinding.trekBannerAdView.loadAd(trekAdRequest);
```
{% endtab %}
{% endtabs %}
