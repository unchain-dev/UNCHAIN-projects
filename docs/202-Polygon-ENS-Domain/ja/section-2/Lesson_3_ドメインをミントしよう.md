### ð ã¦ã¼ã¶ã¼ãããã¼ã¿ãåå¾ãã

ååã¾ã§ã§ã¦ã§ããµã¤ãã®ãã­ã³ãã¨ã³ããä½æããªãããã¦ã©ã¬ããæ¥ç¶ãªã©ã®æ©è½ãå°ããã¤å®è£ãã¦ãã¾ããã ã¹ãã¼ãã³ã³ãã©ã¯ããããã­ã¤ããã¦ã©ã¬ãããæ¥ç¶ãã¾ããã æ¬¡ã«ãMetaMask ããã¢ã¯ã»ã¹ã§ããæå ±ãä½¿ç¨ãã¦ãã¦ã§ãã¢ããªããå®éã«ã¹ãã¼ãã³ã³ãã©ã¯ããå¼ã³åºãå¿è¦ãããã¾ãã

ã¾ããã¦ã¼ã¶ã¼ã®ãã¡ã¤ã³åã¨ä¿å­ãããã¼ã¿ãåå¾ããå¿è¦ãããã®ã§ããããå®è¡ãã¾ãããã

```javascript
// App.js
import React, { useEffect, useState } from "react";
import "./styles/App.css";
import twitterLogo from "./assets/twitter-logo.svg";
import { ethers } from "ethers";

// ã³ã³ãã©ã¯ã
const TWITTER_HANDLE = "_UNCHAIN";
const TWITTER_LINK = `https://twitter.com/${TWITTER_HANDLE}`;
// ç»é²ããããã¡ã¤ã³ã§ããå¥½ã¿ã§å¤ãã¦ã¿ã¾ãããã
const tld = ".ninja";
const CONTRACT_ADDRESS = "YOUR_CONTRACT_ADDRESS_HERE";

const App = () => {
  const [currentAccount, setCurrentAccount] = useState("");
  // stateç®¡çãããã­ããã£ãè¿½å ãã¦ãã¾ãã
  const [domain, setDomain] = useState("");
  const [record, setRecord] = useState("");

  const connectWallet = async () => {
    try {
      const { ethereum } = window;

      if (!ethereum) {
        alert("Get MetaMask -> https://metamask.io/");
        return;
      }

      const accounts = await ethereum.request({
        method: "eth_requestAccounts",
      });

      console.log("Connected", accounts[0]);
      setCurrentAccount(accounts[0]);
    } catch (error) {
      console.log(error);
    }
  };

  const checkIfWalletIsConnected = async () => {
    const { ethereum } = window;

    if (!ethereum) {
      console.log("Make sure you have metamask!");
      return;
    } else {
      console.log("We have the ethereum object", ethereum);
    }

    const accounts = await ethereum.request({ method: "eth_accounts" });

    if (accounts.length !== 0) {
      const account = accounts[0];
      console.log("Found an authorized account:", account);
      setCurrentAccount(account);
    } else {
      console.log("No authorized account found");
    }
  };

  // ã¬ã³ããªã³ã°é¢æ°ã§ãã
  const renderNotConnectedContainer = () => (
    <div className="connect-wallet-container">
      <img
        src="https://media.giphy.com/media/3ohhwytHcusSCXXOUg/giphy.gif"
        alt="Ninja donut gif"
      />
      {/* ãã¿ã³ã¯ãªãã¯ã§connectWalleté¢æ°ãå¼ã³åºãã¾ãã */}
      <button
        onClick={connectWallet}
        className="cta-button connect-wallet-button"
      >
        Connect Wallet
      </button>
    </div>
  );

  // ãã¡ã¤ã³ãã¼ã ã¨ãã¼ã¿ã®å¥åãã©ã¼ã ã§ãã
  const renderInputForm = () => {
    return (
      <div className="form-container">
        <div className="first-row">
          <input
            type="text"
            value={domain}
            placeholder="domain"
            onChange={(e) => setDomain(e.target.value)}
          />
          <p className="tld"> {tld} </p>
        </div>

        <input
          type="text"
          value={record}
          placeholder="whats ur ninja power"
          onChange={(e) => setRecord(e.target.value)}
        />

        <div className="button-container">
          <button
            className="cta-button mint-button"
            disabled={null}
            onClick={null}
          >
            Mint
          </button>
          <button
            className="cta-button mint-button"
            disabled={null}
            onClick={null}
          >
            Set data
          </button>
        </div>
      </div>
    );
  };

  useEffect(() => {
    checkIfWalletIsConnected();
  }, []);

  return (
    <div className="App">
      <div className="container">
        <div className="header-container">
          <header>
            <div className="left">
              <p className="title">ð±âð¤ Ninja Name Service</p>
              <p className="subtitle">Your immortal API on the blockchain!</p>
            </div>
          </header>
        </div>

        {!currentAccount && renderNotConnectedContainer()}
        {/* ã¢ã«ã¦ã³ããæ¥ç¶ãããã¨ã¤ã³ããããã©ã¼ã ãã¬ã³ããªã³ã°ãã¾ãã */}
        {currentAccount && renderInputForm()}

        <div className="footer-container">
          <img alt="Twitter Logo" className="twitter-logo" src={twitterLogo} />
          <a
            className="footer-text"
            href={TWITTER_LINK}
            target="_blank"
            rel="noreferrer"
          >{`built with @${TWITTER_HANDLE}`}</a>
        </div>
      </div>
    </div>
  );
};

