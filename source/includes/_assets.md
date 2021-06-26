# Assets
A trading flow is pretty straightforward to implement, as you don't have to wrestle with a lot of details.

Specifically if you want ...

* to display information about the assets that people can use
* to display the current orders that users have placed which have not yet been matched
* to go the extra mile sometimes and present historical data
* to have some eye candy with charts about the price history
* to create & delete orders

Fortunately that can be done with only a few calls. Let's dive in.

## Available Assets

```shell
curl https://api.dstoq.com/core/assets/assets/?trading_pair=USDC&time_span=LAST_HOUR

# output:
{
  "count": 11,
  "next": null,
  "previous": null,
  "results": [
   {
    "id": 1,
    "is_trading_pair": false,
    "code": "TSLA",
    "unicode": "",
    "issuer_name": "DSQ AG",
    "issuer": "GBRDHSZL4ZKOI2PTUMM53N3NICZXC5OX3KPCD4WD4NG4XGCBC2ZA3KAG",
    "custodian_name": "Mason PrivatBank",
    "asset_type": "credit_alphanum4",
    "display_decimals": 7,
    "name": "Tesla",
    "company_name": "Tesla, Inc.",
    "desc": "Tesla, Inc., designs, develops, manufactures and sells fully electric vehicles, and energy storage systems, as well as installs, operates and maintains solar and energy storage products. The Company operates through two segments: Automotive, and Energy generation and storage.",
    "image": "https://dstoq-prod-core-storage.s3.amazonaws.com/equities.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASP7JDUVZ75NLNLGF%2F20210626%2Feu-west-1%2Fs3%2Faws4_request&X-Amz-Date=20210626T090745Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEGUaCWV1LXdlc3QtMSJIMEYCIQC2wllKb4%2BGCmiQmc6aneGCFg%2Bf%2BgPkT4ASNZq4N3FVvgIhAIykJM5CEnvNfyjP8iBWvIr%2BqX8sgtvWY9uuHAGIo2kgKosECD4QARoMMTcxNzUwNjk2MzA3Igz4i3pIVLp8Z%2FCFLyQq6AMbvpJGF9FhqaRgI%2FlZ6m1vvu0o02lh4MlgDiA9nBcYyYqRaev6UtL2udMaV3KTac83B13cRBMt%2BvLoZfed80gTSm38FbKTKRV9e%2FbfSWVCUcOlAlC0zetD0pYe9pHBraDpyKwjte7GQkZrSsGWCqnzFjP21WAX3djoXTy2fuNR%2FA%2BrWRFstjA0uqQrA5Av4OzUqB3Z4RatzDxy90iNpTgDRTYYAmnx8U%2BDZm7a9DErM2KUhu9J8Q3qCnHukQI70HWLfXR0tsc%2FUDGemDPvw8M6rBYsgFfBoPH015qD27i2R%2B0eNy4KFZIKaPnYF7k%2FzgE%2BsW0Mkr3y0RYoqepTdizHn7PjhFppEZjcwXVUwEsQvo6Ss9OMAgEKUDVbIk6k%2Fgmv2qNIAqsnAL8%2FRwVoBLIEB%2BsrbU61as9B%2BSWhBaGdXJgfETAz7FOxFZ9HidRk0y%2Ba6j3NYNPo0jzfKdJk2%2BKUOdfe%2FSzNSoSEH2BIyJWpVmsakeYo6OcBe3cdh8RUk2wp4eqFreadJTFG%2Bcn5a4nXdsrg7VVmTGjB9Jw2ZAzTH5Tl6NPOb7de%2BNfmbRK1yuSng6apjqYq6oR2jHFc9xzoBJfCEQSd2Ee9leqflrM3aNa7YkF6pHzX6oPqPhIhDYJED%2Fu53XC1EDCY5NqGBjqkAX5XCGspnZrXA5mrBdlmr7i%2Fs6Fhlz3rMm7Qlune%2B0YxiMDXbZ%2FQvDy3qgJ9TWa6%2F6P9qeXuaNI7iR%2B%2Bo%2BUQ4w9pzQwT6cVZn1AWurL7%2FMvTEeGn3lKKbDESaD4r%2FE0Ui78qZKaJVM6YNEmrBY3goazzmhnFOl%2FSnz9uLytevbnZ9GBB%2BmEFC07cBr2wfSukRvufLX5MDLQrkOCf3x5ttscqHVPx&X-Amz-Signature=b21ff619e53036c35d6de80c43dae8b34c9598d52368da9501f3fca1e35aadf5",
    "isin": "US88160R1014",
    "wkn": "88160R101",
    "product_class": "STOCK",
    "issuance_currency": "USD",
    "aggregation_time_span": "LAST_MONTH",
    "aggregations": [
      {
        "asset_volume": "0.0000142",
        "trading_pair_volume": "0.0099481",
        "avg": "700.5704225",
        "high": "700.5701160",
        "low": "700.5701160",
        "open": "700.5701160",
        "close": "700.5701160",
        "trade_count": 1,
        "timestamp": "2021-06-25T10:00:00"
      },
      ...  
    ],
    "can_be_traded": true
    },
    ...
  ]
}
```

