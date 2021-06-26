# Trading

## Submitting an order

```shell
curl -H "Authorization: JWT eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQ4ODU4NTI4LCJqdGkiOiI3ZjcxZTIwYzE1YjE0MDJlODkyZGRkMTdlMWViODYwZCIsInVzZXJfaWQiOjEsInNjb3BlcyI6WyJmb28iLCJiYXIiLCJiYXoiXSwiaXNfc3RhZmYiOnRydWUsImlzX3N1cGVydXNlciI6dHJ1ZSwiYWRkaXRpb25hbCI6ImRhdGEifQ.fkcrKCBlmX4oDsCHy2CUgp-CEv_z2uFOvkrgZilQowurS0fQDrQDtmJu59JJJ4eCbSgLjo3HJovG6-UJ8B3gGwIOpP3mmkijvx-IDeJ44MOIzkGVO2MvhQhHSUCc2U0AQzgQRUhlI6zD7OUn5Vm8LN9AY0E3gg-OS3XmxmFN-MWC_QC93viT5f" -X POST -H "Content-Type: application/json" -d '{"offer_type": "buy", "asset": "TSLA", "trading_pair": "USDC", "price": "412.12", "amount": "0.1"}' https://api.dstoq.com/core/sign/offer/

# Take the result an head to https://accountviewer.stellar.org/ to broadcast it to the stellar network.
```

```javascript
const StellarSdk = require('stellar-sdk')
const server = new StellarSdk.Server('https://horizon-testnet.stellar.org')

const response = await axios
  .create({
    headers: {'Authorization': 'JWT eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiJ9.eyJ0b2tlbl90eXBlIjoiYWNjZXNzIiwiZXhwIjoxNTQ4ODU4NTI4LCJqdGkiOiI3ZjcxZTIwYzE1YjE0MDJlODkyZGRkMTdlMWViODYwZCIsInVzZXJfaWQiOjEsInNjb3BlcyI6WyJmb28iLCJiYXIiLCJiYXoiXSwiaXNfc3RhZmYiOnRydWUsImlzX3N1cGVydXNlciI6dHJ1ZSwiYWRkaXRpb25hbCI6ImRhdGEifQ.fkcrKCBlmX4oDsCHy2CUgp-CEv_z2uFOvkrgZilQowurS0fQDrQDtmJu59JJJ4eCbSgLjo3HJovG6-UJ8B3gGwIOpP3mmkijvx-IDeJ44MOIzkGVO2MvhQhHSUCc2U0AQzgQRUhlI6zD7OUn5Vm8LN9AY0E3gg-OS3XmxmFN-MWC_QC93viT5f'}
  })
  .post('https://api.dstoq.com/core/sign/offer/', {
  	// can be 'buy' or 'sell'
    offer_type: 'buy',
    // Any asset, can as well be one that can be used as trading pair (e.g. USD as asset against EUR is a valid trading pair)
    asset: 'TSLA',
	// complete the trading pair
    trading_pair: 'USDC',
    // The price is ALWAYS determined in terms of the trading pair (base currency / asset) -
    // for 1 TSLA we are bidding 745.1321252 USD
    price: '745.1321252',
    // how much tsla do we want to buy
    amount: 0.1
  })
 
tx = StellarSdk.xdr.TransactionEnvelope.fromXDR(response.data.xdr, 'base64')
tx.sign(StellarSdk.Keypair.fromSecret(SECRET_PHRASE_OF_THE_USER))
await server.submitTransaction(tx)

```

```python
import requests
from stellar_sdk import Keypair, TransactionEnvelope, Network, Server

keypair = Keypair.from_secret(SECRET_PHRASE_OF_THE_USER)
server = Server(horizon_url='https://horizon.stellar.org/')

payload = requests.post('https://api.dstoq.com/core/sign/offer/', json={
    # can be 'buy' or 'sell'
    'offer_type': 'buy',
    # Any asset, can as well be one that can be used as trading pair (e.g. USD as asset against EUR is a valid trading pair)
    'asset': 'TSLA',
    # complete the trading pair
    'trading_pair': 'USDC',
    # The price is ALWAYS determined in terms of the trading pair (base currency / asset) -
    # for 1 TSLA we are bidding 745.1321252 EUR
    'price': '745.1321252',
    # how much tsla do we want to buy
    'amount': 0.1
}, headers=headers).json()

# the payload contains an xdr - the format of the stellar network and is presigned by our service.
tx = TransactionEnvelope.from_xdr(payload['xdr'], network_passphrase=Network.PUBLIC_NETWORK_PASSPHRASE)

# now we must give consent for ourself by signing the transaction
tx.sign(keypair)

server = Server(horizon_url='https://horizon.stellar.org/')
server.submit_transaction(tx)
```

If you want to place a trade as a user you can simply submit to our offer endpoint. It'll give you a transaction back that you can sign using your private key and broadcast to the stellar network.

**HTTP Request**

`POST https://api.dstoq.com/core/sign/offer`


**JSON Body**

Parameter | Description
--------- | -----------
offer_type | either buy or sell - from the perspective of the asset
asset | the asset code that you want to sell
trading_pair | the base currency to complete the trading pair
price | the price in terms of the trading pair (base currency / asset), e.g. for 1 TSLA we are bidding 1000 USD - the price is then 1000
amount | the amount of the asset you want to buy - hence the total money spend of the base currency is price times amount


## SEP-8
DSTOQ is as well fully compliant to the Stellar SEP-8 Standard. The SEP-8 Standard is [well documented](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0008.md) and implemented in wallets such as [LOBSTR(https://lobstr.co/) and [Stellarport](https://stellarport.io/).

The SEP-8 endpoint does support a convenient way to onboard new customers via DSTOQs Customer Identification process.

If your app is as home in the Stellar Universe, head over to the SEP-8 documentation as a good starting point to implement trading. 

<aside class="notice">
The information provided by the DSTOQ API regarding trades, offers and so on are as well available on the stellar blockchain itself. If you wnt to go that route via SEP-8 you may want to retrieve additional information from the stellar horizon blockchain. <a href="https://www.stellar.org/developers">This</a> is a good starting point.
</aside>
