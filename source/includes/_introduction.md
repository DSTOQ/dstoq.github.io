# Introduction

Welcome to the DSTOQ API. Securities trading is only a few lines away. We'll onboard you with everything you'll need to know to build or integrate awesome trading experience of everything out there that can be tokenized.

It doesn't matter if you are a seasoned algorithmic trader or beginner in the field. We have accumulated crystal clear and easily adaptable examples for you.

Fintech or blockchain novice? Don't sweat, we'll explain the important concepts along the way.

Ping us [@dstoq](https://twitter.com/dstoq) whenever you get stuck!

## Prerequisites

```shell
curl https://api.dstoq.com/core/

# output:
# {"success":true,"message":"Hooray, we're here to deliver awesomeness!"}
```

```python
import requests

data = requests.get('https://api.dstoq.com/core/').json()
print(data)

# output:
{'success': True, 'message': "Hooray, we're here to deliver awesomeness!"}
```

```javascript
const axios = require('axios')

axios
  .get('https://api.dstoq.com/core/')
  .then(response => console.log(response.data))
  .catch(console.log)

// output:
{"success":true,"message":"Hooray, we're here to deliver awesomeness!"}
```

We prepared code snippets to onboard you ASAP. So before we start learning the concepts, let's give it a go!

Copy, paste & play a code snippet from the right side to get comfortable! You'll need the [axios library](https://github.com/axios/axios) for JavaScript or [requests](http://docs.python-requests.org/en/master/) for python.

However: It's a REST API, it should be straightforward to adapt this to your needs & tooling. There are Stellar Wrappers for almost [any language](https://www.stellar.org/developers/reference/) around.

All snippets use the stellar testnet and our staging infrastructure.

## Basic Concepts

Securities trading is complicated, luckily we abstract away the heavy lifting to a few API endpoints.

DSTOQ is a trading facility platform where partner banks of ours can issue tokens representing securities. Those securities are held in custody by the bank which in turn is regulated and licenced to do so.

However, the D in DSTOQ stands for decentralized. This has a few implications with the important one being that we don't hold customers tokens. They are held on-chain.

<aside class="notice">
Whenever we refer to the term on-chain, we mean that the action in question is performed on the stellar blockchain. Actions on-chain are immutable and verifiable.
</aside>

Consequently, the customer needs to know something that no one else knows - a private key to verify ownership over assets and transactions need to be signed with said private key before it can be send to the underlying chain.

We'll explain the concept in more depth below and we have an additional section for best practises that will guide you through the process.

