# Prerequisites

### Configure AdMob Ad Units

Add `adUnit` in your mediation group and fill in `Class Name`, `Parameter`.

* Class Name

It must be the same name as your "**Custom Event**" class file name, for example:\
\
\- Native Ad: `AotterTrekNativeCustomEvent`\
\- Supr.Ad: `AotterTrekNativeCustomEvent`

* Parameter

Please follow the format: `{"place_name":"xxx", "adType":"xxx"}`&#x20;

|           | place\_name                  | adType          |
| --------- | ---------------------------- | --------------- |
| Native Ad | **AotterTrek Ad Place UUID** | `NATIVE`        |
| Supr.Ad   | **AotterTrek Ad Place UUID** | `NATIVE_SUPRAD` |

