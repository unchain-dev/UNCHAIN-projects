### ðª Web ãµã¤ããæ§ç¯ãã

ããããããªãªã¸ãã«ã® Web ãµã¤ããæ§ç¯ããã¦ã¼ã¶ã¼ã Web ãµã¤ãããç´æ¥ NFT ã Mint ã§ããæ©è½ãå®è£ãã¦ããã¾ãã

- ã¦ã¼ã¶ã¼ã MetaMask ã¦ã©ã¬ããã Web ãµã¤ãã«æ¥ç¶ã§ãã

- ã¦ã¼ã¶ã¼ãã³ã³ãã©ã¯ãé¢æ°ãå¼ã³åºããæ¯æããè¡ããã³ã¬ã¯ã·ã§ã³ãã NFT ãä½æã§ããããã«ãã

ãã®ã¬ãã¹ã³ãçµäºããã¨ãReact ã§æ§ç¯ããã dApp ãå®æãã¾ãã

ã¾ããæ±ç¨çãª dApp ã®ãã­ã³ãã¨ã³ããæ§ç¯ããããã«å¿è¦ãªåºç¤ç¥è­ãç¿å¾ã§ãã¾ãã

### ð  ãã­ã¸ã§ã¯ããã»ããã¢ãããã

ã¾ããReact ã®ãã­ã¸ã§ã¯ããä½æãã¦ããã¾ãã

ã¿ã¼ããã«ãéãã¦ã`Polygon-Generative-NFT` ãã£ã¬ã¯ããªã«ç§»åããä»¥ä¸ã®ã³ãã³ããå®è¡ãã¦ãã ããã

```
npx create-react-app nft-collectible-frontend
```

ã¤ã³ã¹ãã¼ã«ã«ã¯ 2 ï½ 10 åã»ã©ãããã¾ãã

> â ï¸: æ³¨æ
>
> ã¤ã³ã¹ãã¼ã«ããã¾ããããªãå ´åããä½¿ãã® `npm node` ã®ãã¼ã¸ã§ã³ãå¤ãå¯è½æ§ãããã¾ãã
> ä¸è¨ãå®è¡ãã¦ããããä¸åº¦ `create-react-app` ã³ãã³ããå®è¡ãã¦ã¿ã¦ãã ããã
>
> ```
> npm install npm --global # Upgrade npm to the latest version
> ```
>
> ã¤ã³ã¹ãã¼ã«ãå®äºããããã¿ã¼ããã«ã§ä»¥ä¸ãå®è¡ãã¦ããã¹ã¦ããã¾ããã£ã¦ãããã¨ãç¢ºèªãã¦ãã ããã

```
cd nft-collectible-frontend
npm start
```

ãã¾ãããã¨ããã©ã¦ã¶ã§ `localhost://3000` ã«æ°ããã¿ããéããä»¥ä¸ã®ãããªç»é¢ãè¡¨ç¤ºãããã¯ãã§ãã

ããã¯ãæ¨æºçãª React ã®ãã³ãã¬ã¼ãã§ãã

![](/public/images/201-Polygon-Generative-NFT/section-4/4_1_1.png)

ã§ã¯ããã­ã³ãã¨ã³ããæ§ç¯ãããã¡ã¤ã«ã®ä¸­èº«ãæ´çãã¦ããã¾ãããã

`nft-collectible-frontend/public/index.html` ãéãã¦ãã¿ã¤ãã«ã¨ã¡ã¿ãã£ã¹ã¯ãªãã·ã§ã³ãå¤æ´ãã¾ãããã®ã¹ãããã¯ä»»æã§ãã

ä¸è¨ã«ãä»åã®ãã­ã¸ã§ã¯ãã®ããã«ç¨æãããã³ãã¬ã¼ããç´¹ä»ãã¾ãã

```html
// index.html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta name="theme-color" content="#000000" />
    <meta
      name="Collectible NFT on Polygonâ¨"
      content="Solidity + Alchemy + Polygon + React + Vercel = Generative Art NFT ã Mint ãããð«"
    />
    <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
    <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
    <title>Collectible NFT on Polygon</title>
  </head>
  <body>
    <noscript>You need to enable JavaScript to run this app.</noscript>
    <div id="root"></div>
  </body>
</html>
```

æ¬¡ã«ã`nft-collectible-frontend/src` ãã©ã«ãã«ç§»åãã¦ã`App.test.js` , `logo.svg` , `setupTests.js` ãã¡ã¤ã«ãåé¤ãã¦ãã ããã

ãã®ã¬ãã¹ã³ã§ã¯ããããã®ãã¡ã¤ã«ã¯å¿è¦ããã¾ããã

æ¬¡ã«ã`src` ãã©ã«ãã®ä¸­ã«ãã `App.js` ãã¡ã¤ã«ãéããåå®¹ããä»¥ä¸ã®å®åæã«ç½®ãæãã¾ãã

```javascript
// App.js
import "./App.css";
function App() {
  return <h1>Hello World</h1>;
}
export default App;
```

`src/App.css` ã®åå®¹ããã¹ã¦åé¤ãã¦ãã ããã

ãã ãããã®ãã¡ã¤ã«èªä½ã¯åé¤ããªãã§ãã ããã

å¾ã§ããã®ãã¢ãã­ã¸ã§ã¯ãã«ä½¿ç¨ããåºæ¬çãª CSS ã¹ã¿ã¤ã«ãæä¾ãã¾ãã

