# APIs

The tab below explains different kinds of AotterTrek Web APIs. Please take a look if needed.

{% tabs %}
{% tab title="INIT" %}
## AotterTrek('init', 'CLIENT\_ID')

> Initialize AotterTrek SDK

#### Arguments

| order | name       | type     | note                           |
| ----- | ---------- | -------- | ------------------------------ |
| 1     | init       | `string` | Accept "**init**" **** only    |
| 2     | CLIENT\_ID | `string` | Your client id from AotterTrek |

#### Example

```javascript
AotterTrek('init', 'CLIENT_ID');
```
{% endtab %}

{% tab title="ADTYPE" %}
## AotterTrek(ADTYPE, OPTIONS)

> Send HTTP request to get ad and injecting response data to specific element.

#### Arguments

| order | name    | type     | note                 |
| ----- | ------- | -------- | -------------------- |
| 1     | ADTYPE  | `string` | Only accept "suprAd" |
| 2     | OPTIONS | `object` | See Options below.   |

#### Options

| name        | type                  | note                                                                            |
| ----------- | --------------------- | ------------------------------------------------------------------------------- |
| selector    | `string` or `element` | The CSS selector or target element.                                             |
| place       | `string`              | Custom placement name, you can check out analytics data in Trek Dashboard.      |
| trekNetwork | `string`              | Set ad network "trek" or "house", **default by "trek"**.                        |
| mobile      | `boolean`             | If set to true, the ad will only be displayed on the mobile device.             |
| fixed       | `'top'` or `'bottom'` | If set to top or bottom, the ad will be fixed at the top or bottom of the page. |
| onAdLoad    | `function`            | Trigger when ad successfully loaded.                                            |
| onAdFail    | `function`            | Trigger when ad fails to load.                                                  |

#### Example

```javascript
AotterTrek('suprAd', {
    selector: '#supr-ad',
    place: 'placement_UUID',
    onAdLoad: function(node) {
        // Do something.
    },
    onAdFail: function(node) {
        // Do something.
    }
})
```
{% endtab %}

{% tab title="SETUSER" %}
## AotterTrek('setUser', USER)

> Ref:[ ](user-setting.md)[User info Setting](user-setting.md)

#### Arguments

| order | name    | type     | note                           |
| ----- | ------- | -------- | ------------------------------ |
| 1     | setUser | `string` | Accept "**setUser**" **** only |
| 2     | USER    | `object` | See User below                 |

#### User

| name     | type     | note                                             |
| -------- | -------- | ------------------------------------------------ |
| email    | `string` | User's email                                     |
| birthday | `string` | User's birthday, only accept `yyyy/MM/dd format` |
| fbid     | `string` | User's facebook id                               |
| gender   | `string` | User's gender                                    |

#### Example

```javascript
AotterTrek('setUser', {
  email: 'example@aotter.net',  
  birthday: '1999/01/01',
  fbId: '[USER_FACEBOOK_ID]',
  gender: 'MALE'
});

AotterTrek('init', 'CLIENT_ID');

AotterTrek('suprAd', {
  selector: '#supr-ad'
});
```
{% endtab %}

{% tab title="TKADN" %}
## AotterTrek('tkadn', EVENT)

> Ref: [Tkadn](tkadn.md)

#### Arguments

| order | name  | type     | note                          |
| ----- | ----- | -------- | ----------------------------- |
| 1     | tkadn | `string` | Accept "**tkadn**" **** only. |
| 2     | EVENT | `string` | See Standard Events below.    |

#### Standard Events

| Event        | Description                                                               |
| ------------ | ------------------------------------------------------------------------- |
| `PageView`   | A person lands on your website pages.                                     |
| `PageViewed` | A person staying on your page for more than 10s or scrolling exceeds 50%. |
| `ClickBtn`   | A person clicks on a button.                                              |
| `FormSubmit` | A person submits a form.                                                  |
| `AddToCart`  | A person clicks on an add to cart button.                                 |
| `Purchased`  | A person has finished the purchase                                        |

#### Example

```javascript
function reportEvent(){
    AotterTrek('tkadn', 'FormSubmit');
}
```
{% endtab %}

{% tab title="SEND" %}
## AotterTrek('send')

> Send an event for trek to analytic page information.

#### Example

```javascript
AotterTrek('send');
```
{% endtab %}
{% endtabs %}



