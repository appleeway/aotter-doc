# Installation

### Getting Started

We have provided demo and mediation adapter source.

To receive release updates, subscribe to our [GitHub repository.](https://github.com/aotter/aotter-trek-mediation-android)

### Add the SDK to the Project

**Using Gradle**

Add the following dependencies to your **app-level** build.gradle (not project!), to use the latest AotterTrek adapter:

{% hint style="info" %}
**In order to achieve better version integration and normalization, Aotter Trek SDK adjusted the `dependency paths` and `mediation class name paths.`**\
****\
**``We recommend that developers install new `mediation class name` paths and new dependency paths.**\
****\
**Please note,we will  deprecated old Trek SDK dependency paths and old `mediation class name` paths.**
{% endhint %}

****\
**Old Trek Admob mediation dependency paths  ,please refer to the following.**

```groovy
dependencies {

implementation 'com.aotter.net:trek-sdk-android-admob-mediation-kotlin:4.7.2'

}
```

**New Trek Admob mediation dependency paths  ,please refer to the following.**

```groovy
dependencies {

implementation 'com.aotter.android:trek-admob-mediation:4.7.2'

}
```

Also, add the following code snippet in your **project-level** build.gradle.

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
