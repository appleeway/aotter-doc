# Banner Ad

Follow these steps to build a banner ad layout and then requests it.

Step 1: [Create Banner Ad Layout](banner-ad-layout.md#step-1-create-banner-ad-layout)\
Step 2: [Create `AdView`](banner-ad-layout.md#step-2-create-adview)\
Step 3: [Set Ad Listener](banner-ad-layout.md#step-3-set-ad-listener)\
Step 4: [Set Ad Layout](banner-ad-layout.md#step-4-set-ad-layout)\
Step 5: [Create `AdRequest`](banner-ad-layout.md#step-5-create-adrequest)\
Step 6: [Request an Ad](banner-ad-layout.md#step-6-request-an-ad)

### Step 1: Create Banner Ad Layout

#### **Example Banner ad layout**

```kotlin
<LinearLayout
        android:id="@+id/linearLayout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="vertical"
/>
```

### **Step 2: Create `AdView`**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val bannerAdView = AdView(context)

bannerAdView.adSize = AdSize.BANNER

bannerAdView.adUnitId = "YOUR_ADUNID"
```
{% endtab %}

{% tab title="Java" %}
```java
AdView bannerAdView = new AdView(context);

bannerAdView.setAdSize(AdSize.BANNER); 

bannerAdView.setAdUnitId("YOUR_ADUNID"); 
```
{% endtab %}
{% endtabs %}

### Step 3: Set Ad Listener

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
bannerAdView.adListener = object : AdListener() {
            override fun onAdLoaded() {
                super.onAdLoaded()
                //load ad success
            }

            override fun onAdFailedToLoad(loadAdError: LoadAdError) {
                super.onAdFailedToLoad(loadAdError)
                //load ad Failed
            }
        }
```
{% endtab %}

{% tab title="Java" %}
```java
bannerAdView.setAdListener(new AdListener() {

            @Override
            public void onAdLoaded() {
                super.onAdLoaded();    
                //load ad success 
            }

            @Override
            public void onAdFailedToLoad(@NonNull LoadAdError loadAdError) {
                super.onAdFailedToLoad(loadAdError); 
                 //load ad Failed           
            }
            
        });
```
{% endtab %}
{% endtabs %}

### Step 4: Set Ad Layout

Set layout in the callback function of `onAdLoaded`.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
.....

override fun onAdLoaded() {
    super.onAdLoaded()
    linearLayout.addView(bannerAdView)
}

.....
```
{% endtab %}

{% tab title="Java" %}
```java
.....

@Override
public void onAdLoaded() {
    super.onAdLoaded();           
    linearLayout.addView(bannerAdView);          
}

.....
```
{% endtab %}
{% endtabs %}

### **Step 5: Create `AdRequest`**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val adRequest = AdRequest
    .Builder()
    .build()

//or you can bundle a category

val bundle = Bundle()

bundle.putString(TrekAdmobDataKey.CATEGORY, "YOU_CATEGORY")//ex."news"

val adRequest = AdRequest
    .Builder()
    .addCustomEventExtrasBundle(TrekAdmobCustomEventBanner::class.java, bundle)
    .build()
```
{% endtab %}

{% tab title="Java" %}
```java
AdRequest adRequest = new AdRequest
    .Builder()
    .build();

//or you can bundle a category

Bundle bundle = new Bundle();

bundle.putString(TrekAdmobDataKey.CATEGORY, "YOU_CATEGORY");//ex."news"

AdRequest adRequest = new AdRequest
    .Builder()
    .addCustomEventExtrasBundle(TrekAdmobCustomEventBanner.class, bundle)
    .build();
```
{% endtab %}
{% endtabs %}

### Step 6: Request an Ad

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
bannerAdView.loadAd(adRequest)
```
{% endtab %}

{% tab title="Java" %}
```java
bannerAdView.loadAd(adRequest);
```
{% endtab %}
{% endtabs %}
