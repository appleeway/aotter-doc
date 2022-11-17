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
**In order to achieve better version integration and normalization, Aotter Trek adjusted the `dependency path` and `mediation class name path`.**\
****[**See Change Log**](../changelog.md)
{% endhint %}

{% hint style="warning" %}
**We are about to deprecated versions prior to 4.4.5**

**Recommend developer install above version 4.7.2**
{% endhint %}

**Before version 4.4.5 ,please refer to the following.**

<pre class="language-groovy"><code class="lang-groovy">dependencies {

<strong>implementation 'com.aotter.net:trek-sdk-android-kotlin:4.4.5'
</strong>
}</code></pre>

**Above version 4.7.2 ,please refer to the following.**

<pre class="language-groovy"><code class="lang-groovy">dependencies {

<strong>implementation 'com.aotter.android:trek-ads:4.8.1'
</strong>
}</code></pre>

Please add the following code snippet in your **project-level** build.gradle.

<pre class="language-groovy"><code class="lang-groovy">allprojects {
    repositories {
        google()
        mavenCentral()
        
        // Add this 
<strong>        maven { url 'https://deps.aotter.net/artifactory/libs-release-local' }
</strong>        
    }
}</code></pre>

**AndroidManifest.XML**

Please add the following code snippet in your AndroidManifest.XML

```xml
<uses-permission android:name="com.google.android.gms.permission.AD_ID" />
```

### Step 2: Initialization

After including SDK in your project, you will also need to implement the following line of code to initialize SDK. If you have implemented extensions to the application class, it is recommended to initialize the AotterTrek service in `onCreate()` method. In the following example, the `context` variable represents an `Application` or `Activity`.\
\
Please use **your client id** for initialization which can be found in the [application list](https://trek.aotter.net/publisher/list/app).&#x20;

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        //Please fill in trek clent id yourself
        TrekAds.initialize(this, Trek_client_id ,object :TrekAds.OnInitializationCompleteListener{
            override fun onInitializationComplete() {

            }
        })
        
    }
}
```
{% endtab %}

{% tab title="Java" %}
```java
public class MainActivity extends AppCompatActivity {
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        //Please fill in trek clent id yourself
       TrekAds.INSTANCE.initialize(this, Trek_client_id ,new TrekAds.OnInitializationCompleteListener(){
            @Override
            public void onInitializationComplete() {
                
            }
        });
        
    }
}
```
{% endtab %}
{% endtabs %}

### Test ad units

{% hint style="info" %}
**Key Point:** Make sure you replace these client id and place uid with your own ad unit ID before publishing your app.
{% endhint %}

| Ad Format | Client Id            | Place Uid                            |
| --------- | -------------------- | ------------------------------------ |
| Native Ad | DNgNhOwfbUkOqcQFI+uD | 45419fb5-a846-4c4a-837f-3b391ec7b45a |
| Supr.Ad   | DNgNhOwfbUkOqcQFI+uD | 81608f91-8b2b-4f8f-86a1-539a1959f836 |
| Banner Ad | DNgNhOwfbUkOqcQFI+uD | 68856f90-83b7-4f09-98d4-7f480842cb02 |

## Next Steps

* Follow our guides for integrating different Ad Formats in your app:
  * [Native Ad](../ad-formats/native-ad.md)
  * [Banner Ad](../ad-formats/banner-ad.md)
* Or you would like to check out the demo app:
  * [Demo](trek-example-app-demo.md)
