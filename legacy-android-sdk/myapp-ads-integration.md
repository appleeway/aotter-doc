# MyApp Ads Integration

## Guide <a href="#guide" id="guide"></a>

* AotterTrek Android SDK contains tracking and native advertising service.
* Minimum sdk Version: 16

## Install SDK <a href="#install-sdk" id="install-sdk"></a>

In order to use that repository, you need to refer to it in the app's project-level `build.gradle` file. Open yours and looking for an `allprojects` section:

* **Example project-level build.gradle (excerpt)**

```java
allprojects {
    repositories {
        google()
        jcenter()
        maven {
          url "https://deps.aotter.net/artifactory/libs-release-local"
        }
    }
}
```

Add the maven directive

* **Example app-level build.gradle (excerpt)**

```java
dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'com.google.android.gms:play-services-ads:18.1.1'
    implementation 'com.aotter.net:trek-sdk:3.1.0_rc1'
}
```

Pull in the latest version of the AotterTrek-Android-SDK and additional related dependencies.

## Update your AndroidManifest.xml and Application <a href="#update-your-androidmanifestxml-and-application" id="update-your-androidmanifestxml-and-application"></a>

Declare the following permissions:

```java
<uses-permission android:name="android.permission.INTERNET"/>
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
```

```java
//If you are shipping an app, extend the Application class if you are not already doing so:

public class MyApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();

        // init AotterTrek
        AotterTrek.initMyAppService(this, YOUR_CLIENT_ID, YOUR_CLIENT_SECRET);
    }
}
```

| Test Key       | Value                                                                      |
| -------------- | -------------------------------------------------------------------------- |
| CLIENT\_ID     | `DNgNhOwfbUkOqcQFI+uD`                                                     |
| CLIENT\_SECRET | `1k+sYKMLZrclCRmgw/esYNZbjAhArT7Vn42cxfn3f/tgmT0XJZI4mNiNwBYLu9GOet7YtiT6` |

## Overwrite click event for MyApp ads <a href="#overwrite-click-event-for-myapp-ads" id="overwrite-click-event-for-myapp-ads"></a>

`setAdTKMyAppListener`(boolean isCustomClick, TKAdListener adapter)

If `isCustomClick` set true, default sdk click event will be turn off. `isCustomClick` defult is false.

```java
tkAdN = new TKAdN(this, "post_third", "category_name", "NATIVE");
tkAdN.setAdTKMyAppListener(true, new TKAdListener() {

  @Override
  public void onAdLoaded(TKAdNative nativeAd) {
    ...
  }

  @Override
  public void onAdError(TKError tkError) {
    ...
  }

  @Override
  public void onAdClicked(TKAdNative nativeAd) {
    ...
  }

  @Override
  public void onAdImpression(TKAdNative nativeAd) {
    ...
  }
});
```

[To the top](myapp-ads-integration.md)
