---
description: This article describes how to generate income from liquid staking
---

# Getting Income

Unlike other liquid steaking cents hNEAR is fixed and always equal to 1 NEAR.

Income is accumulated in the form of dividends, which are recalculated after any balance change (transfer, withdrawal, deposit). You can check the amount of accumulated dividends by calling the

```bash
NEAR_ENV=mainnet near view storage.herewallet.near  get_user  '{"account_id":"komour.near"}'
```

The accumulated dividends can be transferred to the account at any time by calling the `claim_dividends` method or by pressing the claim button in the application or on the website.

```bash
NEAR_ENV=mainnet near call storage.herewallet.near  claim_dividends  '' --accountId bob.near
```

After that, your balance in hNEAR will be increased. \
**For example:** if you held 1 hNEAR for a year with a yield of 9.5%, your balance will increase by 0.095 NEAR and become 1.095 hNEAR

### Reasoning

HERE Storage does not have a minimum anstaking fee, but we still have to balance so that space is always available. That's why users have different yields. It will go up if you hold money for a long time and go down if you use liquidity often. In order for each user to have his own yield it is necessary to count independently
