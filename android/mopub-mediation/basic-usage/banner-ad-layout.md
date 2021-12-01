---
description: Banner Ad
---

# Banner Ad

Follow these steps to build a banner ad layout and then load it.

Step 1: [Create Banner Ad Layout](banner-ad-layout.md#step-1-create-banner-ad-layout)\
Step 2: [Initialize Configuration](banner-ad-layout.md#step-2-initialize-configuration)\
Step 3: [Set Ad Unit Id](banner-ad-layout.md#step-3-set-ad-unit-id)\
Optional: [Set Category](banner-ad-layout.md#optional-set-category)\
Step 4: **** [Load Ads](banner-ad-layout.md#step-4-load-ads)

### Step 1: Create Banner Ad Layout

#### Example Banner Ad layout

```kotlin
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".banner_ad.MoPubBannerAdRecyclerViewActivity">


    <com.mopub.mobileads.MoPubView
        android:id="@+id/mopubBannerView"
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintEnd_toEndOf="parent"
        app:layout_constraintStart_toStartOf="parent" />

</androidx.constraintlayout.widget.ConstraintLayout>
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

### Step 3: Set Ad Unit Id

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
viewBinding.mopubBannerView.setAdUnitId("YOUR_ADUNIT_FROM_MOPUB")
```
{% endtab %}

{% tab title="Java" %}
```java
viewBinding.mopubBannerView.setAdUnitId("YOUR_ADUNIT_FROM_MOPUB")
```
{% endtab %}
{% endtabs %}

### Optional: Set Category

{% tabs %}
{% tab title="Kotlin" %}
```
val hasMap = hashMapOf(TrekMoPubDataKey.CATEGORY to "YOUR_CATEGORY") EX:"news"
        
viewBinding.mopubBannerView.setLocalExtras(hasMap)
```
{% endtab %}

{% tab title="Java" %}
```java
HashMap<String, Object> hasMap = new HashMap<String, Object>();

hasMap.put(TrekMoPubDataKey.CATEGORY, "YOUR_CATEGORY");
        
mopubBannerView.setLocalExtras(hasMap);
```
{% endtab %}
{% endtabs %}

### Step 4: Load Ads

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
viewBinding.mopubBannerView.loadAd()
```
{% endtab %}

{% tab title="Java" %}
```
viewBinding.mopubBannerView.loadAd();
```
{% endtab %}
{% endtabs %}

{% hint style="warning" %}
Note: The`onDestroy()`method will destroy `MoPubView` when your Activity or Fragment be destroyed.
{% endhint %}

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
override fun onDestroy() {
    super.onDestroy()

    viewBinding.mopubBannerView.destroy()

}
```
{% endtab %}

{% tab title="Java" %}
```java
@Override
protected void onDestroy() {
    super.onDestroy();
    
    viewBinding.mopubBannerView.destroy();
    
}
```
{% endtab %}
{% endtabs %}
