# Event Tag

### Create [Event](broken-reference) with Google Tag Manager Creative following steps:

#### **Step 1.**[**Create Basic Tag**](event-tag.md#create-basic-tag)****

#### **Step 2.**[**Create Event Tag**](event-tag.md#create-event-tag)****

### [Create Basic Tag](event-tag.md#step-1.create-basic-tag)

<figure><img src="../../../.gitbook/assets/Event Tag setp 1.webp" alt=""><figcaption></figcaption></figure>

1. Click on `Tags` in the sidebar.
2. Click the `New` button on the right to add a Tag.

<figure><img src="../../../.gitbook/assets/Event Tag setp 2.webp" alt=""><figcaption></figcaption></figure>

3\. Click `Tag Configuration`.

<figure><img src="../../../.gitbook/assets/Event Tag setp 3.webp" alt=""><figcaption></figcaption></figure>

4\. After the Drawer slides out, select `Custom HTML` in the list.

<figure><img src="../../../.gitbook/assets/Event Tag setp 4.png" alt=""><figcaption></figcaption></figure>

5\. After the Drawer is closed, paste the following code into the `HTML` block.

```html
<script>
        (function(w, d, s, src, n) {
                var js, ajs = d.getElementsByTagName(s)[0];
                if (d.getElementById(n)) return;
                js = d.createElement(s); js.id = n;
                w[n] = w[n] || function() { (w[n].q = w[n].q || []).push(arguments) }; w[n].l = 1 * new Date();
                js.async = 1; js.src = src; ajs.parentNode.insertBefore(js, ajs)
        })(window, document, 'script', 'https://static.aottercdn.com/trek/sdk/3.5.4/sdk.js', 'AotterTrek');
        AotterTrek('tkadn', 'PageView');
</script>
```

<figure><img src="../../../.gitbook/assets/Event Tag setp 5.png" alt=""><figcaption></figcaption></figure>

6\. After pasting the code, click on the `Triggering` section below to add a trigger condition.

<figure><img src="../../../.gitbook/assets/Event Tag setp 6.png" alt=""><figcaption></figcaption></figure>

7\. When the Drawer slides out, select `All Pages`in the list.

<figure><img src="../../../.gitbook/assets/Event Tag setp 7.png" alt=""><figcaption></figcaption></figure>

8\. Click the `Save` button in the upper right corner to set the Basic Tag required to complete Trek.

### [Create Event Tag](event-tag.md#step-2.create-event-tag)

<figure><img src="../../../.gitbook/assets/Event Tag setp 8.png" alt=""><figcaption></figcaption></figure>

1. Click on `Triggers` in the sidebar.
2. Click the `New` button on the right to add a Trigger.

<figure><img src="../../../.gitbook/assets/Event Tag setp 9.png" alt=""><figcaption></figcaption></figure>

3\. Click `Trigger Configuration` section.

<figure><img src="../../../.gitbook/assets/Event Tag setp 10.png" alt=""><figcaption></figcaption></figure>

4\. After the Drawer slides out, select `All Elements` in the list.

<figure><img src="../../../.gitbook/assets/Event Tag setp 11.png" alt=""><figcaption></figcaption></figure>

5\. Set your click trigger conditions, the example here is triggered when the Element id attribute is `trek-id`.

6\. Click the `Save` button in the upper right corner.

<figure><img src="../../../.gitbook/assets/Event Tag setp 12.png" alt=""><figcaption></figcaption></figure>

7\. Click on `Triggers` in the sidebar.

8\. Click the `New` button on the right to add a Tag.

<figure><img src="../../../.gitbook/assets/Event Tag setp 13.png" alt=""><figcaption></figcaption></figure>

9\. Click `Tag Configuration`.

<figure><img src="../../../.gitbook/assets/Event Tag setp 14.png" alt=""><figcaption></figcaption></figure>

10\. After the Drawer slides out, select `Custom HTML` in the list.

<figure><img src="../../../.gitbook/assets/Event Tag setp 15.png" alt=""><figcaption></figcaption></figure>

11\. After the Drawer is closed, paste the following code into the `HTML` block.

```html
<script>
  AotterTrek('tkadn', 'EVENT_NAME');
</script>
```

<figure><img src="../../../.gitbook/assets/Event Tag setp 16.png" alt=""><figcaption></figcaption></figure>

12\. Click on the `Advanced Settings` below to expand advanced settings.

13\. Click on the `Tag Sequencing` below.

14\. Check the box `Fire a tag before {name} fires` , And click `Select tag`.

<figure><img src="../../../.gitbook/assets/Event Tag setp 17.png" alt=""><figcaption></figcaption></figure>

15\. After the Drawer slides out, select the [Basic tag](event-tag.md#create-basic-tag) we have just created.

<figure><img src="../../../.gitbook/assets/Event Tag setp 18.png" alt=""><figcaption></figcaption></figure>

16\. After the Drawer is closed, click `Triggering` section.

<figure><img src="../../../.gitbook/assets/Event Tag setp 19.webp" alt=""><figcaption></figcaption></figure>

17\. When the Drawer slides out, select `All Elements`, which trigger we just creted.

<figure><img src="../../../.gitbook/assets/Event Tag setp 20.png" alt=""><figcaption></figcaption></figure>

18\. Click the `Save` button in the upper right corner to create an Event tag.
