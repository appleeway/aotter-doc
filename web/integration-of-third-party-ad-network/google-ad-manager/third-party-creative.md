# Third-party Creative

### Create [ads](broken-reference) with Google Ad Manager Creative following steps:

#### **Step 1.**[**Find where can create third-party creative in Google Ad Manager**](third-party-creative.md#find-where-can-create-third-party-creative-in-google-ad-manager)****

#### **Step 2.**[**Create a new third-party creative**](third-party-creative.md#create-a-new-third-party-creative)****

### [Find where can create third-party creative in Google Ad Manager](third-party-creative.md#step-1.find-where-can-create-third-party-creative-in-google-ad-manager)

<figure><img src="../../../.gitbook/assets/Third-party Creative step1.webp" alt=""><figcaption></figcaption></figure>

1. Click on `Delivery` in the sidebar.
2. `Creatives` This subcategory will appear, click on it.
3. The content on the right will change to Creative and we will click `New creative` button.

<figure><img src="../../../.gitbook/assets/Third-party Creative step2.png" alt=""><figcaption></figcaption></figure>

1. Next, choose the advertiser that Creative belongs to.
2. Then find the category Third-party and select the link `Select`.

### [Create a new third-party creative](third-party-creative.md#step-2.create-a-new-third-party-creative)

<figure><img src="../../../.gitbook/assets/Third-party Creative step3.webp" alt=""><figcaption></figcaption></figure>

1. After filling in the other information, it is important to note that the Standard field should be filled in with our Google Ad Manager special HTML content.

**Example HTML content:**

```html
<div id="supr-ad-container"></div>
<script>
  AotterTrekConfig = {
    // Notice: This client ID is for test only. Replace it with your own for official operation.
    clientId: '[Trek client id]',
    selector: '#supr-ad-container',
    place: '[Your Trek SuprAd PlaceUid]',
    onAdLoad: () => {
       // Ad shows. Do something.
    },
    onAdFail: () => {
       // Ad fail. Do something.
    }
  }
  
 !function(){"use strict";const e=window.top||window,t=e.document,n=document,o="TREK_SESSION",r="https://static.aottercdn.com/trek/sdk/3.5.4/sdk.js",c="web_3.5.4",i=n.createElement("link");n.getElementById("trek-catrun-preconnect")||(i.href="https://tkcatrun.aotter.net",i.rel="preconnect",n.head.insertAdjacentElement("beforeend",i));const s=n.createElement("link");n.getElementById("trek-sdk-preload")||(s.href=r,s.rel="preload",s.as="script",n.head.insertAdjacentElement("beforeend",s));const d=(e="")=>e?((Number(e)^16*Math.random())>>Number(e)/4).toString(16):"10000000-1000-4000-8000-100000000000".replace(/[018]/g,d),a=()=>(t.cookie.split(";").find((e=>e.includes(o)))||"").split("=")[1],l=()=>{const n=(()=>{const t=`__tk${Math.random()}`,n=new Date(0),o=e.location.hostname.split("."),r=[];for(r.unshift(o.pop());o.length;){r.unshift(o.pop());const e=r.join("."),c=`${t}=;domain=${e}`;if(document.cookie=c,document.cookie.includes(t))return document.cookie=`${c};expires=${n}`,e}})(),o=new Date((new Date).getTime()+94608e6).toUTCString();t.cookie=`TREK_SESSION=${d()};path=/;domain=${n};expires=${o}`},m=new Promise((e=>{let n=a();n||(l(),n=a());const o=encodeURIComponent(JSON.stringify({device:{webSessionId:n},fetchNumber:1,returnBlank:!1,user:{},payload:{place:AotterTrekConfig.place,meta:{dr:t.referrer,dt:t.title,dl:t.location.href}},sdkVersionCode:10,sdkVersion:c}));fetch(`https://r2d2.aotter.net/web/fetch?q=${o}`,{method:"GET",headers:{"x-aotter-clientid":AotterTrekConfig.clientId,"x-aotter-version":c},credentials:"include",mode:"cors"}).then((e=>e.json())).then((({success:t=[]})=>{e(t)})).catch((()=>{e([])}))})),k=new Promise((e=>{!function(t,n,o,r,c){let i,s=n.getElementsByTagName(o)[0];n.getElementById(c)||(i=n.createElement(o),i.id=c,t[c]=t[c]||function(){(t[c].q=t[c].q||[]).push(arguments)},t[c].l=1*new Date,i.async=1,i.src="https://static.aottercdn.com/trek/sdk/3.5.4/sdk.js",i.onload=()=>{e()},s.parentNode.insertBefore(i,s))}(window,document,"script",0,"AotterTrek")}));Promise.all([m,k]).then((([e])=>{AotterTrek("init",AotterTrekConfig.clientId),AotterTrek("suprAd",AotterTrekConfig,e),AotterTrek("send")}))}();
