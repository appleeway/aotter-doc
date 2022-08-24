# Prerequisites

Before you can integrate mediation that **AotterTrek Network as a third-party ad network** for an ad format, you need to integrate that ad format into your AdMob app:

* ****[**AdMob Native Ads**](https://developers.google.com/admob/ios/native/start)****
* ****[**AdMob Banner Ads**](https://developers.google.com/admob/ios/banner)****

If you don't familiar with AdMob, please refer to the links below:

* **New to Google AdMob? Read** [**Admob - Get Started**](https://developers.google.com/admob/ios/quick-start)****
* **New to mediation? Read** [**AdMob mediation - Overview**](https://developers.google.com/admob/ios/mediate)****

### Configure AdMob Ad Units

Add **`adUnit`** in your mediation group and fill in **`Class Name`**, **`Parameter`**.

#### **Class Name**&#x20;

* Native Ad :**`AotterTrekGADCustomEventNativeAd` **&#x20;
* Supr.Ad: **`AotterTrekGADCustomEventNativeAd`**
* Banner Ad :**`AotterTrekGADCustomEventBannerAd`**

#### Parameter

* `{:"adType":"`**YOUR\_AD\_TYPE**`", "adPlace":"`**YOUR\_PLACE\_UUID**`"}`

Please following the format:&#x20;

| **`nativeAd`** | **AotterTrek Ad Place UUID** |
| -------------- | ---------------------------- |
| **`suprAd`**   | **AotterTrek Ad Place UUID** |
| **`suprAd`**   | **AotterTrek Ad Place UUID** |

Take native ad as an example, its configuring will be set like below:

![](../../.gitbook/assets/Admob\_native\_noTestUUID.png)
