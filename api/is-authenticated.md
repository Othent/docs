---
description: Othent JS SDK isAuthenticated property
---

# Is Authenticated

Indicates whether the user is currently authenticated.

```
isAuthenticated: boolean;
```

## Example usage

```ts
const handleDispatchTx = () => {
    // Manually make sure the user is authenticated, or prompt them to authenticate:
    if (!othent.isAuthenticated) {
        await othent.connect();
    }

    // Dispatch a transaction (requires being authenticated):
    await othent.sign(tx);
}
```
