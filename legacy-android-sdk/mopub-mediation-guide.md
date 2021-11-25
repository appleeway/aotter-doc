# MoPub Mediation Guide

### Integrating MoPub SDK <a href="integrating-mopub-sdk" id="integrating-mopub-sdk"></a>

Follow the instructions on the MoPub Site for setting up MoPub SDK.\


> [https://developers.mopub.com/publishers/android/get-started/](https://developers.mopub.com/publishers/android/get-started/)

### Integrated MoPub native ads <a href="integrated-mopub-native-ads" id="integrated-mopub-native-ads"></a>

In order to mediate native ads, be sure you already integrated [MoPub native ads](https://developers.mopub.com/publishers/android/native-adplacer/).

### Native Third-Party Integration Guide <a href="native-third-party-integration-guide" id="native-third-party-integration-guide"></a>

#### 1. Setup a Third-Party Network in your MoPub Account <a href="_1-setup-a-third-party-network-in-your-mopub-account" id="_1-setup-a-third-party-network-in-your-mopub-account"></a>

AotterTrek Native Ads should be set up as **custom native networks** in your MoPub account.

> MoPub Support Site:
>
> &#x20;[https://developers.mopub.com/publishers/android/integrate-networks/](https://developers.mopub.com/publishers/android/integrate-networks/)

Please set up AotterTrek Native Ads as follows:

| Type      | Custom Event Class             | Custom Event Class Data                                              |
| --------- | ------------------------------ | -------------------------------------------------------------------- |
| Native Ad | com.mopub.nativeads.TrekNative | {"place\_name":"< enter your place name here >"}                     |
| Supr Ad   | com.mopub.nativeads.TrekNative | {"place\_name":"< enter your place name here >,"adType":"SUPR\_AD""} |

#### 2. Add the custom event files to your project <a href="_2-add-the-custom-event-files-to-your-project" id="_2-add-the-custom-event-files-to-your-project"></a>

Add the folder "**nativeads**" into com.mopub under your app’s src/ directory and copy the adapters from [檔案下載](https://github.com/aotter/AotterTrek-Android-SDK/releases/download/3.1.8/TrekNative\_mediation\_v3.0.0.zip) that you want to include into the folder.

#### 3. Install AotterTrek SDK <a href="_3-install-aottertrek-sdk" id="_3-install-aottertrek-sdk"></a>

Follow the instructions on the [Initialize SDK](https://trek.aotter.net/publisher/show/sdk?platform=ANDROID#doc\_1) for setting up AotterTrek SDK.

#### 4. Use Mediation with category <a href="_4-use-mediation-with-category" id="_4-use-mediation-with-category"></a>

```java
Map<String, Object> localExtras = new HashMap<>();
localExtras.put(TREK_AD_CATEGORY, "NBA");
TrekNativeAdSource adSource = new TrekNativeAdSource();
adSource.setLocalExtras(localExtras);
// Create an ad adapter that gets its positioning information from the MoPub Ad Server.
// This adapter will be used in place of the original adapter for the ListView.
mAdAdapter = new TrekMoPubAdAdapter((Activity) mContext, mAdapter, new MoPubServerPositioning(), adSource);
```

#### 5. Use Mediation Supr Ad <a href="_5-use-mediation-supr-ad" id="_5-use-mediation-supr-ad"></a>

```java
// Trek Audience Network
final TrekAdRenderer trekAdRenderer = new TrekAdRenderer(getActivity(),
        new ViewBinder.Builder(R.layout.native_ad_list)
                .titleId(R.id.ad_title)
                .mainImageId(R.id.postImg)
                .textId(R.id.ad_summary)
                .callToActionId(R.id.post_button)
                .addExtra("sponsor", R.id.ad_publisher)
                .addExtra("mediaView", R.id.ad_mediaview) //TKMediaView
                .build());

mAdAdapter.registerAdRenderer(trekAdRenderer);
```

{% hint style="success" %}
Checkout [MoPub Support Site](https://developers.mopub.com/publishers/mediation/integrate-android/) for more details.
{% endhint %}