</script>
```

#### Example **HTML content** with Passback:

```html
<div id="gpt-passback">
   <div id="supr-ad-container"></div>
</div>
<script async src="https://securepubads.g.doubleclick.net/tag/js/gpt.js"></script>
<script>
  AotterTrekConfig = {
    // Notice: This client ID is for test only. Replace it with your own for official operation.
    clientId: '[Trek client id]',
    selector: '#supr-ad-container',
    place: '[Your Trek SuprAd PlaceUid]',
    onAdLoad: () => {
       // Ad shows. Do something.
    },
    onAdFail: () => {
      window.googletag = window.googletag || {cmd: []};
         googletag.cmd.push(function() {
            googletag.defineSlot('slot_name', [[300, 250], [336, 280]], 'gpt-passback').addService(googletag.pubads());
            googletag.enableServices();
            googletag.display('gpt-passback');
         });
    }
  }
  
 !function(){"use strict";const e=window.top||window,t=e.document,n=document,o="TREK_SESSION",r="https://static.aottercdn.com/trek/sdk/3.5.1/sdk.js",c="web_3.5.1",i=n.createElement("link");n.getElementById("trek-catrun-preconnect")||(i.href="https://tkcatrun.aotter.net",i.rel="preconnect",n.head.insertAdjacentElement("beforeend",i));const s=n.createElement("link");n.getElementById("trek-sdk-preload")||(s.href=r,s.rel="preload",s.as="script",n.head.insertAdjacentElement("beforeend",s));const d=(e="")=>e?((Number(e)^16*Math.random())>>Number(e)/4).toString(16):"10000000-1000-4000-8000-100000000000".replace(/[018]/g,d),a=()=>(t.cookie.split(";").find((e=>e.includes(o)))||"").split("=")[1],l=()=>{const n=(()=>{const t=`__tk${Math.random()}`,n=new Date(0),o=e.location.hostname.split("."),r=[];for(r.unshift(o.pop());o.length;){r.unshift(o.pop());const e=r.join("."),c=`${t}=;domain=${e}`;if(document.cookie=c,document.cookie.includes(t))return document.cookie=`${c};expires=${n}`,e}})(),o=new Date((new Date).getTime()+94608e6).toUTCString();t.cookie=`TREK_SESSION=${d()};path=/;domain=${n};expires=${o}`},m=new Promise((e=>{let n=a();n||(l(),n=a());const o=encodeURIComponent(JSON.stringify({device:{webSessionId:n},fetchNumber:1,returnBlank:!1,user:{},payload:{place:AotterTrekConfig.place,meta:{dr:t.referrer,dt:t.title,dl:t.location.href}},sdkVersionCode:10,sdkVersion:c}));fetch(`https://r2d2.aotter.net/web/fetch?q=${o}`,{method:"GET",headers:{"x-aotter-clientid":AotterTrekConfig.clientId,"x-aotter-version":c},credentials:"include",mode:"cors"}).then((e=>e.json())).then((({success:t=[]})=>{e(t)})).catch((()=>{e([])}))})),k=new Promise((e=>{!function(t,n,o,r,c){let i,s=n.getElementsByTagName(o)[0];n.getElementById(c)||(i=n.createElement(o),i.id=c,t[c]=t[c]||function(){(t[c].q=t[c].q||[]).push(arguments)},t[c].l=1*new Date,i.async=1,i.src="https://static.aottercdn.com/trek/sdk/3.5.1/sdk.js",i.onload=()=>{e()},s.parentNode.insertBefore(i,s))}(window,document,"script",0,"AotterTrek")}));Promise.all([m,k]).then((([e])=>{AotterTrek("init",AotterTrekConfig.clientId),AotterTrek("suprAd",AotterTrekConfig,e),AotterTrek("send")}))}();
</script>
```

2\.  Serve into a SafeFrame

{% hint style="danger" %}
Please note that "**Serve into a SafeFrame**" is not supported. **Please** **Do not select the checkbox**.
{% endhint %}

3\. Click `Save and preview` button, your creative is ready to go.

