# Authentication

```shell
curl -X POST -H "Content-Type: application/json" -d '{"username": "emailaddressofuser@dstoq.com", "password": "AVerySecretPassword"}' https://api.dstoq.com/accounts/auth/jwt/create/

# output
{
   "refresh": "... some refresh token ...",
   "access": ... some access token ..."
}
```

```javascript
const axios = require('axios')

axios
  .post('https://api.dstoq.com/accounts/auth/jwt/create/', {
    username: 'emailaddressofuser@dstoq.com',
    password: 'AVerySecretPassword'
  })
  .then(response => console.log(response.data))
  .catch(console.log)

// output
{
   "refresh": "... some refresh token ...",
   "access": "... some access token ..."
 }
```

```python
import requests

data = requests.post('https://api.dstoq.com/accounts/auth/jwt/create/', json={
  'username': 'emailaddressofuser@dstoq.com'
  'password': 'AVerySecretPassword'
}).json()
print(data)

# output
{
   "refresh": "... some refresh token ...",
   "access": "... some access token ..."
 }
```

This section explains how you can interact with the DSTOQ API as an existing customer. We'll explain how you can bring your own customer base to the platform and use a whitelabeld-DSTOQ version!

You can obtain a JWT token to use subsequent services that require authentication.

**HTTP Request**

`POST https://api.dstoq.com/accounts/auth/jwt/create/`


**JSON Body**

Parameter | Description
--------- | -----------
email | The email of the user.
password | The password of the user.


The endpoint returns, among other information, a token that can be used to authenticate against the API. Subsequent calls must then send an `Authorization` header using the given token:

`Authorization: JWT TOKEN_GOES_HERE`

```shell
curl -H "Authorization: JWT eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQ4ODU4NTI4LCJqdGkiOiI3ZjcxZTIwYzE1YjE0MDJlODkyZGRkMTdlMWViODYwZCIsInVzZXJfaWQiOjEsInNjb3BlcyI6WyJmb28iLCJiYXIiLCJiYXoiXSwiaXNfc3RhZmYiOnRydWUsImlzX3N1cGVydXNlciI6dHJ1ZSwiYWRkaXRpb25hbCI6ImRhdGEifQ.fkcrKCBlmX4oDsCHy2CUgp-CEv_z2uFOvkrgZilQowurS0fQDrQDtmJu59JJJ4eCbSgLjo3HJovG6-UJ8B3gGwIOpP3mmkijvx-IDeJ44MOIzkGVO2MvhQhHSUCc2U0AQzgQRUhlI6zD7OUn5Vm8LN9AY0E3gg-OS3XmxmFN-MWC_QC93viT5f" https://api.dstoq.com/accounts/auth/users/me/

# output
{
    "country_code": "br",
    "email": "emailaddressofuser@dstoq.com",
    "kyc_status": "pending"
}


curl -H "Authorization: JWT eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQ4ODU4NTI4LCJqdGkiOiI3ZjcxZTIwYzE1YjE0MDJlODkyZGRkMTdlMWViODYwZCIsInVzZXJfaWQiOjEsInNjb3BlcyI6WyJmb28iLCJiYXIiLCJiYXoiXSwiaXNfc3RhZmYiOnRydWUsImlzX3N1cGVydXNlciI6dHJ1ZSwiYWRkaXRpb25hbCI6ImRhdGEifQ.fkcrKCBlmX4oDsCHy2CUgp-CEv_z2uFOvkrgZilQowurS0fQDrQDtmJu59JJJ4eCbSgLjo3HJovG6-UJ8B3gGwIOpP3mmkijvx-IDeJ44MOIzkGVO2MvhQhHSUCc2U0AQzgQRUhlI6zD7OUn5Vm8LN9AY0E3gg-OS3XmxmFN-MWC_QC93viT5f" https://api.dstoq.com/core/accounts/accounts/me/

# output
{
    "account_provider": 1,
    "country_code": "br",
    "email": "emailaddressofuser@dstoq.com",
    "first_name": "Christian",
    "has_deposited": true,
    "id": 19232,
    "last_name": "Peters",
    "public_key": "GCXETER4MRRY7WNOLIXETD6OZ46P6KGUMOORXF2JCJUXIKBW2BS6GZGA",
    "referral_short_link": "https://app.dstoq.com/9vUm",
    "signer_key": "GCXETER4MRRY7WNOLIXETD6OZ46P6KGUMOORXF2JCJUXIKBW2BS6GZGA",
    "status": "kyc_passed"
}

```

