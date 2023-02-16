# Load an ad

Implementing native ads in your app following steps:

* ****[**Build an AdLoader**](load-an-ad.md#build-an-adloader)****
* ****[**Build an AdRequest**](load-an-ad.md#build-an-adrequest)****
* ****[**Loading ads**](load-an-ad.md#loading-ads)****

### Build an AdLoader

{% hint style="info" %}
**Key Point:** Make sure all call to the AdMob SDK on the main thread.
{% endhint %}

{% hint style="warning" %}
**Notice:** In the constructor for a new ad object (for example, **`AdView`** or **`AdLoader`**), you must pass in an object of type Context. This Context is passed on to other ad networks when using mediation. Some ad networks require a more restrictive Context that is of type Activity and may not be able to serve ads without an Activity instance. Therefore, we recommend passing in an Activity instance when initializing ad objects to ensure a consistent experience with your mediated ad networks.
{% endhint %}

The following code demonstrates how to build an **`AdLoader`** that can load native ads:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val adLoader = AdLoader
    .Builder(context, "[Your AdMob AdUnit]")
    .forNativeAd { nativeAd ->
        // Show the ad.
    }
    .build()
```
{% endtab %}

{% tab title="Java" %}
```java
AdLoader adLoader = new AdLoader.Builder(context,"[Your AdMob AdUnit]")
    .forNativeAd(new NativeAd.OnNativeAdLoadedListener() {
        @Override
            public void onNativeAdLoaded(@NonNull @NotNull NativeAd nativeAd) {
                // Show the ad.
            }
        })
    .build();
```
{% endtab %}
{% endtabs %}

### Build an **AdRequest**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val bundle = Bundle()

bundle.putString(TrekAdmobDataKey.CATEGORY, "[Page Category]")//ex."news"
bundle.putString(TrekAdmobDataKey.CONTENT_URL, "[Page Url]")//ex."https://agirls.aotter.net/"
bundle.putString(TrekAdmobDataKey.CONTENT_TITLE, "[Page Title]")//ex."電獺少女"

val adRequest = AdRequest
    .Builder()
    .addNetworkExtrasBundle(TrekAdmobCustomEventNative::class.java, bundle)
    .build()
```
{% endtab %}

{% tab title="Java" %}
```java
Bundle bundle = new Bundle();

bundle.putString(TrekAdmobDataKey.CATEGORY, "[Page Category]");//ex."news"
bundle.putString(TrekAdmobDataKey.CONTENT_URL, "[Page Url]");//ex."https://agirls.aotter.net/"
bundle.putString(TrekAdmobDataKey.CONTENT_TITLE, "[Page Title]");//ex."電獺少女"

AdRequest adRequest = new AdRequest
    .Builder()
    .addNetworkExtrasBundle(TrekAdmobCustomEventNative.class, bundle)
    .build();
```
{% endtab %}
{% endtabs %}

### **Loading ads**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
adLoader.loadAd(adRequest)
```
{% endtab %}

{% tab title="Java" %}
```java
adLoader.loadAd(adRequest);
```
{% endtab %}
{% endtabs %}
