# Event

If you are a publisher and also own a website, you might want to track the conversion rate. After integrating AotterTrek SDK on every page of your website, it can record a series of user's behavior when they click an ad. Therefore, you can calculate the conversion rate and optimize the advertising strategy.

{% hint style="danger" %}
Notice that this feature will not work properly when the page is **redirect-needed**.
{% endhint %}

Implementing tracker in your website following steps:

* ****[**Send event**](event.md#send-event)****

### **Send event**

Call `AotterTrek('tkadn', 'EVENT_NAME')` and pass event name via the second parameter.

Here is a when the form submits an example code:

```html
  <form action="/form" onsubmit="reportEvent()">
    <input type="text" name="name" placeholder="你的名字">
    <button type="submit">送出</button>
  </form>
  <script>
  function reportEvent(){
    AotterTrek('tkadn', 'FormSubmit');
  }
  </script>
```

Here is another page view example code:

```html
  <script>
    AotterTrek('tkadn', 'PageView');
  </script>
```

#### **Event**

`AotterTrek('tkadn', 'EVENT_NAME')`second parameter `EVENT_NAME` can provides the following commonly used events. Using these events will simplify the analysis process and directly provide AotterTrek optimization algorithms to achieve automatic optimization.

{% hint style="info" %}
But if you really want to use your own EVENT\_NAME, we can also let you fill in any string you want.
{% endhint %}

| Name       | Description                                                               |
| ---------- | ------------------------------------------------------------------------- |
| PageView   | A person lands on your website pages.                                     |
| PageViewed | A person staying on your page for more than 10s or scrolling exceeds 50%. |
| ClickBtn   | A person clicks on a button.                                              |
| FormSubmit | A person submits a form.                                                  |
| AddToCart  | A person clicks on an add to cart button.                                 |
| Purchased  | A person has finished the purchase                                        |

