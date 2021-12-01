---
description: Native ads
---

# Native Ad (RecyclerView)

Follow these steps to build a native ad layout and then load it.

Step 1: [Create Native Ad Layout](native-ad-layout-recyclerview.md#step-1-create-native-ad-layout)\
Step 2: [Initialize Configuration](native-ad-layout-recyclerview.md#step-2-initialize-configuration)\
Step 3: [Create `MoPubRecyclerAdapter`](native-ad-layout-recyclerview.md#step-3-create-mopubrecycleradapter)\
Step 4: [Create ViewBinder](../../ad-formats/native-ad.md#step-4-request-an-ad)\
Step 5: [Render ViewBinder and Register Renderer](native-ad-layout-recyclerview.md#step-5-render-viewbinder-and-register-renderer)\
Step 6: **** [Load Ads](native-ad-layout-recyclerview.md#step-6-load-ads)

### Step 1: Create Native Ad Layout

#### **Example Native Ad layout (item\_local\_ad.XML)**

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

### **Step 2: Initialize Configuration**

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

### **Step 3: Create `MoPubRecyclerAdapter`**

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

### **Step 4: Create ViewBinder**

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

### **Step 5: Render ViewBinder and Register Renderer**

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

### **Step 6: Load Ads**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
moPubAdapter.loadAds("YOUR_ADUNIT_FROM_MOPUB")
```
{% endtab %}

{% tab title="Java" %}
```
moPubAdapter.loadAds("YOUR_ADUNIT_FROM_MOPUB");
```
{% endtab %}
{% endtabs %}
