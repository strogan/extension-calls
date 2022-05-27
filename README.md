# Extension Calls


# Get all tokens
Request all addresses and token balances

```js

runnableService()
        .get('fetch.balances')
        .on('updated', (data) => {
          dispatch(fetchRawHDBalances(data, true));
          dispatch(removeLoadingIndicator('hdBalances'));
        });

```
Data responce example
```js
{
  activeUser: "00ace1c8-3228-42e4-a745-910f463e9f02"
  formattedTotalFiat: "1,468.85"
  tokens: (13) [{…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}, {…}]
  totalChange: "5.14"
  totalFiat: "1468.85"
}
```
Single token example

```js
{
    "address": "anatha1m7fwxjqp92kftasvgr0pzy8sqg0cay3ghzgwea",
    "name": "ANATHA",
    "token": "ANATHA",
    "fullName": "ANATHA",
    "balance": 3676.99843413,
    "fiatBalance": 1217.82,
    "marketPrice": 0.33119873,
    "formattedBalance": "3,676.99843413",
    "formattedFiatBalance": "1,217.82",
    "change": 0,
    "isFailed": false,
    "error": "",
    "24hChange": 0,
    "color": "#a98375",
    "isDisabled": true,
    "isEnabled": true
}

```



# Connect to extension
Login and then select active user

```js

await runnableService().get('anatha.current.wallet').call({
        cmd: 'init',
        mnemonic: mnemonic, //user seed
        activeUserId: user.id,
        isTestnetMode: isTestnetMode,
      });

```

# Get token name
Returns token name in code format "BNB"
```js
await runnableService().get('anatha.helper').call({ cmd: 'getToken', token });
```



# Send transaction


```js

await runnableService()
          .get('anatha.helper')
          .call({
            cmd: 'send',
            options: rateData.options, // options from Rate Data object
            addresses: addresses?.map((element) => element?.address), // from address
            token, // "BNB"
          });

```


Rate Data object
```js
{
    "validAmount": 0.001,
    "fee": 0.000375,
    "feeToken": "BNB",
    "feeFiat": 0.12309375,
    "totalCost": [
        {
            "amount": 0.001375,
            "token": "BNB"
        }
    ],
    "totalCostFiat": 0.45134375,
    "remainingBalance": 0.05497091,
    "remainingBalanceFiat": 18.0442012075,
    "options": {
        "to": "bnb182vmzxjntaz46cg5gds5gf5dld0p29pg0t20gw",
        "memo": "",
        "token": "BNB",
        "amount": "0.00100000",
        "from": "bnb167dxtc3cvg999au7ylm6rnz8l38gkkkpjw5qz2",
        "sequenceId": 454,
        "readable": {
            "to": "bnb182vmzxjntaz46cg5gds5gf5dld0p29pg0t20gw",
            "amount": "0.00100000",
            "fee": "0.000375",
            "from": "bnb167dxtc3cvg999au7ylm6rnz8l38gkkkpjw5qz2"
        }
    },
    "tokenPrice": 328.25,
    "hra": ""
}
```
