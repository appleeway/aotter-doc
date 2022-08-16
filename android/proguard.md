# ProGuard

### &#x20;- SDK

If you use ProGuard in your application, please add the following code snippet in your proguard-rules.pro.

```groovy
-keep class com.aotter.net.** {*;}
```

### - AdMob Mediation

For developers integrating with _**AdMob Mediation**_, please add the code snippet below in your proguard-rules.pro.

```groovy
-keep class com.aotter.trek.admob.mediation.** {*;}
```

