# Trek SDK migration 3.x

This migration guide help developer who like to update AotterTrek iOS SDK to **version 3.x** from 1.x. If you haven't updated, we highly recommend upgrading for a better integration experience and optimized Ads.

## Key Differences

* [Change SDK Name](../../aottertrek-3.x-migration-guide.md#\_1-sdk-name-changed)
* [Change Class Prefix ](../../aottertrek-3.x-migration-guide.md#\_2-class-prefix-changed)
* [Combine Video Ad and Interactive Ad into **Supr.Ad**](../../aottertrek-3.x-migration-guide.md#combine-video-ad-and-interactive-ad-into-supr-ad)****
* [Remove XcodeColor Logs](../../aottertrek-3.x-migration-guide.md#\_4-xcodecolor-logs-removed)
* [Ad Cache Setting](../../aottertrek-3.x-migration-guide.md#\_5-ad-cache-setting-changed)

### Change: SDK Name  <a href="#_1-sdk-name-changed" id="_1-sdk-name-changed"></a>

* SDK 1.x : `AotterService`
* SDK 3.x : `AotterTrek-iOS-SDK`
* Import class change to `#import <AotterTrek-iOS-SDK/AotterTrek-iOS-SDK.h>`

### Change: Class Prefix  <a href="#_2-class-prefix-changed" id="_2-class-prefix-changed"></a>

*   SDK 1.x: `AT`

    \- e.g. `ATAdNative`, `ATAdVideo`, `ATAdManager`, `ATTracker`
*   SDK 3.x: `TK`

    \- e.g. `TKAdNative`, `TKAdMaganer`, `TKTracker`

### Combine Video Ad and Interactive Ad into **Supr.Ad**

Video Ad and Interactive Ad will be removed after SDK 3.x, a new ad format `SuprAd` for multimedia ad is added instead.

|                | 1.x            | 3.x          |
| -------------- | -------------- | ------------ |
| Native Ad      | `ATAdNative`   | `TKAdNative` |
| Video Ad       | `ATAdVideo`    | _(removed)_  |
| Interactive Ad | `ATAdInteract` | _(removed)_  |
| Supr Ad        | -              | `TKAdSuprAd` |

### Remove XcodeColor Logs <a href="#_4-xcodecolor-logs-removed" id="_4-xcodecolor-logs-removed"></a>

Since Xcode 8 stop supporting third-party plug-ins, the [XcodeColors](https://github.com/robbiehanson/XcodeColors) are not available anymore.

| 1.x                               | 3.x                 |
| --------------------------------- | ------------------- |
| ATLoggerLevelNone                 | TKLoggerLevelNone   |
| ATLoggerLevelNormal               | TKLoggerLevelNormal |
| ATLoggerLevelNormalWithXcodeColor | _(removed)_         |
| ATLoggerLevelDetail               | TKLoggerLevelDetail |
| ATLoggerLevelDetailWithXcodeColor | _(removed)_         |

### Ad Cache Setting Changed. <a href="#_5-ad-cache-setting-changed" id="_5-ad-cache-setting-changed"></a>

* 1.x : `ATsetIndividualAdPoolSize:`
* 3.0\~3.1: `disableAdCachePool` and `enableAdCachePoolWithIndiviaulPoolSize:`
* 3.2\~: Removed enable/disable cache setting, which will always be **on** and the cache system has been improved.
* 3.5.0\~: Removed cache pool.
