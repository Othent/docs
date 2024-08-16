---
description: Othent JS SDK completeConnectionAfterRedirect() function
---

# Complete Connection After Redirect

If and only if you set the [`auth0LogInMethod = "redirect"`](./constructor.md#auth0loginmethod-auth0loginmethod) option,
users will be redirected to Auth0 to authenticate and then back to your application. When they land bank in your
application, you must call `completeConnectionAfterRedirect()` to complete the authentication process.

By default, `callbackUriWithParams = location.href`, if you environment supports it. Otherwise, you'll have to manually
pass an URI with the `code` and `state` params provided by Auth0, which handles the redirect callback.

See [Auth0's `handleRedirectCallback`](https://auth0.github.io/auth0-spa-js/classes/Auth0Client.html#handleRedirectCallback).

## API

```ts
completeConnectionAfterRedirect(
  callbackUriWithParams?: Auth0RedirectUriWithParams,
): Promise<UserDetails | null>;
```

## Example usage

```ts
import { Othent } from "@othent/kms";

const MyComponent = () => {
  const othent = useMemo(() => {
    return new Othent(options);
  }, [options]);

  useEffect(() => {
    othent.completeConnectionAfterRedirect();
  }, [othent])
}
```