# Banner Ad

**Banner Ad Size**

\- 320x50    - 640x100

We provide different kinds of sizes in banner ads, but the size has been decided by you in the ad slot phase. See [Create an Ad Slot](../web-sdk/prerequisites.md#step-3-create-an-ad-slot).

Follow these steps to build a banner ad layout and then requests it.

Step 1: [Insert `<div>` tag ](banner-ad.md#step-1-insert-less-than-div-greater-than-tag)\
Step 2: [Execute Ad Request](banner-ad.md#step-2-execute-ad-request)

### Step 1: Insert `<div>` Tag

You can insert the following line to where you want to show the ad.\
Please replace`placement_UUID` with your ad place UUID.

```markup
<div id="bannerAdContainer" data-place="placement_UUID"></div>
```

We also provide **top/bottom** of the page ads by simply adding the following dataset attributes.

* **Top of the Page Ad** : `data-fixed="top"`

```markup
    <div
      id="bannerAdContainer"
      data-fixed="top"
      data-mobile
      data-place="placement_UUID"
    ></div>
```

* **Bottom of the Page Ad** : `data-fixed="bottom"`

```markup
<div
      id="bannerAdContainer"
      data-fixed="bottom"
      data-mobile
      data-place="placement_UUID"
    ></div>
```

{% hint style="warning" %}
Noted that when you add dataset attribute `data-mobile`, the ad will only be shown on the **mobile web**.
{% endhint %}

### Step 2: Execute Ad Request

```markup
<script>
  AotterTrek('suprAd', {
    selector: 'bannerAdContainer',
    onAdLoad: () => {
        // Ad shows. Do something.
    },
    onAdFail: () => {
        // Ad fail. Do something.
    }
  })
</script>
```

### Done! 👏🏼

![](<../../.gitbook/assets/截圖 2022-06-10 上午11.28.47.png>)
