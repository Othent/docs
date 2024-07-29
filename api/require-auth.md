---
description: Othent JS SDK requireAuth() function
---

# Require Authentication

Automatically checks if the user is authenticated. If they are not, and...

- `autoConnect === "eager"`: Prompts them to sign in/up again. It throws an error if authentication fails.
- `autoConnect === "lazy"`: Authenticates them automatically, either from an existing session or by prompting them
  to sign in/up again. It throws an error if authentication fails.
- `autoConnect === "off"`: It throws an error.

```
requireAuth(): Promise<void>;
```

{% hint style="info" %}
**Note:** This function offers a simpler alternative to checking `Othent.isAuthenticated` and calling `Othent.connect`
if the user is not authenticated.
{% endhint %}

## Example usage

```ts
const handleDispatchTx = () => {
    // Make sure the user is authenticated, or prompt them to authenticate:
    await othent.requireAuth();

    // Dispatch a transaction (requires being authenticated):
    await othent.sign(tx);
}
```
