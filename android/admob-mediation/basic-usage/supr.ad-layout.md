# Supr.Ad

Follow these steps to build a Supr.Ad layout and then requests it.

Step 1: [Create Supr.Ad Layout](supr.ad-layout.md#step-1-create-supr-ad-layout)\
Step 2: [Create `AdLoader`](supr.ad-layout.md#step-2-create-adloader)\
Step 3: [Set Ad Layout and Bind Ad View](supr.ad-layout.md#step-3-set-ad-layout-and-bind-ad-view)\
Step 4: [Create `AdRequest`](supr.ad-layout.md#step-4-create-adrequest)\
Step 5: [Request an Ad](supr.ad-layout.md#step-5-request-an-ad)

### Step 1: Create Supr.Ad Layout

#### **Example Supr.Ad layout**

{% hint style="warning" %}
**Notice: Please use `NativeAdView` as the container of your layout**
{% endhint %}

```kotlin
<com.google.android.gms.ads.nativead.NativeAdView
    android:id="@+id/admobNativeView"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">

        <com.google.android.gms.ads.nativead.MediaView
            android:id="@+id/admobMediaView"
            android:layout_width="match_parent"
            android:layout_height="wrap_content" 
            />

</com.google.android.gms.ads.nativead.NativeAdView>
```

### Step 2: Create `AdLoader`

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

### Step 3: Set Ad Layout and Bind Ad View

Set layout and bind ad view in the callback function of `forNativeAd`.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
.....

forNativeAd { nativeAd ->

  //Please binding ad view
  viewBinding.admobNativeView.mediaView = viewBinding.admobMediaView

  admobNativeView.setNativeAd(nativeAd)

  nativeAd.extras.getSerializable(TrekAdmobDataKey.AD_DATA)?.let{

  val adData = it as AdData
  
  TrekAdmobAdViewBinder.bindingAdView(adData,admobNativeView)

  } 
  //      
   
}

.....
```
{% endtab %}

{% tab title="Java" %}
```java
.....


.forNativeAd(new NativeAd.OnNativeAdLoadedListener() {
  @Override
    public void onNativeAdLoaded(@NonNull @NotNull NativeAd nativeAd) {
                        
     //Please binding ad view
      viewBinding.admobNativeView.setMediaView(viewBinding.admobMediaView);
  
      admobNativeAdView.setNativeAd(nativeAd);
  
      if(nativeAd.getExtras().getSerializable(TrekAdmobDataKey.AD_DATA) != null){

        AdData adData = (AdData)nativeAd.getExtras().getSerializable(TrekAdmobDataKey.AD_DATA);
  
        TrekAdmobAdViewBinder.INSTANCE.bindingAdView(adData,admobNativeAdView);
  
      }
  
      //      

    }
})

.....
```
{% endtab %}
{% endtabs %}

### **Step 4: Create `AdRequest`**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val adRequest = AdRequest
    .Builder()
    .build()

//or you can bundle a category

val bundle = Bundle()

bundle.putString(TrekAdmobDataKey.CATEGORY, "YOU_CATEGORY")//ex."news"

val adRequest = AdRequest
    .Builder()
    .addCustomEventExtrasBundle(TrekAdmobCustomEventNative::class.java, bundle)
    .build()
```
{% endtab %}

{% tab title="Java" %}
```java
AdRequest adRequest = new AdRequest
    .Builder()
    .build();

//or you can bundle a category

Bundle bundle = new Bundle();

bundle.putString(TrekAdmobDataKey.CATEGORY, "YOU_CATEGORY");//ex."news"

AdRequest adRequest = new AdRequest
    .Builder()
    .addCustomEventExtrasBundle(TrekAdmobCustomEventNative.class, bundle)
    .build();
```
{% endtab %}
{% endtabs %}

### **Step 5: Request an Ad**

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
