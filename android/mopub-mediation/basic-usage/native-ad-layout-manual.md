---
description: Native ads
---

# Native Ad (Manual)

Follow these steps to build a native ad layout and then load it.

Step 1: [Create Native Ad Layout](native-ad-layout-manual.md)\
Step 2: [Initialize Configuration](native-ad-layout-manual.md#step-2-initialize-configuration)\
Step 3: [Create `AdapterHelper`](native-ad-layout-manual.md#step-3-create-adapterhelper)\
Step 4: [Create `MoPubNative`](native-ad-layout-manual.md#step-4-create-mopubnative)\
Optional: [Set Category](native-ad-layout-manual.md#optional-set-category)\
Step 5: [Create `MoPubNativeNetworkListener`](../../../ios/ad-formats/native-ad.md#5-remove-and-release)\
Step 6: [Create ViewBinder](native-ad-layout-manual.md#step-6-create-viewbinder)\
Step 7: [Render ViewBinder and Register Renderer](native-ad-layout-manual.md#step-7-render-viewbinder-and-register-renderer)\
Step 8: [Load Ads](native-ad-layout-manual.md#step-8-load-ads)\
Step 9: [Get Ad View](native-ad-layout-manual.md#step-9-get-ad-view)

### Step 1: Create Native Ad Layout

#### **Example parent layout**

```kotlin
<?xml version="1.0" encoding="utf-8"?>

<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:id="@+id/linearLayout"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical" 
/>
```

#### **Example native ad layout (item\_local\_ad.XML)**

```kotlin
<?xml version="1.0" encoding="utf-8"?>

<androidx.cardview.widget.CardView xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:layout_marginStart="16dp"
    android:layout_marginLeft="16dp"
    android:layout_marginTop="16dp"
    android:layout_marginEnd="16dp"
    android:layout_marginRight="16dp"
    android:layout_marginBottom="16dp"
    app:layout_constraintBottom_toBottomOf="parent"
    app:layout_constraintEnd_toEndOf="parent"
    app:layout_constraintStart_toStartOf="parent"
    app:layout_constraintTop_toTopOf="parent">

    <androidx.constraintlayout.widget.ConstraintLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content">

        <TextView
            android:id="@+id/adText"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_marginStart="8dp"
            android:layout_marginTop="8dp"
            android:layout_marginEnd="8dp"
            android:textColor="@android:color/holo_red_dark"
            android:textSize="18sp"
            android:textStyle="bold"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/adImg" />

        <TextView
            android:id="@+id/adTitle"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_marginStart="8dp"
            android:layout_marginTop="8dp"
            android:layout_marginEnd="8dp"
            android:textSize="14sp"
            android:textStyle="bold"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/adText" />

        <TextView
            android:id="@+id/adAdvertiser"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_marginStart="8dp"
            android:layout_marginTop="8dp"
            android:layout_marginEnd="8dp"
            android:layout_marginBottom="16dp"
            android:gravity="end"
            android:textSize="14sp"
            android:textStyle="bold"
            app:layout_constraintBottom_toBottomOf="parent"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintHorizontal_bias="1.0"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toBottomOf="@+id/adTitle" />

        <ImageView
            android:id="@+id/adImg"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_marginTop="8dp"
            android:background="@color/purple_200"
            app:layout_constraintEnd_toEndOf="parent"
            app:layout_constraintStart_toStartOf="parent"
            app:layout_constraintTop_toTopOf="parent" />
    </androidx.constraintlayout.widget.ConstraintLayout>

</androidx.cardview.widget.CardView>
```

### Step 2: Initialize Configuration

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val sdkConfiguration = 
            SdkConfiguration.Builder("YOUR_ADUNIT_FROM_MOPUB")
            .withLogLevel(MoPubLog.LogLevel.DEBUG)
            .withLegitimateInterestAllowed(false)
            .build()

MoPub.initializeSdk(this, sdkConfiguration, initSdkListener())

private fun initSdkListener(): SdkInitializationListener {
        return SdkInitializationListener { }
}

```
{% endtab %}

{% tab title="Java" %}
```
SdkConfiguration sdkConfiguration =
                new SdkConfiguration.Builder("YOUR_ADUNIT_FROM_MOPUB")
                    .withLogLevel(MoPubLog.LogLevel.DEBUG)
                    .withLegitimateInterestAllowed(false)
                    .build();

MoPub.initializeSdk(this, sdkConfiguration, initSdkListener());

private SdkInitializationListener initSdkListener() {
        return new SdkInitializationListener() {
            @Override
            public void onInitializationFinished() {

            }
        };
    }
```
{% endtab %}
{% endtabs %}

### **Step 3: Create `AdapterHelper`**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val adapterHelper = AdapterHelper(this, 0, 3) // When stand alone, any range will be fine.
```
{% endtab %}

{% tab title="Java" %}
```java
AdapterHelper adapterHelper = new AdapterHelper(this, 0, 3);// When standalone, any range will be fine.
```
{% endtab %}
{% endtabs %}

### **Step 4: Create `MoPubNative`**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val moPubNative =
            MoPubNative(this, "YOUR_ADUNIT_FROM_MOPUB", moPubNativeNetworkListener)
```
{% endtab %}

{% tab title="Java" %}
```java
MoPubNative moPubNative =
               new MoPubNative(this, "YOUR_ADUNIT_FROM_MOPUB", moPubNativeNetworkListener);
```
{% endtab %}
{% endtabs %}

### **Optional: Set Category**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val hasMap = hashMapOf<String, Any>(TrekMoPubDataKey.CATEGORY to "YOUR_CATEGORY") //EX:"news"  

moPubNative.setLocalExtras(hasMap)
```
{% endtab %}

{% tab title="Java" %}
```
HashMap<String, Object> hasMap = new HashMap<String, Object>();

hasMap.put(TrekMoPubDataKey.CATEGORY,"YOUR_CATEGORY"); //EX:"news"  

moPubNative.setLocalExtras(hasMap);
```
{% endtab %}
{% endtabs %}

### **Step 5: Create `MoPubNativeNetworkListener`**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
private val moPubNativeNetworkListener = object : MoPubNative.MoPubNativeNetworkListener {
           
             override fun onNativeLoad(nativeAd: NativeAd) {
          
               //get ad success
            
            }

            override fun onNativeFail(nativeErrorCode: NativeErrorCode) {
               //get ad fail
            }
            
}
```
{% endtab %}

{% tab title="Java" %}
```java
private MoPubNative.MoPubNativeNetworkListener moPubNativeNetworkListener = new MoPubNative.MoPubNativeNetworkListener() {

        @Override
        public void onNativeLoad(NativeAd nativeAd) {
          //get ad success
        }

        @Override
        public void onNativeFail(NativeErrorCode nativeErrorCode) {
          //get ad fail
        }
        
};
```
{% endtab %}
{% endtabs %}

### **Step 6: Create ViewBinder**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val trekMoPubViewBinder = TrekMoPubViewBinder()
            .Builder(R.layout.item_local_ad)
            .titleId(R.id.adTitle)
            .textId(R.id.adText)
            .mainImageId(R.id.adImg) //image size 1200x628 
            .iconImageHdId(R.id.adImg) //image size 300x300
            .iconImageId(R.id.adImg) //image size 82x82
            .sponsoredTextId(R.id.sponsor)
            .advertiserNameId(R.id.adAdvertiser)
            .build()
```
{% endtab %}

{% tab title="Java" %}
```java
TrekMoPubViewBinder trekMoPubViewBinder = new TrekMoPubViewBinder()
                .new Builder(R.layout.item_local_ad)
                .titleId(R.id.adTitle)
                .textId(R.id.adText)
                .mainImageId(R.id.adImg) //image size 1200x628 
                .iconImageHdId(R.id.adImg) //image size 300x300
                .iconImageId(R.id.adImg) //image size 82x82
                .sponsoredTextId(R.id.sponsor)
                .advertiserNameId(R.id.adAdvertiser)
                .build();
```
{% endtab %}
{% endtabs %}

### **Step 7: Render ViewBinder and Register Renderer**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val trekMoPubAdRenderer = TrekMoPubAdRenderer(trekMoPubViewBinder)

moPubNative.registerAdRenderer(trekMoPubAdRenderer)
```
{% endtab %}

{% tab title="Java" %}
```java
TrekMoPubAdRenderer trekMoPubAdRenderer = new TrekMoPubAdRenderer(trekMoPubViewBinder);

moPubNative.registerAdRenderer(trekMoPubAdRenderer);
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Note: If you are integrating multiple third-party ad networks like Facebook and Pangle, you must set up, create, and register the appropriate renderer for each ad network. **Remember to register the default`MoPubStaticNativeAdRenderer`last**. The order of renderer registering is crucial. Wrong ordering might lead to ad malfunction which affects your revenue. \
Refer to [MoPub Integrate Third-Party Ad Networks](https://developers.mopub.com/publishers/mediation/integrate-android/) for more detail.
{% endhint %}

### **Step 8: Load Ads**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
moPubNative.makeRequest()
```
{% endtab %}

{% tab title="Java" %}
```
moPubNative.makeRequest();
```
{% endtab %}
{% endtabs %}

### **Step 9: Get Ad View**

Get the ad view in the callback function of `onNativeLoad` .

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
override fun onNativeLoad(nativeAd: NativeAd) {

            val adView =
                adapterHelper.getAdView(
                    null,
                    null,
                    nativeAd,
                    ViewBinder.Builder(0).build()
                )
                
            // It a parent view
            viewBinding.linearLayout.addView(adView)

}
```
{% endtab %}

{% tab title="Java" %}
```java
@Override
public void onNativeLoad(NativeAd nativeAd) {
       
          
   View adView = adapterHelper.getAdView(
                        null,
                        null,
                        nativeAd,
                       new ViewBinder.Builder(0).build()
                );
                
   // It a parent view
   viewBinding.linearLayout.addView(adView)
         
                   
}
```
{% endtab %}
{% endtabs %}
