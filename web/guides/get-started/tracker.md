# Tracker

Trek is shipped with a powerful big data tool that is free to all publishers. Sending the first party data of your users not only enables personalized ad experience even in the absence of AdID/IDFA, but also unlocks more revenue shares from out DMP partners.

Implementing tracker in your website following steps:

* ****[**Build user profiling data**](tracker.md#build-user-profiling-data)****
* ****[**Send user profiling**](tracker.md#send-user-profiling)****

### **Build user profiling data**

Call `AotterTrek('setUser', USER_OBJECT)` and pass in user information via the second parameter to set User.

{% hint style="danger" %}
We strongly recommend that you run this after AotterTrek('init'), i.e. before calling the ad or doing anything else.
{% endhint %}

Here is an example code:

```html
<script>
  AotterTrek('setUser', {
    email: 'xxx@aotter.net',
    hashedPhone: '20faf05baccf8a477fa337b77c0acb0e8bff77f34664feec6a057bd3cf23235b',
    birthYear: '1999',
    gender: 'f',
  })
</script>
```

#### **User**

`AotterTrek('setUser', USER_OBJECT)` second parameter `USER_OBJECT` schema:

| Name        | Type   | Description                                                                         |
| ----------- | ------ | ----------------------------------------------------------------------------------- |
| email       | String | User's email.                                                                       |
| hashedEmail | String | User's hashed email. Should hash it with sha256, Trek won't be hashed again.        |
| phone       | String | User's phone number.                                                                |
| hasedPhone  | String | User's hashed phone number. Should hash it with sha256, Trek won't be hashed again. |
| gender      | String | User's gender. Use _**m** _ for male, _**f**_ for female.                           |
| birthYear   | String | Year of birth of the user in the format `YYYY` ex. 1990.                            |
| birthMonth  | String | Month of birth of the user in the `MM` ex. 01.                                      |
| birthDate   | String | Day of birth of the user in the `DD` ex. 10.                                        |
| country     | String | User's country of residence.                                                        |
| city        | String | User's city of residence.                                                           |
| state       | String | User's state of residence.                                                          |
| zip         | String | User's residential postal code.                                                     |
| fbId        | String | User's fbId. We Won't be hashed this attribute.                                     |

### **Send user profiling**

If you have called `AotterTrek('setUser', USER_OBJECT)` and set up user profile, just call `AotterTrek('send')` and you're done!

```html
<script>
  // Set user profile
  AotterTrek('setUser', {
    email: 'xxx@aotter.net',
    hashedPhone: '20faf05baccf8a477fa337b77c0acb0e8bff77f34664feec6a057bd3cf23235b',
    birthYear: '1999',
    gender: 'f',
  })
  
  // Send track
  AotterTrek('send')
</script>
```
