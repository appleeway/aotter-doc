# User Setting

By sending user's info to AotterTrek, our system will analyze data and optimize the ad content delivering to your application. To channel them into ads they are interested in.

Step 1: [Set User When Login](user-setting.md#step-1-set-user-when-login)\
Step 2: [Update User](user-setting.md#step-2-update-user) \
Step 3: [Remove User When Logout](user-setting.md#step-3-remove-user-when-logout)

### Step 1: Set User When Login

```objectivec
[[AotterTrek sharedAPI] setCurrentUserWithEmail:<user_email>
    phone:<user_phone>
    fbId:<user_fbId>
    gender:<user_gender>
    birthday:<user_birthday>
    addtionalMeta:<meta>
];
```

### Step 2: Update User&#x20;

```objectivec
[[AotterTrek sharedAPI] updateCurrentUserWithValue:@true
                                     forKey:TKUserKeyGender];
```

**- enum: ATUserKey**

| Enum Name           | Value Type | Descriptions            |
| ------------------- | ---------- | ----------------------- |
| `TKUserKeyEmail`    | NSString   | Ex: "a111111@gmail.com" |
| `TKUserKeyPhone`    | NSString   | Ex: "09XXXXXXXXX"       |
| `TKUserKeyFbId`     | NSString   |                         |
| `TKUserKeyGender`   | BOOL       | true for male           |
| `TKUserKeyBirthday` | String     | YYYY/MM/DD              |

### Step 3: Remove User When Logout

```
  [[AotterTrek sharedAPI] removeCurrentUser];
```
