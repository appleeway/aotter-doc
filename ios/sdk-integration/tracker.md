# Tracker

Besides [sending user's info](user-setting.md) to AotterTrek for a better ad experience to your users, we provide an advanced service _Tracker._ Base on `User`, `Entity` and `Action` data, our system will use these data for **user profiling**. AotterTrek groups these users with similar behavior and send them personalized ads that improve advertising relevance for users and increases revenue for you.

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

Step 1: [Create Objects of Tracker Event](tracker.md#step-1-create-objects-of-tracker-event)\
Step 2: [Engage Tracker Event with Objects](tracker.md#step-2-engage-trakcer-event-with-these-parts)\
Step 3: [Update Tracker Items' Specific Part (Optional)](tracker.md#step3-optional-update-the-tracker-items39-specific-part-if-needed)\
Step 4: [Exit Tracker item (Optional)](tracker.md#step-4-optional-exit-tracker-item-if-the-tracker-event-has-clear-end-time)\
Step 5: [Send Tracker Items](tracker.md#step-5-send-tracker-items)\
[Full Example](tracker.md#example)

### Step 1. Create Objects of Tracker Event

Create`entityObject` / `userObject` (optional)/ `locationObject` (optional)

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

### Step 2. Engage Tracker Event with Objects <a href="#step-2-engage-trakcer-event-with-these-parts" id="step-2-engage-trakcer-event-with-these-parts"></a>

```objectivec
//engage trakcer item with POST type
[[TKTracker sharedAPI] trackerEngageItemWithItemId:@"myPostId" type:kTKTTypeREAD_POST userObject:userObject entityObject:entityObject locationObject:locationObject];
```

### Step 3. (Optional)  Update Tracker Items' Specific Part <a href="#step3-optional-update-the-tracker-items39-specific-part-if-needed" id="step3-optional-update-the-tracker-items39-specific-part-if-needed"></a>

Update `entity object` / `user object` / `location object` for specific items if it's necessary for your app's life cycle.

```objectivec
[[TKTracker sharedAPI] trackerUpdateItem:@"myPostId" withEntityObject:@{@"foo":@"bar"}];
[[TKTracker sharedAPI] trackerUpdateItem:@"myPostId" withUserObject:@{@"foo":@"bar"}];
[[TKTracker sharedAPI] trackerUpdateItem:@"myPostId" withLocationObject:@{@"foo":@"bar"}];
```

### Step 4. (Optional) Exit Tracker item <a href="#step-4-optional-exit-tracker-item-if-the-tracker-event-has-clear-end-time" id="step-4-optional-exit-tracker-item-if-the-tracker-event-has-clear-end-time"></a>

Exit tracker item if the tracker event has finished its action. For Example, when users leave the posting page, means that the user finished reading the post.

```objectivec
[[TKTracker sharedAPI] trackerExitItem:@"myPostId"];
```

### Step 5. Send Tracker Items <a href="#step-5-send-tracker-items" id="step-5-send-tracker-items"></a>

```objectivec
[[TKTracker sharedAPI] trackerSendItems];        
```

## Full Example <a href="#example" id="example"></a>

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

