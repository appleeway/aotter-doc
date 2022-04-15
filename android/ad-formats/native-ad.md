# Native Ad

## Add Native Ads to an Android APP

The Native Ad API allows you to build a customized experience for the ads you show in your app. When using Native Ad API, instead of receiving an ad ready to be displayed, you will receive a group of **ad parameters** such as a title, an image, a call to action, and you are able to use them to construct a custom view where the ad is shown.\
\
****Follow these steps to build a native ad layout that fits your application and then requests it.

Step 1: [Create Native Ad Layout](native-ad.md#step-1-create-native-ad-layout)\
Step 2: [Create `trekAd` Object Instance](native-ad.md#step-2-create-trekad-object-instance)\
Step 3: [Set Ad Status Listener Callback](native-ad.md#step-3-set-ad-status-listener-callback)\
Step 4: [Create `TrekAdRequest` and Request an Ad](native-ad.md#step-4-create-trekadrequest-and-request-an-ad)\
Step 5: [Register Ad View and Set Layout](native-ad.md#step-5-register-ad-view-and-set-layout)

### AdData Parameters

| Variable         | Type   | Description     |  **Always have value** |  Required to be displayed |
| ---------------- | ------ | --------------- | ---------------------- | ------------------------- |
| `advertiserName` | String | Advertiser Name | Yes                    | Recommended               |
| `title`          | String | Ad Headline     | Yes                    | Required                  |
| `text`           | String | Ad Text         | No, could be empty     | Recommended               |
| `imgMain`        | String | Size: 1200x628  | Yes                    | Recommended               |
| `imgIcon`        | String | Size: 82x82     | Yes                    | Recommended               |
| `imgIconHd`      | String | Size: 300x300   | Yes                    | Recommended               |
| `callToAction`   | String | Ex: "瞭解詳情"      | Yes                    | Recommended               |
| `sponsor`        | String | Sponsored       | Yes                    | Required                  |

![](<../../.gitbook/assets/截圖 2021-09-10 下午5.36.49.png>)

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

### Step 1: Create Native Ad Layout

Build your own native ad layout or you can check out the example layout below.

#### **Example Native Ad Layout**

```kotlin
<androidx.cardview.widget.CardView
                android:id="@+id/nativeAdView"
                android:layout_width="match_parent"
                android:layout_height="100dp"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent">

                <androidx.constraintlayout.widget.ConstraintLayout
                    android:layout_width="match_parent"
                    android:layout_height="match_parent">

                    <TextView
                        android:id="@+id/advertiser"
                        android:layout_width="0dp"
                        android:layout_height="wrap_content"
                        android:layout_marginStart="8dp"
                        android:layout_marginLeft="8dp"
                        android:layout_marginTop="8dp"
                        android:layout_marginEnd="8dp"
                        android:layout_marginRight="8dp"
                        android:text="Sponsored"
                        android:textColor="@android:color/holo_red_dark"
                        android:textSize="18sp"
                        android:textStyle="bold"
                        app:layout_constraintEnd_toEndOf="parent"
                        app:layout_constraintStart_toEndOf="@+id/adImg"
                        app:layout_constraintTop_toTopOf="parent" />

                    <TextView
                        android:id="@+id/adTitle"
                        android:layout_width="0dp"
                        android:layout_height="0dp"
                        android:layout_marginStart="8dp"
                        android:layout_marginTop="8dp"
                        android:layout_marginEnd="8dp"
                        android:layout_marginBottom="8dp"
                        android:text="TextView"
                        android:textSize="18sp"
                        android:textStyle="bold"
                        app:layout_constraintBottom_toBottomOf="parent"
                        app:layout_constraintEnd_toEndOf="parent"
                        app:layout_constraintStart_toEndOf="@+id/adImg"
                        app:layout_constraintTop_toBottomOf="@+id/advertiser" />

                    <ImageView
                        android:id="@+id/adImg"
                        android:layout_width="100dp"
                        android:layout_height="0dp"
                        app:layout_constraintBottom_toBottomOf="parent"
                        app:layout_constraintStart_toStartOf="parent"
                        app:layout_constraintTop_toTopOf="parent" />

                </androidx.constraintlayout.widget.ConstraintLayout>

            </androidx.cardview.widget.CardView>
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

You need to register for in **onAdloaded** method ads to receive impressions and click events.

In  **onAdLoaded** of **TrekAdStatusListener** method register ad view and set layout.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
override fun onAdLoaded(adData: AdData) {
    
    val advertiserName:String = adata.advertiserName

    val title:String = adData.title
    
    val text:String = adData.text
    
    var imgMain:String = adData.imgMain //size:1200x628
    
    var imgIcon:String = adData.imgIcon //size:82x82
    
    var imgIconHd:String = adData.imgIconHd //size:300x300
    
    val callToAction:String = adData.callToAction
    
    val sponsor:String = adData.sponsor
    
    //Registered an ad view
    trekAd.registerNativeAd(nativeAdView,adData)
       
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

      String imgMain = adData.getImgMain(); //size:1200x628

      String imgIcon = adData.getImgIcon(); //size:82x82

      String imgIconHd = adData.getImgIconHd(); //size:300x300

      String callToAction = adData.getCallToAction();

      String sponsor = adData.getSponsor();


      //Registered an ad view
      trekAd.registerNativeAd(context,nativeAdView,adData);

}
```
{% endtab %}
{% endtabs %}
