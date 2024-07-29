---
description: Othent JS SDK disconnect() function
---

# Disconnect

Logs out the user (disconnect the user's wallet). This will require the user to log back in after called.

```
disconnect(): Promise<void>;
```

{% hint style="info" %}
**Note:** It is recommended to only use this function once the user clicks a clearly marked "Disconnect" button in your application.
{% endhint %}

## Example usage

```ts
// User signs in/up:
await othent.connect();

// User logs out:
await wothent.disconnect();
```
