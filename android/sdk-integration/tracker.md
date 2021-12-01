# Tracker

Besides [sending user's info](user-setting.md) to AotterTrek for a better ad experience to your users, we provide an advanced service _Tracker._ Base on `User`, `Entity` and `Action` data, our system will use these data for **user profiling**. AotterTrek groups these users with similar behavior and send them personalized ads that improve advertising relevance for users and increases revenue for you.

Step 1: [Initialize Tracker Service](tracker.md#step-1-initialize-tracker-service)\
Step 2: [Create `Entity` / `User` Object Instance](tracker.md#step-2-create-entity-user-object-instance)\
Step 3: [Choose Action Types](tracker.md#step-3-choose-action-types)\
Step 4: [Send Tracker](tracker.md#step-4-send-tracker-to-aottertrek-server)

### Step 1: Initialize Tracker Service

Notice that you should initialize `AotterTrek.TrackerService` before using _Tracker_, otherwise, an exception will be thrown.

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
var tracker = AotterTrek.trackerService(context)
```
{% endtab %}

{% tab title="Java" %}
```java
Tracker tracker = AotterTrek.INSTANCE.trackerService(context);
```
{% endtab %}
{% endtabs %}

### Step 2: Create `Entity` / `User` Object Instance

{% tabs %}
{% tab title="Entity" %}
The following table shows **entity** constructor parameters which including basic information about the entity such us `id`, `title` and `type` and so on.

#### Entity constructor parameter

| Name         | Type          | description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| ------------ | ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `id`         | String        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `title`      | String        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `type`       | String        | <p>The Parameter type of the type:</p><p><code>EntityType.POST.type</code>    </p><p><code>EntityType.PLACE.type</code>   </p><p><code>EntityType.GAME.type</code>    </p><p><code>EntityType.MUSIC.type</code>   </p><p><code>EntityType.VIDEO.type</code>   </p><p><code>EntityType.MERCHANT.type</code></p><p><code>EntityType.ITEM.type</code>    </p><p><code>EntityType.UNKNOWN.type</code> </p><p></p>                                                                                                                                                                                                                                                                                                                                                                         |
| `url`        | String        |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `categories` | List\<String> |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `tags`       | List\<String> |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `meta`       | JsonObject    | <p><code>val jsonObject = JsonObject() //Kotlin</code></p><p><code>JsonObject jsonObject  = new JsonObject()  // Java</code>         </p><p></p><p>Options:</p><p><code>jsonObject.addProperty(TrekDataKey.REFERENCE,VALUE) //Ex: "dips" jsonObject.addProperty(TrekDataKey.PUBLISHED_DATE,VALUE)//Ex:1438090882490L jsonObject.addProperty(TrekDataKey.IMG,VALUE)//Ex:"http://pnn.aotter.net/Media/show/cna.jpg"</code></p><p><code>jsonObject.addProperty(TrekDataKey.AUTHOR,VALUE)//Ex: "skybear"</code> </p><p><code>jsonObject.addProperty(TrekDataKey.ADDRESS,VALUE)//Ex: "105台北市松山區南京東路四段2號"</code> </p><p><code>jsonObject.addProperty(TrekDataKey.LAT, VALUE)//Ex: 25.0463684</code> </p><p><code>jsonObject.addProperty(TrekDataKey.LNG, VALUE)//Ex: 121.5501565</code></p> |
{% endtab %}

{% tab title="User" %}
The following table shows the **user**`birthday`, `email` and `gender` and so on.

#### User constructor parameter

| Name       | Type       | description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| ---------- | ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `birthday` | String     | Ex: "1999/10/10"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| `email`    | String     | Ex: "a111111@gmail.com"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| `fbId`     | String     |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        |
| `gender`   | String     | "M" for male, "F" for female                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| `phone`    | String     | Ex: "09XXXXXXXXX"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| `meta`     | JsonObject | <p><code>val jsonObject = JsonObject() //Kotlin</code></p><p><code>JsonObject jsonObject  = new JsonObject()  // Java</code></p><p></p><p><code>//add you want to define key and value</code></p><p><code>jsonObject.add(KEY, VALUE)</code>                       <br><code>jsonObject.add(KEY, VALUE)</code>            <br><code>//or</code>                                  <br><code>jsonObject.addProperty(KEY, VALUE)</code>    <br><code>jsonObject.addProperty(KEY, VALUE)</code><br><code></code><br><code>Ex:</code><br><code>jsonObject.addProperty("publishedDate", 123456L)</code> </p><p><code>jsonObject.addProperty("reference", "aotter")</code></p> |
{% endtab %}
{% endtabs %}

#### - Entity Object

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val entity = Entity(
   "00-00000-00000-0", //id
   "I am a title", //title
   EntityType.GAME.type, //type
   "https://", //url
   listOf("News"), //categories
   listOf("News_domestic"), //tags
   jsonObject //meta
)
```
{% endtab %}

{% tab title="Java" %}
```java
Entity entity = new Entity(
   "00-00000-00000-0", //id
   "I am a title", //title
   EntityType.GAME.INSTANCE.getType(), //type
   "https://", //url
   CollectionsKt.listOf("News", "News_domestic"), //categories
   CollectionsKt.listOf("News", "News_domestic"), //tags
   jsonObject //meta
);
```
{% endtab %}
{% endtabs %}

#### **- User Object**

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

### Step 3: Choose Action Types

| setActionType | Description                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `ActionType`  | <p>The parameter type of the actionType:</p><p></p><p>ActionType.READ_POST.action</p><p>ActionType.CREATE_POST.action</p><p>ActionType.INITIAL_USAGE.action</p><p>ActionType.VISIT_PLACE.action</p><p>ActionType.PLAY_GAME.action</p><p>ActionType.LISTEN_MUSIC.action</p><p>ActionType.WATCH_VIDEO.action</p><p>ActionType.CALL_MERCHANT.action</p><p>ActionType.BUY_ITEM.action</p><p>ActionType.UNKNOWN.action</p><p></p> |

### Step 4: Send Tracker to AotterTrek Server

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
tracker
     .timeSpan(1) //[Integer Type] seconds
     .setUser(user) // If you haven't set user, you can still set User().
     .setEntity(entity)
     .setActionType(ActionType.READ_POST)
     .sendTrackerReport()
```
{% endtab %}

{% tab title="Java" %}
```java
tracker
     .timeSpan(1) //[Integer Type] seconds 
     .setUser(user) // If you have not set user, you can set new User().
     .setEntity(entity)
     .setActionType(ActionType.READ_POST.INSTANCE)
     .sendTrackerReport()
```
{% endtab %}
{% endtabs %}
