---
description: Connect HERE Wallet to your site to push access to more users
---

# HERE Connect (js)

[The Here Wallet Connector](https://web.herewallet.app/) is a simple web service that allows web3 applications to interact with the Here mobile wallet. It uses the same transaction signing interface as the official Near Wallet. This allows web3 apps to integrate Here Wallet without changing their code.



To sign a transaction you need to scan the QR code with the phone on which the installed Here Wallet:

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### Connect @here-wallet/connect

The easiest way to integrate Here Wallet

{% embed url="https://www.npmjs.com/package/@here-wallet/connect" %}

Here Wallet Connect integrates itself into the `near-api-js` library, so you don't have to add extra logic to work with the wallet.

Import here-wallet/connect into the main js/ts file of your project:

<pre class="language-javascript"><code class="lang-javascript">import * as near from "near-api-js"
import runHereWallet from "@here-wallet/connect"
import "@here-wallet/connect/index.css" // you need css loader

// Initialize here wallet bridge
runHereWallet({ near })

<strong>// You dont need change your code! js
</strong></code></pre>

Now all `near-api-js` calls that automatically redirect to `wallet.near.org` will open a built-in modal window in which the user can choose which wallet he wants to use to log in or upvote a transaction:

<figure><img src="../.gitbook/assets/image (4) (2).png" alt=""><figcaption></figcaption></figure>

If you want to use only Here Wallet in your application, add only HERE: true to the library initializer:

```javascript
runHereWallet({ near, onlyHere: true }) 
```

If you have any questions about using our library, you can always email us at [github](https://github.com/here-wallet/herewallet-connect)

### Advance. Change the near-api-js configuration

If you do not want to install unnecessary dependencies, you can simply change the configuration of `near-api-js`. This is done as follows:

```javascript
import * as near from "near-api-js"

const config = {
    networkId: "mainnet",
    walletUrl: "https://web.herewallet.app", // <<< that!
    nodeUrl: "https://rpc.mainnet.near.org",
    helperUrl: "https://helper.mainnet.near.org",
    explorerUrl: "https://explorer.mainnet.near.org"
    keyStore: new keyStores.BrowserLocalStorageKeyStore(),
}

// Just keep using the near api just like you did before!
const initialize = async () => {
    const near = await connect(config)
    const wallet = new WalletConnection(near, "app");

    wallet.requestSignIn({
      contractId: "contract",
      methodNames: ["method"],
    });
}ja
```

### Testnet

```javascript
const config = {
    networkId: "testnet",
    walletUrl: "https://web.testnet.herewallet.app", // <<< this!
    // default testnet setup...
}
```

### Result

{% embed url="https://youtu.be/W7kPvL7Cujk" %}
