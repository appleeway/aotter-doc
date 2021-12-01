---
description: Audiovisual advertising、Interactive advertising
---

# Supr.Ad (RecyclerView)

Follow these steps to build a Supr.Ad layout and then load it.

Step 1: [Create Supr.Ad Layout](supr.ad-layout-recyclerview.md#step-1-create-supr-ad-layout)\
Step 2: [Initialize configuration](supr.ad-layout-recyclerview.md#step-2-initialize-configuration)\
Step 3: [Create `MoPubRecyclerAdapter`](supr.ad-layout-recyclerview.md#step-3-create-mopubrecycleradapter)\
Step 4: [Create ViewBinder](supr.ad-layout-recyclerview.md#step-4-create-viewbinder)\
Step 5: [Render ViewBinder and Register Renderer](supr.ad-layout-recyclerview.md#step-5-render-viewbinder-and-register-renderer)\
Step 6: **** [Load Ads](supr.ad-layout-recyclerview.md#step-6-load-ads)

### Step 1: Create Supr.Ad Layout

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

### Step 3: Create `MoPubRecyclerAdapter`

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val adPositioning = MoPubNativeAdPositioning.serverPositioning() // Server-Side Positioning
or
val adPositioning = MoPubNativeAdPositioning.clientPositioning(); //Client-Side Positioning
// If you use MoPubNativeAdPositioning.clientPositioning(),you can set position where you want show the ad.
adPositioning.addFixedPosition(1) 
adPositioning.addFixedPosition(3)
adPositioning.addFixedPosition(7)

val moPubAdapter = MoPubRecyclerAdapter(context, originalAdapter, adPositioning) // originalAdapter is own RecyclerView.Adapter 

viewBinding.moPubNativeAdRecyclerView.adapter = moPubAdapter // set moPubAdapter for your RecyclerView 
```
{% endtab %}

{% tab title="Java" %}
```java
MoPubNativeAdPositioning.MoPubServerPositioning adPositioning = MoPubNativeAdPositioning.serverPositioning();// Server-Side Positioning
//or
MoPubNativeAdPositioning.MoPubClientPositioning adPositioning = MoPubNativeAdPositioning.clientPositioning();; //Client-Side Positioning
// If you use MoPubNativeAdPositioning.clientPositioning(),you can set position where you want show the ad.
adPositioning.addFixedPosition(1);
adPositioning.addFixedPosition(3);
adPositioning.addFixedPosition(7);

MoPubRecyclerAdapter moPubAdapter = MoPubRecyclerAdapter(context, originalAdapter, adPositioning); // originalAdapter is own RecyclerView.Adapter

viewBinding.moPubNativeAdRecyclerView.setAdapter(moPubAdapter); // set moPubAdapter for your RecyclerView
```
{% endtab %}
{% endtabs %}

### Step 4: Create ViewBinder

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

### Step 5: Render ViewBinder and Register Renderer

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val trekMoPubAdRenderer = TrekMoPubAdRenderer(trekMoPubViewBinder)

moPubAdapter.registerAdRenderer(trekMoPubAdRenderer)
```
{% endtab %}

{% tab title="Java" %}
```java
TrekMoPubAdRenderer trekMoPubAdRenderer = new TrekMoPubAdRenderer(trekMoPubViewBinder);

moPubAdapter.registerAdRenderer(trekMoPubAdRenderer);
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Note: If you are integrating multiple third-party ad networks like Facebook and Pangle, you must set up, create, and register the appropriate renderer for each ad network. **Remember to register the default`MoPubStaticNativeAdRenderer`last**. The order of renderer registering is crucial. Wrong ordering might lead to ad malfunction which affects your revenue. \
Refer to [MoPub Integrate Third-Party Ad Networks](https://developers.mopub.com/publishers/mediation/integrate-android/) for more detail.
{% endhint %}

### Step 6: **** Load Ads

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
moPubAdapter.loadAds("YOUR_ADUNIT_FROM_MOPUB")
```
{% endtab %}
{% endtabs %}
