# Tkadn

If you are a publisher and also own a website, you might want to track the conversion rate. After integrating AotterTrek SDK on every page of your website, it can record a series of user's behavior when they click an ad. Therefore, you can calculate the conversion rate and optimize the advertising strategy.

{% hint style="warning" %}
Notice that this feature will not work properly when the page is **redirect-needed**.
{% endhint %}

### How it works 🤔 ?

1\. When users click on an ad, it will open a new page (which lead to your website) and then the URL will be attached a tracking parameter `_tkadbc`.

> Ex:https://example.com/page/camp2017/\_tkadbc=fd91c867eff1b33bf5936d910589...

2\. If your website has integrated AotterTrek SDK already, the parameter `_tkadbc` will be stored in cookies for one day.

3\. It will record user's behavior on pages in the same domain.&#x20;

> Ex. http://example.com/page/camp2017/anotherPage

4\.  You can set events, for example, submit a form or buy things. Whenever users trigger, records will be sent to the AotterTrek server. See [standard events](tkadn.md#standard-events).

```javascript
AotterTrek('tkadn', 'FormSubmit');
```

**Custom events** are also available. You can replace `EVENT_NAME` to your custom event name.

```javascript
AotterTrek('tkadn', 'EVENT_NAME');
```

### Usage&#x20;

Step 1: Integrate AotterTrek SDK on every User-flow page.\
Step 2: Set some targets for users. &#x20;

```javascript
AotterTrek('tkadn', 'PageView')
```

> &#x20;If event includes multiple steps, AotterTrek will use conversion funnel to analyze every step.

### Standard Events

AotterTrek provides the following commonly used events. Using these events will simplify the analysis process and directly provide AotterTrek optimization algorithms to achieve automatic optimization.

| Event        | Description                                                               |
| ------------ | ------------------------------------------------------------------------- |
| `PageView`   | A person lands on your website pages.                                     |
| `PageViewed` | A person staying on your page for more than 10s or scrolling exceeds 50%. |
| `ClickBtn`   | A person clicks on a button.                                              |
| `FormSubmit` | A person submits a form.                                                  |
| `AddToCart`  | A person clicks on an add to cart button.                                 |
| `Purchased`  | A person has finished the purchase                                        |

### Sample Code&#x20;

```markup
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  ...
  ...
</head>
<body>

  <form action="/form" onsubmit="reportEvent()">
    <input type="text" name="name" placeholder="你的名字">
    <button type="submit">送出</button>
  </form>
  <!-- Please check sdk has been installed -->
  <script>
  function reportEvent(){
    AotterTrek('tkadn', 'FormSubmit');
  }
  </script>
</body>
</html>
```
