# Load an ad

Implementing banner ads in your app following steps:

* ****[**Add AdView to layout**](load-an-ad.md#add-adview-to-layout)****
* ****[**Loading ads**](load-an-ad.md#loading-ads)****
* ****[**Destroy ad**](load-an-ad.md#destroy-ad)****

### Add `AdView` to layout

The first step toward displaying a banner is to place **`AdView`** in the layout for the **`Activity`** or **`Fragment`** in which you'd like to display it.&#x20;

Here's an example that shows an activity's **`AdView`**:

<pre class="language-xml"><code class="lang-xml">&#x3C;com.google.android.gms.ads.AdView
    android:id="@+id/bannerAdView"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
<strong>    app:adSize="BANNER"
</strong><strong>    app:adUnitId="[Your AdMob Banner AdUnit]"
</strong>/>
</code></pre>

### **Loading ads**

{% hint style="info" %}
If request ad is  success , AdView is going to render view automatically.
{% endhint %}

{% tabs %}
{% tab title="Kotlin" %}
<pre class="language-kotlin"><code class="lang-kotlin">bannerAdView.adListener = object : AdListener() {
    override fun onAdLoaded() {
<strong>        super.onAdLoaded()
</strong>            //load ad success
    }
    override fun onAdFailedToLoad(loadAdError: LoadAdError) {
        super.onAdFailedToLoad(loadAdError)
            //load ad Failed
    }
}

val bundle = Bundle()

bundle.putString(TrekAdmobDataKey.CATEGORY, "[Page Category]")//ex."news"
bundle.putString(TrekAdmobDataKey.CONTENT_URL, "[Page Url]")//ex."https://agirls.aotter.net/"
bundle.putString(TrekAdmobDataKey.CONTENT_TITLE, "[Page Title]")//ex."電獺少女"

val adRequest = AdRequest
    .Builder()
    .addNetworkExtrasBundle(TrekAdmobCustomEventBanner::class.java, bundle)
    .build()
    
bannerAdView.loadAd(adRequest)
</code></pre>
{% endtab %}

{% tab title="Java" %}
<pre class="language-java"><code class="lang-java">bannerAdView.setAdListener(new AdListener() {
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
<strong>});
</strong>
Bundle bundle = new Bundle();

bundle.putString(TrekAdmobDataKey.CATEGORY, "[Page Category]");//ex."news"
bundle.putString(TrekAdmobDataKey.CONTENT_URL, "[Page Url]");//ex."https://agirls.aotter.net/"
bundle.putString(TrekAdmobDataKey.CONTENT_TITLE, "[Page Title]");//ex."電獺少女"

AdRequest adRequest = new AdRequest
    .Builder()
    .addNetworkExtrasBundle(TrekAdmobCustomEventBanner.class, bundle)
    .build();
    
bannerAdView.loadAd(adRequest);
</code></pre>
{% endtab %}
{% endtabs %}

### **Destroy ad**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
bannerAdView.destroy()
```
{% endtab %}

{% tab title="Java" %}
```java
bannerAdView.destroy();
```
{% endtab %}
{% endtabs %}