`localhost://3000` ã«æ»ãã¨ã`Hello World` ã¨ããç»é¢ãè¡¨ç¤ºãããã¯ãã§ãã

ããã§ãReact ãã­ã¸ã§ã¯ãã®ã»ããã¢ãããå®äºãã¾ããã

### ð ã³ã³ãã©ã¯ãã® ABI ã¨ã¢ãã¬ã¹ãåå¾ãã

ãã­ã³ãã¨ã³ããã¹ãã¼ãã³ã³ãã©ã¯ãã«æ¥ç¶ããéä¿¡ã§ããããã«ããããã«ã¯ãã³ã³ãã©ã¯ãã® ABI ã¨ã¢ãã¬ã¹ãå¿è¦ã§ãã

ABIï¼ã¾ãã¯ Application Binary Interfaceï¼ã¯ãã³ã³ãã©ã¯ãã®ã³ã³ãã¤ã«æã«èªåçã«çæããã JSON ãã¡ã¤ã«ã§ãã

ããã­ã¤åã®ãã­ãã¯ãã§ã¼ã³ã¯ãã¹ãã¼ãã³ã³ãã©ã¯ãããã¤ãã³ã¼ãã®å½¢ã§ä¿å­ãã¦ãã¾ãã

ãã®ããã§é¢æ°ãå¼ã³åºããæ­£ãããã©ã¡ã¼ã¿ãæ¸¡ãæ»ãå¤ãè§£æããããã«ã¯ãé¢æ°ã¨ã³ã³ãã©ã¯ãã«é¢ããè©³ç´°ï¼ååãå¼æ°ãåãªã©ï¼ããã­ã³ãã¨ã³ãã«æå®ããå¿è¦ãããã¾ãã

ãããã¾ãã« ABI ãã¡ã¤ã«ã®å½¹å²ã§ãã

`/nft-collectible/artifacts/contracts/NFTCollectible.sol/NFTCollectible.json` ã VS Code ã§éãä¸­èº«ãç¢ºèªãã¦ã¿ã¾ãããã

![](/public/images/201-Polygon-Generative-NFT/section-4/4_1_2.png)

`NFTCollectible.json` ã«è¨è¼ããã¦ãããã¹ã¦ã®ã³ã¼ãããABI ãã¡ã¤ã«ã§ãã

ã¾ããJSON ãã¡ã¤ã«ã React ãã­ã¸ã§ã¯ãã«ã³ãã¼ããå¿è¦ãããã¾ãã

`nft-collectible-frontend/src` ãã©ã«ãã« `contracts` ã¨ããæ°ãããã©ã«ããä½æãã`NFTCollectible.json` ãã¡ã¤ã«ãã³ãã¼ãã¦è²¼ãä»ãã¾ãããã

æ¬¡ã«ãååã®ã¬ãã¹ã³ã§ Polygon ãã¹ããããã«ããã­ã¤ããã¹ãã¼ãã³ã³ãã©ã¯ãã®ã¢ãã¬ã¹ãåå¾ãã¦ãã ããã

ååã®ã¬ãã¹ã³ã§ç§ãä½¿ç¨ããã³ã³ãã©ã¯ãã®ã¢ãã¬ã¹ã¯ `0xF899DeB963208560a7c667FA78376ecaFF684b8E` ã§ãã

ãã®ã¬ãã¹ã³ã§ãããã®ã³ã³ãã©ã¯ããä½¿ç¨ãã¦ããã¾ãã

ããã§ã¯ãã³ã³ãã©ã¯ã ABI ãã¤ã³ãã¼ããã¦ã`App.js` ãã¡ã¤ã«ã«ã³ã³ãã©ã¯ãã¢ãã¬ã¹ãå®ç¾©ãã¦ããã¾ãããã

```javascript
// App.js
import "./App.css";
import contract from "./contracts/NFTCollectible.json";

const contractAddress =
  "ããªãã®ã³ã³ãã©ã¯ãã¢ãã¬ã¹ããã¡ãã«è²¼ãä»ãã¦ãã ãã";
const abi = contract.abi;

function App() {
  return <h1>Hello World</h1>;
}
export default App;
```

### ð  HTMLãCSSãJS ãè¨­å®ãã

ä»åä½æãã Web ãµã¤ãã¯ãã·ã³ãã«ãªãã®ã«ãªãã¾ãã

ããã®ã¯è¦åºãã¨ `Connect Wallet` ãã¿ã³ã ãã§ãã

ã¦ã©ã¬ãããæ¥ç¶ãããã¨ã`Connect Wallet` ãã¿ã³ã `Mint NFT` ãã¿ã³ã«ç½®ãæããã¾ãã

åå¥ã®ã³ã³ãã¼ãã³ããã¡ã¤ã«ãä½æããå¿è¦ã¯ããã¾ããã

ä»£ããã«ããã¹ã¦ã® HTML ã¨ã­ã¸ãã¯ã `App.js` ã«ããã¹ã¦ã® CSS ã `App.css` ã«è¨è¿°ãã¾ãã

ä»¥ä¸ã®åå®¹ãã`App.js` ãã¡ã¤ã«ã«ã³ãã¼ãã¦ãã ããã