```javascript
const axios = require('axios')

axios
  .create({
    headers: {'Authorization': 'JWT eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQ4ODU4NTI4LCJqdGkiOiI3ZjcxZTIwYzE1YjE0MDJlODkyZGRkMTdlMWViODYwZCIsInVzZXJfaWQiOjEsInNjb3BlcyI6WyJmb28iLCJiYXIiLCJiYXoiXSwiaXNfc3RhZmYiOnRydWUsImlzX3N1cGVydXNlciI6dHJ1ZSwiYWRkaXRpb25hbCI6ImRhdGEifQ.fkcrKCBlmX4oDsCHy2CUgp-CEv_z2uFOvkrgZilQowurS0fQDrQDtmJu59JJJ4eCbSgLjo3HJovG6-UJ8B3gGwIOpP3mmkijvx-IDeJ44MOIzkGVO2MvhQhHSUCc2U0AQzgQRUhlI6zD7OUn5Vm8LN9AY0E3gg-OS3XmxmFN-MWC_QC93viT5f'}
  })
  .get('https://api.dstoq.com/accounts/accounts/user/')
  .then(response => console.log(response.data))
  .catch(console.log)

// output
{
    "country_code": "br",
    "email": "emailaddressofuser@dstoq.com",
    "kyc_status": "pending"
}

axios
  .create({
    headers: {'Authorization': 'JWT eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQ4ODU4NTI4LCJqdGkiOiI3ZjcxZTIwYzE1YjE0MDJlODkyZGRkMTdlMWViODYwZCIsInVzZXJfaWQiOjEsInNjb3BlcyI6WyJmb28iLCJiYXIiLCJiYXoiXSwiaXNfc3RhZmYiOnRydWUsImlzX3N1cGVydXNlciI6dHJ1ZSwiYWRkaXRpb25hbCI6ImRhdGEifQ.fkcrKCBlmX4oDsCHy2CUgp-CEv_z2uFOvkrgZilQowurS0fQDrQDtmJu59JJJ4eCbSgLjo3HJovG6-UJ8B3gGwIOpP3mmkijvx-IDeJ44MOIzkGVO2MvhQhHSUCc2U0AQzgQRUhlI6zD7OUn5Vm8LN9AY0E3gg-OS3XmxmFN-MWC_QC93viT5f'}
  })
  .get('https://api.dstoq.com/core/accounts/accounts/me/')
  .then(response => console.log(response.data))
  .catch(console.log)

// output
{
    "account_provider": 1,
    "country_code": "br",
    "email": "emailaddressofuser@dstoq.com",
    "first_name": "Christian",
    "has_deposited": true,
    "id": 19232,
    "last_name": "Peters",
    "public_key": "GCXETER4MRRY7WNOLIXETD6OZ46P6KGUMOORXF2JCJUXIKBW2BS6GZGA",
    "referral_short_link": "https://app.dstoq.com/9vUm",
    "signer_key": "GCXETER4MRRY7WNOLIXETD6OZ46P6KGUMOORXF2JCJUXIKBW2BS6GZGA",
    "status": "kyc_passed"
}
```

```python
import requests

data = requests.get('https://api.dstoq.com/accounts/accounts/user/', headers={
  'Authorization': 'JWT eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQ4ODU4NTI4LCJqdGkiOiI3ZjcxZTIwYzE1YjE0MDJlODkyZGRkMTdlMWViODYwZCIsInVzZXJfaWQiOjEsInNjb3BlcyI6WyJmb28iLCJiYXIiLCJiYXoiXSwiaXNfc3RhZmYiOnRydWUsImlzX3N1cGVydXNlciI6dHJ1ZSwiYWRkaXRpb25hbCI6ImRhdGEifQ.fkcrKCBlmX4oDsCHy2CUgp-CEv_z2uFOvkrgZilQowurS0fQDrQDtmJu59JJJ4eCbSgLjo3HJovG6-UJ8B3gGwIOpP3mmkijvx-IDeJ44MOIzkGVO2MvhQhHSUCc2U0AQzgQRUhlI6zD7OUn5Vm8LN9AY0E3gg-OS3XmxmFN-MWC_QC93viT5f'
}).json()
print(data)

# output
{
    "country_code": "br",
    "email": "emailaddressofuser@dstoq.com",
    "kyc_status": "pending"
}

data = requests.get('https://api.dstoq.com/core/accounts/accounts/me/', headers={
  'Authorization': 'JWT eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQ4ODU4NTI4LCJqdGkiOiI3ZjcxZTIwYzE1YjE0MDJlODkyZGRkMTdlMWViODYwZCIsInVzZXJfaWQiOjEsInNjb3BlcyI6WyJmb28iLCJiYXIiLCJiYXoiXSwiaXNfc3RhZmYiOnRydWUsImlzX3N1cGVydXNlciI6dHJ1ZSwiYWRkaXRpb25hbCI6ImRhdGEifQ.fkcrKCBlmX4oDsCHy2CUgp-CEv_z2uFOvkrgZilQowurS0fQDrQDtmJu59JJJ4eCbSgLjo3HJovG6-UJ8B3gGwIOpP3mmkijvx-IDeJ44MOIzkGVO2MvhQhHSUCc2U0AQzgQRUhlI6zD7OUn5Vm8LN9AY0E3gg-OS3XmxmFN-MWC_QC93viT5f'
}).json()
print(data)

# output
{
    "account_provider": 1,
    "country_code": "br",
    "email": "emailaddressofuser@dstoq.com",
    "first_name": "Christian",
    "has_deposited": true,
    "id": 19232,
    "last_name": "Peters",
    "public_key": "GCXETER4MRRY7WNOLIXETD6OZ46P6KGUMOORXF2JCJUXIKBW2BS6GZGA",
    "referral_short_link": "https://app.dstoq.com/9vUm",
    "signer_key": "GCXETER4MRRY7WNOLIXETD6OZ46P6KGUMOORXF2JCJUXIKBW2BS6GZGA",
    "status": "kyc_passed"
}
```

Try it with the `user` endpoint that gives you a few basic information about the user behind the given token:

**HTTP Request**

***Auth Information***

`GET  https://api.dstoq.com/accounts/accounts/user/`


***Trading Information***

`GET https://api.dstoq.com/core/accounts/accounts/me/`
<aside class="notice">
We want to keep the samples clean, so we just use a variable `token` for subsequent samples instead of including a token that you need to adjust anyway.
</aside>