# Prerequisites

Before you can integrate mediation that **AotterTrek Network as a third-party ad network** into your MoPub app, the following steps are high-level to Integrate MoPub SDK:

Step 1: [Download the MoPub Android SDK](https://developers.mopub.com/publishers/android/integrate/#step-1-download-the-mopub-android-sdk)\
Step 2: [Add the MoPub SDK to your project](https://developers.mopub.com/publishers/android/integrate/#step-2-add-the-mopub-sdk-to-your-project)\
Step 3: [Update your Android Manifest](https://developers.mopub.com/publishers/android/integrate/#step-3-update-your-android-manifest) (Skip this step if you use v5.10.0 or above)\
Step 4: [Use Proguard](https://developers.mopub.com/publishers/android/integrate/#step-5-optionally-use-proguard) (Optional)\
Step 5: [Configure ad units in your app](https://developers.mopub.com/publishers/android/integrate/#step-6-configure-ad-units-in-your-app)

### MoPub Networks configuring

You can find "**App & ad unit setup**" in Networks and fill in **Custom event class** & **Custom event class**

*   **Custom event class**\
    **- **Native Ads:** **

    * _com.mopub.mediation.kotlin.ads.TrekMoPubCustomEventNative _

    \- Banner Ads:

    * _com.mopub.mediation.kotlin.ads.TrekMoPubCustomEventBanner_
* **Custom event class data**
  * {"clientId":"**TREK\_CLIENT\_ID**","placeUid":"**TREK\_PLACE\_UUID**"}

![](<../../.gitbook/assets/截圖 2021-09-14 下午3.37.27.png>)
