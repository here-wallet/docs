---
description: How to integrate your dApps with HERE
---

# dApps HERE

### Motivation

dApps must do a lot of transactions and have liquidity at every point in time. That's why they cannot use stacking. Liquid stacking with withdrawal fees is not profitable either. You will have to pay 0.3-0.5% of the amount for each transaction. That's more than the potential income from staking.

In this case, liquid steaking HERE might be a very good solution. You can to keep the entire balance of your dApps on your HERE contract, use it at any time, and still earn passive income.

{% hint style="info" %}
This works because we have part of the balance of all users and dApps free for instant use. You can read more in the HERE Storage section
{% endhint %}

### How to use HERE Storage



Contract NEAR: `storage.herewallet.app`

1. \*\*Cash in\*\*: call \`storage\_deposit()\`
2. \*\*Withdraw\*\*: call \`storage\_withdraw(amount, to\_account\_id)\`&#x20;
   * &#x20;use to\_account\_id=None to withdraw NEAR
   * use to\_account\_id=bob.near to send NEAR from dApp to bob.near account

