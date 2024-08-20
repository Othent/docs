---
description: Othent JS SDK disconnect() function
---

# Disconnect

Signs out the user (disconnect the user's wallet). This will require the user to log back in after called.

{% hint style="info" %}
It is recommended to only use this function once the user clicks a clearly marked "Disconnect" button in your application.
{% endhint %}

## API

```ts
disconnect(): Promise<void>;
```

## Example usage

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ ... });

// The user signed in/up before:
await othent.connect();

// ...

const handleLogOut = async () => {
  await othent.disconnect();
};
```
