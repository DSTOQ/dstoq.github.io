# Wallet

## Balances

```shell
curl -X GET -H "Authorization: JWT $TOKEN" https://api.dstoq.com/core/accounts/accounts/me/balances/\?trading_pair\=USDC

# output
[
  {
        "balance": "0.4409302",
        "buying_liabilities": "0.2577763",
        "code": "FB",
        "estimated_total": "150.520342374",
        "image": "https://dstoq-prod-core-storage.s3.amazonaws.com/equities_Rpa76lQ.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASP7JDUVZ75NLNLGF%2F20210626%2Feu-west-1%2Fs3%2Faws4_request&X-Amz-Date=20210626T092133Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEGUaCWV1LXdlc3QtMSJIMEYCIQC2wllKb4%2BGCmiQmc6aneGCFg%2Bf%2BgPkT4ASNZq4N3FVvgIhAIykJM5CEnvNfyjP8iBWvIr%2BqX8sgtvWY9uuHAGIo2kgKosECD4QARoMMTcxNzUwNjk2MzA3Igz4i3pIVLp8Z%2FCFLyQq6AMbvpJGF9FhqaRgI%2FlZ6m1vvu0o02lh4MlgDiA9nBcYyYqRaev6UtL2udMaV3KTac83B13cRBMt%2BvLoZfed80gTSm38FbKTKRV9e%2FbfSWVCUcOlAlC0zetD0pYe9pHBraDpyKwjte7GQkZrSsGWCqnzFjP21WAX3djoXTy2fuNR%2FA%2BrWRFstjA0uqQrA5Av4OzUqB3Z4RatzDxy90iNpTgDRTYYAmnx8U%2BDZm7a9DErM2KUhu9J8Q3qCnHukQI70HWLfXR0tsc%2FUDGemDPvw8M6rBYsgFfBoPH015qD27i2R%2B0eNy4KFZIKaPnYF7k%2FzgE%2BsW0Mkr3y0RYoqepTdizHn7PjhFppEZjcwXVUwEsQvo6Ss9OMAgEKUDVbIk6k%2Fgmv2qNIAqsnAL8%2FRwVoBLIEB%2BsrbU61as9B%2BSWhBaGdXJgfETAz7FOxFZ9HidRk0y%2Ba6j3NYNPo0jzfKdJk2%2BKUOdfe%2FSzNSoSEH2BIyJWpVmsakeYo6OcBe3cdh8RUk2wp4eqFreadJTFG%2Bcn5a4nXdsrg7VVmTGjB9Jw2ZAzTH5Tl6NPOb7de%2BNfmbRK1yuSng6apjqYq6oR2jHFc9xzoBJfCEQSd2Ee9leqflrM3aNa7YkF6pHzX6oPqPhIhDYJED%2Fu53XC1EDCY5NqGBjqkAX5XCGspnZrXA5mrBdlmr7i%2Fs6Fhlz3rMm7Qlune%2B0YxiMDXbZ%2FQvDy3qgJ9TWa6%2F6P9qeXuaNI7iR%2B%2Bo%2BUQ4w9pzQwT6cVZn1AWurL7%2FMvTEeGn3lKKbDESaD4r%2FE0Ui78qZKaJVM6YNEmrBY3goazzmhnFOl%2FSnz9uLytevbnZ9GBB%2BmEFC07cBr2wfSukRvufLX5MDLQrkOCf3x5ttscqHVPx&X-Amz-Signature=c908c160ac8488ac72a6c0720690ab251c4542c6faa564263e56a73450901ead",
        "is_trading_pair": false,
        "name": "Facebook",
        "selling_liabilities": "0.3968371",
        "type": "asset"
    },
    ...
]
```

