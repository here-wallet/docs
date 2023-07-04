---
description: In this article we will look at how Santa Token 2022 works
cover: ../.gitbook/assets/Santa token.png
coverY: 0
---

# 🎅 Santa Token

## Abstract

Santa Token is a fungible token token run on NEAR Protocol. It was launched on December 1st and is available for trading until January 1st, 2023. Tokens can be obtained during an airdrop or can be mined.

On January 1st all tokens can be burned and swap to USDT, NEAR, NFT, or increased staking APY for a year in the HERE app.

A total of 1,000,000 tokens have been issued, all tokens are distributed to contest partners, who in turn conduct airdrops to their users. 100 STT ≈ 1$.

## Earn

Santa Token can be earned. To do this, you just need to transfer it to a friend by phone number. For each transfer, you and your friend will earn 50 Santa tokens. We think this is a great way to surprise your friends and give them a real Christmas miracle.

{% embed url="https://phone.herewallet.app/" %}

## Handing out gifts

Santa Token has a transparent draw algorithm. All prizes will be handed out based on the results of a decentralized randomization call on the smart contract.

At 12:00 PST, the `happy_new_year()` contract method will become available. It will freeze all transfers and generate a random number via  `env::random_seed()` call. You can see this number by calling `get_seed()`.

Then all users will be sorted by `hash(account_id+seed)` and the sequence number of each of their tokens will be superimposed on the prize number from this table. Then each of the sponsors will be given an instruction to whom and how many prizes to send.

The table with prizes is uploaded to IPFS by link and is not changeable. Any user will be able to check their prizes after the contest ends.

## Example

prize table

1 USDC\
0.2 NEAR\
1 USDC\
NFT HERE

**Bob and Alice participated in the contest:**

<table><thead><tr><th width="280.3333333333333"> </th><th>Bob</th><th>Alisa</th></tr></thead><tbody><tr><td>account id</td><td>bob.near</td><td>alisa.near</td></tr><tr><td>Token balance</td><td>1 SANTA</td><td>3 SANTA</td></tr><tr><td>SEED</td><td><strong>123</strong></td><td><strong>123</strong></td></tr><tr><td>sha256(account_id+SEED)</td><td>06e1966d9df7d550f3a3dc71d801afb44dbaa20d1c19cf9405655c6fdacdec0a</td><td>6b6183a63e3dc66cf472a36a9b7b811c44026797cd0b36263f261b6be182bc1d</td></tr></tbody></table>

**Order:**

1. Bob (06...)
2. Alisa (6b...)

1 USDC <> BOB\
0.2 NEAR <> ALISA\
0.5 USDC <> ALISA\
NFT HERE <> ALISA



**Full prize list:** [https://nftstorage.link/ipfs/bafybeia6r4gx3f4obyurdiyknza2ejqcsqboihbkogsqgs3jul3mx5hdoi](https://nftstorage.link/ipfs/bafybeia6r4gx3f4obyurdiyknza2ejqcsqboihbkogsqgs3jul3mx5hdoi)

### Site

{% embed url="https://herewallet.app/santa/" %}

###

### Contract code

{% embed url="https://github.com/here-wallet/santa-token" %}

### Contact

{% embed url="https://explorer.near.org/accounts/santa_token.near" %}

