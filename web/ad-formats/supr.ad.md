# Supr.Ad

**Supr.Ad Size**

\- 300x250    - 336x280

Follow these steps to build a Supr.Ad layout and then requests it.

Step 1: [Insert `<div>` tag ](supr.ad.md#step-1-insert-less-than-div-greater-than-tag)\
Step 2: [Execute Ad Request](supr.ad.md#step-2-execute-ad-request)

### Step 1: Insert `<div>` tag&#x20;

You can insert the following line to where you want to show the ad.

```markup
<div id="suprAdContainer"></div>
```

### Step 2: Execute Ad Request

Please replace`placement_UUID` with your ad place UUID.

```markup
<script>
  AotterTrek('suprAd', {
    selector: '#suprAdContainer',
    place: 'placement_UUID',
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

![](<../../.gitbook/assets/截圖 2021-12-07 下午4.26.30.png>)
