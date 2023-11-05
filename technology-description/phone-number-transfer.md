---
description: >-
  Transfers by phone number are available in HERE Wallet even for those users
  who don't have a wallet yet. In this article let's see how it works.
---

# 📞 Phone number transfer



### Sending by phone number takes place in several steps

1. Sending money to a smart counter - a storage with a unique key.
2. Verification of the phone number
3. Receipt of payment by phone number
4. Sending to the linked phone number

### Verification.&#x20;

Verifying phone numbers in web3 applications is a very non-trivial task. There is someone who sends SMS, and most importantly centralized verification. These problems are solved by the LIT Protocol. They provide a decentralized SMS verification protocol. When confirming a number, each of the 16 validators independently verifies the code via API Twilio and if it is correct, signs the transaction. Instead, the validators use multi-signature to ensure that the code is indeed correct.

The user then uses this signature to add his phone number data to the smart contract.

### How to store a phone number.

Storing a phone number is another non-trivial task. If you put it in plaintext or hash, it can be recovered and used for spamming and deanonymization.

Instead of a phone number, the proof of account ownership is stored. hash(account\_id, phone\_number, nonce). This is unrecoverable data, but using this proof the sender can find out who actually needs to make the transfer. The data about the linked account is stored encrypted with limits on the number of requests and cannot be retrieved by brute force!

### Receiving a transfer.

Each transfer is a phone number encrypted via LIT protocol, the decryption function is non-public.

Once the user binds his phone number he can retrieve incoming transfers using proof from LIT Protocol. In the `proof` he passes transfer\_id, nonce and his address.

Inside the LIT validator function:

1. Decrypt the phone number
2. check that `hash(account_id, phone_number, nonce)` is in the smart contract.
3. if so, the node signs the `account_id` and `transfer_id` via muti-signature.

After receiving the signature from the LIT Protocol, the user takes his transfer from the smart contract. The phone number itself is not displayed anywhere in decrypted form, if the validator did not find proof of ownership, an error will be returned without the real phone number hidden in the transfer\_id.

### Conclusion

Thus, sending, receiving and verification of the phone number are decentralized and anonymous, allowing the sender and receiver to transfer money by phone number.
