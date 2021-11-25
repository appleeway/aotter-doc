# Installation

### Including the SDK

**Using Gradle**

Add the following dependencies to your **app-level** build.gradle (not project!), to use the latest AotterTrek adapter:

```kotlin
dependencies {
    implementation 'com.aotter.net:trek-sdk-android-mopub-mediation-kotlin:4.1.8'
}
```

Also, add the following code snippet in your **project-level** build.gradle.

```kotlin
allprojects {
    repositories {
        google()
        
        // add below 
        mavenCentral() 
        maven { url 'https://deps.aotter.net/artifactory/libs-release-local' }
        
    }
}
```

**AndroidManifest.XML**

Please add the following code snippet in your AndroidManifest.XML

```
<uses-permission android:name="com.google.android.gms.permission.AD_ID" />
```