```javascript
const axios = require('axios')

axios.get('https://api.dstoq.com/core/assets/assets/?trading_pair=USDC&time_span=LAST_HOUR')
  .then(response => console.log(response.data))
  .catch(console.log)

// output:
{
  "count": 11,
  "next": null,
  "previous": null,
  "results": [
   {
    "id": 1,
    "is_trading_pair": false,
    "code": "TSLA",
    "unicode": "",
    "issuer_name": "DSQ AG",
    "issuer": "GBRDHSZL4ZKOI2PTUMM53N3NICZXC5OX3KPCD4WD4NG4XGCBC2ZA3KAG",
    "custodian_name": "Mason PrivatBank",
    "asset_type": "credit_alphanum4",
    "display_decimals": 7,
    "name": "Tesla",
    "company_name": "Tesla, Inc.",
    "desc": "Tesla, Inc., designs, develops, manufactures and sells fully electric vehicles, and energy storage systems, as well as installs, operates and maintains solar and energy storage products. The Company operates through two segments: Automotive, and Energy generation and storage.",
    "image": "https://dstoq-prod-core-storage.s3.amazonaws.com/equities.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASP7JDUVZ75NLNLGF%2F20210626%2Feu-west-1%2Fs3%2Faws4_request&X-Amz-Date=20210626T090745Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEGUaCWV1LXdlc3QtMSJIMEYCIQC2wllKb4%2BGCmiQmc6aneGCFg%2Bf%2BgPkT4ASNZq4N3FVvgIhAIykJM5CEnvNfyjP8iBWvIr%2BqX8sgtvWY9uuHAGIo2kgKosECD4QARoMMTcxNzUwNjk2MzA3Igz4i3pIVLp8Z%2FCFLyQq6AMbvpJGF9FhqaRgI%2FlZ6m1vvu0o02lh4MlgDiA9nBcYyYqRaev6UtL2udMaV3KTac83B13cRBMt%2BvLoZfed80gTSm38FbKTKRV9e%2FbfSWVCUcOlAlC0zetD0pYe9pHBraDpyKwjte7GQkZrSsGWCqnzFjP21WAX3djoXTy2fuNR%2FA%2BrWRFstjA0uqQrA5Av4OzUqB3Z4RatzDxy90iNpTgDRTYYAmnx8U%2BDZm7a9DErM2KUhu9J8Q3qCnHukQI70HWLfXR0tsc%2FUDGemDPvw8M6rBYsgFfBoPH015qD27i2R%2B0eNy4KFZIKaPnYF7k%2FzgE%2BsW0Mkr3y0RYoqepTdizHn7PjhFppEZjcwXVUwEsQvo6Ss9OMAgEKUDVbIk6k%2Fgmv2qNIAqsnAL8%2FRwVoBLIEB%2BsrbU61as9B%2BSWhBaGdXJgfETAz7FOxFZ9HidRk0y%2Ba6j3NYNPo0jzfKdJk2%2BKUOdfe%2FSzNSoSEH2BIyJWpVmsakeYo6OcBe3cdh8RUk2wp4eqFreadJTFG%2Bcn5a4nXdsrg7VVmTGjB9Jw2ZAzTH5Tl6NPOb7de%2BNfmbRK1yuSng6apjqYq6oR2jHFc9xzoBJfCEQSd2Ee9leqflrM3aNa7YkF6pHzX6oPqPhIhDYJED%2Fu53XC1EDCY5NqGBjqkAX5XCGspnZrXA5mrBdlmr7i%2Fs6Fhlz3rMm7Qlune%2B0YxiMDXbZ%2FQvDy3qgJ9TWa6%2F6P9qeXuaNI7iR%2B%2Bo%2BUQ4w9pzQwT6cVZn1AWurL7%2FMvTEeGn3lKKbDESaD4r%2FE0Ui78qZKaJVM6YNEmrBY3goazzmhnFOl%2FSnz9uLytevbnZ9GBB%2BmEFC07cBr2wfSukRvufLX5MDLQrkOCf3x5ttscqHVPx&X-Amz-Signature=b21ff619e53036c35d6de80c43dae8b34c9598d52368da9501f3fca1e35aadf5",
    "isin": "US88160R1014",
    "wkn": "88160R101",
    "product_class": "STOCK",
    "issuance_currency": "USD",
    "aggregation_time_span": "LAST_MONTH",
    "aggregations": [
      {
        "asset_volume": "0.0000142",
        "trading_pair_volume": "0.0099481",
        "avg": "700.5704225",
        "high": "700.5701160",
        "low": "700.5701160",
        "open": "700.5701160",
        "close": "700.5701160",
        "trade_count": 1,
        "timestamp": "2021-06-25T10:00:00"
      },
      ...  
    ],
    "can_be_traded": true
    },
    ...
  ]
}
```

