---
description: Migrating from version 3.x to version 4.x
---

# Migration Guide

This migration guide help developer who like to update AotterTrek Android SDK to version 4.x from 3.x. If you haven't updated, we highly recommend upgrading for a better integration experience and optimized Ads.  For some seasons, you still stick to version 3. Please check the Legacy SDK page below.

{% content-ref url="../legacy-android-sdk/" %}
[legacy-android-sdk](../legacy-android-sdk/)
{% endcontent-ref %}

## Key Differences

* [SDK Installation](migration-guide.md#install-sdk)
* [Callback Functions](migration-guide.md#initialization-sdk)
* [Objects / Methods / Media View](migration-guide.md#objects-media-view-methods)
* [Request Ads](migration-guide.md#ad-object-listener)
* [Life Cycle](migration-guide.md#lifecycle)

### SDK Installation <a href="#install-sdk" id="install-sdk"></a>

Dependencies library is upgraded to version 4.x. Version 3.x is no longer be updated.

```kotlin
// Version 4.x: Please use the dependency library as following
implementation 'com.aotter.net:trek-sdk-android-kotlin:4.7.2'

// Version 3.x: It's about to deprecate the following dependency library
implementation 'com.google.android.gms:play-services-ads:18.1.1'
implementation 'com.aotter.net:trek-sdk:3.2.1'
```

### Callback Functions <a href="#initialization-sdk" id="initialization-sdk"></a>

#### SDK Initialization&#x20;

We add a completion callback in version 4 which is useful for publishers who want to do something at this point.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
// Version 4.x
TrekAds.initialize(context,"YOUR_CLIENT_ID"){
   //aotter service init finished callback.
}
```
{% endtab %}

{% tab title="Java" %}
```java
// Version 4.x
TrekAds.INSTANCE.initialize(this, "YOUR_CLIENT_ID", () -> {

            // init finished callback.

            return Unit.INSTANCE;

        });
```
{% endtab %}
{% endtabs %}

In version 4, the following callbacks are still available but please notice that `onAdLoaded` callback use **AdData** model instead of the TKAdNative model.

\- **** onAdFailedToLoad                        ****                        - **onAdLoaded**\
****- **** onAdClicked                                    ****                                    - **** onAdImpression

### Objects / Media View / Methods

#### - Ad Object

In version 4, _TKAdN_ object is deprecated, and uses **TrekAdLoader** object instead.

#### - Media View

In version 4, we use **TrekMediaView** instead of TKMediaView.

****\
**- Methods**

When setting ad listener, version 4 uses **setTrekAdListener** method instead of _setAdListener_. **** Furthermore, **** inject interface to listener use **TrekAdListener** interface instead of _TKAdListener._

When registering ad, _registerAdView_ method is deprecated. In version 4, the register method is as below.

```
 TrekAdViewBinder.registerAdView(adContainer,trekMediaView,trekNativeAd)
```

### Create `TrekAdRequest`&#x20;

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
        .build();j
```
{% endtab %}
{% endtabs %}

### Life Cycle <a href="#lifecycle" id="lifecycle"></a>

The life cycle in version 4 is automatically managed, which means that publishers don't need to do any life cycle management on their own.[\
](https://app.gitbook.com/@a173200488/s/aotter-trek-sdk-document/)\
