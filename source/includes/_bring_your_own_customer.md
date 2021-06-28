# Bring Your Own Customers

This guide will walk you from zero to hero into a full-featured whitboard trading solution with securities such as APPL, TSLA, S&P 500 and more.


If you run into problems, don't hesitate to contact support@dstoq.com. We're here to help!

## API Setup

```
> ssh-keygen -t rsa -b 2048 -m PEM -f jwtRS256.key
> openssl rsa -in jwtRS256.key -pubout -outform PEM -out jwtRS256.key.pub

token = jwt.encode({
    'iss': ISSUER,
    'sub': ISSUER,
    'aud': 'DSTOQ',
    'iat': now(),
    'exp': now() + timedelta(days=30),
  }, SECRET_KEY_GOES_HERE, algorithm='RS256'
).decode()
```

In order to start integrating with DSTOQ you have to be a registered authentication provider. We need to have a small mutual contract in place and have to add you to our partner program. 


The next thing is to provide us with an RSA-256 Public Key, that you will use to sign JSON-Web-Tokens to authenticate with our API:



Send `jwtRS256.key.pub` to us and use `jwtRS256.key` to authenticate against our API. We will then give you your ISSUER name.


Consequently, add an `Authorization` header to each request you make to our API: `JWT YOUR_TOKEN_HERE`.

That's all to get started.


## Registering new users
```
endpoint = 'https://api.dstoq.com/core/accounts/providers/accounts/'
requests.post(endpoint, json={
    'email': 'awesome@dstoq.rocks',
    'public_key': SOME_PUBLIC_KEY
}, headers={'Authorization': f'JWT YOUR_TOKEN_HERE'))
```

The first step in registering a user is telling us her e-mail and the stellar public key.


## Exchanging KYC information
```
endpoint = 'https://api.dstoq.com/core/accounts/providers/kyc-documents/`


# assume you have front_image, back_image and pdf_file as file-like object available
front_b64 = b64encode(front_image.read()).decode()
back_b64 = b64encode(back_image.read()).decode()
pdf_b64 = b64encode(pdf_file.read()).decode()

requests.post(endpoint, json={
    # the email is required to match the kyc to the user
    'email': 'awesome@dstoq.rocks,
    'first_name': 'John',
    'last_name': 'Doe',
    'kyc_provider': 'ONFIDO',
    'country_code': 'ng',
    'passport_front': f'data:image/jpeg;base64,{front_b64}',
    'passport_back': f'data:image/jpeg;base64,{back_b64}',
    'kyc_provider_report': f'data:application/pdf;base64,{pdf_b64}'
}, headers={'Authorization': f'JWT YOUR_TOKEN_HERE'))
```

The user is now in a pending state in our system and we are awaiting KYC information.

We require the `email`, `first_name`, `last_name`, and `country_code` of the user, the name of the `kyc_provider` you are using (supported ones are `PASSBASE` and `ONFIDO`, but we are willing to add more if you have the requirement for that) and a front and back image of the id document. Finally we need the report of KYC Provider as PDF. All binary documents need to be B64 encoded.



Awesome. We are now reviewing the KYC document as fast as possible - and that's very fast.

## Webhook Integration
You can provide us with a Webhook URL where we can send you updates about the account, giving you the option to enhance the experience for the user.

We'll POST updates to this URL like this: `YOUR_WEBHOOK_URL/{email_of_the_user}/{event_name}/`, sometimes with additional (optional) information about the event as the POST body. If you want to secure this endpoint, you may as well give us an API-Key that we send alongside with the Authorization Header.

The following events are currently available:

- `kyc_rejected`
- `kyc_verified` - yikes, the user can now trade!
- `deposited`
- `first_trade` - of DSQ issued assets
- `traded` - DSQ issued assets

## Trading

```
import requests
from stellar_sdk import Server, TransactionBuilder, Network, TransactionEnvelope


APPROVAL_SERVER = 'https://dsq.technology/sep-8/tx-approve/'

server = Server(horizon_url='https://horizon.stellar.org')
builder = TransactionBuilder(server.load_account(PUBLIC_KEY_OF_THE_USER), Network.PUBLIC_NETWORK_PASSPHRASE)

tx_xdr = builder.append_manage_buy_offer_op(
    selling_code='USD',
    selling_issuer='GDUKMGUGDZQK6YHYA5Z6AY2G4XDSZPSZ3SW5UN3ARVMO6QSRDWP5YLEX',
    buying_code='TSLA',
    buying_issuer='GBRDHSZL4ZKOI2PTUMM53N3NICZXC5OX3KPCD4WD4NG4XGCBC2ZA3KAG',
    amount='1.00',
    price='402.9721521'
).build().to_xdr()

xdr = requests.post(APPROVAL_SERVER, data={'tx': tx_xdr}).json()['tx']

envelope = TransactionEnvelope.from_xdr(xdr, Network.PUBLIC_NETWORK_PASSPHRASE)
envelope.sign(PRIVATE_KEY)
server.submit_transaction(envelope)
```

Trading can done via the [SEP-0008](https://github.com/stellar/stellar-protocol/blob/master/ecosystem/sep-0008.md)-Protocol. It essentially means that you create a transaction, send it to the DSQ SEP-8 Endpoint, get it back and broadcast it to the stellar network.



A list of all available assets can be [found in our API](https://api.dstoq.com/core/assets/assets/) or in our [Stellar TOML](https://dsq.technology/.well-known/stellar.toml) definitions.

Trading pairs need to have at least one base currency, defined as having the `is_trading_pair` flag set to true (and `can_be_traded` set to true).

Currently trading of all assets happens against USD-Dollars issued by Anchor USD.

Note, however, that you can as well use all the other endpoints (including the ones for trading) mentioned in this documentation.