### ð ã¦ã©ã¬ããã«æ¥ç¶ãããã¿ã³ãã¬ã³ããªã³ã°ãã

Web ã¢ããªã±ã¼ã·ã§ã³ãã Phantom Wallet ã¸ã®æ¥ç¶ãä¿ãããã«ã`connectWallet` ãã¿ã³ãä½æãã¾ãã

Web3 ã®ä¸çã§ã¯ãã¦ã©ã¬ããæ¥ç¶ãã¿ã³ã¯ãã­ã°ã¤ã³ããã¿ã³ã®å½¹å²ãæããã¾ãã

`App.js` ãã¡ã¤ã«ãä»¥ä¸ã®ã¨ããå¤æ´ãã¾ãããã

```jsx
// App.js

import React, { useEffect } from 'react';
import twitterLogo from './assets/twitter-logo.svg';
import './App.css';

// å®æ°ãå®£è¨ãã¾ãã
const TWITTER_HANDLE = 'ããªãã®Twitterãã³ãã«';
const TWITTER_LINK = `https://twitter.com/${TWITTER_HANDLE}`;

const App = () => {

 /*
  * Phantom Walletãæ¥ç¶ããã¦ãããã©ãããç¢ºèªããããã®é¢æ°ã§ãã
  */
  const checkIfWalletIsConnected = async () => {
    try {
      const { solana } = window;

      if (solana) {
        if (solana.isPhantom) {
          console.log('Phantom wallet found!');
          const response = await solana.connect({ onlyIfTrusted: true });
          console.log(
            'Connected with Public Key:',
            response.publicKey.toString()
          );
        }
      } else {
        alert('Solana object not found! Get a Phantom Wallet ð»');
      }
    } catch (error) {
      console.error(error);
    }
  };

  /*
   * ãConnect to Walletããã¿ã³ãæ¼ããã¨ãã«åä½ããé¢æ°ã§ããï¼ç§»è¡ã®Sectionã§å¤æ´ããã®ã§ãç¾ç¶ã¯åé¨å¦çããªãã¾ã¾é²ã¿ã¾ããï¼
   */
  const connectWallet = async () => {};

  /*
   * ã¦ã¼ã¶ã¼ãWebã¢ããªã±ã¼ã·ã§ã³ãã¦ã©ã¬ããã«æ¥ç¶ãã¦ããªãã¨ãã«è¡¨ç¤ºããUIã§ãã
   */
  const renderNotConnectedContainer = () => (
    <button
      className="cta-button connect-wallet-button"
      onClick={connectWallet}
    >
      Connect to Wallet
    </button>
  );

  /*
   * ååã®ã¬ã³ããªã³ã°æã«ã®ã¿ãPhantom Walletãæ¥ç¶ããã¦ãããã©ããç¢ºèªãã¾ãã
   */
  useEffect(() => {
    const onLoad = async () => {
      await checkIfWalletIsConnected();
    };
    window.addEventListener('load', onLoad);
    return () => window.removeEventListener('load', onLoad);
  }, []);

  return (
    <div className="App">
      <div className="container">
        <div className="header-container">
          <p className="header">ð¼ GIF Portal</p>
          <p className="sub-text">
            View your GIF collection â¨
          </p>
          {/* ããã§ã¦ã©ã¬ããã¸ã®æ¥ç¶ãã¿ã³ãã¬ã³ããªã³ã°ãã¾ãã */}
          {renderNotConnectedContainer()}
        </div>
        <div className="footer-container">
          <img alt="Twitter Logo" className="twitter-logo" src={twitterLogo} />
          <a
            className="footer-text"
            href={TWITTER_LINK}
            target="_blank"
            rel="noreferrer"
          >{`built on @${TWITTER_HANDLE}`}</a>
        </div>
      </div>
    </div>
  );
};

