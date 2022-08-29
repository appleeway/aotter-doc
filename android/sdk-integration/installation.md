# Installation

Follow these steps to download and include SDK in your project:

**Step 1:** [**Including the SDK**](installation.md#including)****\
**Step 2:** [**Initialization**](installation.md#step-2-initialization)

### Step 1: Including the SDK <a href="#including" id="including"></a>

{% hint style="warning" %}
Please noticed that AotterTrek Android SDK Development Environment: `Kotlin version 1.6.21 up`
{% endhint %}

**Using Gradle**

![](../../.gitbook/assets/1631868969014.jpg)

Add the following dependencies to your **app-level** build.gradle (not project!), to use the latest AotterTrek SDK:

{% hint style="info" %}
**In order to achieve better version integration and normalization, Aotter Trek SDK adjusted the `dependency paths` and `mediation class name paths.`**\
****\
**``We recommend that developers install new `mediation class name` paths and new dependency paths.**\
****\
**Please note,we will  deprecated old Trek SDK dependency paths and old `mediation class name` paths.**
{% endhint %}

**Old Trek SDK dependency paths  ,please refer to the following.**

```groovy
dependencies {

implementation 'com.aotter.net:trek-sdk-android-kotlin:4.7.2'

}
```

**New Trek SDK dependency paths  ,please refer to the following.**

```groovy
dependencies {

implementation 'com.aotter.android:trek-ads:4.7.2'

}
```

Please add the following code snippet in your **project-level** build.gradle.

```groovy
allprojects {
    repositories {
        google()
        mavenCentral()
        
        // Add this 
        maven { url 'https://deps.aotter.net/artifactory/libs-release-local' }
        
    }
}
```

**AndroidManifest.XML**

Please add the following code snippet in your AndroidManifest.XML

```xml
<uses-permission android:name="com.google.android.gms.permission.AD_ID" />
```

### Step 2: Initialization

After including SDK in your project, you will also need to implement the following line of code to initialize SDK. If you have implemented extensions to the application class, it is recommended to initialize the AotterTrek service in `onCreate()` method. In the following example, the `context` variable represents an `Application` or `Activity`.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
class MyApplication:Application {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        
        TrekAds.initialize(context,"YOUR_CLIENT_ID"){
            //aotter service init finshed callback.
        }
                   
    }
}


```
{% endtab %}

{% tab title="Java" %}
```java
public class MyApplication extends Application {
    @Override
    public void onCreate() {
        super.onCreate();
       
        TrekAds.INSTANCE.initialize(this, "YOUR_CLIENT_ID", () -> {

            // init finished callback.

            return Unit.INSTANCE;

        });
        
    }
}
```
{% endtab %}
{% endtabs %}

Please use **your client id** for initialization which can be found in the [application list](https://trek.aotter.net/publisher/list/app). \
We also provide test client id for receiving test ads only.

* **Test Client ID :** `DNgNhOwfbUkOqcQFI+uD`

{% hint style="success" %}
Note: You can switch **test / production** mode by changing **test client id to your own client id.**
{% endhint %}

## Next Steps

* Follow our guides for integrating different Ad Formats in your app:
  * [Native Ad](../ad-formats/native-ad.md)
  * [Banner Ad](../ad-formats/banner-ad.md)
* Or you would like to check out the demo app:
  * [Demo](trek-example-app-demo.md)
