# Full Sample Code

```javascript
<head>
    <script async src="https://securepubads.g.doubleclick.net/tag/js/gpt.js"></script>
    <script async src="./prebid.js"></script>
    <script>
        var sizes = [
            [300, 250]
        ]
        var PREBID_TIMEOUT = 1500
        var FAILSAFE_TIMEOUT = 3000;
        var adUnits = [{
            code: '/93702494/aotter_prebid_ad_300x250', // from GAM 
            mediaTypes: {
                banner: {
                    sizes: sizes,
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
        
        var googletag = googletag || {};
        googletag.cmd = googletag.cmd || [];
        googletag.cmd.push(function() {
            googletag.pubads().disableInitialLoad();
        });
        var pbjs = pbjs || {};
        pbjs.que = pbjs.que || [];
        pbjs.que.push(function() {
            pbjs.addAdUnits(adUnits);
            pbjs.setConfig({
              aseal: {
                // your Aottertrek client Id
                clientId: "yEFcFoJaruNorh5RqtuR"
              }
            }); 
            pbjs.requestBids({
                bidsBackHandler: initAdserver,
                timeout: PREBID_TIMEOUT
            });
        });
        function initAdserver() {
            if (pbjs.initAdserverSet) return;
            pbjs.initAdserverSet = true;
            googletag.cmd.push(function() {
                pbjs.setTargetingForGPTAsync && pbjs.setTargetingForGPTAsync();
                googletag.pubads().refresh();
            });
        }
        
        // In case PBJS doesn't load
        setTimeout(function() {
            initAdserver();
        }, FAILSAFE_TIMEOUT);
        // From GAM - GPT code
        googletag.cmd.push(function() {
            googletag.defineSlot('/93702494/aotter_prebid_ad_300x250', [300, 250], 'div-gpt-ad-1642581403289-0').addService(googletag.pubads());
            googletag.pubads().enableSingleRequest();
            googletag.enableServices();
        });
    </script>
</head>
<body>
    <h2>Basic Prebid.js Example</h2>
    <h5>Div-1</h5>
    <div id='div-gpt-ad-1642581403289-0' style='min-width: 300px; min-height: 250px;'>
        <script>
          googletag.cmd.push(function() { googletag.display('div-gpt-ad-1642581403289-0'); });
        </script>
      </div>
</body>
```
