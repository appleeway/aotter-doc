# Prerequisites

Before you can integrate mediation that **AotterTrek Network as a third-party ad network** for an ad format, you need to integrate that ad format into your AdMob app:

* ****[**AdMob Native Ads**](https://developers.google.com/admob/ios/native/start)****
* ****[**AdMob Banner Ads**](https://developers.google.com/admob/ios/banner)****

If you don't familiar with AdMob, please refer to the links below:

* **New to Google AdMob? Read** [**Admob - Get Started**](https://developers.google.com/admob/ios/quick-start)****
* **New to mediation? Read** [**AdMob mediation - Overview**](https://developers.google.com/admob/ios/mediate)****

### Configure AdMob Ad Units

Add **`adUnit`** in your mediation group and fill in **`Class Name`**, **`Parameter`**.



{% hint style="info" %}
**The AotterTrekGADMediaAdapter is new protocal for GAD requirement. trek adapter is implemented since 1.0.9, but the CustomEvent class is still works.**
{% endhint %}

{% hint style="warning" %}
**We are about to deprecated Trek versions prior to 3.7.6 anddeprecated mediation versions prior to 1.0.8**

**Recommend developer install above Trek version 3.7.7 and above** **medaiton version 1.0.9**
{% endhint %}

### **Class Name**&#x20;

#### **B**elow TrekSDK 3.7.6 & admob medaiton 1.0.8

*   Native Ad:

    **AotterTrekGADCustomEventNativeAd**
*   Supr.Ad:

    **AotterTrekGADCustomEventNativeAd**
*   Banner Ad:

    **AotterTrekGADCustomEventBannerAd**

#### Above TrekSDK 3.7.7 & admob medaiton 1.0.9

*   Native Ad / Supr Ad / Banner Ad:&#x20;

    **AotterTrekGADMediaAdapter**

### Parameter

* {"adType":"**YOUR\_AD\_TYPE**","adPlace":"**YOUR\_PLACE\_UUID**"}

You can refer following the format:&#x20;

|           | adType         | adPlace                      |
| --------- | -------------- | ---------------------------- |
| Native Ad | **`nativeAd`** | **AotterTrek Ad Place UUID** |
| Supr.Ad   | **`suprAd`**   | **AotterTrek Ad Place UUID** |
| Banner Ad | **`suprAd`**   | **AotterTrek Ad Place UUID** |

Take native ad as an example, its configuring will be set like below:

![](../../.gitbook/assets/Admob\_native\_noTestUUID.png)
