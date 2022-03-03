# Aseal Prebid.js Adapter

### Aseal Prebid.js Adapter Setup for Web <a href="#aseal-prebid.js-adapter-setup-for-web" id="aseal-prebid.js-adapter-setup-for-web"></a>

​[Step 0: Prerequisites](aseal-prebid.js-adapter.md#step-0-prerequisites) \
[Step 1: Google Ad Manager Setup ](aseal-prebid.js-adapter.md#step-1-google-ad-manager-setup)\
[Step 2: Download Prebid.js with Aseal Adapter selected ](aseal-prebid.js-adapter.md#step-2-download-prebid.js-with-aseal-adapter-selected)\
[Step 3: Registering the Aseal bidder ](aseal-prebid.js-adapter.md#step-3-registering-the-aseal-bidder)\
[Step 4: Configure Client ID​](aseal-prebid.js-adapter.md#step-4-configure-client-id)

### **Step 0: Prerequisites** <a href="#step-0-prerequisites" id="step-0-prerequisites"></a>

See [Prerequisites](../web-sdk/prerequisites.md) section.

### **Step 1: Google Ad Manager Setup** <a href="#step-1-google-ad-manager-setup" id="step-1-google-ad-manager-setup"></a>

See [Google Ad Manager Setup](google-ad-manager-setup.md) section.

### **Step 2: Download Prebid.js with Aseal Adapter selected** <a href="#step-2-download-prebid.js-with-aseal-adapter-selected" id="step-2-download-prebid.js-with-aseal-adapter-selected"></a>

Download prebid.js from [Prebid.org](https://docs.prebid.org/download.html) or manually build from [Github](https://github.com/prebid/Prebid.js/releases), including the Aseal adapter and the required modules.

![](<../../.gitbook/assets/截圖 2022-01-28 下午3.45.13.png>)

### **Step 3: Registering the Aseal bidder** <a href="#step-3-registering-the-aseal-bidder" id="step-3-registering-the-aseal-bidder"></a>

All you will need to do is to register Aseal's bidder to each of your adunits. You will find an example below. Please include the Aseal bidder and the **`placeUid` ** provided by your AotterTrek Ad Slot Management.

{% hint style="info" %}
Note: the snippet below is just an example, **please use the identifiers provided by AotterTrek Ad Slot Management**.
{% endhint %}

```javascript
pbjs.que.push(function () {
    var adUnits = [{
        code: "div-gpt-ad-1642581403289-0",
        mediaTypes: {
            banner: {
                sizes: [[300, 250]]
            }
        },
        bids: [{
            bidder: "aseal",
            params: {
                // your Aottertrek place uuid    
                placeUid: "f1ba50f4-1c7d-4448-b5c8-de26db863180" 
            }
        }, {
            bidder: "appnexus",
            params: { placementId: "234235" }
        }]
    }];
    pbjs.addAdUnits(adUnits);
})
```

| Property   | Type   | Description                                                                                   | Required? |
| ---------- | ------ | --------------------------------------------------------------------------------------------- | --------- |
| `placeUid` | string | AotterTrek ad place id provided by Aseal. For example: `f1ba50f4-1c7d-4448-b5c8-de26db863180` | Required  |

### **Step 4: Configure Client ID** <a href="#step-4-configure-client-id" id="step-4-configure-client-id"></a>

Use the function `pbjs.setConfig` providing your Client ID.

```javascript
pbjs.setConfig({
    aseal: {
      // your Aottertrek client Id
      clientId: "yEFcFoJaruNorh5RqtuR"
  }
}); 
```

| Property   | Type   | Description                                                                 | Required? |
| ---------- | ------ | --------------------------------------------------------------------------- | --------- |
| `clientId` | string | AotterTrek client id provided by Aseal. For example: `yEFcFoJaruNorh5RqtuR` | Required  |
