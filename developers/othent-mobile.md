---
description: https://github.com/Othent/othent-mobile
---

# 📱 Othent Mobile

Othent Mobile is a Safari Web Extension, that allows for an easy & fast
integration of Othent on mobile web apps.&#x20;

## Installation <a href="#installation" id="installation"></a>

Website developers can point Users to download and install Othent Mobile from the [App Store](https://apps.apple.com/us/app/othent/id6452839166).

<div style="display: flex; align-items: center; justify-content: center"><a href="https://apps.apple.com/us/app/othent/id6452839166?itsct=apps_box_badge&amp;itscg=30200" style="display: inline-block; overflow: hidden; border-radius: 13px; width: 250px; height: 83px;"><img src="https://tools.applemediaservices.com/api/badges/download-on-the-app-store/white/en-us?size=250x83&amp;releaseDate=1692576000" alt="Download on the App Store" style="border-radius: 13px; width: 250px; height: 83px;"></a></div>

<meta name="apple-itunes-app" content="app-id=6452839166">

<br/>

Othent uses a pop-up window for the login flow, so users need to disable pop-up blocker in `Settings > Safari`.

Once installed, any user can enable the Extension on any website:

1. Open Safari

![Safari](../.gitbook/assets/othent-mobile/01.safari.icon.png)

2. Tap on the AA icon in the Safari URL bar

![Safari URL Bar](../.gitbook/assets/othent-mobile/02.url.bar.png)

3. Tap on "Manage Extensions"

![Manage Extensions](../.gitbook/assets/othent-mobile/03.manage.extensions.png)

4. Enable "Othent Mobile"

![Enable Othent](../.gitbook/assets/othent-mobile/04.enable.othent.png)

After enabling the extension, users can review permissions for individual sites:

1. iOS shows a "Review Permissions" popup

![Review Permissions](../.gitbook/assets/othent-mobile/05.review.permissions.png)

2. Or users can directly open the extension

![Open Othent Popup](../.gitbook/assets/othent-mobile/06.open.othent.popup.png)

3. Select the duration for the permission to grant

![Permissions](../.gitbook/assets/othent-mobile/07.permisions.png)

After these steps, every website where the extension has been enabled will have a new injected API into the **`window`** object which can be used by your web apps.

## Basic usage <a href="#basic-usage" id="basic-usage"></a>

To use Othent in your application, you don't need to integrate or learn how the Othent Injected API works. Using [arweave-js](https://npmjs.com/arweave), you can easily sign a transaction through Othent in the background:

```javascript
// create Arweave transaction
const tx = await arweave.createTransaction({
  /* tx options */
});

// sign transaction
await arweave.transactions.sign(tx);

// TODO: handle signed transaction
```

When signing a transaction through [arweave-js](https://npmjs.com/arweave), you'll need to omit the second argument of the sign() function, or set it to "use_wallet". This will let the package know to use the extension in the background to sign the transaction.

Once the transaction is signed, you can safely post it to the network

## Advanced Usage <a href="#advanced-usage" id="advanced-usage"></a>

The injected API in **`window`** object can be used from:

- **`window.arweaveWallet`**: This API provides you several methods compatible with other Arweave Wallets such as ArConnect, plus the ones from the Othent [🥪 SDK](./sdk.md).

## Example usage

Your web app can listen to know when the API has been safely injected by adding a simple listener:

```javascript
addEventListener("arweaveWalletLoaded", () => {
  console.log(`You are using the ${window.arweaveWallet.walletName} wallet.`);
  console.log(`Wallet version is ${window.arweaveWallet.walletVersion}`);
});
```

Once this event has been emitted by Othent Mobile you can start using the API methods safely. Here's an example login after the Api has been injected:s

```javascript
addEventListener("arweaveWalletLoaded", () => {
  window.arweaveWallet.logIn().then(console.log);
});
```