```python
import requests

data = requests.get('https://api.dstoq.com/core/assets/assets/?trading_pair=USDC&time_span=LAST_HOUR').json()
print(data)

# output:
{
  "count": 11,
  "next": null,
  "previous": null,
  "results": [
   {
    "id": 1,
    "is_trading_pair": false,
    "code": "TSLA",
    "unicode": "",
    "issuer_name": "DSQ AG",
    "issuer": "GBRDHSZL4ZKOI2PTUMM53N3NICZXC5OX3KPCD4WD4NG4XGCBC2ZA3KAG",
    "custodian_name": "Mason PrivatBank",
    "asset_type": "credit_alphanum4",
    "display_decimals": 7,
    "name": "Tesla",
    "company_name": "Tesla, Inc.",
    "desc": "Tesla, Inc., designs, develops, manufactures and sells fully electric vehicles, and energy storage systems, as well as installs, operates and maintains solar and energy storage products. The Company operates through two segments: Automotive, and Energy generation and storage.",
    "image": "https://dstoq-prod-core-storage.s3.amazonaws.com/equities.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=ASIASP7JDUVZ75NLNLGF%2F20210626%2Feu-west-1%2Fs3%2Faws4_request&X-Amz-Date=20210626T090745Z&X-Amz-Expires=3600&X-Amz-SignedHeaders=host&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEGUaCWV1LXdlc3QtMSJIMEYCIQC2wllKb4%2BGCmiQmc6aneGCFg%2Bf%2BgPkT4ASNZq4N3FVvgIhAIykJM5CEnvNfyjP8iBWvIr%2BqX8sgtvWY9uuHAGIo2kgKosECD4QARoMMTcxNzUwNjk2MzA3Igz4i3pIVLp8Z%2FCFLyQq6AMbvpJGF9FhqaRgI%2FlZ6m1vvu0o02lh4MlgDiA9nBcYyYqRaev6UtL2udMaV3KTac83B13cRBMt%2BvLoZfed80gTSm38FbKTKRV9e%2FbfSWVCUcOlAlC0zetD0pYe9pHBraDpyKwjte7GQkZrSsGWCqnzFjP21WAX3djoXTy2fuNR%2FA%2BrWRFstjA0uqQrA5Av4OzUqB3Z4RatzDxy90iNpTgDRTYYAmnx8U%2BDZm7a9DErM2KUhu9J8Q3qCnHukQI70HWLfXR0tsc%2FUDGemDPvw8M6rBYsgFfBoPH015qD27i2R%2B0eNy4KFZIKaPnYF7k%2FzgE%2BsW0Mkr3y0RYoqepTdizHn7PjhFppEZjcwXVUwEsQvo6Ss9OMAgEKUDVbIk6k%2Fgmv2qNIAqsnAL8%2FRwVoBLIEB%2BsrbU61as9B%2BSWhBaGdXJgfETAz7FOxFZ9HidRk0y%2Ba6j3NYNPo0jzfKdJk2%2BKUOdfe%2FSzNSoSEH2BIyJWpVmsakeYo6OcBe3cdh8RUk2wp4eqFreadJTFG%2Bcn5a4nXdsrg7VVmTGjB9Jw2ZAzTH5Tl6NPOb7de%2BNfmbRK1yuSng6apjqYq6oR2jHFc9xzoBJfCEQSd2Ee9leqflrM3aNa7YkF6pHzX6oPqPhIhDYJED%2Fu53XC1EDCY5NqGBjqkAX5XCGspnZrXA5mrBdlmr7i%2Fs6Fhlz3rMm7Qlune%2B0YxiMDXbZ%2FQvDy3qgJ9TWa6%2F6P9qeXuaNI7iR%2B%2Bo%2BUQ4w9pzQwT6cVZn1AWurL7%2FMvTEeGn3lKKbDESaD4r%2FE0Ui78qZKaJVM6YNEmrBY3goazzmhnFOl%2FSnz9uLytevbnZ9GBB%2BmEFC07cBr2wfSukRvufLX5MDLQrkOCf3x5ttscqHVPx&X-Amz-Signature=b21ff619e53036c35d6de80c43dae8b34c9598d52368da9501f3fca1e35aadf5",
    "isin": "US88160R1014",
    "wkn": "88160R101",
    "product_class": "STOCK",
    "issuance_currency": "USD",
    "aggregation_time_span": "LAST_MONTH",
    "aggregations": [
      {
        "asset_volume": "0.0000142",
        "trading_pair_volume": "0.0099481",
        "avg": "700.5704225",
        "high": "700.5701160",
        "low": "700.5701160",
        "open": "700.5701160",
        "close": "700.5701160",
        "trade_count": 1,
        "timestamp": "2021-06-25T10:00:00"
      },
      ...  
    ],
    "can_be_traded": true
    },
    ...
  ]
}
```

