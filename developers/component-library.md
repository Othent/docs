---
description: https://github.com/Othent/react-components
---

# 🍜 Component Library

The Othent component library is a collection of components that enable interaction with the Othent protocol.&#x20;

### Installation <a href="#installation" id="installation"></a>

To use the library in your project, you can install it using&#x20;

```javascript
npm i @othent/react-components
```

### Usage <a href="#usage" id="usage"></a>

To use the library, you can import it into your project:

```javascript
import { OthentLogin } from '@othent/react-components'
```

### Components <a href="#functions" id="functions"></a>

The following components are available in the Othent React Components library:

#### OthentLogin

_Main component that handles all the logic with the Othent SDK._

```tsx
// Main login component
import { OthentLogin } from "@othent/react-components";

const myLogin = () => <OthentLogin />
```

{% hint style="info" %}
_This component uses the rest of the components as building blocks, it's probably the only one you need._
{% endhint %}

_When a user is not logged in, it shows the LoginButton_

_When the user is logged in, it shows its Avatar. Upon clicking the Avatar, it shows a small Modal with the user info and a LogoutButton. The location of this Modal is customizable with the \`location\` attribute:_

```tsx
// Import ModalLocation to select the modal placement
import { OthentLogin, ModalLocation } from "@othent/react-components";

// Pass one of ModalLocation's members as attribute:
const myCustomLogin = () =>
    <OthentLogin location={ ModalLocation['top-left'] }/>
```

_**ModalLocation**_ members include: _center_, _top_, _bottom_, _left_, _right_, _top-left_, _top-right_, _bottom-left_, _bottom-right_

#### Avatar

_Small component to show the profile picture of the user or the first letter of its name in case there's no profile picture._

```tsx
// Avatar component
import { Avatar } from "@othent/react-components";

const myAvatar = () => <Avatar username="John" src="img-URL" />
```

{% hint style="info" %}
The _src_ attribute receives a URL for the profile image shown as avatar. If the URL is not valid, the Avatar shows the first letter of the _username_ upon a plain background.
{% endhint %}

#### LoginButton

Button with the Othent styling to use as a login button. It has an _onlogin_ attribute that receives a callback function to be able to return the _LogInReturnProps_ with user data from the _logIn()_ function in the Othent SDK.

```tsx
// LoginButton component
import { LoginButton } from "@othent/react-components";
import { type LogInReturnProps } from "othent";

const onlogin = (user: LogInReturnProps) => console.log(user);

const myLoginButton = () => <LoginButton onlogin={ onlogin } />
```

#### LogoutButton

Button to use as a logout button. It has an _onlogout_ attribute that receives a callback function to be able to return the _LogOutReturnProps_ from the _logOut()_ function in the Othent SDK.

```tsx
// LoginButton component
import { LogoutButton } from "@othent/react-components";
import { type LogOutReturnProps } from "othent";

const onlogout = (response: LogOutReturnProps) => console.log(response);

const myLogoutButton = () => <LoginButton onlogin={ onlogin } />
```