```javascript
const axios = require('axios')

axios
  .create({
    headers: {'Authorization': `JWT ${TOKEN}`}
  })
  .get('https://api.dstoq.com/core/accounts/accounts/me/balances/?trading_pair=USDC')
  .then(response => console.log(response.data))
  .catch(console.log)

  // output
  [
  {
        "balance": "0.4409302",
        "buying_liabilities": "0.2577763",
        "code": "FB",
        "estimated_total": "150.520342374",
        "image": "https://dstoq-prod-core-storage.s3.amazonaws.com/equities_Rpa76lQ.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASP7JDUVZ75NLNLGF%2F20210626%2Feu-west-1%2Fs3%2Faws4_request&X-Amz-Date=20210626T092133Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEGUaCWV1LXdlc3QtMSJIMEYCIQC2wllKb4%2BGCmiQmc6aneGCFg%2Bf%2BgPkT4ASNZq4N3FVvgIhAIykJM5CEnvNfyjP8iBWvIr%2BqX8sgtvWY9uuHAGIo2kgKosECD4QARoMMTcxNzUwNjk2MzA3Igz4i3pIVLp8Z%2FCFLyQq6AMbvpJGF9FhqaRgI%2FlZ6m1vvu0o02lh4MlgDiA9nBcYyYqRaev6UtL2udMaV3KTac83B13cRBMt%2BvLoZfed80gTSm38FbKTKRV9e%2FbfSWVCUcOlAlC0zetD0pYe9pHBraDpyKwjte7GQkZrSsGWCqnzFjP21WAX3djoXTy2fuNR%2FA%2BrWRFstjA0uqQrA5Av4OzUqB3Z4RatzDxy90iNpTgDRTYYAmnx8U%2BDZm7a9DErM2KUhu9J8Q3qCnHukQI70HWLfXR0tsc%2FUDGemDPvw8M6rBYsgFfBoPH015qD27i2R%2B0eNy4KFZIKaPnYF7k%2FzgE%2BsW0Mkr3y0RYoqepTdizHn7PjhFppEZjcwXVUwEsQvo6Ss9OMAgEKUDVbIk6k%2Fgmv2qNIAqsnAL8%2FRwVoBLIEB%2BsrbU61as9B%2BSWhBaGdXJgfETAz7FOxFZ9HidRk0y%2Ba6j3NYNPo0jzfKdJk2%2BKUOdfe%2FSzNSoSEH2BIyJWpVmsakeYo6OcBe3cdh8RUk2wp4eqFreadJTFG%2Bcn5a4nXdsrg7VVmTGjB9Jw2ZAzTH5Tl6NPOb7de%2BNfmbRK1yuSng6apjqYq6oR2jHFc9xzoBJfCEQSd2Ee9leqflrM3aNa7YkF6pHzX6oPqPhIhDYJED%2Fu53XC1EDCY5NqGBjqkAX5XCGspnZrXA5mrBdlmr7i%2Fs6Fhlz3rMm7Qlune%2B0YxiMDXbZ%2FQvDy3qgJ9TWa6%2F6P9qeXuaNI7iR%2B%2Bo%2BUQ4w9pzQwT6cVZn1AWurL7%2FMvTEeGn3lKKbDESaD4r%2FE0Ui78qZKaJVM6YNEmrBY3goazzmhnFOl%2FSnz9uLytevbnZ9GBB%2BmEFC07cBr2wfSukRvufLX5MDLQrkOCf3x5ttscqHVPx&X-Amz-Signature=c908c160ac8488ac72a6c0720690ab251c4542c6faa564263e56a73450901ead",
        "is_trading_pair": false,
        "name": "Facebook",
        "selling_liabilities": "0.3968371",
        "type": "asset"
    },
    ...
]
```