```javascript
// App.js
import { useEffect } from "react";
import "./App.css";
import contract from "./contracts/NFTCollectible.json";

const contractAddress = "ããªãã®ã³ã³ãã©ã¯ãã¢ãã¬ã¹ãè²¼ãä»ãã¾ããã";
const abi = contract.abi;

function App() {
  const checkWalletIsConnected = () => {};

  const connectWalletHandler = () => {};

  const mintNftHandler = () => {};

  const connectWalletButton = () => {
    return (
      <button
        onClick={connectWalletHandler}
        className="cta-button connect-wallet-button"
      >
        Connect Wallet
      </button>
    );
  };

  const mintNftButton = () => {
    return (
      <button onClick={mintNftHandler} className="cta-button mint-nft-button">
        Mint NFT
      </button>
    );
  };

  useEffect(() => {
    checkWalletIsConnected();
  }, []);

  return (
    <div className="main-app">
      <h1>Scrappy Squirrels Tutorial</h1>
      <div>{connectWalletButton()}</div>
    </div>
  );
}

export default App;
```

`App.js` ã® 5 è¡ç®ã§ããªãã®ã³ã³ãã©ã¯ãã¢ãã¬ã¹ãè¨­å®ãã¦ãã ããã

```javascript
// App.js
const contractAddress = "ããªãã®ã³ã³ãã©ã¯ãã¢ãã¬ã¹ãè²¼ãä»ãã¾ããã";
```

ç¾æç¹ã§ã¯ãé¢æ°ãããã¤ãå®ç¾©ãã¦ãããã¨ã«æ³¨æãã¦ãã ãããå¾ã§ããã®ç®çãèª¬æããã­ã¸ãã¯ãçµã¿è¾¼ãã§ããäºå®ã§ãã

ã¾ããWeb ã¢ããªã±ã¼ã·ã§ã³ã®ããã«ãCSS ãç¨æãã¾ããã

ä»¥ä¸ã `App.css` ãã¡ã¤ã«ã«ã³ãã¼ãã¦ãã ããã

```css
// App.css
.main-app {
    text-align: center;
    margin: 100px;
}

.cta-button {
    padding: 15px;
    border: none;
    border-radius: 12px;
    min-width: 250px;
    color: white;
    font-size: 18px;
    cursor: pointer;
}

.connect-wallet-button {
    background: rgb(32, 129, 226);
}

.mint-nft-button {
    background: orange;
}
```

ããªãã® Web ãµã¤ãã¯ããã®ããã«è¡¨ç¤ºãããã¯ãã§ãã

![](/public/images/201-Polygon-Generative-NFT/section-4/4_1_3.png)

CSS ã¹ã¿ã¤ã«ãéçè¦ç´ ï¼ç»åãããããããã¿ãã½ã¼ã·ã£ã«ã¡ãã£ã¢ãªã³ã¯ãªã©ï¼ãè¿½å ãã¦ãWeb ãµã¤ãã®å¤è¦³ãèªç±ã«ã«ã¹ã¿ãã¤ãºãã¦ãã ããã

ããã¾ã§ããã­ã¸ã§ã¯ãã®åºç¤ã¨ãªããã­ãã¯ã¯ã»ã¼ãããã¾ããã

ããã§ãã¦ã¼ã¶ã¼ãã¦ã©ã¬ããã Web ãµã¤ãã«æ¥ç¶ããæºåãæ´ãã¾ããã

### ð¦ MetaMask ã¦ã©ã¬ããã¨ã®æ¥ç¶

ã¦ã¼ã¶ã¼ãã³ãã©ã¯ããå¼ã³åºãããã«ã¯ãèªåã®ã¦ã©ã¬ããã Web ãµã¤ãã«æ¥ç¶ããå¿è¦ãããã¾ãã

ã¦ã©ã¬ããæ¥ç¶ã¯ãã¦ã¼ã¶ã¼ã NFT ã Mint ããã¬ã¹ä»£ã¨è²©å£²ä¾¡æ ¼ãæ¯æããã¨ãå¯è½ã«ãã¾ãã

ãã®ã¬ãã¹ã³ã§ã¯ãMetaMask ã¦ã©ã¬ããã¨ MetaMask API ã®ã¿ãä½¿ç¨ãã¾ãã

ã¾ããã¦ã¼ã¶ã¼ã®ãã©ã¦ã¶ã«ãMetaMask ã¦ã©ã¬ãããå­å¨ãããç¢ºèªãã¦ããã¾ãã

ã¦ã¼ã¶ã¼ã¯ MetaMask ã¦ã©ã¬ãããæã£ã¦ããªããã°ãWeb ãµã¤ãä¸ã§ NFT ã Mint ã§ãã¾ããã

MetaMask ã¦ã©ã¬ãããå­å¨ãããã©ãããç¢ºèªããã­ã¸ãã¯ãã`checkWalletIsConnected` é¢æ°ã«å¥åãã¾ãããã

```javascript
// App.js
const checkWalletIsConnected = async () => {
  const { ethereum } = window;

  if (!ethereum) {
    console.log("Make sure you have MetaMask installed!");
    return;
  } else {
    console.log("Wallet exists! We're ready to go!");
  }
};
```

ãªãã`App.js` ãã­ã¼ããããéã«ãMetaMask ã®å­å¨ãç¢ºèªãã `useEffect` ããã¯ãå®ç¾©ãã¦ãã¾ãã

ã¢ããªã±ã¼ã·ã§ã³ã® `localhost` ãã¼ã¸ã§ Console ãéãã¦ãã ããã

