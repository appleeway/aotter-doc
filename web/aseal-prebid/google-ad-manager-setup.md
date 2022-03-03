# Google Ad Manager Setup

If this is the first time you are setting up a Prebid campaign in Google Ad Manager, please contact our FAE for help. Also, You can check out the steps below for a brief step-step description. For more detail, please check the official Prebid documentation [here](https://docs.prebid.org/adops/step-by-step.html).

### Step 1: Add key / value

The keyword `hb_pb` is used to define the line item targeting criteria (image below). **You must enter the value to two decimal places, e.g., `1.50`. If you don’t use two decimal places, header bidding will not work.**

![](<../../.gitbook/assets/PlUCtSEg (1).png>)

### Step 2: Add a line item

Create a new line item. Enter all of the inventory sizes that your website has. Because header bidding partners return prices, set the Line Item **Type** to **Price priority** to enable them to compete on price.

![](<../../.gitbook/assets/5JN1DWtw (1).png>)

Other settings include：

* **Rate**: _Set to $0.50 so that this line item will compete with your other demand sources at $0.50 ECPM_.
* **Display Creatives**: _One or More since we’ll have one or more creatives attached to this line item_.
* **Rotate Creatives**: _Evenly_.
* **Targeting**: Target the inventory you would like to show Ad and keyword `hb_pb`.

![](<../../.gitbook/assets/fZvcsr7u (1) (1).png>)

### Step 3: Add a Creative

Note that this has to be a **Third-party** creative. Copy this creative code snippet and paste it into the **Code snippet** box.

(Creative code - Prebid Universal Creative)

```html
<script src = "https://cdn.jsdelivr.net/npm/prebid-universal-creative@latest/dist/creative.js"></script>
<script>
  var ucTagData = {};
  ucTagData.adServerDomain = "";
  ucTagData.pubUrl = "%%PATTERN:url%%";
  ucTagData.targetingMap = %%PATTERN:TARGETINGMAP%%;
  ucTagData.hbPb = "%%PATTERN:hb_pb%%";

  try {
    ucTag.renderAd(document, ucTagData);
  } catch (e) {
    console.log(e);
  }
</script>
```

### Step 4: Attach the Creative to the Line Item

Next, let’s attach the creative to the $0.50 line item you just created. Click into the Line Item, then the **Creatives** tab. There will be a yellow box showing each ad spot that you haven’t uploaded creatives for yet. Since you’ve already made the creatives, click **use existing creatives** next to each size.

![](<../../.gitbook/assets/zIbE8BSj (1).png>)