export default App;
```

Web ã¢ããªã±ã¼ã·ã§ã³ã«ãConnect to Walletããã¿ã³ãè¡¨ç¤ºããã¦ãããã©ãããã¤ã³ã¿ãã§ã¼ã¹ãç¢ºèªãã¦ã¿ã¾ãããã

**ã¦ã¼ã¶ã¼ãã¦ã©ã¬ããã Web ã¢ããªã±ã¼ã·ã§ã³ã«æ¥ç¶ãã¦ããªãå ´åã®ã¿ã`Connect to Wallet` ãã¿ã³ãè¡¨ç¤ºããã¾ãã**

![interface](/public/images/301-Solana-dApp/section-1/1_2_1.jpg)

æ¬¡ã«ãReact ã® `useState` ãç¨ãã¦ã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¢ãã¬ã¹ã® `state` ãç®¡çãã`Connect to Wallet` ãã¿ã³ãè¡¨ç¤ºãããã©ãããå¤æ­ããããã®ãã©ã°ã¨ãã¦å©ç¨ãã¦ããã¾ãããã

ã¾ãã¯ã`App.js` ã® 1 è¡ç®ã§ `useState` ãã¤ã³ãã¼ããã¾ãã

```jsx
// App.js

import React, { useEffect, useState } from "react";
```

æ¬¡ã«ã`checkIfWalletIsConnected` é¢æ°ã®ããä¸ã« `state` ã®å®£è¨ãè¿½å ãã¾ãã

```jsx
// App.js

const [walletAddress, setWalletAddress] = useState(null);
```

ããã§ãã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¢ãã¬ã¹ã® `state` ãç®¡çããããã®æºåãæ´ãã¾ããã

ç¶ãã¦ã`App.js` ãä»¥ä¸ã®ã¨ããä¿®æ­£ãã¦ããã¾ãããã

```jsx
//App.js

import React, { useEffect, useState } from 'react';
import twitterLogo from './assets/twitter-logo.svg';
import './App.css';

// å®æ°ãå®£è¨ãã¾ãã
const TWITTER_HANDLE = 'ããªãã®Twitterãã³ãã«';
const TWITTER_LINK = `https://twitter.com/${TWITTER_HANDLE}`;

const App = () => {
  // ã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¢ãã¬ã¹ã®stateãç®¡çããããuseStateãä½¿ç¨ããã
  const [walletAddress, setWalletAddress] = useState(null);

 /*
  * Phantom Walletãæ¥ç¶ããã¦ãããã©ãããç¢ºèªããããã®é¢æ°ã§ãã
  */
  const checkIfWalletIsConnected = async () => {
    try {
      const { solana } = window;

      if (solana) {
        if (solana.isPhantom) {
          console.log('Phantom wallet found!');
          const response = await solana.connect({ onlyIfTrusted: true });
          console.log(
            'Connected with Public Key:',
            response.publicKey.toString()
          );

          /*
           * walletAddressã«ã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¢ãã¬ã¹ã®stateãæ´æ°ãã¾ãã
           */
          setWalletAddress(response.publicKey.toString());
        }
      } else {
        alert('Solana object not found! Get a Phantom Wallet ð»');
      }
    } catch (error) {
      console.error(error);
    }
  };

  const connectWallet = async () => {};

  const renderNotConnectedContainer = () => (
    <button
      className="cta-button connect-wallet-button"
      onClick={connectWallet}
    >
      Connect to Wallet
    </button>
  );

  /*
   * ååã®ã¬ã³ããªã³ã°æã«ã®ã¿ãPhantom Walletãæ¥ç¶ããã¦ãããã©ããç¢ºèªãã¾ãã
   */
  useEffect(() => {
    const onLoad = async () => {
      await checkIfWalletIsConnected();
    };
    window.addEventListener('load', onLoad);
    return () => window.removeEventListener('load', onLoad);
  }, []);

  return (
    <div className="App">
			<div className={walletAddress ? 'authed-container' : 'container'}>
        <div className="header-container">
          <p className="header">ð¼ GIF Portal</p>
          <p className="sub-text">
            View your GIF collection â¨
          </p>
          {/* ã¦ã©ã¬ããã¢ãã¬ã¹ãæã£ã¦ããªãå ´åã«ã®ã¿è¡¨ç¤ºããæ¡ä»¶ãããã«è¿½å ãã¾ãã */}
          {!walletAddress && renderNotConnectedContainer()}
        </div>
        <div className="footer-container">
          <img alt="Twitter Logo" className="twitter-logo" src={twitterLogo} />
          <a
            className="footer-text"
            href={TWITTER_LINK}
            target="_blank"
            rel="noreferrer"
          >{`built on @${TWITTER_HANDLE}`}</a>
        </div>
      </div>
    </div>
  );
};

