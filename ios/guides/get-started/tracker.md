# Tracker

Trek is shipped with a powerful big data tool that is free to all publishers. Sending the first party data of your users not only enables personalized ad experience even in the absence of AdID/IDFA, but also unlocks more revenue shares from out DMP partners.

## Sending user's info <a href="#before_you_begin" id="before_you_begin"></a>

By sending user's info to AotterTrek, our system will analyze data and optimize the ad content delivering to your application. To channel them into ads they are interested in.

### 1. Set User When Login

{% tabs %}
{% tab title="Objective-C" %}
```objectivec
[[AotterTrek sharedAPI] setCurrentUserWithEmail:<user_email>
    phone:<user_phone>
    fbId:<user_fbId>
    gender:<user_gender>
    birthday:<user_birthday>
    addtionalMeta:<meta>
]
```
{% endtab %}

{% tab title="Swift" %}
```swift
AotterTrek.sharedAPI().setCurrentUserWithEmail("user_email",
    phone: "user_phone",
    fbId: "user_fbId",
    gender: "user_gender", 
    birthday: "user_birthday", 
    addtionalMeta: ["meta":"meta"]
)
```
{% endtab %}
{% endtabs %}

### 2. Update User

{% tabs %}
{% tab title="Objective-C" %}
```objectivec
[[AotterTrek sharedAPI] updateCurrentUserWithValue:@true
                                     forKey:TKUserKeyGender];
```
{% endtab %}

{% tab title="Swift" %}
```swift
AotterTrek.sharedAPI().updateCurrentUser(withValue: true, for: TKUserKeyGender)
```
{% endtab %}
{% endtabs %}

**- Enum : ATUserKey**

| Enum Name           | Value Type |                         |
| ------------------- | ---------- | ----------------------- |
| `TKUserKeyEmail`    | NSString   | Ex: "a111111@gmail.com" |
| `TKUserKeyPhone`    | NSString   | Ex: "09XXXXXXXXX"       |
| `TKUserKeyFbId`     | NSString   |                         |
| `TKUserKeyGender`   | BOOL       | true for male           |
| `TKUserKeyBirthday` | String     | YYYY/MM/DD              |

### Step 3: Remove User When Logout

{% tabs %}
{% tab title="Objective-C" %}
```objectivec
[[AotterTrek sharedAPI] removeCurrentUser];
```
{% endtab %}

{% tab title="Swift" %}
```swift
AotterTrek.sharedAPI().removeCurrentUser()
```
{% endtab %}
{% endtabs %}



