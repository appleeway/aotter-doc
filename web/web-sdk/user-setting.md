# User Setting

By sending user's info to AotterTrek, our system will analyze data and optimize the ad content delivering to your application. To channel them into ads they are interested in.

### Sample Code

```markup
<script>
  AotterTrek('setUser', {
    hashedEmail:
      '0b9e5c891bdea5395fc69ca88206b92d723eddb228fe65f63e1945067484bfda',
    hashedPhone:
      '20faf05baccf8a477fa337b77c0acb0e8bff77f34664feec6a057bd3cf23235b',
    birthYear: '1999',
    gender: 'MALE',
  })
  
  AotterTrek('send')
</script>
```

We provide the following attributes. Except for the marked ones, all of the data will be **hashed** before send to AotterTrek server.

| Key            | Guidelines                                                                                                                                                                                   |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `email`        | Trim leading and trailing white space, and convert all characters to lowercase.                                                                                                              |
| `hashedEmail`  | Trim leading and trailing white space and convert all characters to lowercase. You should hash it with sha256, **Trek won't be hashed again.**                                               |
| `phone`        | Remove symbols, letters, and any leading zeroes. You should prefix the country code if the`country`field is not specified.                                                                   |
| `hashedPhone`  | Remove symbols, letters, and any leading zeroes. You should prefix the country code if the `country` field is not specified. You should hash it with sha256, **Trek won't be hashed again.** |
| `gender`       | Use _**m** _ for male, _**f**_ for female.                                                                                                                                                   |
| `birthYear`    | Use the _YYYY_ format: 1900 to the current year.                                                                                                                                             |
| `birthMonth`   | Use the _MM_ format: `01` to `12`.                                                                                                                                                           |
| `birthDate`    | Use the _DD_ format: `01` to `31`.                                                                                                                                                           |
| `country`      |                                                                                                                                                                                              |
| `city`         |                                                                                                                                                                                              |
| `state`        |                                                                                                                                                                                              |
| `zip`          |                                                                                                                                                                                              |
| `fbId`         | **Trek won't be hashed this attribute.**                                                                                                                                                     |

### Test Result

![](<../../.gitbook/assets/截圖 2021-03-26 上午11.19.27.png>)
