# Banner Ad

Follow these steps to build a banner ad layout and then requests it.

Step 1: [Create Banner Ad Layout](banner-ad.md#step-1-create-banner-ad-layout)\
Step 2: [Create `trekAd` Object Instance](banner-ad.md#step-2-create-trekad-object-instance)\
Step 3: [Set TrekAdListener](banner-ad.md#step-3-set-trekadlistener)\
Step 4: [Create `TrekAdRequest` and Request an Ad](banner-ad.md#step-4-create-trekadrequest-and-request-an-ad)\
Step 5: [Register Ad View and Set Layout](banner-ad.md#step-5-register-ad-view-and-set-layout)

### **AdData**

#### - isExpired

You can use this method to check if the ad is expired or not.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
adData.isExpired()
```
{% endtab %}

{% tab title="Java" %}
```
adData.isExpired();
```
{% endtab %}
{% endtabs %}

### Step 1: Create Banner Ad Layout

Build your own banner ad layout or you can check out the example layout below.

#### **Example banner ad layout**

```kotlin
<com.aotter.net.trek.ads.TrekBannerView
  android:id="@+id/trekBannerView"
  android:layout_width="match_parent"
  android:layout_height="wrap_content"
/>
```

### Step 2: Create `trekAd` Object Instance

Notice that you should initialize `AotterTrek.TrekService` before using `trekAd`, otherwise, an exception will be thrown.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
var trekAd:TrekAd = AotterTrek.trekService(context)
```
{% endtab %}

{% tab title="Java" %}
```java
TrekAd trekAd = AotterTrek.INSTANCE.trekService(context);
```
{% endtab %}
{% endtabs %}

### Step 3: Set TrekAdListener

Please inject **TrekAdListener** interface in **setTrekAdListener** method.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
//you have to set the method that is or not get a AdData.
trekAd.setTrekAdListener(object : TrekAdListener{

    override fun onAdFailedToLoad(message: String) {
       //ad error callback
    }

    override fun onAdLoaded(adData: AdData) {
       //In this callback, it means that you will receive an advertisement.
       //adData is an ad data.
    }

    override fun onAdClicked() {
       //In this callback, it means that the  ad was clicked.
    }

    override fun onAdImpression() {
       //In this callback, this means that the ad has been displayed.
    }

 })
```
{% endtab %}

{% tab title="Java" %}
```java
//you have to set the method that is or not get a AdData.
    trekAd.setTrekAdListener(new TrekAdListener() {
            @Override
            public void onAdFailedToLoad(@NotNull String message) {
                //ad error callback
            }

            @Override
            public void onAdLoaded(@NotNull AdData adData) {
                //In this callback, it means that you will receive an advertisement.
                //adData is an ad data.
            }

            @Override
            public void onAdClicked() {
                //In this callback, it means that the  ad was clicked.
            }

            @Override
            public void onAdImpression() {
                //In this callback, this means that the ad has been displayed.
            }
     });
```
{% endtab %}
{% endtabs %}

### Step 4: Create `TrekAdRequest` and Request an Ad

* **Create `TrekAdRequest`**

The **`setCategory()`, `setContentUrl()`, `setContentTitle()` ** method is optional. You can skip it if you don't want to set it.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val trekAdRequest = TrekAdRequest().Builder()
        .setCategory("YOUR_CATEGORY_STRING_OF_THE_DISPLAY_PAGE")//Ex."3C"
        .setContentUrl("YOUR_URL_STRING_OF_THE_DISPLAY_PAGE")//Ex."https://agirls.aotter.net/"
        .setContentTitle("YOUR_TITLE_STRING_OF_THE_DISPLAY_PAGE")//Ex."電獺少女"
        .build()
```
{% endtab %}

{% tab title="Java" %}
```java
TrekAdRequest trekAdRequest = new TrekAdRequest().Builder()
        .setCategory("YOUR_CATEGORY_STRING_OF_THE_DISPLAY_PAGE")//Ex."3C"
        .setContentUrl("YOUR_URL_STRING_OF_THE_DISPLAY_PAGE")//Ex."https://agirls.aotter.net/"
        .setContentTitle("YOUR_TITLE_STRING_OF_THE_DISPLAY_PAGE")//Ex."電獺少女"
        .build();
```
{% endtab %}
{% endtabs %}

* **Request an Ad**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
trekAd.setPlaceUid("YOUR_UUID").loadAd(trekAdRequest)
```
{% endtab %}

{% tab title="Java" %}
```java
trekAd.setPlaceUid("YOUR_UUID").loadAd(trekAdRequest);
```
{% endtab %}
{% endtabs %}

### Step 5: Register Ad View and Set Layout ****&#x20;

You need to register for in **onAdloaded** method ads to receive impression and click events.

In  **onAdLoaded** of **TrekAdStatusListener** method register ad view and set layout.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
override fun onAdLoaded(adData: AdData) {
    
    //Registered an ad view
    trekAd.registerBannerAd(trekBannerView,adData)
       
}
```
{% endtab %}

{% tab title="Java" %}
```java
@Override
public void onAdLoaded(@NotNull AdData adData) {

      //Registered an ad view
       trekAd.registerBannerAd(trekBannerView,adData)

}
```
{% endtab %}
{% endtabs %}