export default App;
```

ç°¡åã«ä¿®æ­£ç¹ãç¢ºèªãã¾ãããã

```javascript
// App.js

const checkIfWalletIsConnected = async () => {
  try {
    const { solana } = window;

    if (solana) {
      if (solana.isPhantom) {
        console.log('Phantom wallet found!');
        const response = await solana.connect({ onlyIfTrusted: true });
        console.log(
          'Connected with Public Key:',
          response.publicKey.toString()
        );

        setWalletAddress(response.publicKey.toString());
      }
    } else {
      alert('Solana object not found! Get a Phantom Wallet ð»');
    }
  } catch (error) {
    console.error(error);
  }
};
```

Phantom Wallet ã Web ã¢ããªã±ã¼ã·ã§ã³ã«æ¥ç¶ããã¦ããå ´åãã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¢ãã¬ã¹ã® `state` ãæ´æ°ããã¾ãã

æ´æ°ããã `state` ã¯ä»¥ä¸ã§å©ç¨ãã¾ãã

```jsx
// App.js

{!walletAddress && renderNotConnectedContainer()}
```

ããã§ã¯ `state` ã« `walletAddress` ãè¨­å®ããã¦ããªãå ´åã®ã¿ã`renderNotConnectedContainer` é¢æ°ãå¼ã³åºãããã«è¨è¿°ãã¦ãã¾ãã

ãããã£ã¦ãã¦ã©ã¬ããã¢ãã¬ã¹ããªãï¼ã¦ã¼ã¶ã¼ãã¦ã©ã¬ãããæ¥ç¶ãã¦ããªãï¼å ´åã¯ãã¦ã©ã¬ãããæ¥ç¶ããããã®ãã¿ã³ãè¡¨ç¤ºãã¾ããï¼æ¡ä»¶ä»ãã¬ã³ããªã³ã°ã¨å¼ã°ããææ³ã§ããï¼


### ð¥ ã¦ã©ã¬ããæ¥ç¶ãã

ä»ã®ã¾ã¾ã ã¨ `Connect to Wallet` ãã¿ã³ãã¯ãªãã¯ãã¦ãä½ãèµ·ããã¾ããã

ãã®ããããããã `Connect to Wallet` ãã¿ã³ãæ¼ä¸ããéã«æ©è½ãã `connectWallet` é¢æ°ã®ã­ã¸ãã¯ãã³ã¼ãã£ã³ã°ãã¦ããã¾ãã

`App.js` ã® `connectWallet` é¢æ°ãä¸è¨ã®ã¨ããä¿®æ­£ãã¾ãããã

```javascript
// App.js

