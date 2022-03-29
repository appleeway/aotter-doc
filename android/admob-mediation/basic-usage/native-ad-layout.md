# Native Ad

Follow these steps to build a native ad layout that fits your application and then requests it.

Step 1: [Create Native Ad Layout](native-ad-layout.md#step-1-create-native-ad-layout)\
Step 2: [Create `AdLoader`](native-ad-layout.md#step-2-create-adloader)\
Step 3: [Set Ad Layout and Bind Ad View](native-ad-layout.md#step-3-set-ad-layout-and-bind-ad-view)\
Step 4: [Create `AdRequest`](native-ad-layout.md#step-4-create-adrequest)\
Step 5: [Request an Ad](native-ad-layout.md#step-5-request-an-ad)

{% hint style="warning" %}
**Initialize your ad object with a context of Activity or Fragment instance:**\
****\
****In the constructor for a new ad object, you must pass in an object of type **Context**. This **Context** is passed on to other ad networks when using mediation. Some ad networks require a more restrictive **Context** that is of type **Activity** or **Fragment** and may not be able to serve ads without an **Activity** or **Fragment** instance. Therefore, we recommend passing in the context of **Activity** or **Fragment** instance when initializing ad objects to ensure a consistent experience with your mediated ad networks.
{% endhint %}

### Step 1: Create Native Ad Layout

#### **Example Native Ad layout**

{% hint style="warning" %}
**Notice: Please use `NativeAdView` as the container of your layout**
{% endhint %}

```kotlin
<com.google.android.gms.ads.nativead.NativeAdView
                android:id="@+id/admobNativeAdView"
                android:layout_width="match_parent"
                android:layout_height="match_parent">

     <androidx.constraintlayout.widget.ConstraintLayout
                    android:id="@+id/adView"
                    android:layout_width="match_parent"
                    android:layout_height="match_parent">

                    <TextView
                        android:id="@+id/sponsored"
                        android:layout_width="0dp"
                        android:layout_height="wrap_content"
                         />

                    <TextView
                        android:id="@+id/admobAdTitle"
                        android:layout_width="0dp"
                        android:layout_height="0dp"
                        />

     </androidx.constraintlayout.widget.ConstraintLayout>

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

### **Step 3: Set Ad Layout and Bind Ad View**

Set layout and bind ad view in the callback function of `forNativeAd`.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
.....

forNativeAd { nativeAd ->

  val advertiser:String = nativeAd.advertiser
               
  val text:String = nativeAd.body

  //Please binding ad view
  admobNativeAdView.setNativeAd(nativeAd)
  
  nativeAd.extras.getSerializable(TrekAdmobDataKey.AD_DATA)?.let {
  
    val adData = it as AdData
    
    TrekAdmobAdViewBinder.bindingAdView(adData,admobNativeAdView)
    
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
                        
      String advertiser = nativeAd.getAdvertiser();
               
      String text = nativeAd.getBody();

      //Please binding ad view
      admobNativeAdView.setNativeAd(nativeAd);
  
      if(nativeAd.getExtras().getSerializable(TrekAdmobDataKey.AD_DATA) != null){

        AdData adData = (AdData)nativeAd.getExtras().getSerializable(TrekAdmobDataKey.AD_DATA) ;
  
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

bundle.putString(TrekAdmobDataKey.CATEGORY, "PAGE_CATEGORY")//ex."3C"
bundle.putString(TrekAdmobDataKey.CONTENT_URL, "PAGE_URL")//ex."https://agirls.aotter.net/"
bundle.putString(TrekAdmobDataKey.CONTENT_TITLE, "PAGE_TITLE")//ex."電獺少女"

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

bundle.putString(TrekAdmobDataKey.CATEGORY, "PAGE_CATEGORY");//ex."3C"
bundle.putString(TrekAdmobDataKey.CONTENT_URL, "PAGE_URL");//ex."https://agirls.aotter.net/"
bundle.putString(TrekAdmobDataKey.CONTENT_TITLE, "PAGE_TITLE");//ex."電獺少女"

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