```python
import requests

data = requests.get(
  'https://api.dstoq.com/core/accounts/accounts/me/balances/?trading_pair=USDC',
  headers={'Authorization': f'JWT {TOKEN}'}
).json()
print(data)

# output
[
  {
        "balance": "0.4409302",
        "buying_liabilities": "0.2577763",
        "code": "FB",
        "estimated_total": "150.520342374",
        "image": "https://dstoq-prod-core-storage.s3.amazonaws.com/equities_Rpa76lQ.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASP7JDUVZ75NLNLGF%2F20210626%2Feu-west-1%2Fs3%2Faws4_request&X-Amz-Date=20210626T092133Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEGUaCWV1LXdlc3QtMSJIMEYCIQC2wllKb4%2BGCmiQmc6aneGCFg%2Bf%2BgPkT4ASNZq4N3FVvgIhAIykJM5CEnvNfyjP8iBWvIr%2BqX8sgtvWY9uuHAGIo2kgKosECD4QARoMMTcxNzUwNjk2MzA3Igz4i3pIVLp8Z%2FCFLyQq6AMbvpJGF9FhqaRgI%2FlZ6m1vvu0o02lh4MlgDiA9nBcYyYqRaev6UtL2udMaV3KTac83B13cRBMt%2BvLoZfed80gTSm38FbKTKRV9e%2FbfSWVCUcOlAlC0zetD0pYe9pHBraDpyKwjte7GQkZrSsGWCqnzFjP21WAX3djoXTy2fuNR%2FA%2BrWRFstjA0uqQrA5Av4OzUqB3Z4RatzDxy90iNpTgDRTYYAmnx8U%2BDZm7a9DErM2KUhu9J8Q3qCnHukQI70HWLfXR0tsc%2FUDGemDPvw8M6rBYsgFfBoPH015qD27i2R%2B0eNy4KFZIKaPnYF7k%2FzgE%2BsW0Mkr3y0RYoqepTdizHn7PjhFppEZjcwXVUwEsQvo6Ss9OMAgEKUDVbIk6k%2Fgmv2qNIAqsnAL8%2FRwVoBLIEB%2BsrbU61as9B%2BSWhBaGdXJgfETAz7FOxFZ9HidRk0y%2Ba6j3NYNPo0jzfKdJk2%2BKUOdfe%2FSzNSoSEH2BIyJWpVmsakeYo6OcBe3cdh8RUk2wp4eqFreadJTFG%2Bcn5a4nXdsrg7VVmTGjB9Jw2ZAzTH5Tl6NPOb7de%2BNfmbRK1yuSng6apjqYq6oR2jHFc9xzoBJfCEQSd2Ee9leqflrM3aNa7YkF6pHzX6oPqPhIhDYJED%2Fu53XC1EDCY5NqGBjqkAX5XCGspnZrXA5mrBdlmr7i%2Fs6Fhlz3rMm7Qlune%2B0YxiMDXbZ%2FQvDy3qgJ9TWa6%2F6P9qeXuaNI7iR%2B%2Bo%2BUQ4w9pzQwT6cVZn1AWurL7%2FMvTEeGn3lKKbDESaD4r%2FE0Ui78qZKaJVM6YNEmrBY3goazzmhnFOl%2FSnz9uLytevbnZ9GBB%2BmEFC07cBr2wfSukRvufLX5MDLQrkOCf3x5ttscqHVPx&X-Amz-Signature=c908c160ac8488ac72a6c0720690ab251c4542c6faa564263e56a73450901ead",
        "is_trading_pair": false,
        "name": "Facebook",
        "selling_liabilities": "0.3968371",
        "type": "asset"
    },
    ...
]
```


You can find out about the current balances that the user has in his or her wallet by querying this endpoint.

Useful information such as liabillities (part of the balance that is in pending offers) images and so on are included.

**URL Params**

Parameter | Description | Default
--------- | ----------- | --------
trading_pair | If added, the `estimated_total` will give you the balance in the given base currecny. | `-`

**HTTP Request**

`GET https://api.dstoq.com/core/accounts/me/balances/`

## Offers