This endpoints returns a list of all available assets on the DSTOQ platform.

It's paginated and gives you back previous and next urls (or `null` if they don't exist) along with the count.

**HTTP Request**

`GET https://api.dstoq.com/core/assets/assets/`

**URL Params**

Parameter | Description | Default
--------- | ----------- | --------
trading_pair | The code of an asset that has `is_trading_pair` set to true. If not set, fields that require a complete trading pair won't populate (e.g. aggregations) | `-`
time_span | The time span as string that should be reflecte in aggregations, options are `LAST_MONTH, LAST_WEEK, LAST_DAY, LAST_HOUR, LAST_YEAR`. | `-`
trading_pairs_only | A value of `1` will return only trading pairs | `0`
securities_only | A value of `1` will return only securities | `0`

<aside class="notice">
Each asset has a details endpoint like `https://api.dstoq.com/core/assets/assets/TSLA/` that as well accepts `trading_pair` and `time_span` URL params with the same output.
</aside>



## Orderbook

```shell
curl https://api.dstoq.com/core/assets/assets/TSLA/orderbook/?trading_pair=USDC

# output
{
   "bids":[
      {
         "price":"682.8967320",
         "amount":"0.0916524"
      },
      ...
   ],
   "asks":[
      {
         "price":"683.4432680",
         "amount":"0.0685818"
      },
      ...
   ]
}
```

```javascript
const axios = require('axios')

axios.get('https://api.dstoq.com/core/assets/assets/TSLA/orderbook/?trading_pair=USDC')
  .then(response => console.log(response.data))
  .catch(console.log)

// output
{
  "bids": [
    {
    "price": "0.0030390",
    "amount": "2905.9551378"
    },
    ...
  ],
  "asks": [
    {
    "price": "0.0031372",
    "amount": "2.3022122"
    },
    ...
  ]
}
```

```python
import requests

data = requests.get('https://api.dstoq.com/core/assets/assets/TSLA/orderbook/?trading_pair=USDC')

# output
{
   "bids":[
      {
         "price":"682.8967320",
         "amount":"0.0916524"
      },
      ...
   ],
   "asks":[
      {
         "price":"683.4432680",
         "amount":"0.0685818"
      },
      ...
   ]
}
```

An orderbook is just a list of currents bids and asks for a `trading pair` against a `security`. Hence, one of your sides (`buying` or `selling`) needs to be a trading pair. Our samples are for USDC (a trading pair) against TSLA (a security).

**HTTP Request**

`GET https://api.dstoq.com/core/assets/assets/<asset_code>/orderbook/?trading_pair=USDC`

**URL Params**

All required URL params can be retrieved from the `/core/assets` call described above.

Parameter | Description | Required
--------- | ----------- | --------
trading_pair | Code of the base currency that completes the trading pair | Yes

