---
description: Audiovisual advertising、Interactive advertising
---

# Supr.Ad (Manual)

Follow these steps to build a Supr.Ad layout and then load it.

Step 1: [Create Native Ad Layout](supr.ad-layout-manual.md#step-1-create-native-ad-layout)\
Step 2: [Initialize configuration](supr.ad-layout-manual.md#step-2-initialize-configuration)\
Step 3: [Create `AdapterHelper`](supr.ad-layout-manual.md#step-3-create-adapterhelper)\
Step 4: [Create `MoPubNative`](supr.ad-layout-manual.md#step-4-create-mopubnative)\
Optional: [Set Category](supr.ad-layout-manual.md#optional-set-category)\
Step 5: [Create `MoPubNativeNetworkListener`](supr.ad-layout-manual.md#step-5-create-mopubnativenetworklistener)\
Step 6: [Create ViewBinder](supr.ad-layout-manual.md#step-6-create-viewbinder)\
Step 7: [Render ViewBinder and Register Renderer](supr.ad-layout-manual.md#step-7-render-viewbinder-and-register-renderer)\
Step 8: [Load Ads](supr.ad-layout-manual.md#step-8-load-ads)\
Step 9: [Get Ad View](supr.ad-layout-manual.md#step-9-get-ad-view)

### Step 1: Create Native Ad Layout

#### Example parent layout

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

#### Example Supr.Ad layout (item\_trek\_media\_view.XML)

```kotlin
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/adContainer"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">


    <com.mopub.mediation.kotlin.ads.TrekMoPubMediaView
        android:id="@+id/trekMoPubMediaView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent"
        app:layout_constraintTop_toTopOf="parent" />


</androidx.constraintlayout.widget.ConstraintLayout>
```

### Step 2: Initialize configuration

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
```java
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

### Step 3: Create `AdapterHelper`

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val adapterHelper = AdapterHelper(this, 0, 3) // When standalone, any range will be fine.
```
{% endtab %}

{% tab title="Java" %}
```java
AdapterHelper adapterHelper = new AdapterHelper(this, 0, 3);// When standalone, any range will be fine.
```
{% endtab %}
{% endtabs %}

### Step 4: Create `MoPubNative`

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

### Optional: Set Category

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val hasMap = hashMapOf<String, Any>(TrekMoPubDataKey.CATEGORY to "YOUR_CATEGORY") //EX:"news"  

moPubNative.setLocalExtras(hasMap)
```
{% endtab %}

{% tab title="Java" %}
```java
HashMap<String, Object> hasMap = new HashMap<String, Object>();

hasMap.put(TrekMoPubDataKey.CATEGORY,"YOUR_CATEGORY"); //EX:"news"  

moPubNative.setLocalExtras(hasMap);
```
{% endtab %}
{% endtabs %}

### Step 5: Create `MoPubNativeNetworkListener`

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

### Step 6: Create ViewBinder

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val trekMoPubViewBinder = TrekMoPubViewBinder()
            .Builder(R.layout.item_trek_media_view)
            .adContainerViewId(R.id.adContainer)
            .trekMoPubMediaViewId(R.id.trekMoPubMediaView)
            .build()
```
{% endtab %}

{% tab title="Java" %}
```java
TrekMoPubViewBinder trekMoPubViewBinder = new TrekMoPubViewBinder()
                .new Builder(R.layout.item_trek_media_view)
                .adContainerViewId(R.id.adContainer)
                .trekMoPubMediaViewId(R.id.trekMoPubMediaView)
                .build();
```
{% endtab %}
{% endtabs %}

### Step 7: Render ViewBinder and Register Renderer

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

### Step 8: Load Ads

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

### Step 9: Get Ad View

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
    
      
        View adView =
                adapterHelper.getAdView(
                    null,
                    null,
                    nativeAd,
                    new ViewBinder.Builder(0).build()
                );
                
            // It a parent view
            viewBinding.linearLayout.addView(adView);        
                            
}
```
{% endtab %}
{% endtabs %}
