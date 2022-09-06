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
<div id="supr-ad-container"></div>
<script>
  AotterTrekConfig = {
    // Notice: This client ID is for test only. Replace it with your own for official operation.
    clientId: "yEFcFoJaruNorh5RqtuR",
    place: "placement_UUID",
    selector: "#supr-ad-container",
    onAdLoad: () => {
       // Ad shows. Do something.},
    onAdFail: () => {
       // Ad fail. Do something.
    }
  }
  
 !function(){const e=window.top||window,t=e.document,n=document,r="TREK_SESSION",o="https://static.aottercdn.com/trek/sdk/3.4.5/sdk.js",c=n.createElement("link");n.getElementById("trek-catrun-preconnect")||(c.href="https://tkcatrun.aotter.net",c.rel="preconnect",n.head.insertAdjacentElement("beforeend",c));const s=n.createElement("link");n.getElementById("trek-sdk-preload")||(s.href=o,s.rel="preload",s.as="script",n.head.insertAdjacentElement("beforeend",s));const a=(e="")=>e?((Number(e)^16*Math.random())>>Number(e)/4).toString(16):"10000000-1000-4000-8000-100000000000".replace(/[018]/g,a),i=()=>(t.cookie.split(";").find((e=>e.includes(r)))||"").split("=")[1],d=new Promise((n=>{let r=i();r||((()=>{const n=e.location.hostname.substring(e.location.hostname.lastIndexOf(".",e.location.hostname.lastIndexOf(".")-1)+1),r=new Date((new Date).getTime()+94608e6).toUTCString();t.cookie=`TREK_SESSION=${a()};path=/;domain=${n};expires=${r}`})(),r=i());const o=encodeURIComponent(JSON.stringify({trekNetwork:"trek",device:{webSessionId:r},fetchNumber:1,returnBlank:!1,user:{},payload:{place:AotterTrekConfig.place,meta:{dr:t.referrer,dt:t.title,dl:t.location.href}}}));fetch(`https://r2d2.aotter.net/web/fetch?q=${o}`,{method:"GET",headers:{"x-aotter-clientid":AotterTrekConfig.clientId,"x-aotter-version":"web_3.4.5"},credentials:"include",mode:"cors"}).then((e=>e.json())).then((({success:e=[]})=>{n(e)})).catch((()=>{n([])}))})),l=new Promise((e=>{!function(t,n,r,o,c){let s,a=n.getElementsByTagName(r)[0];n.getElementById(c)||(s=n.createElement(r),s.id=c,t[c]=t[c]||function(){(t[c].q=t[c].q||[]).push(arguments)},t[c].l=1*new Date,s.async=1,s.src="https://static.aottercdn.com/trek/sdk/3.4.5/sdk.js",s.onload=()=>{e()},a.parentNode.insertBefore(s,a))}(window,document,"script",0,"AotterTrek")}));Promise.all([d,l]).then((([e])=>{AotterTrek("init",AotterTrekConfig.clientId),AotterTrek("suprAd",AotterTrekConfig,e)}))}();
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
