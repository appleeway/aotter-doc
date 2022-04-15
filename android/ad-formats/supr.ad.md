# Supr.Ad

Follow these steps to build a Supr.Ad layout and then requests it.

Step 1: [Create Supr.Ad Layout](supr.ad.md#step-1-create-supr-ad-layout)\
Step 2: [Create `trekAd` Object Instance](supr.ad.md#step-2-create-trekad-object-instance)\
Step 3: [Set Ad Status Listener Callback](supr.ad.md#step-3-set-ad-status-listener-callback)\
Step 4: [//you have to set the method that is or not get an AdData.Create `TrekAdRequest` and Request an Ad](supr.ad.md#step-4-create-trekadrequest-and-request-an-ad)\
Step 5: [Register Ad View and Set Layout](supr.ad.md#step-5-register-ad-view-and-set-layout)

### **AdData Parameter**

| Variable         | Type   | Description     | **Always have value** | Required to be displayed |
| ---------------- | ------ | --------------- | --------------------- | ------------------------ |
| `advertiserName` | String | Advertiser Name | Yes                   | Recommended              |
| `title`          | String | Ad Headline     | Yes                   | Recommended              |
| `text`           | String | Ad Text         | No, could be empty    | Recommended              |
| `callToAction`   | String | Ex: "瞭解詳情"      | Yes                   | Recommended              |

#### - isExpired

You can use this method to check if the ad is expired or not.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
adData.isExpired()
```
{% endtab %}

{% tab title="Java" %}
```java
adData.isExpired();
```
{% endtab %}
{% endtabs %}

#### - is**VideoAd**

You can use this method to check the ad is a video ad or not.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
adData.isVideoAd()
```
{% endtab %}

{% tab title="Java" %}
```java
adData.isVideoAd();
```
{% endtab %}
{% endtabs %}

### Step 1: Create Supr.Ad Layout

Build your own Supr.Ad layout or you can check out the example layout below.

#### **Example Supr.Ad layout**

```kotlin
<androidx.constraintlayout.widget.ConstraintLayout
                android:id="@+id/adContainer"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                >

                <com.aotter.net.trek.ads.TrekMediaView
                  android:id="@+id/trekMediaView"
                  android:layout_width="match_parent"
                  android:layout_height="wrap_content"
                />

</androidx.constraintlayout.widget.ConstraintLayout>
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

### Step 3: Set Ad Status Listener Callback

Please inject **TrekAdListener** interface in **setTrekAdListener** method.

{% hint style="warning" %}
Please noticed that Supr.ad includes video ad. **In the circumstance of video ad display, it will not trigger the `onAdClicked()` and `onAdImpression()` event.**&#x20;
{% endhint %}

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
​//you have to set the method that is or not get a AdData.
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
val trekAdRequest = TrekAdRequest.Builder()
        .setCategory("YOUR_CATEGORY_STRING_OF_THE_DISPLAY_PAGE")//Ex."3C"
        .setContentUrl("YOUR_URL_STRING_OF_THE_DISPLAY_PAGE")//Ex."https://agirls.aotter.net/"
        .setContentTitle("YOUR_TITLE_STRING_OF_THE_DISPLAY_PAGE")//Ex."電獺少女"
        .build()
```
{% endtab %}

{% tab title="Java" %}
```java
TrekAdRequest trekAdRequest = new TrekAdRequest.Builder()
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

### Step 5: Register Ad View and Set Layout

You need to register ads in**`onAdloaded()`**method to receive the impression and click events. More specifically, register ad view and set layout in **`TrekAdStatusListener()`** method of**`onAdLoaded`**.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
override fun onAdLoaded(adData: AdData) {
    
    val advertiserName:String = adata.advertiserName

    val title:String = adData.title
    
    val text:String = adData.text
    
    val callToAction:String = adData.callToAction
       
    //Registered an ad view
    trekAd.registerSuprAd(adContainer,trekMediaView,adData)
       
}
```
{% endtab %}

{% tab title="Java" %}
```java
@Override
public void onAdLoaded(@NotNull AdData adData) {

      String advertiserName = adData.getAdvertiserName();

      String title = adData.getTitle();

      String text = adData.getText();

      String callToAction = adData.getCallToAction();


      //Registered an ad view
      trekAd.registerSuprAd(adContainer,trekMediaView,adData);

}
```
{% endtab %}
{% endtabs %}