[Besides sending user's info](tracker.md#before\_you\_begin) to AotterTrek for a better ad experience to your users, we provide an advanced service _Tracker._ Base on `User`, `Entity` and `Action` data, our system will use these data for **user profiling**. AotterTrek groups these users with similar behavior and send them personalized ads that improve advertising relevance for users and increases revenue for you.

## Guide

A tracker event usually contains the following attributes.

| Attributes                    | Description                                             | Required |
| ----------------------------- | ------------------------------------------------------- | -------- |
| `trackerEngageItemWithItemId` | The unique id of this tracker event                     | Yes      |
| `actionType`                  | The action-type of event (See tabs)                     | Yes      |
| `entityObject`                | The object that represents the tracker event (See tabs) | Yes      |
| `userObject`                  | The person/user who involve in this event               | no       |
| `locationObject`              | The position that this event occurs                     | no       |

{% tabs %}
{% tab title="Action Types" %}
| _**Action Types**_      | Description                                     |
| ----------------------- | ----------------------------------------------- |
| `kTKTTypeREAD_POST`     | when user reads a post or article               |
| `kTKTTypeVISIT_PLACE`   | when user visits somewhere                      |
| `kTKTTypePLAY_GAME`     | when user plays an interactive game or activity |
| `kTKTTypeLISTEN_MUSIC`  | when user plays a song through the music player |
| `kTKTTypeWATCH_VIDEO`   | when user watches a video                       |
| `kTKTTypeCALL_MERCHANT` | When user calls a merchant                      |
| `kTKTTypeBUY_ITEM`      | when user buy an item                           |
{% endtab %}

{% tab title="Entity Types" %}
| Entity types            |
| ----------------------- |
| `kTKEntityTypePOST`     |
| `kTKEntityTypePLACE`    |
| `kTKEntityTypeGAME`     |
| `kTKEntityTypeMUSIC`    |
| `kTKEntityTypeVIDEO`    |
| `kTKEntityTypeMERCHANT` |
| `kTKEntityTypeITEM`     |
{% endtab %}
{% endtabs %}

**Follow the following steps to send a tracker event.**

Step 1: [Create Objects of Tracker Event](../../sdk-integration/tracker.md#step-1-create-objects-of-tracker-event)\
Step 2: [Engage Tracker Event with Objects](../../sdk-integration/tracker.md#step-2-engage-trakcer-event-with-these-parts)\
Step 3: [Update Tracker Items' Specific Part (Optional)](../../sdk-integration/tracker.md#step3-optional-update-the-tracker-items39-specific-part-if-needed)\
Step 4: [Exit Tracker item (Optional)](../../sdk-integration/tracker.md#step-4-optional-exit-tracker-item-if-the-tracker-event-has-clear-end-time)\
Step 5: [Send Tracker Items](../../sdk-integration/tracker.md#step-5-send-tracker-items)\
[Full Example](../../sdk-integration/tracker.md#example)

### Step 1. Create Objects of Tracker Event

Create`entityObject` / `userObject` (optional)/ `locationObject` (optional)

{% tabs %}
{% tab title="Objective-C" %}
{% code overflow="wrap" %}
```objectivec
//create entity object with type 'POST'
NSDictionary *entityPostObject = [TKTracker helper_entityObjectWithTypePOST:@"myPostId" title:@"post title" url:@"http://agirls.aotter.net" tags:nil categories:@[@"news"] reference:nil publishedDate:nil imageUrl:nil author:@"F.D.KKK" meta:@{@"something": @"ffff"}];
   
//or create entityObject with type 'PLACE'
NSDictionary *entityObject = [TKTracker helper_entityObjectWithTypePLACE:[NSString stringWithFormat:@"myPlaceEntityId"] title:@"Taipei" url:@"" tags:@[@"city",@"play",@"Taiwan"] categories:@[@"travel"] address:@"New Taipei City" lat:102.333 lng:63.333 meta:@{@"A": @"how do you turn this on?",@"address": @"new address shoud not be seen"}];

//create user object (optional)
NSDictionary *userObject = [TKTracker helper_userObjectWithEmail:@"<current_user_email>" phone:@"<current_user_phone>" fbId:@"<current_user_fbId>" gender:@"<F or M for current User>" birthday:[NSDate date] additionalMeta:nil];

//create location object (optional)
double user_location_lat = 191.232323;
double user_location_lng = 244.232323;
NSDictionary *locationObject = [TKTracker helper_locationObjectWithLocationId:@"<your_location_id>" title:nil url:@"" categories:@[@"user_location"] address:nil lat:user_location_lat lng:user_location_lng additionalMeta:nil];
```
{% endcode %}
{% endtab %}

{% tab title="Swift" %}
```swift
//create entity object with type 'POST'
let entityPostObject = TKTracker.helper_entityObject(withTypePOST: "myPostId", title: "post title", url: "http://agirls.aotter.net", tags: nil, categories: ["news"], reference: nil, publishedDate: nil, imageUrl: nil, author: "F.D.KKK", meta: ["something" : "ffff"])
        
//or create entityObject with type 'PLACE'
let entityObject = TKTracker.helper_entityObject(withTypePLACE: "myPlaceEntityId", title: "Taipei", url: "", tags: ["city", "play", "Taiwan"], categories: ["travel"], address: "New Taipei City", lat: 102.333, lng: 63.333, meta: ["A" : "how do you turn this on?", "address" : "new address shoud not be seen"])

//create user object (optional)
let userObject = TKTracker.helper_userObject(withEmail: "<current_user_email>", phone: "<current_user_phone>", fbId: "<current_user_fbId>", gender: "<F or M for current User>", birthday: "<current_user_birthday>", addtionalMeta: nil)

//create location object (optional)
let user_location_lat: Double = 191.232323;
let user_location_lng: Double = 244.232323;
let locationObject = TKTracker.helper_locationObject(withLocationId: "<your_location_id>", title: nil, url: "", categories: ["user_location"], address: nil, lat: user_location_lat, lng: user_location_lng, additonalMeta: nil)
```
{% endtab %}
{% endtabs %}

### Step 2. Engage Tracker Event with Objects <a href="#step-2-engage-trakcer-event-with-these-parts" id="step-2-engage-trakcer-event-with-these-parts"></a>

{% tabs %}
{% tab title="Objective-C" %}
{% code overflow="wrap" %}
```objectivec
//engage trakcer item with POST type
[[TKTracker sharedAPI] trackerEngageItemWithItemId:@"myPostId" type:kTKTTypeREAD_POST userObject:userObject entityObject:entityObject locationObject:locationObject];
```
{% endcode %}
{% endtab %}

{% tab title="Swift" %}
{% code overflow="wrap" %}
```swift
//engage tracker item with POST type
TKTracker.sharedAPI().trackerEngageItem(withItemId: "myPostId", type: kTKTTypeREAD_POST, userObject: userObject, entityObject: entityObject, locationObject: locationObject)
```
{% endcode %}
{% endtab %}
{% endtabs %}



### Step 3. (Optional)  Update Tracker Items' Specific Part <a href="#step3-optional-update-the-tracker-items39-specific-part-if-needed" id="step3-optional-update-the-tracker-items39-specific-part-if-needed"></a>

Update `entity object` / `user object` / `location object` for specific items if it's necessary for your app's life cycle.

{% tabs %}
{% tab title="Objective-C" %}
{% code overflow="wrap" %}
```objectivec
[[TKTracker sharedAPI] trackerUpdateItem:@"myPostId" withEntityObject:@{@"foo":@"bar"}];
[[TKTracker sharedAPI] trackerUpdateItem:@"myPostId" withUserObject:@{@"foo":@"bar"}];
[[TKTracker sharedAPI] trackerUpdateItem:@"myPostId" withLocationObject:@{@"foo":@"bar"}];
```
{% endcode %}
{% endtab %}

{% tab title="Swift" %}
{% code overflow="wrap" %}
```swift
let newEntityObject = []
TKTracker.sharedAPI().trackerUpdateItem("myPostId", withEntityObject: newEntityObject)

let newUserObject = []
TKTracker.sharedAPI().trackerUpdateItem("myPostId", withUserObject: newUserObject)

let newLocationObject = []
TKTracker.sharedAPI().trackerUpdateItem("myPostId", withLocationObject: newLocationObject)
```
{% endcode %}
{% endtab %}
{% endtabs %}

### Step 4. (Optional) Exit Tracker item <a href="#step-4-optional-exit-tracker-item-if-the-tracker-event-has-clear-end-time" id="step-4-optional-exit-tracker-item-if-the-tracker-event-has-clear-end-time"></a>

Exit tracker item if the tracker event has finished its action. For Example, when users leave the posting page, means that the user finished reading the post.

{% tabs %}
{% tab title="Objective-C" %}
```objectivec
[[TKTracker sharedAPI] trackerExitItem:@"myPostId"];
```
{% endtab %}

{% tab title="Swift" %}
```swift
TKTracker.sharedAPI().trackerExitItem("myPostId")
```
{% endtab %}
{% endtabs %}

### Step 5. Send Tracker Items <a href="#step-5-send-tracker-items" id="step-5-send-tracker-items"></a>

{% tabs %}
{% tab title="Objective-C" %}
```
[[TKTracker sharedAPI] trackerSendItems];
```
{% endtab %}

{% tab title="Swift" %}
```
TKTracker.sharedAPI().trackerSendItems()
```
{% endtab %}
{% endtabs %}

## Full Example <a href="#example" id="example"></a>

{% tabs %}
{% tab title="Objective-C" %}
{% code overflow="wrap" %}
```objectivec
-(void)engageItemAndSend{
    NSDictionary *entityObject = [TKTracker helper_entityObjectWithTypePOST:@"myPostId" title:@"post title" url:@"http://agirls.aotter.net" tags:nil categories:@[@"news"] reference:nil publishedDate:nil imageUrl:nil author:nil];
    
    NSDictionary *userObject = [TKTracker helper_userObjectWithEmail:@"my@email.net" phone:@"0922333444" fbId:@"" gender:@"M" birthday:@"1999/05/02" additionalMeta:nil];
    
    [[TKTracker sharedAPI] trackerEngageItemWithItemId:@"myPostId" type:kTKTTypeREAD_POST userObject:userObject entityObject:entityObject locationObject:nil];
    
    dispatch_after(dispatch_time(DISPATCH_TIME_NOW, (int64_t)(2 * NSEC_PER_SEC)), dispatch_get_main_queue(), ^{
        [[TKTracker sharedAPI] trackerExitItem:@"myPostId"];
        [[TKTracker sharedAPI] trackerSendItems];
    });
```
{% endcode %}
{% endtab %}

{% tab title="Swift" %}
{% code overflow="wrap" %}
```swift
 func engageItemAndSend(){
   let entityObject = TKTracker.helper_entityObject(withTypePOST: "myPostId", title: "post title", url: "https://foo.bar", tags: nil, categories: ["news"], reference: nil, publishedDate: nil, imageUrl: nil, author: nil, meta: nil)
   let userObject = TKTracker.helper_userObject(withEmail: "current_user-email", phone: "current_user_phone", fbId: "current_user_fbId", gender: "F or M for current User", birthday: "", addtionalMeta: nil)
   
   TKTracker.sharedAPI().trackerEngageItem(withItemId: "myPostId", type: kTKTTypeREAD_POST, userObject: userObject, entityObject: entityObject, locationObject: nil)
   
   DispatchQueue.main.asyncAfter(deadline: .now() + 2) {
       TKTracker.sharedAPI().trackerExitItem("myPostId")
       TKTracker.sharedAPI().trackerSendItems()
   }
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
