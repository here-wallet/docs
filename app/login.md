---
description: How authorization at HERE Wallet works through access keys
coverY: 0
---

# 💻 Login

NEAR keys do not contain the data needed to add records to the blockchain, they are only needed to prove to other validators that you have the right to make the transaction

In NEAR the access keys are implemented very elegantly. Each account keeps a list of public keys with permissions. This allows you to give the application partial access to the data without showing your main private key.

![Authorization](../.gitbook/assets/tg\_image\_3543857128.jpeg)

To add an access key, you need to perform the same transaction as to transfer money. You pass the public key and a list of accesses you want to add. During authorization in HERE a private key is generated locally on your device. Then the public key is added to your account.

To add a key to your account, you need to sign the transaction on the NEAR web wallet. By opening a page on the web wallet with a link from the application, you transfer a public key and a list of rules. After confirmation, the web wallet will send a request to add the public key to the blockchain. Once the public key is added, the HERE application can use the generated private key to sign all transactions.

{% hint style="info" %}
We are the first wallet who uses this method of authorization. Thanks to it users can login into the application through a web wallet without using their seed! This is the fastest and most convenient way to log in to your NEAR account
{% endhint %}

