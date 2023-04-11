---
description: https://github.com/Othent/react-components
---

# 🍜 Component Library

The Othent component library is a collection of functions that enable interaction with the Othent walletless protocol.&#x20;

#### Installation <a href="#installation" id="installation"></a>

To use the library in your project, you can install it using&#x20;

```javascript
npm i @othent/react-components
```

#### Usage <a href="#usage" id="usage"></a>

To use the library, you can import it into your project:import othent from 'othent';

#### Functions <a href="#functions" id="functions"></a>

**The following functions are available in the Othent Library:**_**ping()**: Ping the Othent server._// Ping Othent​try {const response = await othent.ping();console.log(response);} catch (error) {console.error(error);}
