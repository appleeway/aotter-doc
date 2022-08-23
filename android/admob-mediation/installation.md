# Installation

### Getting Started

We have provider demo and mediation adapter source.

To receive release updates, subscribe to our [GitHub repository.](https://github.com/aotter/aotter-trek-mediation-android)

### Add the SDK to the Project

**Using Gradle**

Add the following dependencies to your **app-level** build.gradle (not project!), to use the latest AotterTrek adapter:

```groovy
dependencies {

//before version 4.6.1
implementation 'com.aotter.net:trek-sdk-android-admob-mediation-kotlin:4.6.1'

//above version 4.7.2
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
