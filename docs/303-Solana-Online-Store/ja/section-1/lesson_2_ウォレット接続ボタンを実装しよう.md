### ð¤ ã¦ã©ã¬ãããã­ãã¤ãã¼ãè¨­å®ãã

ä»åæ¥ç¶ããã¦ã©ã¬ããã¯ [Phantom Wallet](https://phantom.app/) ã§ãããSolana ã¦ã©ã¬ãããªãã©ãã§ãä½¿ç¨ã§ããã¯ãã§ããï¼ãã ããä»ã®ã¦ã©ã¬ããã§ã¯ãã¹ããã¦ãã¾ãããï¼

ãã® Web ã¢ããªã±ã¼ã·ã§ã³ãä½æããã«ããããä¸çªå§ãã«ããã¹ããã¨ã¯ã¦ã©ã¬ãããæ¥ç¶ãããã¨ã§ãã

ããã§ã`pages` ãã£ã¬ã¯ããªç´ä¸ã«ãã `_app.js` ãã¡ã¤ã«ãä»¥ä¸ã®ã¨ããæ´æ°ãã¾ãã

```jsx
// _app.js

import React, { useMemo } from "react";
import { WalletAdapterNetwork } from "@solana/wallet-adapter-base";
import { WalletModalProvider } from "@solana/wallet-adapter-react-ui";
import { ConnectionProvider, WalletProvider } from "@solana/wallet-adapter-react";
import {
  GlowWalletAdapter,
  PhantomWalletAdapter,
  SlopeWalletAdapter,
  SolflareWalletAdapter,
  TorusWalletAdapter,
} from "@solana/wallet-adapter-wallets";
import { clusterApiUrl } from "@solana/web3.js";

import "@solana/wallet-adapter-react-ui/styles.css";
import "../styles/globals.css";
import "../styles/App.css";

const App = ({ Component, pageProps }) => {
  // networkã¯devnetãtestnetãã¾ãã¯mainnet-betaã«è¨­å®ã§ãã¾ãã
  const network = WalletAdapterNetwork.Devnet;

  // networkãè¨­å®ãã¦ã¡ã¢åãã¾ãã
  const endpoint = useMemo(() => clusterApiUrl(network), [network]);

  // ããã§è¨­å®ããã¦ã©ã¬ãããWebã¢ããªã±ã¼ã·ã§ã³ã«çµã¿è¾¼ã¾ãã¾ãã
  const wallets = useMemo(
    () => [
      new PhantomWalletAdapter(),
      new GlowWalletAdapter(),
      new SlopeWalletAdapter(),
      new SolflareWalletAdapter({ network }),
      new TorusWalletAdapter(),
    ],
    [network]
  );

  return (
    <ConnectionProvider endpoint={endpoint}>
      <WalletProvider wallets={wallets} autoConnect>
        <WalletModalProvider>
          <Component {...pageProps} />
        </WalletModalProvider>
      </WalletProvider>
    </ConnectionProvider>
  );
};

export default App;
```

ã¾ãã¯ `import` ãã¦ããã©ã¤ãã©ãªãã¢ã¸ã¥ã¼ã«ç­ã«ã¤ãã¦è§¦ãã¦ããã¾ãã

æåã«ã¤ã³ãã¼ããã¦ããã®ã¯ React ã® `useMemo()` [ï¼åèï¼](https://reactjs.org/docs/hooks-reference.html#usememo) ã§ãä¾å­åãå¤æ´ãããå ´åã«ã®ã¿ãã¼ã¿ãã­ã¼ããã React hook ã§ãã

`_app.js` ã§ã¯ãã¦ã¼ã¶ã¼ãæ¥ç¶ãã¦ãã **ãããã¯ã¼ã¯** ãå¤æ´ãããªããã°ã`clusterApiUrl` ã®å¤ã¯å¤æ´ããã¾ããã

æ¬¡ã¯[@solana/wallet-adapter](https://solana-labs.github.io/wallet-adapter/) ã® `wallet-adapter-network` ã§ãã

ããã¯ãå©ç¨å¯è½ãªãããã¯ã¼ã¯ï¼mainnet-beta ãtestnetãdevnetï¼ãç¥è¨ãã[ãªãã¸ã§ã¯ããè¨è¿°ããéå](https://github.com/solana-labs/wallet-adapter/blob/469edb5dd45231d397751b0268c86dffd6ed730a/packages/core/base/src/types.ts)ã§ããï¼è©³ç´°ã¯ãªã³ã¯åãåç§ï¼

æ¬¡ã® `WalletModalProvider` ã¯ã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããé¸æãæãããç´ æ´ããã React ã³ã³ãã¼ãã³ãã§ãã

ãã®æ¬¡ã® `ConnectionProvider` ã¯ RPC ã¨ã³ããã¤ã³ããåãåããSolana ãã­ãã¯ãã§ã¼ã³ä¸ã®ãã¼ãã¨ç´æ¥ããåãã§ããããã«ãã¦ããã¾ãã

ã¤ã¾ããWeb ã¢ããªã±ã¼ã·ã§ã³ã `ConnectionProvider` ãä½¿ç¨ãã¦ Solana ãã­ãã¯ãã§ã¼ã³ã«ãã©ã³ã¶ã¯ã·ã§ã³ãéä¿¡ãã¦ããã¾ãã

æ¬¡ã® `WalletProvider` ã¯ããããã¦ã©ã¬ããã«æ¥ç¶ããéã®æ¨æºã¤ã³ã¿ãã§ã¼ã¹ãæä¾ãããã®ã§ãã

`WalletProvider` ã«ãããããããã®ã¦ã©ã¬ããã®ãã­ã¥ã¡ã³ããèª­ãå¿è¦ããªããªãã¾ãã

ãã®æ¬¡ã® `wallet-adapter-wallets` ããã¯æ§ããªã¦ã©ã¬ããã¢ããã¿ãæä¾ãããã®ã§ãå¿è¦ãªã¢ããã¿ãã¤ã³ãã¼ããã¦ã`WalletProvider` ã«ã¦ã©ã¬ããã®ãªã¹ããæ¸¡ãã¾ãã

â»ã¦ã©ã¬ããã¢ããã¿ãå¿è¦ãªçç±ã«ã¤ãã¦ã¯[ãã¡ã](https://solana.com/ja/news/solana-why-you-should-use-wallet-adapter)ãåç§ãã ããã

æå¾ã® `clusterApiURL` ã¯æå®ãããããã¯ã¼ã¯ã«åºã¥ãã¦ RPC ã¨ã³ããã¤ã³ããçæããé¢æ°ã§ãã

React App ã³ã³ãã¼ãã³ãåã® return ã¹ãã¼ãã¡ã³ãã§ã¯ãå­ï¼ã¢ããªã®æ®ãã®é¨åï¼ãããã¤ãã®[context](https://reactjs.org/docs/context.html#contextprovider)ãã­ãã¤ãã¼ã§ã©ãããã¦ãã¾ãã

ããã§ãã¦ã©ã¬ãããæ¥ç¶ããããã®æºåãæ´ãã¾ããã


### ð§ââï¸ ãã­ãã¤ãã¼ãä½¿ç¨ãã¦ã¦ã©ã¬ããã«æ¥ç¶ãã

ããã§ã¯ãã¦ã©ã¬ãããæ¥ç¶ãã¦ããã¾ãããã

`index.js` ãä»¥ä¸ã®ã¨ããæ´æ°ãã¾ãã

```jsx
// index.js

import React from 'react';
import { PublicKey } from '@solana/web3.js';
import { useWallet } from '@solana/wallet-adapter-react';
import { WalletMultiButton } from '@solana/wallet-adapter-react-ui';

// å®æ°ãå®£è¨ãã¾ãã
const TWITTER_HANDLE = "ããªãã®Twitterãã³ãã«";
const TWITTER_LINK = `https://twitter.com/${TWITTER_HANDLE}`;

const App = () => {
  // ãµãã¼ããã¦ããã¦ã©ã¬ããããã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¢ãã¬ã¹ãåå¾ãã¾ãã
  const { publicKey } = useWallet();

  const renderNotConnectedContainer = () => (
    <div>
      <img src="https://media.giphy.com/media/FWAcpJsFT9mvrv0e7a/giphy.gif" alt="anya" />
      <div className="button-container">
        <WalletMultiButton className="cta-button connect-wallet-button" />
      </div>
    </div>
  );

  return (
    <div className="App">
      <div className="container">
        <header className="header-container">
          <p className="header"> ð³ UNCHAIN Image Store ð</p>
          <p className="sub-text">The only Image store that accepts shitcoins</p>
        </header>

        <main>
          {/* ã¦ã©ã¬ããã¢ãã¬ã¹ãå­å¨ããªãå ´åã¯Connectãã¿ã³ãè¡¨ç¤ºãã¾ãã */}
          {publicKey ? 'Connected!' : renderNotConnectedContainer()}
        </main>

        <div className="footer-container">
          <img alt="Twitter Logo" className="twitter-logo" src="twitter-logo.svg" />
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

`useWallet()` ããã¯ãä½¿ç¨ãããã¨ã§ãWeb ã¢ããªã±ã¼ã·ã§ã³ã®ã©ãããã§ãæ¥ç¶ãããã¦ã¼ã¶ã¼ã®ã¢ãã¬ã¹ãåå¾ã§ãã¾ãã

ããã§ãã¦ã©ã¬ãããæ¥ç¶ãããã¨ãã§ããããã«ãªãã¾ããã

â» Twitter ãã³ãã«ãå¿ããã«æ´æ°ãã¦ãã ããã­!

```jsx
const TWITTER_HANDLE = "ããªãã®Twitterãã³ãã«";
```

ãã¦ãããã§ç»åã®ä¸ã« `Select Wallet` ãã¿ã³ãè¡¨ç¤ºãããããã«ãªã£ãã¯ãã§ãã


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

æ¬¡ã®ã¬ãã¹ã³ã§ã¯ãååãç¨æãã¦ãã¦ã³ã­ã¼ãæ©è½ãå®è£ãã¦ããã¾ã!
