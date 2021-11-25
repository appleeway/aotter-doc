# Supr.Ad

Follow these steps to build a Supr.Ad layout and then requests it.

Step 1: [Insert `<div>` tag ](supr.ad.md#step-1-insert-less-than-div-greater-than-tag)\
Step 2: [Execute Ad Request](supr.ad.md#step-2-execute-ad-request)

### Step 1: Insert `<div>` tag&#x20;

You can insert the following line to where you want to show the ad.\
Please replace`placement_UUID` with your ad place UUID.

```markup
<div id="suprAdContainer" data-place="placement_UUID"></div>
```

### Step 2: Execute Ad Request

```markup
<script>
  AotterTrek('suprAd', {
    selector: '#suprAdContainer',
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

![](<../../.gitbook/assets/截圖 2021-04-01 下午3.40.15.png>)