- ã¹ããã: Web ãã¼ã¸ä¸ã§å³ã¯ãªãã¯ â `Inspect` â `Console`

MetaMask ãã¤ã³ã¹ãã¼ã«ããã¦ããã°ã`Wallet exists! Weâre ready to go!` ã¨ããã¡ãã»ã¼ã¸ã Console ã«è¡¨ç¤ºããã¦ããã¯ãã§ãã

![](/public/images/201-Polygon-Generative-NFT/section-4/4_1_4.png)

MetaMask ã¨ã¯ã¹ãã³ã·ã§ã³ãã¤ã³ã¹ãã¼ã«ããããã¨ãã£ã¦ãã¢ã¯ã»ã¹ãããã¹ã¦ã® Web ãµã¤ãã« MetaMask ãèªåçã«æ¥ç¶ãããããã§ã¯ããã¾ããã

MetaMask ãã¦ã¼ã¶ã¼ã«ã¦ã©ã¬ãããæ¥ç¶ããããã«ä¿ãå¿è¦ãããã®ã§ãã

ããã§ç»å ´ããã®ã `Connect Wallet` æ©è½ã§ãã

ããã¯ Web3 ã®ã­ã°ã¤ã³ãã¿ã³ã«ç¸å½ãã¾ãã

ãã®ã­ã°ã¤ã³ãã¿ã³ã¯ãã¦ã¼ã¶ã¼ããã­ã³ãã¨ã³ããéãã¦ãã­ãã¯ãã§ã¼ã³ãããã¯ã¼ã¯ã«æ¥ç¶ããã³ã³ãã©ã¯ããå¼ã³åºããã¨ãå¯è½ã«ãã¾ãã

MetaMask ã¯ `window.ethereum.request` ã¡ã½ããã§ãã®ãã­ã»ã¹ã·ã³ãã«ã«å®è¡ãã¾ãã

ã¾ããã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¢ãã¬ã¹ãè¿½è·¡ããããã«ã`App()` ã§ `useState` ããã¯ãä½¿ã£ã¦å¤æ°ãå®ç¾©ãã¾ãããã

ã¾ããReact ãã `useState` ãã¤ã³ãã¼ãããããã«ã`App.js` ãã¡ã¤ã«ã® 1 è¡ç® `import from 'react'` ã®ä¸­èº«ãä¸è¨ã®ããã«æ´æ°ãã¦ãã ããã

```javascript
// App.js
import { useEffect, useState } from "react";
```

ãããããä¸è¨ã `checkWalletIsConnected` é¢æ°ã®çä¸ã«è¿½å ãã¦ãã ããã

```javascript
// App.js
const [currentAccount, setCurrentAccount] = useState(null);
```

`currentAccount` ã«ã¯ãã¦ã¼ã¶ã¼ã®å¬éã¦ã©ã¬ããã¢ãã¬ã¹ãæ ¼ç´ããã¾ãã

`setCurrentAccount` ã¯ã`currentAccount` ã®ç¶æãæ´æ°ããé¢æ°ã§ãã

`useState(null)` ã§ `currentAccount` ã¨ `setCurrentAccount` ãåæåãã¦ãã¾ãã

æ¬¡ã«ã`connectWalletHandler` é¢æ°ãå®ç¾©ãã¾ãããã

```javascript
// App.js
const connectWalletHandler = async () => {
  const { ethereum } = window;

  if (!ethereum) {
    alert("Please install MetaMask!");
  }

  try {
    const accounts = await ethereum.request({ method: "eth_requestAccounts" });
    console.log("Found an account! Address: ", accounts[0]);
    setCurrentAccount(accounts[0]);
  } catch (err) {
    console.log(err);
  }
};
```

`connectWalletHandler` é¢æ°ãä½ãããã®ããç°¡åã«èª¬æãã¾ãããã

ã¾ããMetaMask ãã¤ã³ã¹ãã¼ã«ããã¦ãããã©ããããã§ãã¯ãã¾ãã

ã¤ã³ã¹ãã¼ã«ããã¦ããªãå ´åã¯ãMetaMask ã®ã¤ã³ã¹ãã¼ã«ãä¿ããããã¢ãããè¡¨ç¤ºããã¾ãã

```javascript
// App.js
const { ethereum } = window;

if (!ethereum) {
  alert("Please install MetaMask!");
}
```

MetaMask ã«ã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããæ¥ç¶ãä¿ããã¢ãã¬ã¹ã®åå¾ãè©¦ã¿ã¾ãã

```javascript
// App.js
const accounts = await ethereum.request({ method: "eth_requestAccounts" });
console.log("Found an account! Address: ", accounts[0]);
```

ã¦ã¼ã¶ã¼ã Web ãµã¤ãã¨ã®æ¥ç¶ã«åæããã¨ãæåã«å©ç¨å¯è½ãªã¦ã©ã¬ããã¢ãã¬ã¹ãåå¾ããããã`currentAccount` å¤æ°ã®å¤ã¨ãã¦è¨­å®ãã¾ãã

```javascript
// App.js
setCurrentAccount(accounts[0]);
```

ä½ãåé¡ãçºçããå ´åï¼ã¦ã¼ã¶ã¼ãæ¥ç¶ãæå¦ãããªã©ï¼ãå¦çãä¸­æ­ãã¦ã³ã³ã½ã¼ã«ã«ã¨ã©ã¼ã¡ãã»ã¼ã¸ãè¡¨ç¤ºããã¾ãã

