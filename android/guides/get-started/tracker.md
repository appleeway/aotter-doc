# Tracker

Trek is shipped with a powerful big data tool that is free to all publishers. Sending the first party data of your users not only enables personalized ad experience even in the absence of AdID/IDFA, but also unlocks more revenue shares from out DMP partners.

Implementing tracker in your app following steps:

* ****[**Build a Tracker**](tracker.md#build-a-tracker)****
* ****[**Build data for user profiling**](tracker.md#build-data-for-user-profiling)****
* ****[**Send user profiling for Tracker**](tracker.md#send-user-profiling-for-tracker)****

### **Build a Tracker**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val tracker= Tracker(context)
```
{% endtab %}

{% tab title="Java" %}
```java
Tracker tracker = new Tracker(context);
```
{% endtab %}
{% endtabs %}

### **Build data for user profiling**

* #### [Entity](tracker.md#entity-1)
* ****[**User**](tracker.md#user)****
* ****[**Loaction**](tracker.md#loaction)****
* ****[**ActionType**](tracker.md#actiontype)****

#### Entity&#x20;

Entity constructor parameter:

| Name       | Type           | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| ---------- | -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| id         | String         | Page's id.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| title      | String         | Page's title.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| type       | String         | <p>Page's type.</p><p>Tracker provides the following <strong>EntityType</strong> options.<br>1. <strong>EntityType.POST.type</strong></p><p>2. <strong>EntityType.PLACE.type</strong></p><p>3. <strong>EntityType.GAME.type</strong></p><p>4. <strong>EntityType.MUSIC.type</strong></p><p>5. <strong>EntityType.VIDEO.type</strong></p><p>6. <strong>EntityType.MERCHANT.type</strong></p><p>7. <strong>EntityType.ITEM.type</strong></p><p>8. <strong>EntityType.UNKNOWN.type</strong></p> |
| url        | String         | Page's url.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| categories | List\<String>  | Page's categories.                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| tags       | List\<String>  | Page's tags.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| meta       | TrekJsonObject | <p>Custom meta data.<br>Tracker provides the following options.<br>1.<strong>TrekDataKey.REFERENCE</strong></p><p>2.<strong>TrekDataKey.PUBLISHED_DATE</strong></p><p>3.<strong>TrekDataKey.IMG</strong></p><p>4.<strong>TrekDataKey.AUTHOR</strong></p><p>5.<strong>TrekDataKey.ADDRESS</strong></p><p>6.<strong>TrekDataKey.LAT</strong></p><p>7.<strong>TrekDataKey.LNG</strong></p>                                                                                                      |

Here is an example code:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val pageId = "0000-00000-00000"
val pageTitle = "I am a title"
val pageType = EntityType.POST.type
val pageUrl = "https://xxxx.xxxx.xxx/"
val pageCategories = listOf("News","3C")
val pageTags = listOf("News","3C")

val entityMetaData = TrekJsonObject()
entityMetaData.put(TrekDataKey.REFERENCE, "Aotter")
entityMetaData.put(TrekDataKey.PUBLISHED_DATE, 1438090882490L)
entityMetaData.put(TrekDataKey.IMG, "http://pnn.aotter.net/xxx/xxx/xxx.jpg")
entityMetaData.put(TrekDataKey.AUTHOR, "skybear")
entityMetaData.put(TrekDataKey.ADDRESS, "105台北市松山區南京東路四段")
entityMetaData.put(TrekDataKey.LAT, 25.0463684)
entityMetaData.put(TrekDataKey.LNG, 121.5501565)

val entity = Entity(pageId,pageTitle,pageType,pageUrl,pageCategories,pageTags,entityMetaData)
```
{% endtab %}

{% tab title="Java" %}
```java
String pageId = "0000-00000-00000";
String pageTitle = "I am a title";
String pageType = EntityType.POST.type;
String pageUrl = "https://xxxx.xxxx.xxx/";
List<String> pageCategories = CollectionsKt.listOf("News","3C");
List<String> pageTags = CollectionsKt.listOf("News","3C");

TrekJsonObject entityMetaData = new TrekJsonObject();
entityMetaData.put(TrekDataKey.REFERENCE, "Aotter");
entityMetaData.put(TrekDataKey.PUBLISHED_DATE, 1438090882490L);
entityMetaData.put(TrekDataKey.IMG, "http://pnn.aotter.net/xxx/xxx/xxx.jpg");
entityMetaData.put(TrekDataKey.AUTHOR, "skybear");
entityMetaData.put(TrekDataKey.ADDRESS, "105台北市松山區南京東路四段");
entityMetaData.put(TrekDataKey.LAT, 25.0463684);
entityMetaData.put(TrekDataKey.LNG, 121.5501565);

Entity entity = new Entity(pageId,pageTitle,pageType,pageUrl,pageCategories,pageTags,entityMetaData);
```
{% endtab %}
{% endtabs %}

#### **User**

User constructor parameter:

| Name     | Type           | Description       |
| -------- | -------------- | ----------------- |
| birthday | String         | User's birthday.  |
| fbId     | String         | User's fbId.      |
| gender   | String         | User's gender.    |
| email    | String         | User's email.     |
| phone    | String         | User's phone.     |
| meta     | TrekJsonObject | Custom meta data. |

Here is an example code:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val birthday = "1991/10/10"
val fbId = "0000-00000-00000"
val gender = "M" //"M" for male, "F" for female.
val email = "axxxxxxxx@gmail.com"
val phone = "0900000000"
val meta = TrekJsonObject()

val user = User(birthday,email,fbId,gender,phone,meta)

UserInfoUtils.setUserInfo(user)
```
{% endtab %}

{% tab title="Java" %}
```java
String birthday = "1991/10/10";
String fbId = "0000-00000-00000";
String gender = "M"; //"M" for male, "F" for female.
String email = "axxxxxxxx@gmail.com";
String phone = "0900000000";
TrekJsonObject meta = TrekJsonObject();

User user = new User(birthday,email,fbId,gender,phone,meta);

UserInfoUtils.INSTANCE.setUserInfo(user);
```
{% endtab %}
{% endtabs %}

#### **Loaction**

{% hint style="info" %}
This step can be skipped.
{% endhint %}

Loaction **** constructor parameter:

| Name       | Type           | Description            |
| ---------- | -------------- | ---------------------- |
| id         | String         | Loaction's id.         |
| title      | String         | Loaction's title.      |
| address    | String         | Loaction's address.    |
| url        | String         | Loaction's url.        |
| categories | List\<String>  | Loaction's categories. |
| lat        | Double         | Loaction's latitude.   |
| lng        | Double         | Loaction's longitude.  |
| meta       | TrekJsonObject | Custom meta data.      |

Here is an example code:

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
val id = "0000-00000-00000"
val title = "I am a title"
val address = "105台北市松山區南京東路四段"
val url = "https://xxxx.xxxx.xxx/"
val categories = listOf("News","3C")
val lat = 25.0463684
val lng = 25.0463684
val meta = TrekJsonObject()

val loaction = Loaction(address,categories,id,lat,lng,meta,title,url)

```
{% endtab %}

{% tab title="Java" %}
```java
String id = "0000-00000-00000";
String title = "I am a title";
String address = "105台北市松山區南京東路四段";
String url = "https://xxxx.xxxx.xxx/";
List<String> categories = CollectionsKt.listOf("News","3C");
Double lat = 25.0463684;
Double lng = 25.0463684;
TrekJsonObject meta = TrekJsonObject();

Loaction loaction = new Loaction(address,categories,id,lat,lng,meta,title,url);

```
{% endtab %}
{% endtabs %}

#### ActionType

| Name       | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ActionType | <p>Tracker provides the following options.</p><p>1. <strong>ActionType.READ_POST.action</strong></p><p>2. <strong>ActionType.CREATE_POST.action</strong></p><p>3. <strong>ActionType.INITIAL_USAGE.action</strong></p><p>4. <strong>ActionType.VISIT_PLACE.action</strong></p><p>5. <strong>ActionType.PLAY_GAME.action</strong></p><p>6. <strong>ActionType.LISTEN_MUSIC.action</strong></p><p>7. <strong>ActionType.WATCH_VIDEO.action</strong></p><p>8. <strong>ActionType.CALL_MERCHANT.action</strong></p><p>9. <strong>ActionType.BUY_ITEM.action</strong></p><p>10. <strong>ActionType.UNKNOWN.action</strong></p> |

### **Send user profiling for Tracker**

{% tabs %}
{% tab title="Kotlin" %}
```kotlin
tracker
.timeSpan(1) //Seconds to stay on the current page
.setUser(user)
.setEntity(entity)
.setLocation(null or loaction)
.setActionType(ActionType.READ_POST.action)
.sendTrackerReport()
```
{% endtab %}

{% tab title="Java" %}
```java
tracker
.timeSpan(1)//Seconds to stay on the current page
.setUser(user)
.setEntity(entity)
.setLocation(null or loaction)
.setActionType(ActionType.READ_POST.action)
.sendTrackerReport();
```
{% endtab %}
{% endtabs %}
