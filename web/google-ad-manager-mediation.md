# Google Ad Manager Mediation

This section provides instructions on using Google Ad Manager for displaying AotterTrek ads. Please follow the steps below set your Google Ad Manager.

Step 1: [Add Creatives](google-ad-manager-mediation.md#step-1-add-creatives)\
Step 2: [Set Up Orders, Line Items](google-ad-manager-mediation.md#step-2-set-up-orders-line-items)\
Step 3: [Create Ad Unit and Generate Publisher Tag](google-ad-manager-mediation.md#step-3-create-ad-unit-and-generate-publisher-tag)

### Step 1: Add Creatives

1. Click "**ADD CREATIVES**" to add a new creative.&#x20;
2. Choose "**Third-Party**" section to use code from the third-party ad server.
3. Copy the code block below and paste it to the "Code snippet" in GAM.
4. Replace the `"placement_UUID"` with your own ad place UUID and use your **client ID** instead of the test client ID in the following code block.

```markup
 <div id="suprAdContainer" data-place="placement_UUID"></div>

<!-- start: trek sdk -->
<script>
    (function(w, d, s, src, n) {
        var js, ajs = d.getElementsByTagName(s)[0];
        if (d.getElementById(n)) return;
        js = d.createElement(s); js.id = n;
        w[n] = w[n] || function() { (w[n].q = w[n].q || []).push(arguments) }; w[n].l = 1 * new Date();
        js.async = 1; js.src = src; ajs.parentNode.insertBefore(js, ajs)
    })(window, document, 'script', 'https://static.aottercdn.com/trek/sdk/3.3.2/sdk.js', 'AotterTrek');

// Notice: This client ID is for test only. Replace it with your own for official operation.
    AotterTrek('init', 'yEFcFoJaruNorh5RqtuR');
</script>
<!-- end: trek sdk -->

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

{% hint style="warning" %}
Please replace`placement_UUID`with your ad place UUID.
{% endhint %}

Please refer to the screenshot below and note that "**Serve into a SafeFrame**" is not supported currently. **Do not select the checkbox**.

![](../.gitbook/assets/1636013796274.jpg)

### Step 2: Set Up Orders, Line Items

To run a new ad campaign through Google Ad Manager you have to create a new order, set up line items, add creatives, and approve the order to serve the ads.&#x20;

1. Click `Orders` tab on the left-side column in Google Ad Manager.
2. Click `New order` to create a new order.
3. Fill in the information.
4. Click `Create Line Items` the button below.
5. Fill in the line item name, which must be unique.
6. Enter the type of line item, size of the creates, dates, quantity, and cost.&#x20;
7. Select the inventory in which you would like to deliver ads. You can target ad units, placements, or both. ( If you set to serve as run-of-network, it means that the line item can serve to any ad unit on your website.)
8. After finishing the line item set, click `Save` to save it.

### Step 3: Create Ad Unit and Generate Publisher Tag

1. Create a new ad unit.
2. Set up name, size, and other items for the ad unit.
3. Enter the ad unit and click the Code tab on the top.
4. Choose Publish Tag and click continue.
5. Select tag options. (Make sure you check the "Enable single request" checkbox.)
6. Paste the code snippet into your website.&#x20;