```javascript
// App.js
} catch (err) {
	console.log(err)
}
```

### ð ã¦ã©ã¬ããæ¥ç¶ã®ãã¹ããå®è¡ãã

ä¸è¨ã®ã³ã¼ãããã¹ã¦ `App.js` ã«åæ ãããããMetaMask ã®ãã©ã°ã¤ã³ãã¯ãªãã¯ããããªãã®ã¦ã©ã¬ããã¢ãã¬ã¹ã®æ¥ç¶ç¶æ³ãç¢ºèªãã¾ãããã

ãããä¸å³ã®ããã« `Connected` ã¨è¡¨ç¤ºããã¦ããå ´åã¯ã`Connected` ã®æå­ãã¯ãªãã¯ãã¾ãã

![](/public/images/201-Polygon-Generative-NFT/section-4/4_1_5.png)

ããã§ãWeb ãµã¤ãã¨ããªãã®ã¦ã©ã¬ããã¢ãã¬ã¹ã®æ¥ç¶ãä¸åº¦è§£é¤ãã¾ãã

- `Disconnect this account` ãé¸æãã¦ãã ããã

![](/public/images/201-Polygon-Generative-NFT/section-4/4_1_6.png)

æ¬¡ã«ã­ã¼ã«ã«ãµã¼ãã«ãã¹ãããã¦ããããªãã® Web ãµã¤ãããªãã¬ãã·ã¥ãã¦ã`Connect Wallet` ãã¿ã³ãæ¼ãã¦ãã ããã

MetaMask ã Web ãµã¤ãã¨ã®æ¥ç¶ãä¿ãã¦ãã¾ãã®ã§ãåæãã¾ãããã

ä¸è¨ã®ããã«ãConsole ã«ããªãã®ãããªãã¯ã¦ã©ã¬ããã¢ãã¬ã¹ãåºåããã¦ããã°ãã¦ã©ã¬ããæ¥ç¶ã®ãã¹ãã¯æåã§ãã

![](/public/images/201-Polygon-Generative-NFT/section-4/4_1_7.png)

ã¦ã©ã¬ãããæ¥ç¶ããããã`Connect Wallet` ãã¿ã³ã `Mint NFT` ãã¿ã³ã«ç½®ãæãã¦ããã¾ãããã

`App.js` ã®æ»ãå¤ã§ã`Connect Wallet` ãã¿ã³ã®ã¬ã³ããªã³ã°ãæ¡ä»¶ä»ãã¬ã³ããªã³ã°ã«ç½®ãæãã¦ã¿ã¾ãããã

`return ()` ã®ä¸­èº«ãä¸è¨ã®ããã«å¤æ´ãã¦ãã ããã

```javascript
// App.js
return (
  <div className="main-app">
    <h1>Scrappy Squirrels Tutorial</h1>
    <div>{currentAccount ? mintNftButton() : connectWalletButton()}</div>
  </div>
);
```

ããã§ãç§ãã¡ã® Web ãµã¤ãã¯ãã®ããã«ãªãã¾ãã

![](/public/images/201-Polygon-Generative-NFT/section-4/4_1_8.png)

ãã¼ã¸ãæ´æ°ãã¦ãMetaMask ã¨ã¯ã¹ãã³ã·ã§ã³ãç¢ºèªãã¦ã¿ã¾ãããã

MetaMask ã¯ã¾ã  Web ãµã¤ãã«æ¥ç¶ããã¦ãããã¨ãä¼ãã¦ãã¾ãããWeb ãµã¤ãã«ã¯ã¾ã  Connect Wallet ãã¿ã³ãè¡¨ç¤ºããã¦ãããã¨ããããã¾ãã

![](/public/images/201-Polygon-Generative-NFT/section-4/4_1_9.png)

React ã«æ£ãã¦ããäººãªãããªããã®ãããªãã¨ãèµ·ããã®ããåããã§ãããã

çµå±ã®ã¨ããã`connectWallet` é¢æ°ã®ä¸­ã ãã§ `setCurrentAccount` ãè¨­å®ãã¦ããã®ã§ãã

å®éã«ã¯ã`App.js` ãã­ã¼ãããããã³ã«ï¼ã¤ã¾ãæ´æ°ãããã³ã«ï¼ãã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã Web ãµã¤ãã«æ¥ç¶ããã¦ãããç¢ºèªããå¿è¦ãããã¾ãã

ããã§ã`checkWalletIsConnected` é¢æ°ãæ¡å¼µãã¦ãWeb ãµã¤ããã­ã¼ããããã¨åæã«ã¢ã«ã¦ã³ãããã§ãã¯ããã¦ã©ã¬ããããã§ã«æ¥ç¶ããã¦ããå ´åã¯ `currentAccount` ãè¨­å®ããããã«ãã¾ãããã

ä¸è¨ã®ããã«ã`checkWalletIsConnected` é¢æ°ãæ´æ°ãã¦ãã ããã

```javascript
// App.js
const checkWalletIsConnected = async () => {
  const { ethereum } = window;

  if (!ethereum) {
    console.log("Make sure you have MetaMask installed!");
    return;
  } else {
    console.log("Wallet exists! We're ready to go!");
  }

  const accounts = await ethereum.request({ method: "eth_accounts" });

  if (accounts.length !== 0) {
    const account = accounts[0];
    console.log("Found an authorized account: ", account);
    setCurrentAccount(account);
  } else {
    console.log("No authorized account found");
  }
};
```

