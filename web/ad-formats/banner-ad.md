# Banner Ad

**Banner Ad Size**

\- 320x50    - 640x100

We provide different kinds of sizes in banner ads, but the size has been decided by you in the ad slot phase. See [Create an Ad Slot](../web-sdk/prerequisites.md#step-3-create-an-ad-slot).

Follow these steps to build a banner ad layout and then requests it.

Step 1: [Insert `<div>` tag ](banner-ad.md#step-1-insert-less-than-div-greater-than-tag)\
Step 2: [Execute Ad Request](banner-ad.md#step-2-execute-ad-request)

### Step 1: Insert `<div>` Tag

You can insert the following line to where you want to show the ad.

```markup
<div id="bannerAdContainer"></div>
```

### Step 2: Execute Ad Request

Please replace`placement_UUID` with your ad place UUID.

```markup
<script>
  AotterTrek('suprAd', {
    selector: '#bannerAdContainer',
    place: 'placement_UUID',
    mobile: true,
    fixed: 'bottom',
    onAdLoad: () => {
        // Ad shows. Do something.
    },
    onAdFail: () => {
        // Ad fail. Do something.
    }
  })
</script>
```

{% hint style="warning" %}
Noted that when you set `mobile: true`, the ad will only be shown on the **mobile web**.
{% endhint %}

We also provide **top** of the page ads by simply change the `fixed: 'bottom'`  to `fixed: 'top'`.

### Done! 👏🏼

![](broken-reference)
