# Change logs

### 2022/12/2 release - SDK `3.5.4` (Recommend) <a href="#2022-12-2-release-sdk-3.5.4" id="2022-12-2-release-sdk-3.5.4"></a>

* Feat Popup new UI and aspect ratio
* Fix adm missing width and height
* Fix iframe postMessage will lose act sometime
* Fix imp will not send

### 2022/09/30 release - SDK `3.5.1` <a href="#2022-09-30-release-sdk-3.5.1" id="2022-09-30-release-sdk-3.5.1"></a>

* Fix Popup when close not clean up iframe src
* Refactor Popup

### 2022/09/23 release - SDK `3.4.6` <a href="#2022-09-23-release-sdk-3.4.6" id="2022-09-23-release-sdk-3.4.6"></a>

* Add `sdkVersionCode`
* Add trek extra script support
* Fix Cookie can't be placed correctly
* Refactor get Cookie method
* Update GAM snippet

### 2022/09/01 release - SDK `3.4.5` <a href="#2022-09-01-release-sdk-3.4.5" id="2022-09-01-release-sdk-3.4.5"></a>

* Add Google Ad Manager parallel loading
* Add new HTML ads
* Add new logger
* Add detect params **trek-debug** to enable debug mode
* Add detect params **trek-debug-catrun** to override Catrun’s URL
* Add catrun PARALLAX event
* Fix tracker not send with webSessionId
* Fix the config override issue
* Fix prevent bridge print error logs
* Update browserslist
* Update dependency
* Refactor remove unused code to reduce bundle size
* Refactor whole create suprAd flow
* Refactor get website meta from window.top
* Deprecated NativeAd and VideoAd support
* Deprecated Popup post-robot
* Deprecated adType
* Deprecated Mapping config from Element

### 2022/06/10 release - SDK `3.3.5` <a href="#2022-06-10-release-sdk-3.3.5" id="2022-06-10-release-sdk-3.3.5"></a>

* Minor adjustment in Web SDK log.
* Remove the close button.

### 2021/11/03 release - SDK `3.3.3` <a href="#2021-11-03-release-sdk-3.3.3" id="2021-11-03-release-sdk-3.3.3"></a>

* Adjust Ad supply logic.
* Add custom ad selector feature.
* Fix ad impression report issue.

### 2021/03/25 release - SDK `3.2.19` <a href="#2021-03-25-release-sdk-3.2.19" id="2021-03-25-release-sdk-3.2.19"></a>

* Add dataset attributes for top-of-page & btm-of-page ad.
* Add data-mobile dataset attribute.
* Fix user context.

### 2020/06/10 release - SDK `3.2.9` <a href="#2020-06-10-release-sdk-3.2.9" id="2020-06-10-release-sdk-3.2.9"></a>

* Adjust ad impression report trigger.

### 2020/02/20 release - SDK `3.2.7` <a href="#2020-02-20-release-sdk-3.2.7" id="2020-02-20-release-sdk-3.2.7"></a>

* Add trigger `onAdLoad()` with more ad information.
* Fix trek-popup will cover entire page. It leads iOS device can't select.

### 2020/01/20 release - SDK `3.2.5` <a href="#2020-01-20-release-sdk-3.2.5" id="2020-01-20-release-sdk-3.2.5"></a>

* Upgrade post-robot to `10.0.29.`
* Add suprad popup support by web component.
* Remove whatwg-fetch polyfill from project.

### 2019/11/19 release - SDK `3.1.9` <a href="#2019-11-19-release-sdk-3.1.9" id="2019-11-19-release-sdk-3.1.9"></a>

* Fix `adOnFail` possible not working property.
* Add `CatRun(SuprAd)` support.
* Add HouseAd support.
* New APIs path.
* Deprecated CatWalk.
* Deprecated Video Native code.
* Reduce package size.
* New Babel and Webpack.
