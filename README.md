# CryptiSwap API Documentation
This is the official API Document for aggregators, other exchanges and websites to use the [CryptiSwap] exchange. Anyone can request an API key and it's a really simple process, please email us at admin@cryptiswap.org or visit the [contact us] page on our website to chat with us live.

[Cryptiswap]: https://cryptiswap.org/
[contact us]: https://cryptiswap.org/contact

API URL : https://admin.cryptiswap.org/api/v1/

**Overview**
This API document was created for aggregators, other websites and exchanges to use the Cryptiswap exchange to allow users to swap crypto without registration.

**Authentication**
To have access to this API, you must have an API key, please [contact us] for this and it should be available on the same day. When typing in the API command, add "?APIKEY=yourapikeyhere" Replace "yourapikeyhere" with your actual API key. So for exmaple: https://admin.cryptiswap.org/api/v1/get-currencies?APIKEY=yourapikeyhere

**Error Codes**
Depending on the type of error, the API will return a specific error message, for example:

{ error: 'pair is unavailable for exchanges' }

**Rate limit**
There currently is no limit on the amount of calls to the server. This might change if we ever face problems.

## API's
### getCurrencies
The result is a list of all the Cryptocurrencies available on the Cryptiswap exchange
```bash
https://admin.cryptiswap.org/api/v1/get-currencies
```
**Method** : GET <br />
<br />
**Parameters** : <br />
APIKEY: Your API key here <br />
<br />
**Response** <br />
```bash
[
  "BTC",
  "ETH",
  "LTC",
  ....
]
```
### getLimit
The result is the minimum and maximum of a certain crypto pair. The min/max is given for the “from” coin and not the “to” coin. E.g. if the pair is “from” LTC “to" ETH, the min/max amounts will be for LTC.
```bash
https://admin.cryptiswap.org/api/v1/get-limits
```
**Method** <br /> 
GET <br />
<br />
**Parameters** <br />
APIKEY: Your API key here <br />
from: coin user send <br />
to: coin user receive <br />
<br />
**Response** <br />
```bash
{
  "from": "LTC",
  "to": "DOGE",
  "min": 0.51234,
  "max": 20.79758
}
```
### getEstimate
The result will show the amount to receive for exchanging a pair.
```bash
https://admin.cryptiswap.org/api/v1/get-estimate
```
**Method** <br />
POST <br />
<br />
**Parameters** <br />
APIKEY: Your API key here <br />
from: coin user send <br />
to: coin user receive <br />
amount:  amount of user send coin <br />
<br />
**Response** <br />
```bash
{
  "from": "DOGE",
  "to": "LTC",
  "amountFrom": 457.85747,
  "amountTo": 1.0282
}
```
### createOrder
This will open an order on the cryptiswap server
```bash
https://admin.cryptiswap.org/api/v1/create-order
```
**Method** : <br />
POST <br />
<br />
**Parameters**<br />
APIKEY: Your API key here <br />
from: coin user send <br />
to: coin user receive <br />
amount: amount of user send <br />
addressReceive: user's receipitent address <br />
extraIdTo: ??? <br />
<br />
**Response** <br />
```bash
{
  "status": "Awaiting Desposit",
  "from": "BTC",
  "to": "ETH",
  "orderId": "9y6PdXg8XdVSEtX",
  "addressReceive": "0x123123",
  "addressDeposit": "1246RgKhAj3KDBBDy5BZu9NuNmM4HxWY9Q",
  "extraIdDeposit": "???"
}
```
### getOrderData
The result will show the status of the order. The 6 status’ are Awaiting deposit, Confirming, Swapping, Sending, Exchange finished and Expired.
```bash
https://admin.cryptiswap.org/api/v1/get-order-data
```

**Method** : <br />
GET <br />
<br />
**Parameters** : <br />
APIKEY: Your API key here <br />
orderId: Trade Order ID <br />
<br />
**Response** : <br />
```bash
{
  "status": "Exchange finished",
  "hashDeposit": "c653f77c881782e2d7ab76a3dcb5ac3c1871da358bd54d771a7d4c6910a7ba22",
  "hashReceive": "",
  "addressReceive": "46ehEW2XnhDTyTVW1x3sKQ2g1EB3B8w58JRxbzDLp4H7XCt9Vv2tL1vQaKWs5ZWAo3W4AmR7LbRJ6SS1TrjQH6TH3mnrsoT",
  "extraIdReceive": "",
  "from": "BTC",
  "amountDeposit": 0.0002347591015625,
  "to": "XMR",
  "amountReceive": 0.049291
}
```
