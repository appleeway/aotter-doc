# Installation

### Getting Started

We have provided demo and mediation adapter source.

To receive release updates, subscribe to our [GitHub repository.](https://github.com/aotter/aotter-trek-mediation-android)

### Add the SDK to the Project

**Using Gradle**

Add the following dependencies to your **app-level** build.gradle (not project!), to use the latest AotterTrek adapter:

{% hint style="info" %}
**In order to achieve better version integration and normalization, Aotter Trek adjusted the `dependency path` and `mediation class name path`.**\
****[**See Change Log**](../changelog.md)
{% endhint %}

{% hint style="warning" %}
**We are about to deprecated versions prior to 4.4.5**

**Recommend developer install above version 4.7.2**
{% endhint %}

****\
**Before version 4.4.5 ,please refer to the following.**

<pre class="language-groovy"><code class="lang-groovy">dependencies {

<strong>implementation 'com.aotter.net:trek-sdk-android-admob-mediation-kotlin:4.4.5'
</strong>
}
</code></pre>

**Above version 4.7.2 ,please refer to the following.**

<pre class="language-groovy"><code class="lang-groovy">dependencies {

<strong>implementation 'com.aotter.android:trek-admob-mediation:4.8.3'
</strong>
}
</code></pre>

Also, add the following code snippet in your **project-level** build.gradle.

<pre class="language-groovy"><code class="lang-groovy">allprojects {
    repositories {
        google()
        mavenCentral()
        
        // Add this
<strong>        maven { url 'https://deps.aotter.net/artifactory/libs-release-local' }
</strong>        
    }
}
</code></pre>

**AndroidManifest.XML**

Please add the following code snippet in your AndroidManifest.XML

```xml
<uses-permission android:name="com.google.android.gms.permission.AD_ID" />
```
