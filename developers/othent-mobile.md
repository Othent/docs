---
description: https://github.com/Othent/othent-mobile
---

# 📱 Othent Mobile

Othent Mobile is a Safari Web Extension, that allows for an easy & fast
integration of Othent on mobile web apps.&#x20;

## Installation <a href="#installation" id="installation"></a>

Website developers can point Users to download and install Othent Mobile from
the AppStore.

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

After these steps, every website where the extension has been enabled will have
the **`window.othent`** object injected to be used by your web apps.

## Usage <a href="#usage" id="usage"></a>

The injected **`window.othent`** object has the same properties as the
<a href="#sdk" id="sdk">SDK</a>. This typescript library has its docs outlined
in [🥪 SDK](./sdk.md).

## Example usage

There are many ways to access the `window.othent` obect injected in the DOM

### React/Javascript

```javascript
  const tryOthent = () => {
    const othent = window.othent;

    if (!othent) {
      alert("Please install and enable Othent Mobile");
      return;
    }

    const details = await othent.logIn();
    console.log(details);

  };
```