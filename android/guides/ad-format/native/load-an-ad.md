# Load an ad

Native ads are loaded via the **`TrekAdLoader`** class, which has its own **`Builder`** class to customize it during creation. By adding listeners to the **`TrekAdLoader`** while building it, an app specifies which types of native ads it is ready to receive. The **`TrekAdLoader`** then requests just those types.

Implementing native ads in your app following steps:

* [**Build a TrekAdLoader**](load-an-ad.md#build-an-trekadloader)****
* [**Build a TrekAdRequest**](load-an-ad.md#build-an-trekadrequest)****
* [**Loading ads**](load-an-ad.md#loading\_ads)****
* ****[**Always test with test ads**](load-an-ad.md#always\_test\_with\_test\_ads)****

### Build an TrekAdLoader

{% hint style="info" %}
**Key Point:** Make sure all call to the Trek ads SDK on the main thread.
{% endhint %}

The following code demonstrates how to build an **`TrekAdLoader`** that can load native ads:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val trekAdLoader  = TrekAdLoader.Builder(context,"[Your Trek Native or SuprAd PlaceUid]")
    .withAdListener(object:TrekAdListener {
    
        override fun onAdFailedToLoad(message: String) {
            super.onAdFailedToLoad(message)
            // Handle the failure by logging
        }
        
        override fun onAdLoaded(trekNativeAd: TrekNativeAd) {
            super.onAdLoaded(trekNativeAd)
            // Show the ad.
        }
        
        override fun onAdsFailedToLoad(messages: List<String>) {
            super.onAdsFailedToLoad(messages)
            //If you send a request for multiple,
            //please override this callback.
            // Handle the failure by logging
        }

        override fun onAdsLoaded(trekNativeAds: List<TrekNativeAd>) {
            super.onAdsLoaded(trekNativeAds)
            //If you send a request for multiple,
            //please override this callback.
            //Show the ad
        }

        override fun onAdClicked() {
            super.onAdClicked()
            //ad clicke
        }

        override fun onAdImpression() {
            super.onAdImpression()
            //ad displayed.
         }
         
    }).build()
```
{% endtab %}

{% tab title="Java" %}
```java
TrekAdLoader trekAdLoader  = new TrekAdLoader.Builder(context,"[Your Trek Native or SuprAd PlaceUid]")
    .withAdListener(new TrekAdListener(){
    
        @override
        public void onAdFailedToLoad(String message) {
            super.onAdFailedToLoad(message)
            // Handle the failure by logging
        }
        
        @override
        public void onAdLoaded(TrekNativeAd trekNativeAd) {
            super.onAdLoaded(trekNativeAd)
            // Show the ad.
        }
        
        @override
        public void onAdsFailedToLoad(List<String> messages) {
            super.onAdsFailedToLoad(messages)
            //If you send a request for multiple,
            //please override this callback.
            // Handle the failure by logging
        }

        @override
        public void onAdsLoaded(List<TrekNativeAd> trekNativeAds) {
            super.onAdsLoaded(trekNativeAds)
            //If you send a request for multiple,
            //please override this callback.
            //Show the ad
        }

        @override
        public void onAdClicked() {
            super.onAdClicked()
            //ad clicked.
        }
        
        @override
        public void onAdImpression() {
            super.onAdImpression()
            //ad displayed.
         }
         
    }).build();
```
{% endtab %}
{% endtabs %}

### Build an **TrekAdRequest**

{% hint style="info" %}
These methods are optional. You can skip it if you don't want to set it.

* **`setCategory()`**
* **`setContentUrl()`**
* **`setContentTitle()`**
{% endhint %}

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val trekAdRequest = TrekAdRequest.Builder()
    .setCategory("[your category string]")//Ex."news"
    .setContentUrl("[your content url string]")//Ex."https://agirls.aotter.net/"
    .setContentTitle("[your content title string]")//Ex."電獺少女"
    .build()
```
{% endtab %}

{% tab title="Java" %}
```java
TrekAdRequest trekAdRequest = new TrekAdRequest.Builder()
    .setCategory("[your category string]")//Ex."news"
    .setContentUrl("[your content url string]")//Ex."https://agirls.aotter.net/"
    .setContentTitle("[your content title string]")//Ex."電獺少女"
    .build();
```
{% endtab %}
{% endtabs %}

### Loading ads <a href="#loading_ads" id="loading_ads"></a>

Once you've finished building an **`TrekAdLoader`**, it's time to use it to load ads. There are two methods available for this: **`loadAd()`** and **`loadAds()`**.

The **`loadAd()`** method sends a request for a single ad:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
trekAdLoader.loadAd(trekAdRequest)
```
{% endtab %}

{% tab title="Java" %}
```java
trekAdLoader.loadAd(trekAdRequest);
```
{% endtab %}
{% endtabs %}

The **`loadAds()`** method sends a request for multiple ads (up to 5):

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
trekAdLoader.loadAds(trekAdRequest,3)
```
{% endtab %}

{% tab title="Java" %}
```java
trekAdLoader.loadAds(trekAdRequest,3);
```
{% endtab %}
{% endtabs %}

### Always test with test ads <a href="#always_test_with_test_ads" id="always_test_with_test_ads"></a>

The easiest way to load test ads is to use our test client id and test place uid for Native Advanced.

For more information about how the Trek Ads SDK's test ads work, see [**Enable test ads**](broken-reference)**.**
