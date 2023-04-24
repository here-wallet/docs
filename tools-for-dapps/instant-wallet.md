---
description: App Clip HERE Wallet documentation
---

# Instant wallet

**You can use instant wallet to authorize the user without leaving the site.**

We wrote a small library which is fully compatible with wallet selector. We can use it to show a QR code to the user. As soon as he scans the QR code, it will trigger a successful sub-operation and return the result of the transaction

## @herewallet/near-selector

{% embed url="https://github.com/here-wallet/near-selector" %}

This library allows you to interact asynchronously with the here-wallet together with the near-selector.

In contrast to the synchronous signing of transactions in MyNearWallet and official near wallet, where the user is redirected to the wallet site for signing -- **HERE Wallet** provides the ability to sign transactions using async/await API calls.

```bash
npm i near-api-js@^0.44.2
npm i @near-wallet-selector/core --save
npm i @here-wallet/near-selector --save
```

### Usage

```typescript
import "@near-wallet-selector/modal-ui/styles.css";
import { setupWalletSelector } from "@near-wallet-selector/core";
import { setupNearWallet } from "@near-wallet-selector/near-wallet";
import { setupModal } from "@near-wallet-selector/modal-ui";
import { HereWallet, setupHereWallet } from "@here-wallet/near-selector";

const selector = await setupWalletSelector({
  modules: [setupNearWallet(), setupHereWallet()],
  network: "mainnet",
});

// Force login with here-wallet easy!
const here = await selector.wallet<HereWallet>("here-wallet");
const accounts = await here.signIn({ contractId: "social.near" });

console.log(`Hello ${accounts[0].accountId}!`);
```

### How it works

By default, all near-selector api calls that you make with this library run a background process and generate a unique link that the user can go to their mobile wallet and confirm the transaction. This is a link of the form:\
**https://h4n.app/TRX\_SHA1\_IN\_BASE64\_URL\_SAFE**\


If a user has logged into your application from a phone and has a wallet installed, we immediately transfer him to the application for signing. In all other cases, we open a new window on the web.herewallet.app site, where the user can find information about installing the wallet and sign the transaction there.

All this time while user signing the transaction, a background process in your application will monitor the status of the transaction requested for signing.

### Instant Wallet with AppClip

If your goal is to provide the user with a convenient way to log in to your desktop app, you can use Here Instant Wallet, which allows users without a wallet to instantly create one via appclip.

> At the moment here wallet is only available for IOS users

You have the option to override how your user is delivered the signing link. This is how you can create a long-lived transaction signature request and render it on your web page:

```typescript
import { Strategy } from "@here-wallet/near-selector";
import { QRCodeStrategy } from "@here-wallet/near-selector/qrcode-strategy";

// Instant wallet signin HERE!
const here = await selector.wallet<HereWallet>("here-wallet");
const element = document.getElementById("qrcode")

await here.signIn({
  contractId: "social.near",
  strategy: new QRCodeStrategy({ element, theme: "dark" }), // override new window
});
```

You can also look at an example in this repository /example/index.ts or in sandbox: [https://codesandbox.io/s/here-wallet-instant-app-6msgmn](https://codesandbox.io/s/here-wallet-instant-app-6msgmn)

### Strategy and Events

Methods **signIn**, **signAndSendTransaction**, **signAndSendTransactions** have additional parameters:

```typescript
export interface AsyncHereSignDelegate {
  // DefaultStrategy by default called new window popup, you can override it
  strategy?: Strategy;
  signal?: AbortSignal;

  // Just Events, called before strategy, 
  // use this if you don't need to change strategy
  onInitialized?: () => void;
  onRequested?: (link: string) => void;
  onApproving?: (HereProviderResult) => void;
  onSuccess?: (HereProviderResult) => void;
  onFailed?: (HereProviderResult) => void;
}
```

You can also set the default strategy for `setupHereWallet`:

```typescript
setupHereWallet({ strategy: () => new CustomStrategy() })
```

### Security

To transfer data between the application and the phone, we use our own proxy service. On the client side, a transaction confirmation request is generated with a unique request\_id, our wallet receives this request\_id and requests this transaction from the proxy.

**To make sure that the transaction was not forged by the proxy service, the link that opens inside the application contains a hash-sum of the transaction. If the hashes do not match, the wallet will automatically reject the signing request**

### Near Selector

This library was created to speed up development, the most stable version of this module will be available in the official @near-selector/here-wallet library in the future!ty

{% embed url="https://codesandbox.io/s/here-wallet-instant-app-6msgmn?file=/src/index.ts" %}

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption><p>Example on paras</p></figcaption></figure>
