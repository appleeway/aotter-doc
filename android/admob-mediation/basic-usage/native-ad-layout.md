# Native Ad

Follow these steps to build a native ad layout that fits your application and then requests it.

Step 1: [Create NativeAdView](native-ad-layout.md#step-1-create-treknativeadview)\
Step 2: [How to build and request ad](native-ad-layout.md#step-2-how-to-build-and-request-ad) \
Step 3: [Render NativeAdView layout](native-ad-layout.md#step-3-render-treknativeadview-layout)

### Step 1: Create NativeAdView

{% hint style="warning" %}
**Notice: Please use NativeAdView** **as the container of your layout**
{% endhint %}

Create NativeAdView or you can check out the example layout below.

```xml
<com.google.android.gms.ads.nativead.NativeAdView
        android:id="@+id/nativeAdView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <androidx.constraintlayout.widget.ConstraintLayout
            android:layout_width="match_parent"
            android:layout_height="match_parent">

            <TextView
                android:id="@+id/advertiser"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_marginStart="8dp"
                android:layout_marginTop="8dp"
                android:layout_marginEnd="8dp"
                android:text="Sponsored"
                android:textColor="@android:color/holo_red_dark"
                android:textSize="18sp"
                android:textStyle="bold"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintStart_toEndOf="@+id/adImg"
                app:layout_constraintTop_toBottomOf="@+id/trekMediaView2" />

            <TextView
                android:id="@+id/adTitle"
                android:layout_width="0dp"
                android:layout_height="wrap_content"
                android:layout_marginTop="8dp"
                android:text="TextView"
                android:textSize="18sp"
                android:textStyle="bold"
                app:layout_constraintEnd_toEndOf="@+id/advertiser"
                app:layout_constraintStart_toStartOf="@+id/advertiser"
                app:layout_constraintTop_toBottomOf="@+id/advertiser" />

            <com.google.android.gms.ads.nativead.MediaView
                android:id="@+id/mediaView"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                app:layout_constraintDimensionRatio="16:9"
                app:layout_constraintEnd_toEndOf="parent"
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toTopOf="parent" />

            <ImageView
                android:id="@+id/adImg"
                android:layout_width="80dp"
                android:layout_height="80dp"
                android:layout_marginStart="8dp"
                android:layout_marginTop="8dp"
                android:layout_marginBottom="8dp"
                android:background="@color/purple_200"
                android:scaleType="fitXY"
                app:layout_constraintBottom_toBottomOf="parent"
                app:layout_constraintDimensionRatio=""
                app:layout_constraintStart_toStartOf="parent"
                app:layout_constraintTop_toBottomOf="@+id/trekMediaView2" />
        </androidx.constraintlayout.widget.ConstraintLayout>

    </com.google.android.gms.ads.nativead.NativeAdView>
```

### Step 2: How to build and request ad&#x20;

#### Initialize your ad object with an **context of** Activity or Fragment instance <a href="#initialize_your_ad_object_with_an_activity_instance" id="initialize_your_ad_object_with_an_activity_instance"></a>

In the constructor for a new ad object , you must pass in an object of type **`Context`**. This **`Context`**` ``` is passed on to other ad networks when using mediation. Some ad networks require a more restrictive **`Context`** that is of type **`Activity`** or **`Fragment`** and may not be able to serve ads without an **`Activity`** or **`Fragment`** instance. Therefore, we recommend passing in an context of **`Activity`** or **`Fragment`** instance when initializing ad objects to ensure a consistent experience with your mediated ad networks.

**Create AdLoader**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val adLoader = AdLoader
    .Builder(context, "YOUR_ADUNIT")
    .forNativeAd { nativeAd ->
          //successfully get an ad
     }
    .build()
```
{% endtab %}

{% tab title="Java" %}
```java
AdLoader  adLoader = new AdLoader.Builder(context,"YOUR_ADUNIT")
    .forNativeAd(new NativeAd.OnNativeAdLoadedListener() {
        @Override
        public void onNativeAdLoaded(@NonNull @NotNull NativeAd nativeAd) {
            //successfully get an ad
        }
    })
.build();
```
{% endtab %}
{% endtabs %}

**Create AdRequest**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val bundle = Bundle()

bundle.putString(TrekAdmobDataKey.CATEGORY, "YOU_CATEGORY")//ex."news"
bundle.putString(TrekAdmobDataKey.CONTENT_URL, "YOU_URL")//ex."https://agirls.aotter.net/"
bundle.putString(TrekAdmobDataKey.CONTENT_TITLE, "YOU_TITLE")//ex."電獺少女"

val adRequest = AdRequest
    .Builder()
    .addNetworkExtrasBundle(TrekAdmobCustomEventNative::class.java, bundle)
    .build()
```
{% endtab %}

{% tab title="Java" %}
```java
Bundle bundle = new Bundle();

bundle.putString(TrekAdmobDataKey.CATEGORY, "YOU_CATEGORY")//ex."news"
bundle.putString(TrekAdmobDataKey.CONTENT_URL, "YOU_URL")//ex."https://agirls.aotter.net/"
bundle.putString(TrekAdmobDataKey.CONTENT_TITLE, "YOU_TITLE")//ex."電獺少女"

AdRequest adRequest = new AdRequest
    .Builder()
    .addNetworkExtrasBundle(TrekAdmobCustomEventNative.class, bundle)
    .build();
    
```
{% endtab %}
{% endtabs %}

**Load ad**

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

### **Step 3:** Render NativeAdView layout

Render **NativeAdView** in the callback function of `forNativeAd`.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
.....

forNativeAd { nativeAd ->

   val sponsor:String = nativeAd.extras.getString(TrekAdmobDataKey.SPONSOR)?:"" 

   val mainImage:String = nativeAd.extras.getString(TrekAdmobDataKey.MAIN_IMAGE)?:"" //1200x628

   val icon:String = nativeAd.extras.getString(TrekAdmobDataKey.ICON_IMAGE)?:""//82x82

   val iconHd:String = nativeAd.extras.getString(TrekAdmobDataKey.ICON_IMAGE_HD)?:""//300x300

   viewBinding.advertiser.text = nativeAd.advertiser

   viewBinding.adTitle.text = nativeAd.body

   viewBinding.nativeAdView.headlineView = viewBinding.adTitle

   viewBinding.nativeAdView.advertiserView = viewBinding.advertiser

   viewBinding.nativeAdView.mediaView =  viewBinding.mediaView

   viewBinding.nativeAdView.setNativeAd(nativeAd)
   
}

.....
```
{% endtab %}

{% tab title="Java" %}
```java

forNativeAd { nativeAd ->

   String sponsor= nativeAd.extras.getString(TrekAdmobDataKey.SPONSOR) ;

   String mainImage = nativeAd.extras.getString(TrekAdmobDataKey.MAIN_IMAGE) ;//1200x628

   String icon = nativeAd.extras.getString(TrekAdmobDataKey.ICON_IMAGE);//82x82

   String iconHd = nativeAd.extras.getString(TrekAdmobDataKey.ICON_IMAGE_HD);//300x300

   viewBinding.advertiser.text = nativeAd.advertiser;

   viewBinding.adTitle.text = nativeAd.body;

   viewBinding.nativeAdView.headlineView = viewBinding.adTitle;

   viewBinding.nativeAdView.advertiserView = viewBinding.advertiser;

   viewBinding.nativeAdView.mediaView =  viewBinding.mediaView;

   viewBinding.nativeAdView.setNativeAd(nativeAd);
    
}
```
{% endtab %}
{% endtabs %}
