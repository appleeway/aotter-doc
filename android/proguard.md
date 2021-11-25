# ProGuard

### &#x20;- SDK

If you use ProGuard in your application, please add the following code snippet in your proguard-rules.pro.

```
-keep class com.aotter.net.** {*;}
```

### - AdMob Mediation

For developers integrating with _**AdMob Mediation**_, please add the code snippet below in your proguard-rules.pro.

```java
-keep class com.admob.mediation.kotlin.** {*;}
```

### - MoPub Mediation

For developers integrating with _**MoPub Mediation**_, please add the code snippet below in your proguard-rules.pro.

```kotlin
-keep class com.mopub.mediation.kotlin.** {*;}
```
