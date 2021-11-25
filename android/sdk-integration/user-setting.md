# User Setting

By sending user's info to AotterTrek, our system will analyze data and optimize the ad content delivering to your application. To channel them into ads they are interested in.

Step 1: [Create User Object Instance](user-setting.md#step-1-create-a-user-object-instance)\
Step 2: [Invoke `setUserInfo()` Method](user-setting.md#step-2-invoke-setuserinfo-method)

The following table is the user constructor parameter which including basic information about this user such us `birthday`, `email` and `gender` and so on.

#### User constructor parameter

| Name       | Type       | description                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ---------- | ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `birthday` | String     | Ex: "1999/10/10"                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `email`    | String     | Ex: "a111111@gmail.com"                                                                                                                                                                                                                                                                                                                                                                                                                |
| `fbId`     | String     |                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `gender`   | String     | "M" for male, "F" for female.                                                                                                                                                                                                                                                                                                                                                                                                          |
| `phone`    | String     | Ex: "09XXXXXXXXX"                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `meta`     | JsonObject | <p><code>val jsonObject = JsonObject() //Kotlin</code></p><p><code>JsonObject jsonObject  = new JsonObject()  // Java</code></p><p></p><p><code>//Add key and value that you want to define</code></p><p><code>jsonObject.add(KEY, VALUE)            </code><br><code>jsonObject.add(KEY, VALUE)</code><br><code>//or</code><br><code>jsonObject.addProperty(KEY, VALUE)</code><br><code>jsonObject.addProperty(KEY, VALUE)</code></p> |

### Step 1: Create a User object instance

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val user = User(
    "1999/9/9", //birthday
    "aaaa@gmail.com" //email
    "", //fbId
    "M", //gender
   "0901xxxxxxxxx",//phone
   jsonObject, //meta
)
```
{% endtab %}

{% tab title="Java" %}
```java
User user = new User(
    "1999/9/9", //birthday
    "aaaa@gmail.com" //email
    "", //fbId
    "M", //gender
   "0901xxxxxxxxx",//phone
   jsonObject, //meta
)
```
{% endtab %}
{% endtabs %}

### Step 2: Invoke `setUserInfo()` Method

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
UserInfoUtils.setUserInfo(user)
```
{% endtab %}

{% tab title="Java" %}
```java
UserInfoUtils.INSTANCE.setUserInfo(user);
```
{% endtab %}
{% endtabs %}

