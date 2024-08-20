---
description: Othent JS SDK isAuthenticated property
---

# Is Authenticated

Indicates whether the user is currently authenticated.

## API

```ts
isAuthenticated: boolean;
```

## Example usage

```ts
import { Othent } from "@othent/kms";

const othent = new Othent({ ... });

// ...

const storeSecret = async (key: string, plaintext: string) => {
    // Manually make sure the user is authenticated, or prompt them to authenticate:
    if (!othent.isAuthenticated) {
        await othent.connect();
    }

    // Now we can call other functions from Othent:
    const encryptedData = await othent.encrypt(plaintext);

    localStorage.set(key, encryptedData);
}
```