ãã® `checkWalletIsConnected` é¢æ°ã¯ã[éåæ](https://zenn.dev/tentel/articles/8146043d1101b5ea873d)ï¼`async`ï¼ã§ãã

ãã®é¢æ°ãä½ãããã®ããç°¡åã«è§¦ãã¦ããã¾ãããã

- MetaMask ãã¤ã³ã¹ãã¼ã«ããã¦ãããã©ããããã§ãã¯ããçµæãã³ã³ã½ã¼ã«ã«åºåãã¾ãã

  ```javascript
  // App.js
  if (!ethereum) {
    console.log("Make sure you have MetaMask installed!");
    return;
  } else {
    console.log("Wallet exists! We're ready to go!");
  }
  ```

- Web ãµã¤ãã«æ¥ç¶ä¸­ã®ã¢ã«ã¦ã³ãã«å¯¾ãã¦ MetaMask ã®ãªã¯ã¨ã¹ããè©¦ã¿ã¾ãã

```javascript
// App.js
const accounts = await ethereum.request({ method: "eth_accounts" });
```

- MetaMask ããã§ã« Web ãµã¤ãã«æ¥ç¶ããã¦ããå ´åã¯ããã®é¢æ°ã«ã¢ã«ã¦ã³ãã®ãªã¹ããæ¸¡ãã¦è¦æ±ãåºãã¾ãã

```javascript
// App.js
if (accounts.length !== 0) {
  const account = accounts[0];
  console.log("Found an authorized account: ", account);
```

- ãªã¹ããç©ºã§ãªãå ´åã`checkWalletIsConnected` é¢æ°ã¯ MetaMask ããåå¾ããæåã®ã¢ã«ã¦ã³ãã¢ãã¬ã¹ãé¸ã³ãããã `currentAccount` ã«è¨­å®ãã¾ãã

```javascript
// App.js
setCurrentAccount(account);
```

- ãªã¹ããç©ºã®å ´åã¯ãç©ºã®ãªã¹ããè¿ãããçµæãã³ã³ã½ã¼ã«ã«åºåãã¾ãã

```javascript
// App.js
} else {
  console.log("No authorized account found");
}
```

`checkWalletIsConnected` é¢æ°ãæ´æ°ãã¦ããããã¼ã¸ããªãã¬ãã·ã¥ããã¨ãWeb ãµã¤ãã«ã¯ `Mint NFT` ãã¿ã³ãè¡¨ç¤ºããã¦ããã¯ãã§ãã

### ð» Web ãµã¤ããã NFT ã Mint ãã

ããã§ã¯ãWeb ãµã¤ãã®ä¸­æ ¸ã¨ãªãæ©è½ãå®è£ãã¦ããã¾ãããã

ã¦ã¼ã¶ã¼ã `Mint NFT` ãã¿ã³ãã¯ãªãã¯ããã¨ãæ¬¡ã®ãããªãã¨ãèµ·ããã¨äºæ³ããã¾ãã

1\. MetaMask ã¯ãNFT ã®è²©å£²ä¾¡æ ¼ã¨ã¬ã¹ä»£ãæ¯æãããã¦ã¼ã¶ã¼ã«ä¿ãã¾ãã

2\. ã¦ã¼ã¶ã¼ãåæããã¨ãMetaMask ã¯ããªãã®ã³ã³ãã©ã¯ããã `mintNFT` é¢æ°ãå¼ã³åºãã¾ãã

3\. åå¼ãå®äºããã¨ãåå¼ã®çµæï¼æåããããã¯å¤±æï¼ãã¦ã¼ã¶ã¼ã«éç¥ãã¾ãã

ããããã­ã³ãã¨ã³ãã§è¡ãã«ã¯ãã¹ãã¼ãã³ã³ãã©ã¯ãã«å«ã¾ãã `ethers` ã©ã¤ãã©ãªãå¿è¦ã§ãã

ã¿ã¼ããã«ã§ã`nft-collectible-frontend` ã«ç§»åããä»¥ä¸ã®ã³ãã³ããå®è¡ãã¦ãã ããã

```
npm install ethers
```

æ¬¡ã«ã`App.js` ã§ `ethers` ã©ã¤ãã©ãªãã¤ã³ãã¼ããã¾ãããã

`import contract from './contracts/NFTCollectible.json';` ã®ç´ä¸ã«ãä¸è¨ãè¿½å ãã¦ãã ããã

```javascript
// App.js
import { ethers } from "ethers";
```

æå¾ã«ãä¸è¨ã®ããã« `mintNftHandler` é¢æ°ãæ´æ°ãã¾ãããã

```javascript
// App.js
const mintNftHandler = async () => {
  try {
    const { ethereum } = window;

    if (ethereum) {
      const provider = new ethers.providers.Web3Provider(ethereum);
      const signer = provider.getSigner();
      const nftContract = new ethers.Contract(contractAddress, abi, signer);

      console.log("Initialize payment");
      let nftTxn = await nftContract.mintNFTs(1, {
        value: ethers.utils.parseEther("0.01"),
      });

      console.log("Mining... please wait");
      await nftTxn.wait();

      console.log(`Mined, see transaction: ${nftTxn.hash}`);
    } else {
      console.log("Ethereum object does not exist");
    }
  } catch (err) {
    console.log(err);
  }
};
```

ãã® `mintNftHandler` é¢æ°ã¯ã[éåæ](https://zenn.dev/tentel/articles/8146043d1101b5ea873d)ï¼`async`ï¼ã§ãã

ãã¤ãã®ããã«ããã®é¢æ°ãä½ãããã®ãã«è§¦ãã¦ã¿ã¾ãããã

1\. MetaMask ããæå¥ããã `ethereum` ãªãã¸ã§ã¯ãã«ã¢ã¯ã»ã¹ãããã¨ãã¾ãã

```javascript
// App.js
const { ethereum } = window;
```

2\. `ethereum` ãå­å¨ããå ´åãMetaMask ã RPC ãã­ãã¤ãã¨ãã¦è¨­å®ãã¾ãã
ããã¯ãMetaMask ã®ã¦ã©ã¬ãããä½¿ã£ã¦ãã¤ãã¼ã«ãªã¯ã¨ã¹ããçºè¡ãããã¨ãæå³ãã¾ãã

```javascript
// App.js
  if (ethereum) {
    const provider = new ethers.providers.Web3Provider(ethereum);
	:
```

3\. ãªã¯ã¨ã¹ããçºè¡ããããã«ã¯ãã¦ã¼ã¶ã¼ã¯èªåã®ç§å¯éµãä½¿ã£ã¦ãã©ã³ã¶ã¯ã·ã§ã³ã«ç½²åããå¿è¦ãããã¾ãããã®ããã« `signer` ã«ã¢ã¯ã»ã¹ãã¾ãã

```javascript
// App.js
const signer = provider.getSigner();
```

4\. æ¬¡ã«ãããã­ã¤ãããã³ã³ãã©ã¯ãã®ã¢ãã¬ã¹ãã³ã³ãã©ã¯ã ABIãããã³ `signer` ãä½¿ç¨ãã¦ã`ethers` ã®ã³ã³ãã©ã¯ãã¤ã³ã¹ã¿ã³ã¹ãéå§ãã¾ãã

```javascript
// App.js
const nftContract = new ethers.Contract(contractAddress, abi, signer);
console.log("Initialize payment");
```

5\. ããã§ãåè¿°ã®ã³ã³ãã©ã¯ããªãã¸ã§ã¯ããéãã¦ã³ã³ãã©ã¯ãä¸ã®é¢æ°ãå¼ã³åºããã¨ãã§ãã¾ãã`mintNFT` é¢æ°ãå¼ã³åºããMetaMask ã« `0.01 ETH`ï¼ããã¯ NFT ã«è¨­å®ããä¾¡æ ¼ï¼ãéä¿¡ããããä¾é ¼ãã¾ãã

```javascript
// App.js
let nftTxn = await nftContract.mintNFTs(1, {
  value: ethers.utils.parseEther("0.01"),
});
console.log("Mining... please wait");
```

6\. ãã©ã³ã¶ã¯ã·ã§ã³ãå¦çãããã®ãå¾ã¡ãå¦çãå®äºãããããã©ã³ã¶ã¯ã·ã§ã³ã®ããã·ã¥ãã³ã³ã½ã¼ã«ã«åºåãã¾ãã

```javascript
// App.js
await nftTxn.wait();
console.log(`Mined, see transaction: ${nftTxn.hash}`);
```

<!-- textlint-disable -->

7\. ãã©ã³ã¶ã¯ã·ã§ã³ãå¤±æããå ´åï¼ééã£ãé¢æ°ãå¼ã³åºããããééã£ããã©ã¡ã¼ã¿ãæ¸¡ãããã0.01 ETH ä»¥ä¸ãéããããã¦ã¼ã¶ã¼ãåå¼ãæå¦ããããªã©ï¼ãã¨ã©ã¼ãã³ã³ã½ã¼ã«ã«åºåããã¾ãã

<!-- textlint-enable -->

```javascript
// App.js
  } catch (err) {
    console.log(err);
  }
```

### â¨ `App.js` ã®å®æ

ããã¾ã§ãã­ã³ãã¨ã³ãã®ã³ã¢æ©è½ã®å®è£ãçµããã¾ããã

`App.js` ã®æçµç¤ã¯ãã¡ãã§ãã

```javascript
// App.js

import { useEffect, useState } from "react";
import "./App.css";
import contract from "./contracts/NFTCollectible.json";
import { ethers } from "ethers";

const contractAddress = "0x7aDBc3497BE70a903c5b17BEf184782dD0A7eFAa";
const abi = contract.abi;

function App() {
  const [currentAccount, setCurrentAccount] = useState(null);

  const checkWalletIsConnected = async () => {
    const { ethereum } = window;

    if (!ethereum) {
      console.log("Make sure you have MetaMask installed!");
      return;
    } else {
      console.log("Wallet exists! We're ready to go!");
    }

    const accounts = await ethereum.request({ method: "eth_accounts" });

    if (accounts.length !== 0) {
      const account = accounts[0];
      console.log("Found an authorized account: ", account);
      setCurrentAccount(account);
    } else {
      console.log("No authorized account found");
    }
  };

  const connectWalletHandler = async () => {
    const { ethereum } = window;

    if (!ethereum) {
      alert("Please install MetaMask!");
    }

    try {
      const accounts = await ethereum.request({
        method: "eth_requestAccounts",
      });
      console.log("Found an account! Address: ", accounts[0]);
      setCurrentAccount(accounts[0]);
    } catch (err) {
      console.log(err);
    }
  };

  const mintNftHandler = async () => {
    try {
      const { ethereum } = window;

      if (ethereum) {
        const provider = new ethers.providers.Web3Provider(ethereum);
        const signer = provider.getSigner();
        const nftContract = new ethers.Contract(contractAddress, abi, signer);

        console.log("Initialize payment");
        let nftTxn = await nftContract.mintNFTs(1, {
          value: ethers.utils.parseEther("0.01"),
        });

        console.log("Mining... please wait");
        await nftTxn.wait();

        console.log(`Mined, see transaction: ${nftTxn.hash}`);
      } else {
        console.log("Ethereum object does not exist");
      }
    } catch (err) {
      console.log(err);
    }
  };

  const connectWalletButton = () => {
    return (
      <button
        onClick={connectWalletHandler}
        className="cta-button connect-wallet-button"
      >
        Connect Wallet
      </button>
    );
  };

  const mintNftButton = () => {
    return (
      <button onClick={mintNftHandler} className="cta-button mint-nft-button">
        Mint NFT
      </button>
    );
  };

  useEffect(() => {
    checkWalletIsConnected();
  }, []);

  return (
    <div className="main-app">
      <h1>Scrappy Squirrels Tutorial</h1>
      <div>{currentAccount ? mintNftButton() : connectWalletButton()}</div>
    </div>
  );
}

export default App;
```

ããã§ã¯ãWeb ãµã¤ãã«åããããã©ã¦ã¶ã® Console ãéããMining ç¶æ³ããªã¢ã«ã¿ã¤ã ã§ç¢ºèªã§ããããã«ãã¾ãããã

**MetaMask ã®ãããã¯ã¼ã¯ã `Polygon Testnet` ã«ãã¦**ã`Mint NFT` ãã¿ã³ãã¯ãªãã¯ãã¾ãã

MetaMask ã 0.01 ETH + ã¬ã¹ä»£ãæ¯æãããä¿ãã®ã§ãåæãã¦ãã ããã

ãã©ã³ã¶ã¯ã·ã§ã³ã®å¦çã«ã¯ç´ 15 ï½ 20 ç§ãããã¾ãã

å¦çãå®äºããããMetaMask ã®ãããã¢ããã¨ã³ã³ã½ã¼ã«åºåã®ä¸¡æ¹ã§ãã©ã³ã¶ã¯ã·ã§ã³ãç¢ºèªã§ãã¾ãã

![](/public/images/201-Polygon-Generative-NFT/section-4/4_1_10.png)

> â ï¸: 2022 å¹´ 4 æ 1 æ¥ãããMint ãã¿ã³ããã¨ä¸è¨ã®ãããªã¨ã©ã¼ãçºçãã¦ãã¾ãã
>
> ```
> MetaMask - RPC Error: Internal JSON-RPC error.
> {code: -32603, message: 'Internal JSON-RPC error.', data: {â¦}}
> code: -32603
> ```
>
> ãã®ã¨ã©ã¼ã«é¢ãã¦ã¯ã2022 å¹´ 4 æ 1 æ¥ä»¥åã«ã¯åé¡ãªãåãã¦ããåãã­ã¸ã§ã¯ãã«ãçºçãã¦ããã®ã§ãå¯¾å¿ãæ¨¡ç´¢ãã¦ãã¾ãã
> ããªãã®ãã­ã¸ã§ã¯ãã§ããã®ã¨ã©ã¼ãçºçããå ´åãå¼ãç¶ãæ¬¡ã®ã¹ãããã«é²ãã§ãã ããã

Polygon ãã»ãã®ãµã¤ããã§ã¼ã³ã¨ç°ãªãæå¤§ã®å©ç¹ã¯ãä¸çæå¤§ã® NFT ãã¼ã±ãããã¬ã¤ã¹ã§ãã OpenSea ã«ãµãã¼ãããã¦ãããã¨ã§ãã

[testnets.opensea.io](https://testnets.opensea.io/) ã«ã¢ã¯ã»ã¹ããããªãã®ã³ã³ãã©ã¯ãã¢ãã¬ã¹ãæ¤ç´¢ãã¦ãã ããã

Mint ããã NFT ãã³ã¬ã¬ã¯ã·ã§ã³ã¨ãã¦ã¢ããã­ã¼ãããã¦ããã®ããããã§ãããã

![](/public/images/201-Polygon-Generative-NFT/section-4/4_1_11.png)

### ðââï¸ è³ªåãã

ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã® `#section-4` ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã® 3 ç¹ãè¨è¼ãã¦ãã ãã â¨

```
1. è³ªåãé¢é£ãã¦ããã»ã¯ã·ã§ã³çªå·ã¨ã¬ãã¹ã³çªå·
2. ä½ããããã¨ãã¦ããã
3. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
4. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```

---

ããã§ã¨ããããã¾ã!ãããªãã® NFT ã³ã¬ã¯ã·ã§ã³ã Mint ããã¾ãã!

ããªãã® OpenSea ã®ãªã³ã¯ã `#section-4` ã«æç¨¿ãã¦ãã ãã ð

ããªãã®æåãã³ãã¥ããã£ã§ç¥ãã¾ããã ð

æ¬¡ã®ã¬ãã¹ã³ã§ã¯ãVercel ã§ Web ãµã¤ãããã¹ããã¾ã!
