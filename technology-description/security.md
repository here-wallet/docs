---
description: What solutions do we use to ensure security of storage in HERE Wallet
cover: ../.gitbook/assets/Export This (1).png
coverY: -249.20127795527156
---

# Security

### Funds Control.

We were faced with a difficult task: the development team must manage the balance of frozen and free NEAR. This management allows us to maximize profits from staking. At the same time, the community must have a control tool and the ability to hand over control to a simple and open algorithm.

### Red Button

To solve this problem, we have created the "Red Button" approach in our contract. It is a set of public methods that are available only if liquidity drops below 5% of the total users balance. These methods will allow you to unstake all the money and return it to the contract vaults. Also, if the "Red Button" is pressed, the management methods will be blocked for 6 epochs. During this time, the money will have time to unstake and all users will be able to withdraw it from the smart contract.

This approach ensures that even if the contract is mismanaged, users can always access the money. At the same time it gives more freedom of management since it is not necessary to put all the logic of money management into a smart contract. External management works more accurately and gives more profit.

{% hint style="warning" %}
The "Red Button" will be pressed automatically in the HERE Wallet application if low liquidity is detected when checking the status of the contract.
{% endhint %}

### **Cost forecasting**

An important task in smart contract management is forecasting expenses in order to have enough available NEAR. We use machine learning algorithms to predict the amount of NEAR that will be withdrawn over the next 4 eras. This makes our prediction the closest to reality.

### Interest Payment

Interest accrual is automatic. When you open the HERE Wallet app, the background makes a request for a smart contract and requests a transfer profit NEAR to the user's account. Withdrawal can be requested at least every second. All accumulated interest since the last withdrawal NEAR will be withdrawn. The interest rate is fixed. Only the contract owner may change it, for example if the yield of the staking changes. It is guaranteed to be between 2 and 10% APY.

It is the task of the contract management team to get the income. The user is guaranteed to get his percentage. If the management is not good enough, the money will be paid out of reserves. If there is not enough money in the reserves to pay dividends, the HERE Wallet app will automatically transfer all NEAR to the cold wallet and you will use it as usual, like on the web wallet. Interest will never be paid at the expense of other users' balances.

{% hint style="info" %}
The amount of commissions. Now the price of gas for transfer, deposit and withdrawal is less than 0.0001N. They are recouped by the income from the staking.
{% endhint %}

### Сonclusion

Today, liquid staking on the HERE Wallet is the most advanced available in the NEAR ecosystem. We can provide good income without blocking NEAR and still leave the control to the community.
