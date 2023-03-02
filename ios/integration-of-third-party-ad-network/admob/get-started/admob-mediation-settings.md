# admob mediation settings



#### Configure AdMob Ad Units <a href="#configure-admob-ad-units" id="configure-admob-ad-units"></a>

Add **`adUnit`** in your mediation group and fill in **`Class Name`**, **`Parameter`**.**The AotterTrekGADMediaAdapter is new protocal for GAD requirement. trek adapter is implemented since 1.0.9, but the CustomEvent class is still works.**Exit with⌘↩

#### **Class Name**  <a href="#class-name" id="class-name"></a>

*   Native Ad:

    **AotterTrekGADCustomEventNativeAd**
*   Supr.Ad:

    **AotterTrekGADCustomEventNativeAd**
*   Banner Ad:

    **AotterTrekGADCustomEventBannerAd**

#### &#x20;Above Trek SDK 3.7.7 & admob mediation 1.0.9, you can use the new adapter

*   Native Ad / Supr Ad / Banner Ad:&#x20;

    **AotterTrekGADMediaAdapter**

#### Parameter <a href="#parameter" id="parameter"></a>

* {"adType":"**YOUR\_AD\_TYPE**","adPlace":"**YOUR\_PLACE\_UUID**"}

You can refer following the format:​

|           | adType         | adPlace                      |
| --------- | -------------- | ---------------------------- |
| Native Ad | **`nativeAd`** | **AotterTrek Ad Place UUID** |
| Supr.Ad   | **`suprAd`**   | **AotterTrek Ad Place UUID** |
| Banner Ad | **`suprAd`**   | **AotterTrek Ad Place UUID** |

Take native ad as an example, its configuring will be set like below:​![](https://files.gitbook.com/v0/b/gitbook-legacy-files/o/assets%2F-MXBBY-celz8mxgOcV5f%2F-McCt79GbD0Tflg66\_rD%2F-McCupeu7CqWx6G5bIXo%2FAdmob\_native\_noTestUUID.png?alt=media\&token=d7bdaeb6-01cf-41b8-afe9-95ac87a12034)



##
