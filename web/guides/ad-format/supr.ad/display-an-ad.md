# Display an ad

### Implementing banner ads in your website following steps:

#### **Step 1.**[**Insert \<div>\</div> Tag**](display-an-ad.md#insert-less-than-div-greater-than-less-than-div-greater-than-tag)****

#### **Step 2.**[**Execute ad request**](display-an-ad.md#execute-ad-request)****

### ****[**Insert \<div>\</div> Tag**](display-an-ad.md#step-1.insert-less-than-div-greater-than-less-than-div-greater-than-tag)****

The first step toward displaying a suprAd is to place `<div></div>` in the website's `<body></body>` in which you'd like to display it.

Here's an example that shows an `<div></div>`

```html
<div id="supr-ad-container"></div>
```

### [Execute ad request](display-an-ad.md#step-2.execute-ad-request)

The second step is to execute AotterTrek('suprAd') . When SDK was loaded, SDK will attach an AotterTrek method in a global window. So you can call it method in page anywhere.

{% hint style="info" %}
If request ad is success, \<div>\</div> is going to render ad automatically.
{% endhint %}

```html
<script>
  AotterTrek('suprAd', {
    selector: '#supr-ad-container',
    place: '[Your Trek SuprAd PlaceUid]',
    onAdLoad: () => {
        // Ad shows. Do something.
    },
    onAdFail: () => {
       // Ad fail or no ads. Do something.
    }
  })
</script>
```
