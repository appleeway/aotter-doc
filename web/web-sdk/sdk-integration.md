# Installation

This guide is for web developers who want to monetize a website with AotterTrek. Integrating AotterTrek SDK into your web pages will be the first step before displaying Ads and earning revenue. Follow the steps below to get started!

Step 1: [Including the SDK](sdk-integration.md#step-1-including-the-sdk)\
Step 2: [Execute `AotterTrek()` ](sdk-integration.md#step-2-execute-aottertrek)\
Step 3: [Insert \<div>\</div> tag with trek-ad attribute](sdk-integration.md#step-3-insert-less-than-div-greater-than-less-than-div-greater-than-tag-with-trek-ad-attribute)\
[Full Example](sdk-integration.md#full-example)

{% hint style="info" %}
Note: AotterTrek SDK only supports displaying Ads on **mobile and tablet websites** currently.&#x20;
{% endhint %}

### Step 1: Including the SDK

Please copy the following code snippet then paste it within the `<body>` section of your pages. It's better to put it right before the closing tag.

{% hint style="info" %}
Please use **your client id** for initialization which can be found in the [application list](https://trek.aotter.net/publisher/list/app).&#x20;
{% endhint %}

```markup
<!-- start: trek sdk -->
<script>
  (function(w, d, s, src, n) {
    var js, ajs = d.getElementsByTagName(s)[0];
    if (d.getElementById(n)) return;
    js = d.createElement(s); js.id = n;
    w[n] = w[n] || function() { (w[n].q = w[n].q || []).push(arguments) }; w[n].l = 1 * new Date();
    js.async = 1; js.src = src; ajs.parentNode.insertBefore(js, ajs)
  })(window, document, 'script', 'https://static.aottercdn.com/trek/sdk/3.5.1/sdk.js', 'AotterTrek');

  // Notice: replace your own client id or use our test id.
  AotterTrek('init', 'CLIENT_ID');
  AotterTrek('send');
</script>
<!-- end: trek sdk -->
```

### Test ad units

We also provide test client id and test place id for receiving test ads only.

{% hint style="info" %}
* Test Client ID **:**&#x20;
  * **yEFcFoJaruNorh5RqtuR**
* Test Place ID **:**&#x20;
  * banner 640x100:
    * **8624cdd7-c71a-4df2-b9c9-cd93fe79b890**
{% endhint %}

### Step 2: Execute AotterTrek()

To displaying Ads, you need to invoke `AotterTrek()`. Put the following code snippet after trek SDK.

```markup
<script>
 AotterTrek('suprAd', {
    selector: '#adContainer', //#id, .class or any other selector
    place: 'placement_UUID',
    onAdLoad: () => {
        // Ad shows. Do something.
    },
    onAdFail: () => {
        // Ad fail. Do something.
    }   
} )
</script>
```

{% hint style="warning" %}
Please replace`placement_UUID` with the ad place UUID in the ad slot management.

For the publisher who use AotterTrek SDK for the first time and didn't get full access to ad slot management, please contact Aseal representative or [E-mail us](https://aseal.in/contactus).
{% endhint %}

### Step 3: Insert \<div>\</div> tag

Insert the following `<div>` tag to the place you want to display Ad.

```markup
<div id="adContainer"></div>
```

### Done! 👏🏼

AotterTrek web SDK will parse `<div id="adContainer">` to an ad view.

![](<../../.gitbook/assets/截圖 2021-12-07 下午4.26.30.png>)

## Full Example

```markup
<body>
    <div id="adContainer"></div>
    <!-- start: trek sdk -->
    <script>
        (function(w, d, s, src, n) {
            var js, ajs = d.getElementsByTagName(s)[0];
            if (d.getElementById(n)) return;
            js = d.createElement(s); js.id = n;
            w[n] = w[n] || function() { (w[n].q = w[n].q || []).push(arguments) }; w[n].l = 1 * new Date();
            js.async = 1; js.src = src; ajs.parentNode.insertBefore(js, ajs)
        })(window, document, 'script', 'https://static.aottercdn.com/trek/sdk/3.5.1/sdk.js', 'AotterTrek');

        // Notice: This client ID is for test only. Replace it to your own for official operation.
        AotterTrek('init', 'yEFcFoJaruNorh5RqtuR');
        AotterTrek('send')
    </script>
    <!-- end: trek sdk -->
    <script>
        AotterTrek('suprAd', { 
          selector: '#adContainer',
          place: 'placement_UUID',
          onAdLoad: () => {
            // Ad shows. Do something.
          },
          onAdFail: () => {
            // Ad fail. Do something.
          }
        })
    </script>
</body>
```
