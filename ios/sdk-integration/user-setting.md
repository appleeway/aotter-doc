# User Setting

By sending user's info to AotterTrek, our system will analyze data and optimize the ad content delivering to your application. To channel them into ads they are interested in.

Step 1: [Set User When Login](user-setting.md#step-1-set-user-when-login)\
Step 2: [Update User](user-setting.md#step-2-update-user) \
Step 3: [Remove User When Logout](user-setting.md#step-3-remove-user-when-logout)

### Step 1: Set User When Login

{% tabs %}
{% tab title="ObjC" %}
```objectivec
[[AotterTrek sharedAPI] setCurrentUserWithEmail:<user_email>
    phone:<user_phone>
    fbId:<user_fbId>
    gender:<user_gender>
    birthday:<user_birthday>
    addtionalMeta:<meta>
];
```
{% endtab %}

{% tab title="Swift" %}
```
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

### Step 2: Update User&#x20;

{% tabs %}
{% tab title="ObjC" %}
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

**- enum: ATUserKey**

| Enum Name           | Value Type | Descriptions            |
| ------------------- | ---------- | ----------------------- |
| `TKUserKeyEmail`    | NSString   | Ex: "a111111@gmail.com" |
| `TKUserKeyPhone`    | NSString   | Ex: "09XXXXXXXXX"       |
| `TKUserKeyFbId`     | NSString   |                         |
| `TKUserKeyGender`   | BOOL       | true for male           |
| `TKUserKeyBirthday` | String     | YYYY/MM/DD              |

### Step 3: Remove User When Logout

{% tabs %}
{% tab title="ObjC" %}
```objectivec
 [[AotterTrek sharedAPI] removeCurrentUser];
```
{% endtab %}

{% tab title="Swift" %}
```swift
[[AotterTrek sharedAPI] removeCurrentUser];
```
{% endtab %}
{% endtabs %}