export default App;
```

ä»¥åå®ç¾©ãã`currentAccount`å¤æ°ã®ä¸ã« 2 ã¤ã®ç¶æå¤æ°ãè¿½å ããããã«å¥åãã©ã¼ã ãè¿ã`renderInputForm`é¢æ°ãè¿½å ãã¾ããã

ãããã®æ°ããè¿½å ã«ã¤ãã¦ãããç¦ç¹ãçµã£ã¦è¦ã¦ã¿ã¾ãããã

```javascript
// App.js
// ãããã¬ãã«ãã¡ã¤ã³(tld)ãå®ç¾©ãã¾ãã
const tld = '.ninja';

const App = () => {
// domain ã¨ record ã®stateç®¡çããã¾ãã
const [domain, setDomain] = useState('');
const [record, setRecord] = useState('');

return (
	<div className="App">
			...
			{/* ããã«ãããã¼æå ±ãæ¥ã¾ãã */}

			{/* currentAccount ãç¡ããã° Connect Walletãã¿ã³ãè¡¨ç¤ºãã¾ãã */}
			{!currentAccount && renderNotConnectedContainer()}

			{/* ã¢ã«ã¦ã³ããæ¥ç¶ããã¦ããã° å¥åãã©ã¼ã  ãã¬ã³ããªã³ã°ãã¾ãã */}
			{currentAccount && renderInputForm()}

			{/* ããã¿ã¼æå ±ãããã«æ¥ã¾ãã */}
			...
	</div>
);
```

`&&`æ§æã¯å°ãéåæãæããããããã¾ãããã`&&`ã®åã®æ¡ä»¶ã`true`ã®å ´åãã¬ã³ããªã³ã°é¢æ°ãè¿ãã¾ãã ãããã£ã¦ã `currentAccount`ãç©ºã®å ´åï¼ã¤ã¾ããtrue ã§ãªãå ´åï¼ãã¦ã©ã¬ããã®æ¥ç¶ãã¿ã³ãè¡¨ç¤ºããã¾ãã

`renderInputForm`ã®åå®¹ã¯ãReact ã§ç¶æå¤æ°ã«é¢é£ä»ããããå¥åãã©ã¼ã ãä½¿ç¨ããéã«ã¯æ¨æºçãªå½¢å¼ã§ãã ãããã«ã¤ãã¦ã®è©³ç´°ã¯[ãã](https://reactjs.org/docs/hooks-state.html)ã§èª­ããã¨ãã§ãã¾ãã

ã¢ããªãè¦ãã¨ãæ¬¡ã®å¥åãã©ã¼ã ãè¡¨ç¤ºããã¾ãã

![](/public/images/202-Polygon-ENS-Domain/section-2/2_3_1.png)

**æ³¨ï¼** ç¾å¨ãMint ãã¿ã³ã¯ä½ãæ©è½ãã¾ãããããã¯äºæ³ã§ãã¾ãã­ã

ããã§ãã¦ã¼ã¶ã¼ã®å¥åããæå ±ãåå¾ãã¦ãã¹ãã¼ãã³ã³ãã©ã¯ããå¼ã³åºããã¨ãã§ãã¾ãã æ¬¡ã®ã»ã¯ã·ã§ã³ã§ã¯ãã¹ãã¼ãã³ã³ãã©ã¯ãã§ä»¥åã«ä½æããé¢æ°ãå¼ã³åºãã¾ãã

### ð§ ã¹ãã¼ãã³ã³ãã©ã¯ãã¨ã®ããåã

å¥åæå ±ãåå¾ãã¦ã¹ãã¼ãã³ã³ãã©ã¯ãã«éä¿¡ããå®éã«ãã¡ã¤ã³ãä½æããæºåãæ´ãã¾ããã ãã£ã¦ã¿ã¾ããã ð¤

ä»¥åã«ãã¡ã¤ã³ã NFT ã¨ãã¦ä½æããã³ã³ãã©ã¯ãã«ä½æãã`register`é¢æ°ãè¦ãã¦ãã¾ããï¼ æ¬¡ã¯ Web ã¢ããªãããã®é¢æ°ãå¼ã³åºãå¿è¦ãããã¾ãã åã«é²ã¿ã`checkIfWalletIsConnected`é¢æ°ã®ä¸ã«æ¬¡ã®é¢æ°ãè¿½å ãã¾ãã

```javascript
// App.js
const mintDomain = async () => {
  // ãã¡ã¤ã³ãnullã®ã¨ãrunãã¾ããã
  if (!domain) {
    return;
  }
  // ãã¡ã¤ã³ã3æå­ã«æºããªããç­ãããå ´åã«ã¢ã©ã¼ããåºãã¾ãã
  if (domain.length < 3) {
    alert("Domain must be at least 3 characters long");
    return;
  }
  // ãã¡ã¤ã³ã®æå­æ°ã«å¿ãã¦ä¾¡æ ¼ãè¨ç®ãã¾ãã
  // 3 chars = 0.05 MATIC, 4 chars = 0.03 MATIC, 5 or more = 0.01 MATIC
  const price =
    domain.length === 3 ? "0.05" : domain.length === 4 ? "0.03" : "0.01";
  console.log("Minting domain", domain, "with price", price);
  try {
    const { ethereum } = window;
    if (ethereum) {
      const provider = new ethers.providers.Web3Provider(ethereum);
      const signer = provider.getSigner();
      const contract = new ethers.Contract(
        CONTRACT_ADDRESS,
        contractAbi.abi,
        signer
      );

      console.log("Going to pop wallet now to pay gas...");
      let tx = await contract.register(domain, {
        value: ethers.utils.parseEther(price),
      });
      // ãã³ããããã¾ã§ãã©ã³ã¶ã¯ã·ã§ã³ãå¾ã¡ã¾ãã
      const receipt = await tx.wait();

      // ãã©ã³ã¶ã¯ã·ã§ã³ãåé¡ãªãå®è¡ããããç¢ºèªãã¾ãã
      if (receipt.status === 1) {
        console.log(
          "Domain minted! https://mumbai.polygonscan.com/tx/" + tx.hash
        );

        // domain,recordãã»ãããã¾ãã
        tx = await contract.setRecord(domain, record);
        await tx.wait();

        console.log("Record set! https://mumbai.polygonscan.com/tx/" + tx.hash);

        setRecord("");
        setDomain("");
      } else {
        alert("Transaction failed! Please try again");
      }
    }
  } catch (error) {
    console.log(error);
  }
};
```

ããã«ãããããã¤ãã®ã¨ã©ã¼ãåºã¾ããå¿éããªãã§ãã ãããããããä¿®æ­£ãã¾ãã ã³ã¼ããå°ãè¦ã¦ã¿ã¾ãããã

```javascript
// App.js
const provider = new ethers.providers.Web3Provider(ethereum);
const signer = provider.getSigner();
```

`ethers`ã¯ããã­ã³ãã¨ã³ããã³ã³ãã©ã¯ãã¨ããã¨ããããã¨ãã«å½¹ç«ã¤ã©ã¤ãã©ãªã§ãã

å¿ã`ethers`ãã`import { ethers }`ãä½¿ç¨ãã¦ã³ã¼ãä¸é¨ã«ã¤ã³ãã¼ããã¦ãã ããã

`provider`ã¯ãå®éã« Polygon ãã¼ãã¨éä¿¡ããããã«ä½¿ç¨ãã¾ãã Alchemy ãä½¿ç¨ãã¦ããã­ã¤ããæ¹æ³ãè¦ãã¦ãã¾ããï¼ ãã®å ´åãMetaMask ãããã¯ã°ã©ã¦ã³ãã§æä¾ãããã¼ããä½¿ç¨ãã¦ãããã­ã¤ãããã³ã³ãã©ã¯ããããã¼ã¿ãéåä¿¡ãã¾ãã

[ãã¡ã](https://docs.ethers.io/v5/api/signer/#signers)ã¯ if æåã®`signer`ãèª¬æãããªã³ã¯ã§ãããåèãã ããã

```javascript
// App.js
const contract = new ethers.Contract(CONTRACT_ADDRESS, contractAbi.abi, signer);
```

ããã«ã¤ãã¦ã¯å¾ã§èª¬æãã¾ãã ãã®è¡ãå®éã«**ã³ã³ãã©ã¯ãã¸ã®æ¥ç¶ããã**ãã®ã§ãããã¨ãç¥ã£ã¦ããã¦ãã ããã å¿è¦ãªãã®ï¼ã³ã³ãã©ã¯ãã®ã¢ãã¬ã¹ã`abi`ãã¡ã¤ã«ã¨å¼ã°ãããã®ãããã³`signer`ã ãããã¯ããã­ãã¯ãã§ã¼ã³ä¸ã®ã³ã³ãã©ã¯ãã¨éä¿¡ããããã«å¿è¦ãª 3 ã¤ã®é ç®ã§ãã

ãã¡ã¤ã«ã®åé ­ã«ãã`const CONTRACT_ADDRESS`ã«æ³¨ç®ãã¦ãã ããã

**ãã®å¤æ°ã¯ãããã­ã¤ãããææ°ã®ã³ã³ãã©ã¯ãã®ã¢ãã¬ã¹ã«å¿ãå¤æ´ãã¦ãã ãã**ã

å¿ãããç´å¤±ããããã¦ãå¿éã¯ããã¾ãããã³ã³ãã©ã¯ããåããã­ã¤ãã¦æ°ããã³ã³ãã©ã¯ãã¢ãã¬ã¹ãåå¾ãã¦ãã ããã

```javascript
// App.js
console.log("Going to pop wallet now to pay gas...");
let tx = await contract.register(domain, {
  value: ethers.utils.parseEther(price),
});
// ãã©ã³ã¶ã¯ã·ã§ã³ãå¾ã¡ã¾ãã
const receipt = await tx.wait();

// ãã©ã³ã¶ã¯ã·ã§ã³ãå®äºãããç¢ºèªãã¾ãã
if (receipt.status === 1) {
  console.log("Domain minted! https://mumbai.polygonscan.com/tx/" + tx.hash);

  // domain,recordãã»ãããã¾ãã
  tx = await contract.setRecord(domain, record);
  await tx.wait();

  console.log("Record set! https://mumbai.polygonscan.com/tx/" + tx.hash);

  setRecord("");
  setDomain("");
} else {
  alert("Transaction failed! Please try again");
}
```

ãã®é¨åã¯ä»¥åã«ããã­ã¤ããã³ã¼ãã¨æ¥ç¶ãã¦ããããã«è¦ãã¾ãã­ã

ããã§ã¯ãå®éã« 2 ã¤ã®ã³ã³ãã©ã¯ãé¢æ°ãå¼ã³åºãã¾ãã

æåã«`register`é¢æ°ãä½¿ç¨ãããã¤ãã³ã°ãããã®ãå¾ã£ã¦ãããPolygonscan ã® URL ã«ãªã³ã¯ãã¾ãã

2 ã¤ç®ã¯`setRecord`ã§ããããã¯ãä½æãããã¡ã¤ã³ã®ã¬ã³ã¼ããè¨­å®ãã¾ãã ãã¡ã¤ã³ã¯ãã¬ã³ã¼ããè¨­å®ããåã«ã³ã³ãã©ã¯ãã«å­å¨ããå¿è¦ããããããæåã®ãã©ã³ã¶ã¯ã·ã§ã³ãæ­£å¸¸ã«ãã¤ãã³ã°ãããã®ãå¾ã¤å¿è¦ãããã¾ãã `tx.waitï¼ï¼`ã§ã¯ãç¢ºèªå¯è½ãªæå ±ããè¿ãã¦ããã¾ãã

æå¾ã«ãèª°ãã`Mint NFT`ãã¿ã³ãã¯ãªãã¯ããã¨ãã«ã`mintDomain`é¢æ°ãå¼ã³åºãã¾ãã `renderInputForm`é¢æ°ã®ãã³ããã¿ã³ã«`onClick`ãè¿½å ãã¦ããã®é¢æ°ãå¼ã³åºãã¾ãã

ãªãã`set data` ãã¿ã³ã®é¨åã¯ä»ã¯å¿è¦ãªãã®ã§åé¤ãã¦ããã¾ãã

ä»ã¯åãã¾ã¾ã§ãã

```javascript
// App.js
const renderInputForm = () => {
  return (
    <div className="form-container">
      <div className="first-row">
        <input
          type="text"
          value={domain}
          placeholder="domain"
          onChange={(e) => setDomain(e.target.value)}
        />
        <p className="tld"> {tld} </p>
      </div>

      <input
        type="text"
        value={record}
        placeholder="whats ur ninja power?"
        onChange={(e) => setRecord(e.target.value)}
      />

      <div className="button-container">
        {/* ãã¿ã³ã¯ãªãã¯ã§ mintDomainé¢æ° ãå¼ã³åºãã¾ãã */}
        <button className="cta-button mint-button" onClick={mintDomain}>
          Mint
        </button>
      </div>
    </div>
  );
};
```

æ³¨ï¼å¼ãç¶ãã¨ã©ã¼ãè¡¨ç¤ºããã`Mint`ãã¿ã³ã¯æ©è½ãã¾ããã

### ð ABI ãã¡ã¤ã«

ã¹ãã¼ãã³ã³ãã©ã¯ããã³ã³ãã¤ã«ããã¨ãã³ã³ãã¤ã©ã¼ã¯ãã³ã³ãã©ã¯ããæä½ã§ããããã«ããããã«å¿è¦ãªä¸é£ã®ãã¡ã¤ã«ãåãåºãã¾ãã ãããã®ãã¡ã¤ã«ã¯ãSolidity ãã­ã¸ã§ã¯ãã®ã«ã¼ãã«ãã`artifacts`ãã©ã«ãã«ä½æããã¾ãã

ABI ãã¡ã¤ã«ã¨ãããã®ããããããã¯ Web ã¢ããªãã³ã³ãã©ã¯ãã¨éä¿¡ããæ¹æ³ãç¥ãããã«å¿è¦ãªãã®ã§ãã [ãã¡ã](https://docs.soliditylang.org/en/v0.8.11/abi-spec.html)ã«ã¤ãã¦ãèª­ã¿ãã ããã

ABI ãã¡ã¤ã«ã®åå®¹ã¯ãHardhat ãã­ã¸ã§ã¯ãã® JSON ãã¡ã¤ã«ã«ããã¾ãã

åã® section ã§ä½æããããã¯ã¨ã³ãå´ `cool-domains` ããè¦§ãã ããã

`artifacts/contracts/Domains.sol/Domains.json`

`Domains.json`ããã³ã³ãã³ããã³ãã¼ãã¦ãã¦ã§ãã¢ããªï¼ãã­ã³ãã¨ã³ãå´ï¼ã«ç§»åãã¾ãã

(å¨é¸æã¯ Ctrl+A (Windows), Command+A (Mac)ãä½¿ç¨ããã¨ä¾¿å©ã§ãã)

`src`ã®ä¸ã«`utils`ã¨ãããã©ã«ãã«ã`contractABI.json`ã¨ããååã®ãã¡ã¤ã«ãä½æãã¾ãã

(ãã©ã«ãããªãå ´åã¯ä½æãã¦ãã ããã)

ãããã£ã¦ããã«ãã¹ã¯æ¬¡ã®ããã«ãªãã¾ãã

`src/utils/contractABI.json`

ABI ãã¡ã¤ã«ã®åå®¹ãæ°ãããã¡ã¤ã«ã«è²¼ãä»ãã¾ãã

ãã¹ã¦ã® ABI ã³ã³ãã³ããå«ããã¡ã¤ã«ã®æºåãã§ããã®ã§ãæ¬¡ã¯ããã`App.js`ãã¡ã¤ã«ã«ã¤ã³ãã¼ããã¾ãã

æ¬¡ã®ããã«ãªãã¾ãã

```javascript
// App.js
import contractAbi from "./utils/contractABI.json";
```

ãã¹ã¦å®äºãã¾ããã

ããã¨ã©ã¼ã¯ãªãã¯ãã§ãã

ãã®ãããªç»é¢ã«ãªãã¯ãã§ãã

![](/public/images/202-Polygon-ENS-Domain/section-2/2_3_2.png)

ããããè¡ãå¿è¦ãããã®ã¯ããã¡ã¤ã³åã¨ã¬ã³ã¼ããå¥åãã`Mint`ãã¯ãªãã¯ãã¦ãã¬ã¹ãæ¯æãï¼å½ã® MATIC ãä½¿ç¨ï¼ããã©ã³ã¶ã¯ã·ã§ã³ããã¤ãã³ã°ãããã®ãå¾ã¤ã ãã§ãã

ãã¡ã¤ã³ã¯åã® Section ã§ä½¿ç¨ãã Rarible ãªã©ã§ç¢ºèªãã¦ã¿ã¦ãã ããã

ããããã«è¡¨ç¤ºãããªãã¦ã 15 åä»¥åã«ã¯è¡¨ç¤ºãããã§ãããã

### ð¤© ãã¹ã

ãããä½æããã¦ã§ããµã¤ãããç´æ¥ãã¡ã¤ã³ NFT ã«è¡ã£ã¦å®éã«ãã³ããããã¨ãã§ããã¯ãã§ãã

**ãã£ã¦ã¿ã¾ããã!**

NFT ãã³ãã£ã³ã°ãµã¤ããå®éã«ã©ã®ããã«æ©è½ããããç¢ºèªã§ãã¾ãã

ä¸ã¯ä¸ä¾ã§ãã`nin-nin.ninja` ããã³ããã¾ããã

![](/public/images/202-Polygon-ENS-Domain/section-2/2_3_3.png)

(ã¬ã¹ã«ã¤ãã¦è©³ããç¥ãããæ¹ã¯è±èªã«ãªãã¾ãã[ãã](https://ethereum.org/en/developers/docs/gas/)ãåç§ãã¦ã¿ã¦ãã ããã)

### ð ã³ã³ãã©ã¯ãã®åããã­ã¤ã«é¢ããæ³¨æ

ã³ã³ãã©ã¯ããæ´æ°ãããå ´åã¯ãæ¯å 3 ã¤ã®ãã¨ãããå¿è¦ãããã¾ãã

1. ååº¦ããã­ã¤ããå¿è¦ãããã¾ãã
2. ãã­ã³ãã¨ã³ãã®ã³ã³ãã©ã¯ãã¢ãã¬ã¹ãæ´æ°ããå¿è¦ãããã¾ãã
3. ãã­ã³ãã¨ã³ãã® abi ãã¡ã¤ã«ãæ´æ°ããå¿è¦ãããã¾ãã

   2.ã¨ 3. ãããããã©ãã®ç®æãã¯ãããã¾ãã­ã

**ã³ã³ãã©ã¯ããæ´æ°ããã¨ãããã°ãã°ãããã® 3 ã¤ã®ã¹ããããå®è¡ãããã¨ãå¿ãã¾ãããæ¯åå¿è¦ãªæé ã«ãªãã¾ãã®ã§å¿ããªãã§ãã ããã­ã**

ãªãããããã¹ã¦è¡ãå¿è¦ãããã®ã§ãããï¼ ããã¯ãã¹ãã¼ãã³ã³ãã©ã¯ãã**ä¸å¤**ã§ããããã§ããå¤æ´ãããã¨ã¯ã§ãã¾ããã æ°¸ç¶çãªã®ã§ãã ã¤ã¾ããã³ã³ãã©ã¯ããå¤æ´ããã«ã¯ãå®å¨ã«åããã­ã¤ããå¿è¦ãããã¾ãã ããã¯ãã¾ã£ããæ°ããã³ã³ãã©ã¯ãã¨ãã¦æ±ãããããããã¹ã¦ã®å¤æ°ã**ãªã»ãã**ãã¾ãã **ã¤ã¾ããã³ã³ãã©ã¯ãã®ã³ã¼ããæ´æ°ãããå ´åãããã¾ã§ã®ãã¹ã¦ã®ãã¡ã¤ã³ãã¼ã¿ã¯å¼ãç¶ãããªãã®ã§æ³¨æãã¦ãã ããã**

### ðââï¸ è³ªåãã

ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã® `#section-2` ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã® 3 ç¹ãè¨è¼ãã¦ãã ãã â¨

```
1. è³ªåãé¢é£ãã¦ããã»ã¯ã·ã§ã³çªå·ã¨ã¬ãã¹ã³çªå·
2. ä½ããããã¨ãã¦ããã
3. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
4. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```
---

ããã§ã¨ããããã¾ã! Section 2 ãå®äºãã¾ãã! ãã²ããªãã®ãæ°ãã Mint ãã NFT ã Discord ã® `section-2` ã§ã·ã§ã¢ãã¦ãã ããð
