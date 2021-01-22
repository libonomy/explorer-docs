# Transactions

## GET Transactions By Hash

```
http://127.0.0.1:1317/txs/E754A9F49EB49497326D27E324A222AE9C5EB6A58155AD368E70CA5904733115
```

## GET Search Transactions

```
http://127.0.0.1:1317/txs?message.action=send&message.sender=libonomy14rr6gl83lueqqnp4ud9lajxpljj5nftcxzpm4s&page=1&limit=3&tx.minheight=1&tx.maxheight=900000
```

PARAMS

```
message.action         send
                       Optional: For message type

message.sender         libonomy14rr6gl83lueqqnp4ud9lajxpljj5nftcxzpm4s
                       Optional: For specific Account

page                   1
                       Optional: For specific Page number

limit                  3
                       Optional: For page limit

tx.minheight           1
                       Optional: For Minimum Height to get transactions from

tx.maxheight           900000
                       Optional: For Maximum Height to get transactions to
```

## POST Broadcast Transaction

```
http://127.0.0.1:1317/txs
```

In order to broadcast the signed transaction object use the following route . You need to send the tx object with mode type

#### HEADERS

#### Content-Type &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; application/json

#### Body raw

```
{
    "tx": {
        "msg": [
            {
                "type": "cusp-sdk/MsgSend",
                "value": {
                    "from_address": "libonomy1da4v3fxy3xkkgqr5g60cjmcpvjcjdd5e4m0qwa",
                    "to_address": "libonomy1da4v3fxy3xkkgqr5g60cjmcpvjcjdd5e4m0qwa",
                    "amount": [
                        {
                            "denom": "flby",
                            "amount": "10"
                        }
                    ]
                }
            }
        ],
        "fee": {
            "gas": "200000",
            "amount": [
                {
                    "denom": "flby",
                    "amount": "0"
                }
            ]
        },
        "memo": "MY_PY_LIB_TEST_MEMO",
        "signatures": [
            {
                "signature": "wK5YP3nxmuytHILranViQPRhPShxDcMcaMihqTMyGdYp7EEXtEG47QtIlGzaShS4FSsNZSmmo3SUoioiabSosA==",
                "pub_key": {
                    "type": "aphelion/PubKeySecp256k1",
                    "value": "B+AjBvUfpWeG5ycmsDO1Om6DuAwrGBK8SLuqvXnxNzV6"
                },
                "account_number": "16",
                "sequence": "10"
            }
        ]
    },
    "mode": "sync"
}
```

## POST Encode Transaction

```
http://127.0.0.1:1317/txs/encode
```

In order to encode the transaction either signed or signed to hash in amino format use the following route

#### BODY raw

```
{
    "type": "cusp-sdk/StdTx",
    "value": {
        "msg": [
            {
                "type": "cusp-sdk/MsgSend",
                "value": {
                    "from_address": "libonomy1da4v3fxy3xkkgqr5g60cjmcpvjcjdd5e4m0qwa",
                    "to_address": "libonomy1da4v3fxy3xkkgqr5g60cjmcpvjcjdd5e4m0qwa",
                    "amount": [
                        {
                            "denom": "flby",
                            "amount": "100"
                        }
                    ]
                }
            }
        ],
        "fee": {
            "amount": [],
            "gas": "200000"
        },
        "signatures": [
            {
                "pub_key": {
                    "type": "aphelion/PubKeySecp256k1",
                    "value": "B+AjBvUfpWeG5ycmsDO1Om6DuAwrGBK8SLuqvXnxNzV6"
                },
                 "signature": "wK5YP3nxmuytHILranViQPRhPShxDcMcaMihqTMyGdYp7EEXtEG47QtIlGzaShS4FSsNZSmmo3SUoioiabSosA=="
            }
        ],
        "memo":"MY_PY_LIB_TEST_MEMO"
    }
}

```