const connectWallet = async () => {
  const { solana } = window;

  if (solana) {
    const response = await solana.connect();
    console.log("Connected with Public Key:", response.publicKey.toString());
    setWalletAddress(response.publicKey.toString());
  }
};
```

ã¦ã¼ã¶ã¼ã Web ã¢ããªã±ã¼ã·ã§ã³ã« Phantom Wallet ãæ¥ç¶ãããå ´åã`solana` ãªãã¸ã§ã¯ãã® `connect` ã¡ã½ãããå¼ã³åºãã¦ãPhantom Wallet å´ã§ Web ã¢ããªã±ã¼ã·ã§ã³ã®æ¥ç¶ãæ¿èªãã¾ãã

ããããã¨ãWeb ã¢ããªã±ã¼ã·ã§ã³ãã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããæå ±ï¼ã¦ã©ã¬ããã¢ãã¬ã¹ãªã©ï¼ã«ã¢ã¯ã»ã¹ã§ããããã«ãªãã¾ãã

ããã¾ã§ã§ããããã©ã¦ã¶ã§åä½ãç¢ºèªãã¦ã¿ã¾ãããã

ã¾ããWeb ã¢ããªã±ã¼ã·ã§ã³ã¨ã¦ã©ã¬ãããæ¥ç¶ãã¾ãã

`Connect to Wallet` ãã¿ã³ãæ¼ãã¨ Phantom Wallet ããããã¢ãããè¡¨ç¤ºãã¦ãããã®ã§ãæç¤ºã«å¾ã£ã¦æ¥ç¶ãã¾ãããã

æ¥ç¶å¾ã`Connect to Wallet` ãã¿ã³ãè¡¨ç¤ºããã¦ããªããã¨ãç¢ºèªãã¾ãã

`Connect to Wallet` ãã¿ã³ãè¡¨ç¤ºããã¦ããªããã¨ãç¢ºèªã§ããã Web ã¢ããªã±ã¼ã·ã§ã³ãæ´æ°ãã¦ã¿ã¦ãã ããã

æ´æ°ããã¨ `checkIfWalletIsConnected` é¢æ°ãå¼ã³åºãããããã`Connect to Wallet` ãã¿ã³ãããã«æ¶ããã¯ãã§ããï¼ã³ã³ã½ã¼ã«ã«ã¯æ¥ç¶æ¸ã¿ã®ã¦ã©ã¬ããã¢ãã¬ã¹ãåºåããã¦ãã¾ããï¼

ããã§åºæ¬çãª UI ã¨ã¦ã¼ã¶ã¼èªè¨¼ãå®è£ã§ãã¾ããã

> â ï¸ æ³¨æ
>
> Fantom Wallet ã®è¨­å®ç»é¢ï¼æ­¯è»ãã¯ãªãã¯ï¼ã«ã[ä¿¡é ¼æ¸ã¿ã¢ããª]ãããã¾ãã
>
> ãããéãã¨ãã¦ã©ã¬ããã¨æ¢ã«æ¥ç¶ããã¦ãã WEB ã¢ããªãä¸è¦§ã§è¡¨ç¤ºããã[åãæ¶ã]ãã¿ã³ãæ¼ä¸ãããã¨ã§ç°¡åã«é£æºã®è§£é¤ããããã¨ãã§ãã¾ãã
>
> ã­ã¼ã«ã«ã§å®è¡ãã¦ããå ´åã¯ `localhostï¼3000` ã®ãã®ãç¾å¨ä½æãã¦ãã Web ã¢ããªã±ã¼ã·ã§ã³ã§ãã
>
> é£æºãè§£é¤ããããã§ Web ã¢ããªã±ã¼ã·ã§ã³ãæ´æ°ããã¨ã`Connect to Wallet` ãã¿ã³ãè¡¨ç¤ºãããã®ã§ãã²ä¸åº¦è©¦ãã¦ã¿ã¦ãã ããã


### ðââï¸ è³ªåãã

ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã® `#section-1` ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã® 4 ç¹ãè¨è¼ãã¦ãã ãã â¨

```
1. è³ªåãé¢é£ãã¦ããã»ã¯ã·ã§ã³çªå·ã¨ã¬ãã¹ã³çªå·
2. ä½ããããã¨ãã¦ããã
3. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
4. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```

---

æ¬¡ã®ã¬ãã¹ã³ã§ã¯ãWeb ã¢ããªã±ã¼ã·ã§ã³ã« GIF ç»åãè¡¨ç¤ºãã¾ã!
