# ✊ Quick Start

{% hint style="info" %}
**Good to know:** A quick start guide can be good to help you get started using HERE. All you have to do is run a couple of commands and no in-depth understanding of the system is necessary. To learn more, we recommend reading detailed articles about each module of the system
{% endhint %}

{% hint style="danger" %}
The documentation is not finished yet
{% endhint %}

## Install the library and init contract

The best way to interact with HERE is to use [mobile app](https://app.gitbook.com/u/9gJ3V4izZldsrtFmd1sLnd8UrWQ2) or one of NEAR libraries:

{% tabs %}
{% tab title="Node" %}
```
# Install via NPM
npm i near-api-js
```

```javascript
const { connect, keyStores} = nearAPI;

const config = {
  networkId: "mainnet",
  keyStore: new keyStores.BrowserLocalStorageKeyStore(),
  nodeUrl: "https://rpc.mainnet.near.org",
  walletUrl: "https://wallet.mainnet.near.org",
  helperUrl: "https://helper.mainnet.near.org",
  explorerUrl: "https://explorer.mainnet.near.org",
};

// connect to NEAR
const near = await connect(config);

const account = await near.account("storage.herewallet.near");
```
{% endtab %}

{% tab title="Python" %}
```
pip install async-near
```

```python
from async_near.account import Account
from async_near.providers import JsonProvider
from async_near.signer import Signer, KeyPair

rpc_url = "https://rpc.herewallet.app"
json_provider = JsonProvider(rpc_url)
acc = Account(
    json_provider,
    Signer(
        "mydev.near",
        KeyPair("9rhfui3rh.....0fu20f0"),
    ),
)
contract_id = "storage.herewallet.near"
```
{% endtab %}
{% endtabs %}

## Register on smart contract

To get access to the app's api and start earning income from staking, you need to register for a smart contract at a storage

{% tabs %}
{% tab title="Bash" %}
```
NEAR_ENV=mainnet near call storage.herewallet.near register_account '' --gas 300000000000000 --accountId mydev.near 
```
{% endtab %}

{% tab title="Python" %}
```python
await acc.function_call(
    contract_id, "register_account", {}
)
```
{% endtab %}

{% tab title="Java Script" %}
```javascript
await contract.register_account(
  {},
  "300000000000000", // attached GAS
  "0")
);
```
{% endtab %}
{% endtabs %}

Or register via mobile app interface

{% embed url="https://youtu.be/pvq4cVh5viU" %}
HERE app
{% endembed %}

After registration in the application will have access to features, but to start receiving earnings you need to top up your balance in the wallet.

{% tabs %}
{% tab title="Bash" %}
```
NEAR_ENV=mainnet near call storage.herewallet.near storage_deposit '' --deposit 1 --gas 300000000000000  --accountId mydev.near 
```
{% endtab %}

{% tab title="Python" %}
```python
await acc.function_call(
    contract_id, "storage_deposit", {}, amount=1000000000000000000000000
)
```
{% endtab %}

{% tab title="Java Script" %}
```javascript
await contract.storage_deposit(
  {},
  "300000000000000", // attached GAS
  "1000000000000000000000000")
);
```
{% endtab %}
{% endtabs %}
