# Installation

Setup SDK in your website following steps:

* ****[**Setup the Trek Ads SDK**](installation.md#initialize\_the\_mobile\_ads\_sdk)****

## Setup the Trek Ads SDK <a href="#initialize_the_mobile_ads_sdk" id="initialize_the_mobile_ads_sdk"></a>

Before we start, we need to install the Trek Ads SDK on your website.

The following HTML example is placed at the  bottom of inside `<body></body>`, you can of course choose to place it in the `<head></head>` section, but we would prefer that you place it in body.

```html
<!-- start: trek sdk -->
<script>
  (function(w, d, s, src, n) {
    var js, ajs = d.getElementsByTagName(s)[0];
    if (d.getElementById(n)) return;
    js = d.createElement(s); js.id = n;
    w[n] = w[n] || function() { (w[n].q = w[n].q || []).push(arguments) }; w[n].l = 1 * new Date();
    js.async = 1; js.src = src; ajs.parentNode.insertBefore(js, ajs)
  })(window, document, 'script', 'https://static.aottercdn.com/trek/sdk/3.5.4/sdk.js', 'AotterTrek');

  // Notice: replace your own client id or use our test id.
  AotterTrek('init', '[Trek client id]');
  AotterTrek('send');
</script>
<!-- end: trek sdk -->
```
