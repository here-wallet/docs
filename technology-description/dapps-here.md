---
description: How to integrate your dApps with HERE
---

# dApps HERE

## Motivation

dApps must do a lot of transactions and have liquidity at every point in time. That's why they cannot use stacking. Liquid stacking with withdrawal fees is not profitable either. You will have to pay 0.3-0.5% of the amount for each transaction. That's more than the potential income from staking.

In this case, liquid steaking HERE might be a very good solution. You can to keep the entire balance of your dApps on your HERE contract, use it at any time, and still earn passive income.

{% hint style="info" %}
This works because we have part of the balance of all users and dApps free for instant use. You can read more in the HERE Storage section
{% endhint %}

## How to use HERE Storage

Contract NEAR: `storage.herewallet.app`

1. **Cash in**: call `storage_deposit()` and attach NEAR
2. **Withdraw**: call  `storage_withdraw(amount, to_account_id)`&#x20;
   * use to\_account\_id=None to withdraw NEAR
   * use to\_account\_id=bob.near to send NEAR from dApp to bob.near account
3. **Get dividends:** `receive_dividends(to_account_id)`
   1. use to\_account\_id=None to withdraw dividends to dApp account
   2. use to\_account\_id=dappowner.near to withdraw dividends from HERE to owners account

## Example

Let's look at an example of how HERE uses the game app. Users can deposit, play and withdraw at any time. At the same time there are usually 3-4k NEAR on the balance of the dApp and the owners could earn additional income.

### Modify the dApp contract to delegate funds to HERE

```rust
#[payable]
pub fn storage_deposit(&mut self) {
    self.total_balance += env::attached_deposit();
}    
```

```rust
#[ext_contract(ext_here)]
pub trait HereStorage {
    fn storage_deposit(&self);
    fn storage_withdraw(&self, amount: U128, to_account_id: Option<ValidAccountId>);
}
pub static HERE_CONTRACT_ID: &str = "storage.herewallet.near";
pub static GAS: u64 = 50_000_000_000_000;

... 
 
#[payable]
pub fn storage_deposit(&mut self) {
    ext_here::storage_deposit(amount, &HERE_CONTRACT_ID, env::attached_deposit(), GAS)
    self.total_balance += env::attached_deposit();
}   
```

Now after the deposit all the NEAR will be immediately transferred to the HERE storage and begin to bring income

### Modify the dApp contract to use funds from HERE

```rust
#[payable]
pub fn storage_withdraw(&mut self,  amount: U128) {
    assert_one_yocto();
    self.total_balance -= amount.0;
    Promise::new(env::predecessor_account_id()).transfer(amount.0);
}    
```

```rust
#[payable]
pub fn storage_withdraw(&mut self,  amount: U128) {
    assert_one_yocto();
    self.total_balance -= amount.0;
    ext_here::storage_withdraw(amount, env::predecessor_account_id(), &HERE_CONTRACT_ID, 1, GAS)
}    
```

You can now withdraw funds from your HERE balance directly to users. For them it will be a usual transaction from your dApp



### **Get income to** owner.near

Call these methods to get dividends on your HERE account. After that you can withdraw them by turning them into a regular NEAR

```bash
near call storage.herewallet.app  register_account  '' --gas 242794783120800 --accountId owner.near

near call storage.herewallet.app  receive_dividends '{"to_account_id":"owner.near"}' --accountId $ACCOUNT --gas 242794783120800
```

## The Economy

the cost of gas using the HERE Wallet&#x20;

| Action              | Gas    | USD Price       |
| ------------------- | ------ | --------------- |
| withdrawal          | 7 TGas | $$4.2*10^-11$$​ |
| deposit             | 6 TGas | $$3.6*10^-11$$​ |
| receiving dividends | 7 TGas | $$4.2*10^-11$$​ |

Let's calculate the economics of the project using the game as an example. there is

* $100,000 on the contract&#x20;
* 10 000$ daily turnover&#x20;
* 200 transactions a day

Then

* daily gas cost: 2600 TGas \~ 0.00000000026 NEAR
* daily dividends: \~1.3 - 2.5N = 8.2 - 15$
* annual profit: 2993-5475$ \*\*

\*\* The interest rate depends on the ratio of balance to turnover and on the terms of the collaboration and will vary from 3% to 9% APY. Text `team@herewallet.app` to get the best terms for your project.
