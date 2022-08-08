# Changelog

## 2022/08/05 release - SDK `3.7.4`

* adjust impression check method when scrolling.

## 2022/07/25 release - SDK `3.7.3`

* support Gyrometer & Accelerometer detect.
* CoreMotion framework is added.

## 2022/05/18 release - SDK `3.7.2`

* OM SDK: support dynamic omTags(javascriptResourceUrl)
* new optional param: contentTitle & contentUrl for initial an ad
* update OM SDK version

## 2022/04/21 release - SDK `3.7.1`

* Replace Google IMA SDK dependencies with custom VAST player for video ad rendering

## 2021/10/05 release - SDK `3.6.4`

* update OM SDK version

## 2021/09/15 release - SDK `3.6.3`

* Fix IMA player in video ad stitching issue
* Add SDK\_INT, sdkVersionCode, mediationVersion, mediationVersionCode into request
* Add Supr.Ad sponsor parser key

## 2021/07/05 release - SDK `3.6.2`

* Adjust video ad behavior interact with keyboard.

## 2021/06/21 release - SDK `3.6.1`

* Fixbug: suprAd video ads preload image cause background thread crash.

## 2021/06/11 release - SDK `3.6.0`&#x20;

* Fixbug: supr.Ad video ads background thread crash.

## 2021/06/01 release - SDK `3.5.9`

* Support AdMob Mediation Banner Ad.
* Support AdMob Mediation library for AotterTrek SDK, which can be used to Cocoapods install "TrekSDKAdMobMediationObjc".

## 2021/04/26 release iOS AdMob Mediation

* Update AdMob mediation doc&#x20;
* Unify AdMob mediation file between Swift and Object-C

## 2021/04/12 release - SDK `3.5.8`

* Support Google IMA iOS SDK `3.13.0` version and below

> If you use Google IMA iOS SDK in your project for your own purposes, please keep the same version.

## 2021/02/08 release - SDK `3.5.7`

* Add some logs.

## 2021/01/18 release - SDK `3.5.6`

* fixbug: suprAd dealloc & destroy() will cause bad exceess crash.

## 2021/01/18 release - SDK `3.5.5`

* fixbug: suprAd.destroy() would cause creash while in background thread.

## 2021/01/11 release - SDK `3.5.4`

* fixbug: wrong error message when ad no fill.

## 2020/11/17 release - SDK `3.5.3`

* supported iAB OM SDK for natvie ads
* supported adMob mediation files [Download](https://github.com/aotter/AotterTrek-iOS-SDK/releases/download/3.5.3/AotterTrek.adMob.mediation.zip)

## 2020/11/04 release - SDK `3.5.2`

* fix offset issue of suprAd in type parallax.

## 2020/10/22 release - SDK `3.5.1`

* make sure ad place is requried for TKAdNative & TKAdSuprAd initial.

## 2020/10/21 release - SDK `3.5.0`

* remove SDK's cache pool. respone of ad request is real async now.
* add isExpired() to TKAdNative & TKAdSuprAd
* add isVideoAd() to TKAdSuprAd
* add willAdLogClick & willAdLogImpression to TKAdNative & TKAdSuprAd
* change ad loading flow for video type SuprAd.

## 2020/09/24 release - SDK `3.4.2`

* fix SuprAd may get erro when video play to end.

## 2020/08/26 release - SDK `3.4.1`

* support Google-IMA-SDK 3.12.1 at least

## 2020/08/25 release - SDK `3.3.6`

* enable bitcode
* remove all UIWebView in SDK

## 2020/02/19 release - SDK `3.3.5`

* fix bug: TKAdNative.fetchAdWithCallback() getting wrong ads.

## 2020/02/12 release - SDK `3.3.4`

* fix SuprAd's video ad crashing issue
* update supported Google IMA sdk version to `3.11.2`

## 2020/01/15 release - SDK `3.3.2`

* add Parallax ad type for SuprAd
* change SuprAd ad life cycle to support lazy loading

## 2019/12/13 release - SDK `3.2.12`

* improve loading speed for SuprAd's placeholder image

## 2019/11/11 release - SDK `3.2.11`

* ad request change to sync, requestAd() will be response immediatly now.

## 2019/10/22 release - SDK `3.2.4`

* fix bug of SuprAd.destroy() wont kill some child view.