```shell
curl -X GET -H "Authorization: JWT $TOKEN" https://api.dstoq.com/core/accounts/accounts/me/offers/

# output
{
    "next_cursor": "663182819",
    "offers": [
        {
            "amount": "1.6147102",
            "asset": "D5BK",
            "asset_name": "EU Property  Fund",
            "offer_id": "663182843",
            "offer_type": "buy",
            "price": "36.9304857",
            "timestamp": "2021-06-26T09:26:49Z",
            "trading_pair": "USDC"
        },
        ...
    }
}
```

```javascript
const axios = require('axios')

axios.get('https://api.dstoq.com/core/accounts/accounts/me/offers/')
  .then(response => console.log(response.data))
  .catch(console.log)

// output
{
    "next_cursor": "663182819",
    "offers": [
        {
            "amount": "1.6147102",
            "asset": "D5BK",
            "asset_name": "EU Property  Fund",
            "offer_id": "663182843",
            "offer_type": "buy",
            "price": "36.9304857",
            "timestamp": "2021-06-26T09:26:49Z",
            "trading_pair": "USDC"
        },
        ...
    }
}
```

```python
import requests

data = requests.get('https://api.dstoq.com/core/accounts/accounts/me/offers/').json()
print(data)

# output
{
    "next_cursor": "663182819",
    "offers": [
        {
            "amount": "1.6147102",
            "asset": "D5BK",
            "asset_name": "EU Property  Fund",
            "offer_id": "663182843",
            "offer_type": "buy",
            "price": "36.9304857",
            "timestamp": "2021-06-26T09:26:49Z",
            "trading_pair": "USDC"
        },
        ...
    }
}
```

You can use this endpoint to retrieve the outstanding offers for this account.

**URL Params**

Parameter | Description | Default
--------- | ----------- | --------
cursor | The api gives a next_cursor and/or a prev_cursur to retrieve the next page of results. | `-`

HTTP Request

`GET https://api.dstoq.com/core/accounts/me/offers/`


## Trades

```shell
curl -X GET -H "Authorization: JWT $TOKEN" https://api.dstoq.com/core/accounts/accounts/me/trades/

# output
{
    "next_cursor": "154950797858623518-0",
    "prev_cursor": "154959340548751390-0",
    "trades": [
        {
            "amount": "0.0000467",
            "asset": "GME",
            "asset_name": "GameStop",
            "offer_type": "sell",
            "price": "213.0151720",
            "timestamp": "2021-06-26T08:47:28Z",
            "trading_pair": "USDC"
        },
        ...
    ]
}  
```

```javascript
const axios = require('axios')

axios.get('https://api.dstoq.com/core/accounts/accounts/me/trades/')
  .then(response => console.log(response.data))
  .catch(console.log)

// output
{
    "next_cursor": "154950797858623518-0",
    "prev_cursor": "154959340548751390-0",
    "trades": [
        {
            "amount": "0.0000467",
            "asset": "GME",
            "asset_name": "GameStop",
            "offer_type": "sell",
            "price": "213.0151720",
            "timestamp": "2021-06-26T08:47:28Z",
            "trading_pair": "USDC"
        },
        ...
    ]
}  
```

```python
import requests

data = requests.get('https://api.dstoq.com/core/accounts/accounts/me/trades/').json()
print(data)

# output
{
    "next_cursor": "154950797858623518-0",
    "prev_cursor": "154959340548751390-0",
    "trades": [
        {
            "amount": "0.0000467",
            "asset": "GME",
            "asset_name": "GameStop",
            "offer_type": "sell",
            "price": "213.0151720",
            "timestamp": "2021-06-26T08:47:28Z",
            "trading_pair": "USDC"
        },
        ...
    ]
}
```

You can use this endpoint to retrieve the past trades for this account.

**URL Params**

Parameter | Description | Default
--------- | ----------- | --------
cursor | The api gives a next_cursor to retrieve the next page of results. | `-`

HTTP Request

`GET https://api.dstoq.com/core/accounts/me/trades/`
