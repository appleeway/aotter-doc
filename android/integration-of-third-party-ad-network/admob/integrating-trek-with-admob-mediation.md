# Integrating Trek with AdMob Mediation

Integrating Trek with AdMob Mediation in your app following steps:

* ****[**Configure your app**](integrating-trek-with-admob-mediation.md#import\_the\_mobile\_ads\_sdk)****
* ****[**Initialize the Google Mobile Ads SDK**](integrating-trek-with-admob-mediation.md#initialize\_the\_mobile\_ads\_sdk)****

## Configure your app <a href="#import_the_mobile_ads_sdk" id="import_the_mobile_ads_sdk"></a>

1. In your project-level **`build.gradle`** file, include maven  in both your **`allprojects`** sections:

<pre class="language-groovy"><code class="lang-groovy">allprojects {
    repositories {
        google()
        mavenCentral()
        
<strong>        maven { url 'https://deps.aotter.net/artifactory/libs-release-local' }
</strong>        
    }
}

</code></pre>

2\. Add the dependencies for the trek-admob-mediation to your module's app-level Gradle file, normally **`app/build.gradle`**:

<pre class="language-groovy" data-overflow="wrap"><code class="lang-groovy">dependencies {
  
<strong>  implementation 'com.aotter.android:trek-admob-mediation:4.8.3'
</strong>  
}
</code></pre>

3\. Add the required permissions to your app's **`AndroidManifest.xml`** file, as shown below.

<pre class="language-xml"><code class="lang-xml">&#x3C;?xml version="1.0" encoding="utf-8"?>
&#x3C;manifest xmlns:android="http://schemas.android.com/apk/res/android">

.......

<strong>    &#x3C;uses-permission android:name="com.google.android.gms.permission.AD_ID" />
</strong>    
.......

&#x3C;/manifest>
</code></pre>

### Initialize the Google Mobile Ads SDK <a href="#initialize_the_mobile_ads_sdk" id="initialize_the_mobile_ads_sdk"></a>

Before loading ads, have your app initialize the Google Mobile Ads SDK by calling **`MobileAds.initialize()`** which initializes the SDK and calls back a completion listener once initialization is complete (or after a 30-second timeout). This needs to be done only once, ideally at app launch.

Here's an example of how to call the **`initialize()`** method in an Activity:

{% tabs %}
{% tab title="Kotlin" %}
<pre class="language-kotlin"><code class="lang-kotlin">class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

<strong>        MobileAds.initialize(this) {
</strong><strong>        
</strong><strong>        }
</strong>        
    }
}
</code></pre>
{% endtab %}

{% tab title="Java" %}
<pre class="language-java"><code class="lang-java">public class MainActivity extends AppCompatActivity {
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

<strong>        MobileAds.initialize(context, new OnInitializationCompleteListener() {
</strong><strong>            @Override
</strong><strong>            public void onInitializationComplete(InitializationStatus initializationStatus) {
</strong><strong>            
</strong><strong>            }
</strong><strong>        });
</strong>        
    }
}
</code></pre>
{% endtab %}
{% endtabs %}
