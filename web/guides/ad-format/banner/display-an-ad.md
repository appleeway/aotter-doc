# Display an ad

Implementing banner ads in your website following steps:

* ****[**Insert \<div>\</div> Tag**](display-an-ad.md#insert-less-than-div-greater-than-less-than-div-greater-than-tag)****
* ****[**Execute ad request**](display-an-ad.md#execute-ad-request)****

### **Insert \<div>\</div> Tag**

The first step toward displaying a banner is to place `<div></div>` in the website's `<body></body>`.

Here's an example that shows an `<div></div>`

```html
<div id="banner-ad-container"></div>
```

### Execute ad request

The second step is to execute AotterTrek('suprAd') . When SDK was loaded, SDK will attach an AotterTrek method in a global window. So you can call it method in page anywhere.

{% hint style="info" %}
If request ad is success, \<div>\</div> is going to render ad automatically.
{% endhint %}

{% hint style="info" %}
Noted that when you set option `mobile: true`, the ad will only be shown on the **mobile web**.
{% endhint %}

```html
<script>
  AotterTrek('suprAd', {
    selector: '#banner-ad-container',
    place: '[Your Trek Banner PlaceUid]',
    mobile: true,
    fixed: 'bottom',
    onAdLoad: () => {
        // Ad load success. Do something.
    },
    onAdFail: () => {
       // Ad fail or no ads. Do something.
    }
  })
</script>
```

We also provide **top** of the page ads by simply change the `fixed: 'bottom'`  to `fixed: 'top'`.
