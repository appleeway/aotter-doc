# Display an ad

## Implementing native ads in your app following steps:

#### **Step 1.**[**Setting ad layout**](display-an-ad.md#setting-ad-layout)****

#### **Step 2.**[**Populating the asset view with the asset in the ad object**](display-an-ad.md#populating-the-asset-view-with-the-asset-in-the-ad-object)****

#### **Step 3.**[**Destroy ad**](display-an-ad.md#destroy-ad)****

### ****[**Setting ad layout**](display-an-ad.md#step-1.setting-ad-layout)****

{% hint style="warning" %}
**Notice:** Please use **NativeAdView** as the container of your layout
{% endhint %}

Here is an example layout style:

<figure><img src="broken-reference" alt=""><figcaption><p>Example layout style</p></figcaption></figure>

| View | NativeAd asset                                      |
| ---- | --------------------------------------------------- |
| #1   | nativeAd.icon.drawable                              |
| #2   | nativeAd.advertiser                                 |
| #3   | nativeAd.extras.getString(TrekAdmobDataKey.SPONSOR) |
| #4   | mediaView                                           |
| #5   | nativeAd.headline                                   |
| #6   | nativeAd.body                                       |
| #7   | nativeAd.callToAction                               |

```xml
<com.google.android.gms.ads.nativead.NativeAdView
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:id="@+id/nativeAdView"
    android:layout_width="match_parent"
    android:layout_height="wrap_content">

    <TextView
        android:id="@+id/advertiser"/>
        
    <TextView
        android:id="@+id/adTitle"/>

    <TextView
        android:id="@+id/adText"/>

    <ImageView
        android:id="@+id/adMainImg" />
        
    <ImageView
        android:id="@+id/adIcon" />
        
  // Other assets such as sponsor or media view, call to action, etc follow.

</com.google.android.gms.ads.nativead.NativeAdView>
```

### ****[**Populating the asset view with the asset in the ad object**](display-an-ad.md#step-2.populating-the-asset-view-with-the-asset-in-the-ad-object)****

Here is an example function that displays a **`NativeAd`**:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
...
forNativeAd { nativeAd ->

   displayAd(nativeAd);
   
}
...
private void displayAd(NativeAd nativeAd) {
   
   //Extras assets  provided by trek.
   //Skipping if you don't need.
   val sponsor = nativeAd.extras.getString(TrekAdmobDataKey.SPONSOR)?:""
   val mainImage = nativeAd.extras.getString(TrekAdmobDataKey.MAIN_IMAGE)?:""//1200x628
   val icon = nativeAd.extras.getString(TrekAdmobDataKey.ICON_IMAGE)?:""//82x82
   val iconHd = nativeAd.extras.getString(TrekAdmobDataKey.ICON_IMAGE_HD)?:""//300x300

   //Populating asset to asset view
   viewBinding.adIcon.setBackground(nativeAd.icon.drawable);
   viewBinding.advertiser.setText(nativeAd.advertise);
   viewBinding.adTitle.setText(nativeAd.body);
   viewBinding.adCallToAction.setText(nativeAd.callToAction);
   
   //injectting asset view to nativeAdView.
   //it will register view click action.
   viewBinding.nativeAdView.setIconView(viewBinding.adIcon);
   viewBinding.nativeAdView.setHeadlineView(viewBinding.adTitle);
   viewBinding.nativeAdView.setAdvertiserView(viewBinding.advertiser);
   viewBinding.nativeAdView.setCallToActionView(viewBinding.adCallToAction);
   
   //injectting mediaView to nativeAdView.mediaView 
   //it will lanuch mediaview to show media content.
   viewBinding.nativeAdView.setMediaView(viewBinding.mediaView);
   
   ...
    // Repeat the above process for the other assets in the NativeAd using
    // additional view objects (Buttons, ImageViews, etc).
   ...

   //Registering the views in this way allows the SDK to automatically handle tasks such as:
   //Recording clicks
   //Recording impressions
   viewBinding.nativeAdView.setNativeAd(nativeAd);

}
```
{% endtab %}

{% tab title="Java" %}
```java
...
forNativeAd { nativeAd ->

   displayAd(nativeAd);
   
}
...
private void displayAd(NativeAd nativeAd) {
   
   //Extras assets  provided by trek.
   //Skipping if you don't need.
   String sponsor = nativeAd.extras.getString(TrekAdmobDataKey.SPONSOR)?:"";
   String mainImage = nativeAd.extras.getString(TrekAdmobDataKey.MAIN_IMAGE)?:"";//1200x628
   String icon = nativeAd.extras.getString(TrekAdmobDataKey.ICON_IMAGE)?:"";//82x82
   String iconHd = nativeAd.extras.getString(TrekAdmobDataKey.ICON_IMAGE_HD)?:"";//300x300

   //Populating asset to asset view
   viewBinding.adIcon.background = nativeAd.icon?.drawable;
   viewBinding.advertiser.text = nativeAd.advertise;
   viewBinding.adTitle.text = nativeAd.body;
   viewBinding.adCallToAction.text = nativeAd.callToAction;
   
   //injectting asset view to nativeAdView.
   //it will register view click action.
   viewBinding.nativeAdView.iconView = viewBinding.adIcon;
   viewBinding.nativeAdView.headlineView = viewBinding.adTitle;
   viewBinding.nativeAdView.advertiserView = viewBinding.advertiser;
   viewBinding.nativeAdView.callToActionView = viewBinding.adCallToAction;
   
   //injectting mediaView to nativeAdView.mediaView 
   //it will lanuch mediaview to show media content.
   viewBinding.nativeAdView.mediaView = viewBinding.mediaView;
   
   ...
    // Repeat the above process for the other assets in the NativeAd using
    // additional view objects (Buttons, ImageViews, etc).
   ...

   //Registering the views in this way allows the SDK to automatically handle tasks such as:
   //Recording clicks
   //Recording impressions
   viewBinding.nativeAdView.setNativeAd(nativeAd);

}
```
{% endtab %}
{% endtabs %}

### ****[**Destroy ad**](display-an-ad.md#step-3.destroy-ad)****

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
viewBinding.nativeAdView.destroy()
```
{% endtab %}

{% tab title="Java" %}
```java
viewBinding.nativeAdView.destroy();
```
{% endtab %}
{% endtabs %}
