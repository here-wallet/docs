---
description: >-
  In this article we will look at how transfers by phone number work in HERE
  Wallet
---

# Phone number transfer

### Abstract

All transfers take place through a smart contract. Inside the contract, there is a database phone\_hash <> [account.id](http://account.id/)

If we do not know yet to whom it belongs when we send money by phone number the money will go to a temporary trust. After confirming the account the money will be delivered to the recipient

If you already know the number, the money will be redirected to the recipient at once

This is a universal mechanism, which will allow you, to implement payment for web2 services which have a database of client numbers but do not have their NEAR addresses



### Send

Calculate the hash of the recipient's number. For the sake of security, the hash counts as `sha256(phone+key)`, so that it is impossible to compile the hash list from all the existing phone numbers If the transaction is done via the HERE application then the key is hidden in the assembly, if you want to get the hash from the web site you have to make a request. If you use your own assembly you can use any key Request to send NEAR to the user by phone number.

```bash
curl -X 'GET' \
  'https://api.herewallet.app/api/v1/phone/calc_phone_hash?phone=11111111111111' \
  -H 'accept: application/json'
  
response:
{
  "hash": "a18ac4e6fbd3fc024a07a21dafbac37d828ca8a04a0e34f368f1ec54e0d4fffb.ce484643605025f9edba734f8e16fe5d47f437326c9951598f2bca46d23f5b53"
}
```

{% code overflow="wrap" %}
```bash
near call phone.herewallet.testnet send_near_to_phone '{"phone":"PHONE HASH"}' --gas 50000000000000 --accountId petr.testnet --deposit 1

```
{% endcode %}

### Receiving

To get the money you need to have a trusted person confirm that you own the phone number. To do this we use the twilio SMS service in HERE. If you were able to receive SMS and prove that you own the phone number it will be highlighted on the smart contract. This is done by requesting

HERE users just need to click on the link from the SMS. It will open in the application and immediately call to get money.

It can be that the recipient does not have a phone or he for some reason does not want to use a purse HERE. In this case we made a special service for sending and receiving NEAR from the browser. It's available at [phone.herewallet.app](https://phone.herewallet.app).



### Security

The phone herewallet service has 2 potential vulnerabilities:

1. **A rogue attacker can access number allocation**\
   To solve this problem we encrypt all phone numbers. Only the sender and the recipient know the real number and the blockchain stores a hash that makes it impossible to know the original number. We encrypt all the remittance comments with AES using the recipient's phone number as a key. Since only the sender and the recipient know this number, only they can decrypt the comments on the transfers.\

2. **A villain can use phone numbers from the blockchain to send spam**\
   For the extraction of the phone number must be confirmed by sms, it happens through our servers. No one except the team of funders has access to the confirmation key and we comply with all security protocols from.\
   \
   At the same time before the allocation of the phone number we limit the maximum transfer of $1000. After number allocation, you can transfer up to $100,000 by number\


### Cancellations

If the money has not been received within 14 days, you can cancel the transfer by calling

{% code overflow="wrap" %}
```bash
near call phone.herewallet.testnet cancel_near_transaction '{"phone":"HASH", "index":0}' --gas 242794783120800 --accountId herewallet.testnet --depositYocto 1
```
{% endcode %}

In the HERE app it will cancel automatically

