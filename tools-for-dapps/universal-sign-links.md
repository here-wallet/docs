---
description: >-
  HERE supports the new transaction format without having to pass signer_id. In
  this article we will explore the possibilities of this approach
---

# Universal sign links



### Wallet-selector format

In the previous wallet selector format, a fully encoded transaction was required to be passed, which required obtaining the signer\_id beforehand. This added the need for each dApp to have a login functionality and made it impossible to create static links to sign transactions.

### Template format

We have introduced a new transaction signing template that allows you to pass a list of actions and have the final transaction generated on the wallet side. This has several benefits:

1. **Static Links:** With the new template, it is possible to create static links for transaction signatures and use them in QR codes, for example. This enables you to make an airdrop to all event participants.
2. **Signing Transactions Without Authorization**: You can add a button to your site that allows users to post NFT or purchase transactions without requiring them to log in to their accounts. This prevents other developers from using NEAR.
3. **Creating Templates:** With this new feature, it is possible to create templates such as [https://h4n.app/g/keypom/xxxx](https://h4n.app/g/keypom/xxxx), which will immediately generate the transaction and redirect it for signature. This makes it easy to create a simple interface for many dApps.

### Format:&#x20;

base58 encode JSON

**example:**&#x20;

```json
{
    "transactions": [
        {
            "actions": {
                    "type": "function call",
                    "params": {
                        "gas": 30000000000000,
                        "method_name": "hi",
                        "args":"",
                        "deposit": 1
                    },
                },
            "receiverId": "bob.near",
        }
    ],
    "network": "mainnet",
}
```

`ArdZExpjN7ppCHqma1CqBn2KmZEyPVDWpJGvx2hoPJZPsFRyJPjeLvef9PPCg3kRGZNV7Nrfc4GcavoxuqGo8fVH6eq5mu5fYkJDyEkVUVhaJoLDpQTBxtfm8WQgVdLgLApDusQnUq5DjRtzwy95z3GXrxHzyqGVJMNhQPZLsZvzFCHtTX3bNukJ98W1pur1pwZm7afvsgRfng8t25ckGcfE1o7A4vn5N8eB5rhdok5wnecs1QKYssBsnfp1TUfsz`

### Supported action types:

* FunctionCall
* Transfer
* DeleteAccount
* CreateAccount
* AddKey

{% hint style="info" %}
params list same as for NEAR rpc api
{% endhint %}

Waller route: `https://my.herewallet.app/call/{b58transaction}`

### Sign

You can also sign a message with a private key without sending it to the blockchain. This is useful e.g. for authorization via a wallet

Base58 json encode:

```json
{ 
    "receiver": "dapp.name", 
    "message": "auth message to sign", 
    "network": "mainnet" 
}
```

Waller route: `https://my.herewallet.app/sign/{b58request}`\




### Redirect url

`?returnUrl=https://google.com`\
``

if error

`https://google.com?failure=some_error_text`

if success

`https://google.com?success=trxHash,trxHash,trxHash`
