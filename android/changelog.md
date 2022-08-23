# Changelog

## 2022/08/04 release - SDK `4.7.2`(Recommend)

{% hint style="info" %}
**minSdkVersion 21** \
**targetSdkVersion 31**
{% endhint %}

**Change log**

* TrekBannerAdView new feature
  * preload
  * auto refresh
* TrekNativeAd object new feature
  * `images` object provider `drawable` 、`uri`
  * remove unnecessary parameter

{% hint style="warning" %}
**Breaking change:**

**In order to achieve better version integration and normalization, Aotter Trek adjusted the `dependency path` and `mediation class name path` in versions above 4.7.2.**

* **Detail refer** [**Migration Guide**](migration-guide.md)****
* **Detail refer** [**Trek installation**](sdk-integration/installation.md)****
* **Detail refer** [**Admob mediation installation**](admob-mediation/installation.md)****
{% endhint %}

## 2022/07/19 release - SDK `4.6.1`&#x20;

{% hint style="info" %}
**minSdkVersion 21** \
**targetSdkVersion 31**
{% endhint %}

* New Sensor
* `TrekAdLoader` instead of `TrekAd`
* The `TrekAdLoader.loadAds()` method sends a request for multiple ads (up to 5)
* `TrekNativeAd` instead of `AdData`
* `TrekAds.initialize() method` instead of `AotterService.initialize() method`
* `TrekBannerAdView` instead of `TrekBannerView`
* New `TrekAdViewBinder` object (Using the object register ad layout)
* `TrekJsonObject` instead of `JsonObject`
* Kotlinx-serialization instead of Gson
* Updating ExoPlayer version to `2.17.1`
* Updating Kotlin version to `1.6.21`

## 2022/06/22 release - SDK `4.5.0`&#x20;

{% hint style="info" %}
**minSdkVersion 21** \
**targetSdkVersion 31**
{% endhint %}

* new TrekNativeAdImage
* Open browser with chrome
* imp tool optimization
* TrekMediaView optimization
* Log optimization
* Support vertical slide

## 2022/04/15 release - SDK `4.4.5`&#x20;

{% hint style="info" %}
Below this version:

**minSdkVersion 21** \
**targetSdkVersion 30**
{% endhint %}

* Optimized implementation
* Update AdMob mediation custom adapter ( [Migrate to SDK v21](https://developers.google.com/admob/android/migration) )
* The `TrekAdmobAdViewBinder` class has been removed, and trek admob mediation binding view flow has been integrated into the mediation adapter.

## 2022/03/29 release - SDK `4.4.2`

* Change domain
* Add `setContentUrl()` & `setContentTitle()`
* Support OM JSON tag
* Support OM js string dynamic update
* OMSDK obstruction minor adjustment
* Add OMSDK `contentUrl` and `customRefencData`
* Support webview slide
* Improve BackgroundHolder setting
* Update ExoPlayer
* Mapping Admob mediation `hasVideoContent` parameter

## 2021/12/23 release - SDK `4.3.4`

* Use Activity page (instead of DialogFragment page) when context comes from the application

## 2021/12/01 release - SDK `4.3.2`

* Support android 12
* Support kotlin version 1.5.31
* Update exoplayer
* Adjust impression tool
* Adjust third-party click event flow
* Fix banner ad, Supr.Ad impression event

## 2021/09/27 release - SDK `4.3.1`

* Adjust om impressionType

## 2021/09/13 release - SDK `4.3.0`

* Optimize Impression / VTR / CTR
* Adjust TrekMediaView lifecycle
* Adjust TrekMediaView plays video ad when visibility is 50% or more
* New TrekBannerView

## 2021/08/30 release - SDK `4.2.5`

* Remove Supr.Ad third imp

## 2021/08/24 release - SDK `4.2.4`

* Add TrekMediaView default height
* Define key of jsonObject
* Add sdkVersion
* Add mediationVersion
* Proguard optimization&#x20;

## 2021/07/29 release - SDK `4.2.1`

* Add isExpired method
* Add isVideoAd method

## 2021/07/16 release - SDK `4.2.0`

* Optimize adData
* Adjust TrekMediaView lifecycle

## 2021/06/28 release - SDK `4.1.1`

* Fix video ad grab external sound source
* Fix supr.Ad click response issue

## 2021/06/16 release - SDK `4.0.3`

* Native ad mapper optimization
* Modify get ad id method

## 2021/06/15 release - SDK `4.0.0`

* new released Android SDK

