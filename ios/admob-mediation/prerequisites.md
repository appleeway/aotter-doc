# Prerequisites

### Configure AdMob Ad Units

Add `adUnit` in your mediation group and fill in `Class Name`, `Parameter`.

* Class Name

It must be the same name as your "**Custom Event**" class file name, for example:

\- Native Ad:  `AotterTrekGADCustomEvenNativeAd` \
\- Supr.Ad: `AotterTrekGADCustomEvenNativeAd`\
\- Banner Ad: `AotterTrekGADCustomEventBannerAd`

* Parameter

Please follow the format: `{"adType":"xxx", "adPlace":"xxx"}`&#x20;

|           | adType     | adPlace                      |
| --------- | ---------- | ---------------------------- |
| Native Ad | `nativeAd` | **AotterTrek Ad Place UUID** |
| Supr.Ad   | `suprAd`   | **AotterTrek Ad Place UUID** |
| Banner Ad | `suprAd`   | **AotterTrek Ad Place UUID** |

Take native ad as an example, its configuring will be set like below:

![](../../.gitbook/assets/Admob\_native\_noTestUUID.png)
