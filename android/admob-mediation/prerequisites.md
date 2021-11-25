# Prerequisites

Before you can integrate mediation that **AotterTrek Network as a third-party ad network** for an ad format, you need to integrate that ad format into your AdMob app:

* ****[**AdMob Native Ads**](https://developers.google.com/admob/android/native/start)****
* ****[**AdMob Banner Ads**](https://developers.google.com/admob/android/banner)

If you don't familiar with AdMob, please refer to the links below:

* **New to Google AdMob? Read** [**Admob - Get Started**](https://developers.google.com/admob/android/quick-start)****
* **New to mediation? Read **[**AdMob mediation - Overview**](https://developers.google.com/admob/android/mediate)****

### Configure AdMob Ad Units

Add `adUnit` in your mediation group and fill in `Class Name`, `Parameter`.

* Class Name&#x20;
  * Native Ads: _com.admob.mediation.kotlin.ads.TrekAdmobCustomEventNative_
  * Banner Ads: _com.admob.mediation.kotlin.ads.TrekAdmobCustomEventBanner_
* Parameter
  * {"clientId":"**YOUR\_TREK\_CLIENT\_ID**","placeUid":"**YOUR\_TREK\_PLACE\_UUID**"}

![](<../../.gitbook/assets/image (11) (1).png>)
