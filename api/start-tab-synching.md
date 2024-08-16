---
description: Othent JS SDK startTabSynching() function
---

# Start Tab Synching

If and only if you set the [`persistLocalStorage`](./constructor.md#persistlocalstorage-boolean--othentstoragekey)
option to persist and/or sync user details across tabs, you need to call `startTabSynching()` and make sure the cleanup
function it returns is called once you no longer need the `Othent` instance you've created.

## API

```ts
startTabSynching(): void;
```

## Example usage

```ts
import { Othent } from "@othent/kms";

const MyComponent = () => {
  const othent = useMemo(() => {
    return new Othent(options);
  }, [options]);

  useEffect(() => {
    const cleanupFn = othent.startTabSynching();

    return () => {
      cleanupFn();
    };
  }, [othent])
}
```