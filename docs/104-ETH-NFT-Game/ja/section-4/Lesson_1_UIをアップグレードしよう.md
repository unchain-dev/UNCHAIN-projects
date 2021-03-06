### ð« UI ã®ä»ä¸ã

NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ãããããã¹ã®ãã¼ã¿ãåå¾ãããããã¨ãã«ãã­ã¼ãã£ã³ã°ãã¼ã¯ã UI ã«è¡¨ç¤ºãã¦ããã¾ãããã

ãããããä¸è¨ã®ã±ã¼ã¹ã«ã­ã¼ãã£ã³ã°ãã¼ã¯å®è£ãã¦ããã¾ãã

1\. `App.js` : ã¦ã¼ã¶ã¼ã NFT ã­ã£ã©ã¯ã¿ã¼ãæã£ã¦ããããã­ã³ãã¨ã³ããç¢ºèªãã¦ããç¶æ³

2\. `SelectCharacter` ã³ã³ãã¼ãã³ã : ã¦ã¼ã¶ã¼ã NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ããã®ããã­ã³ãã¨ã³ããå¾æ©ãã¦ããç¶æ³

3\. `Arena` ã³ã³ãã¼ãã³ã : æ»æãçµäºããã®ããã­ã³ãã¨ã³ããå¾æ©ãã¦ããç¶æ³

`nft-game-starter-project/src/Components` ãã©ã«ãã« `LoadingIndicator` ã³ã³ãã¼ãã³ããæ ¼ç´ããã¦ãã¾ãã

ãã®ã¬ãã¹ã³ã§ã¯ããã® `LoadingIndicator` ã³ã³ãã¼ãã³ããä½¿ã£ã¦ããã¾ãã

### ð `App.js` ã«ã­ã¼ãã£ã³ã°ãã¼ã¯ãè¿½å ãã

1 ã¤ç®ã®ã±ã¼ã¹ããã¦ã¼ã¶ã¼ã NFT ã­ã£ã©ã¯ã¿ã¼ãæã£ã¦ããããã­ã³ãã¨ã³ããç¢ºèªãã¦ããç¶æ³ãã§ãWeb ã¢ããªã±ã¼ã·ã§ã³ã«ã­ã¼ãã£ã³ã°ãã¼ã¯ãè¡¨ç¤ºãã¦ããã¾ãããã

ã¾ãã`App.js` ãéãã`const [characterNFT, setCharacterNFT] = useState(null);` ã®ç´ä¸ã«ä¸è¨ãè¿½å ãã¾ãããã

```javascript
// App.js
// ã­ã¼ãç¶æãåæåãã¾ãã
const [isLoading, setIsLoading] = useState(false);
```

æ¬¡ã«ãã³ã³ãã©ã¯ããã `checkIfUserHasNFT` é¢æ°ãå¼ã³åºããªã©ãéåææä½ãå®è¡ãã¦ããéã«ãã­ã¼ãç¶æãè¨­å®ããå®è£ãè¡ãã¾ãã

`setIsLoading(true);` ããä¸è¨ 2 ã¤ã® `useEffects` ã«è¿½å ãã¾ãããã

```javascript
// App.js
// ãã¼ã¸ãã­ã¼ããããã¨ãã« useEffect()åã®é¢æ°ãå¼ã³åºããã¾ãã
useEffect(() => {
	// ãã¼ã¸ãã­ã¼ããããããå³åº§ã«ã­ã¼ãç¶æãè¨­å®ããããã«ãã¾ãã
	setIsLoading(true);
	checkIfWalletIsConnected();
}, []);

// ãã¼ã¸ãã­ã¼ããããã¨ãã« useEffect()åã®é¢æ°ãå¼ã³åºããã¾ãã
useEffect(() => {
	// ã¹ãã¼ãã³ã³ãã©ã¯ããå¼ã³åºãé¢æ°ã§ãã
	const fetchNFTMetadata = async () => {
		console.log('Checking for Character NFT on address:', currentAccount);

		const provider = new ethers.providers.Web3Provider(window.ethereum);
		const signer = provider.getSigner();
		const gameContract = new ethers.Contract(
		CONTRACT_ADDRESS,
		myEpicGame.abi,
		signer
		);

	const txn = await gameContract.checkIfUserHasNFT();
	if (txn.name) {
		console.log('User has character NFT');
		setCharacterNFT(transformCharacterData(txn));
	} else {
		console.log('No character NFT found');
	}
	// ã¦ã¼ã¶ã¼ãä¿æãã¦ãã NFT ã®ç¢ºèªãå®äºããããã­ã¼ãç¶æã false ã«è¨­å®ãã¾ãã
	setIsLoading(false);
}, [currentAccount]);
```

æ¬¡ã«ã`App.js` ã®åé ­ã«ä¸è¨ãè¿½å ãã¦ã`LoadingIndicator` ãã¤ã³ãã¼ããã¦ãã ããã

```javascript
// App.js
import LoadingIndicator from "./Components/LoadingIndicator";
```

æ¬¡ã«ã`renderContent` é¢æ°ã®åé ­ã«ãä¸è¨ãè¿½å ãã¾ãããã

```javascript
// App.js
// ã¢ããªãã­ã¼ãä¸­ã®å ´åã¯ãLoadingIndicator ãã¬ã³ããªã³ã°ãã¾ãã
if (isLoading) {
  return <LoadingIndicator />;
}
```

ãã®å¦çã«ãããWeb ã¢ããªã±ã¼ã·ã§ã³ãã³ã³ãã©ã¯ããããã¼ã¿ãèª­ã¿è¾¼ãã§ããéã¯ãã­ã¼ãã£ã³ã°ãã¼ã¯ãè¡¨ç¤ºããã¾ãã

æ¬¡ã«ã`checkIfWalletIsConnected` ã«ä¸è¨ã®ããã«æ´æ°ãã¦ããã­ã³ãã¨ã³ããã¦ã¼ã¶ã¼ã MetaMask ãæã£ã¦ãããç¢ºèªãã¦ããéã«ãã­ã¼ãã£ã³ã°ãã¼ã¯ãè¡¨ç¤ºããã¾ãããã


```javascript
// App.js
// ã¦ã¼ã¶ã¼ã MetaMask ãæã£ã¦ãããç¢ºèªãã¾ãã
const checkIfWalletIsConnected = async () => {
  try {
    const { ethereum } = window;
    if (!ethereum) {
      console.log("Make sure you have MetaMask!");

      // æ¬¡ã®è¡ã§ return ãä½¿ç¨ãããããããã§ isLoading ãè¨­å®ãã¾ãã
      setIsLoading(false);
      return;
    } else {
      console.log("We have the ethereum object", ethereum);

      // accounts ã«WEBãµã¤ããè¨ªããã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¢ã«ã¦ã³ããæ ¼ç´ãã¾ãã
      // ï¼è¤æ°æã£ã¦ããå ´åãå å³ããã£ã¦ account's' ã¨å¤æ°ãå®ç¾©ãã¦ããï¼
      const accounts = await ethereum.request({ method: "eth_accounts" });

      // ããã¢ã«ã¦ã³ããä¸ã¤ã§ãå­å¨ããããä»¥ä¸ãå®è¡ã
      if (accounts.length !== 0) {
        // account ã¨ããå¤æ°ã«ã¦ã¼ã¶ã¼ã®1ã¤ç®ï¼= Javascript ã§ãã0çªç®ï¼ã®ã¢ãã¬ã¹ãæ ¼ç´
        const account = accounts[0];
        console.log("Found an authorized account:", account);

        // currentAccount ã«ã¦ã¼ã¶ã¼ã®ã¢ã«ã¦ã³ãã¢ãã¬ã¹ãæ ¼ç´
        setCurrentAccount(account);
      } else {
        console.log("No authorized account found");
      }
    }
  } catch (error) {
    console.log(error);
  }
  //ãã¹ã¦ã®é¢æ°ã­ã¸ãã¯ã®å¾ã«ãstate ãã­ããã£ãè§£æ¾ãã¾ãã
  setIsLoading(false);
};
```

ã¦ã©ã¬ããã®æ¥ç¶ãè§£é¤ããã¨ãã­ã¼ãã£ã³ã°ãã¼ã¯ãè¡¨ç¤ºãããã¯ãã§ããã¦ã©ã¬ããæ¥ç¶ãã¿ã³ãè¡¨ç¤ºãããããã«ã`isLoading` ç¶æã®ãã­ããã£ãè§£æ¾ããï¼=`false`ã«ããï¼å¿è¦ãããã¾ãã

### ð `SelectCharacter` ã³ã³ãã¼ãã³ãã«ã­ã¼ãã£ã³ã°ãã¼ã¯ãè¿½å ãã

2 ã¤ç®ã®ã±ã¼ã¹ããã¦ã¼ã¶ã¼ã NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ããã®ããã­ã³ãã¨ã³ããå¾æ©ãã¦ããç¶æ³ãã§ãWeb ã¢ããªã±ã¼ã·ã§ã³ã«ã­ã¼ãã£ã³ã°ãã¼ã¯ãè¡¨ç¤ºãã¦ããã¾ãããã

ã¾ãã`nft-game-starter-project/src/Components/SelectCharacter/index.js` ã®åé ­ã«ãä¸è¨ãè¿½å ãã¾ãããã

```javascript
// SelectCharacter/index.js
import LoadingIndicator from "../../Components/LoadingIndicator";
```

æ¬¡ã«ã`SelectCharacter/index.js` ã®ä¸­ã«è¨è¼ããã `const [gameContract, setGameContract] = useState(null);` ã®ç´ä¸ã«ã`const [mintingCharacter, setMintingCharacter] = useState(false);` ãè¿½å ãã¾ãããã

- ä¸è¨ãåç§ãã¦ãã ããã

```javascript
// SelectCharacter/index.js
//NFT ã­ã£ã©ã¯ã¿ã¼ã®ã¡ã¿ãã¼ã¿ãä¿å­ããç¶æå¤æ°ãåæåãã¾ãã
const [characters, setCharacters] = useState([]);

// ã³ã³ãã©ã¯ãã®ãã¼ã¿ãä¿æããç¶æå¤æ°ãåæåãã¾ãã
const [gameContract, setGameContract] = useState(null);

// Minting ã®ç¶æä¿å­ããç¶æå¤æ°ãåæåãã¾ãã
const [mintingCharacter, setMintingCharacter] = useState(false);
```

ããã§ã¯ã`App.js` ã§ `isLoading` ãåæåããæã¨åæ§ã«ã NFT ã® Minting ç¶æãä¿å­ãã `mintingCharacter` ã¨ããç¶æå¤æ°ãåæåãã¦ãã¾ãã

æ¬¡ã«ã`mintCharacterNFTAction` ã®ä¸­ã«ã`setMintingCharacter` ã 3 ã¤è¨­ç½®ãã¦ããã¾ãã

- ä¸è¨ãåèã«ãã¦ãã ããã

```javascript
// SelectCharacter/index.js
// NFT ã Mint ãã¾ãã
const mintCharacterNFTAction = (characterId) => async () => {
  try {
    if (gameContract) {
      // Mint ãéå§ãããããã­ã¼ãã£ã³ã°ãã¼ã¯ãè¡¨ç¤ºããã
      setMintingCharacter(true);

      console.log("Minting character in progress...");
      const mintTxn = await gameContract.mintCharacterNFT(characterId);
      await mintTxn.wait();
      console.log("mintTxn:", mintTxn);
      // Mint ãçµäºããããã­ã¼ãã£ã³ã°ãã¼ã¯ãæ¶ãã
      setMintingCharacter(false);
    }
  } catch (error) {
    console.warn("MintCharacterAction Error:", error);
    // ã¨ã©ã¼ãçºçããå ´åããã­ã¼ãã£ã³ã°ãã¼ã¯ãæ¶ãã
    setMintingCharacter(false);
  }
};
```

æå¾ã«ãNFT ã Mint ããã¦ããéã«ã­ã¼ãã£ã³ã°ãã¼ã¯ãè¡¨ç¤ºãã HTML ãå®è£ãã¾ãããã

- `SelectCharacter/index.js` ã®ä¸­ã«ãã `return();` ã®ä¸­èº«ãä¸è¨ã®ããã«æ´æ°ãã¦ãã ããã

```javascript
// SelectCharacter/index.js
return (
  <div className="select-character-container">
    <h2>â¬ ä¸ç·ã«æ¦ã NFT ã­ã£ã©ã¯ã¿ã¼ãé¸æ â¬</h2>
    {characters.length > 0 && (
      <div className="character-grid">{renderCharacters()}</div>
    )}
    {/* mintingCharacter = trueã®å ´åã®ã¿ãã­ã¼ãã£ã³ã°ãã¼ã¯ãè¡¨ç¤ºãã¾ãã*/}
    {mintingCharacter && (
      <div className="loading">
        <div className="indicator">
          <LoadingIndicator />
          <p>Minting In Progress...</p>
        </div>
      </div>
    )}
  </div>
);
```

`SelectCharacter.css` ã«ãä¸è¨ã® CSS ãè¿½å ãã¾ãããã

- `nft-game-starter-project/src/Components/SelectCharacter` ãã©ã«ãã®ä¸­ã« `SelectCharacter.css` ãæ ¼ç´ããã¦ãã¾ãã

```css
/* SelectCharacter.css */
.select-character-container .loading {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-top: 75px;
}
.select-character-container .loading .indicator {
  display: flex;
}
.select-character-container .loading .indicator p {
  font-weight: bold;
  font-size: 28px;
  padding-left: 5px;
}
.select-character-container .loading img {
  width: 450px;
  padding-top: 25px;
}
```

ä¸è¨ã®å®è£ã¯ãã­ã³ãã¨ã³ãã«ä¸è¨ã®ããã«åæ ããã¾ãã

![](/public/images/104-ETH-NFT-Game/section-4/4_1_1.png)

### ð `Arena` ã³ã³ãã¼ãã³ãã«ã­ã¼ãã£ã³ã°ãã¼ã¯ãè¿½å ãã

3 ã¤ç®ã®ã±ã¼ã¹ããæ»æãçµäºããã®ããã­ã³ãã¨ã³ããå¾æ©ãã¦ããç¶æ³ãã§ãWeb ã¢ããªã±ã¼ã·ã§ã³ã«ã­ã¼ãã£ã³ã°ãã¼ã¯ãè¡¨ç¤ºãã¦ããã¾ãããã

ã¾ãã`nft-game-starter-project/src/Components/Arena/index.js` ã®åé ­ã«ãä¸è¨ãè¿½å ãã¾ãããã

```javascript
// Arena/index.js
import LoadingIndicator from "../LoadingIndicator";
```

æ¬¡ã«ã`Arena/index.js` ã«è¨è¼ããã¦ãã `return();` ã®ä¸­èº«ã«çç®ãã`{boss ..}` ã®ä¸­èº«ãä¸è¨ã®ããã«æ´æ°ãã¦ãã ããã

```javascript
// Arena/index.js
{
  boss && (
    <div className="boss-container">
      {/* attackState è¿½å ãã¾ã */}
      <div className={`boss-content  ${attackState}`}>
        <h2>ð¥ {boss.name} ð¥</h2>
        <div className="image-content">
          <img src={boss.imageURI} alt={`Boss ${boss.name}`} />
          <div className="health-bar">
            <progress value={boss.hp} max={boss.maxHp} />
            <p>{`${boss.hp} / ${boss.maxHp} HP`}</p>
          </div>
        </div>
      </div>
      <div className="attack-container">
        <button className="cta-button" onClick={runAttackAction}>
          {`ð¥ Attack ${boss.name}`}
        </button>
      </div>
      {/* Attack ãã¿ã³ã®ä¸ã«ã­ã¼ãã£ã³ã°ãã¼ã¯ãè¿½å ãã¾ã*/}
      {attackState === "attacking" && (
        <div className="loading-indicator">
          <LoadingIndicator />
          <p>Attacking âï¸</p>
        </div>
      )}
    </div>
  );
}
```

æå¾ã«ãä¸è¨ã® CSS ãã`Arena.css` ãã¡ã¤ã«ã«è¿½å ãã¦ãã ããã

- `nft-game-starter-project/src/Components/Arena` ãã©ã«ãã®ä¸­ã« `Arena.css` ãæ ¼ç´ããã¦ãã¾ãã

```css
/* Arena.css */
.boss-container .loading-indicator {
  display: flex;
  justify-content: center;
  align-items: center;
  padding-top: 25px;
}
.boss-container .loading-indicator p {
  font-weight: bold;
  font-size: 28px;
}
```

ä¸è¨ã®ã³ã¼ããå®è£ããããWeb ã¢ããªã±ã¼ã·ã§ã³ãç¢ºèªãã¦ã¿ã¾ãããã

ã­ã¼ãã£ã³ã°ãã¼ã¯ã `Arena` ãã¼ã¸ã«è¡¨ç¤ºããã¦ããã§ããããï¼ã â¨

### ð¨ `Arena` ãã¼ã¸ã«æ»æã¢ã©ã¼ããè¿½å ãã

æå¾ã«ããã¹ã«ä¸ãããã¡ã¼ã¸ããã­ã³ãã¨ã³ãä¸ã«è¡¨ç¤ºããã³ã¼ããå®è£ãã¦ããã¾ãããã

ã¾ããä¸è¨ã® CSS ã `Arena.css` ãã¡ã¤ã«ã«è¿½å ãã¾ãããã

```css
/* nft-game-starter-project/src/Components/Arena/Arena.css */
/* Toast */
#toast {
  visibility: hidden;
  max-width: 500px;
  height: 90px;
  margin: auto;
  background-color: gray;
  color: #fff;
  text-align: center;
  border-radius: 10px;
  position: fixed;
  z-index: 1;
  left: 0;
  right: 0;
  bottom: 30px;
  font-size: 17px;
  white-space: nowrap;
}
#toast #desc {
  display: flex;
  align-items: center;
  justify-content: center;
  color: #fff;
  font-size: 28px;
  font-weight: bold;
  height: 90px;
  overflow: hidden;
  white-space: nowrap;
}
#toast.show {
  visibility: visible;
  -webkit-animation: fadein 0.5s, expand 0.5s 0.5s, stay 3s 1s, shrink 0.5s 2s,
    fadeout 0.5s 2.5s;
  animation: fadein 0.5s, expand 0.5s 0.5s, stay 3s 1s, shrink 0.5s 4s,
    fadeout 0.5s 4.5s;
}
@-webkit-keyframes fadein {
  from {
    bottom: 0;
    opacity: 0;
  }
  to {
    bottom: 30px;
    opacity: 1;
  }
}
@keyframes fadein {
  from {
    bottom: 0;
    opacity: 0;
  }
  to {
    bottom: 30px;
    opacity: 1;
  }
}
@-webkit-keyframes expand {
  from {
    min-width: 50px;
  }
  to {
    min-width: 350px;
  }
}
@keyframes expand {
  from {
    min-width: 50px;
  }
  to {
    min-width: 350px;
  }
}
@-webkit-keyframes stay {
  from {
    min-width: 350px;
  }
  to {
    min-width: 350px;
  }
}
@keyframes stay {
  from {
    min-width: 350px;
  }
  to {
    min-width: 350px;
  }
}
@-webkit-keyframes shrink {
  from {
    min-width: 350px;
  }
  to {
    min-width: 50px;
  }
}
@keyframes shrink {
  from {
    min-width: 350px;
  }
  to {
    min-width: 50px;
  }
}
@-webkit-keyframes fadeout {
  from {
    bottom: 30px;
    opacity: 1;
  }
  to {
    bottom: 60px;
    opacity: 0;
  }
}
@keyframes fadeout {
  from {
    bottom: 30px;
    opacity: 1;
  }
  to {
    bottom: 60px;
    opacity: 0;
  }
}
```

æ¬¡ã«ã`nft-game-starter-project/src/Components/Arena/index.js` ãéããHTML ãè¨è¼ããã¦ãã `return();` ã®ä¸­èº«ãä¸è¨ã®ããã«æ´æ°ãã¾ãããã

```javascript
// Arena/index.js
return (
  <div className="arena-container">
    {/* æ»æãã¡ã¼ã¸ã®éç¥ãè¿½å ãã¾ã */}
    {boss && characterNFT && (
      <div id="toast" className={showToast ? "show" : ""}>
        <div id="desc">{`ð¥ ${boss.name} was hit for ${characterNFT.attackDamage}!`}</div>
      </div>
    )}
    {/* ãã¹ãã¬ã³ããªã³ã°ãã¾ã */}
    {boss && (
      <div className="boss-container">
        <div className={`boss-content  ${attackState}`}>
          <h2>ð¥ {boss.name} ð¥</h2>
          <div className="image-content">
            <img src={boss.imageURI} alt={`Boss ${boss.name}`} />
            <div className="health-bar">
              <progress value={boss.hp} max={boss.maxHp} />
              <p>{`${boss.hp} / ${boss.maxHp} HP`}</p>
            </div>
          </div>
        </div>
        <div className="attack-container">
          <button className="cta-button" onClick={runAttackAction}>
            {`ð¥ Attack ${boss.name}`}
          </button>
        </div>
        {/* Attack ãã¿ã³ã®ä¸ã«ã­ã¼ãã£ã³ã°ãã¼ã¯ãè¿½å ãã¾ã*/}
        {attackState === "attacking" && (
          <div className="loading-indicator">
            <LoadingIndicator />
            <p>Attacking âï¸</p>
          </div>
        )}
      </div>
    )}
    {/* NFT ã­ã£ã©ã¯ã¿ã¼ ãã¬ã³ããªã³ã°ãã¾ã*/}
    {characterNFT && (
      <div className="players-container">
        <div className="player-container">
          <h2>Your Character</h2>
          <div className="player">
            <div className="image-content">
              <h2>{characterNFT.name}</h2>
              <img
                src={characterNFT.imageURI}
                alt={`Character ${characterNFT.name}`}
              />
              <div className="health-bar">
                <progress value={characterNFT.hp} max={characterNFT.maxHp} />
                <p>{`${characterNFT.hp} / ${characterNFT.maxHp} HP`}</p>
              </div>
            </div>
            <div className="stats">
              <h4>{`âï¸ Attack Damage: ${characterNFT.attackDamage}`}</h4>
            </div>
          </div>
        </div>
        {/* <div className="active-players">
          <h2>Active Players</h2>
          <div className="players-list">{renderActivePlayersList()}</div>
        </div> */}
      </div>
    )}
  </div>
);
```

æå¾ã«ã`Arena/index.js` ãæ´æ°ãã¦ãæ»æãã¡ã¼ã¸ã®è¡¨ç¤ºã¨éè¡¨ç¤ºã®è¨­å®ãè¡ãã¾ãã

`Arena.css` ã®ä¸­ã«ä¸è¨ã®ãããª `show` ã¯ã©ã¹ãå­å¨ãããã¨ãç¢ºèªãã¦ãã ããã

```css
/* nft-game-starter-project/src/Components/Arena/Arena.css */
#toast.show {
  visibility: visible;
  -webkit-animation: fadein 0.5s, expand 0.5s 0.5s, stay 3s 1s, shrink 0.5s 2s,
    fadeout 0.5s 2.5s;
  animation: fadein 0.5s, expand 0.5s 0.5s, stay 3s 1s, shrink 0.5s 4s,
    fadeout 0.5s 4.5s;
}
```

`show` ã¯ã©ã¹ã `Arena/index.js` ä¸ã§æé¤ããã¨ãæ»æã¡ãã»ã¼ã¸ãéè¡¨ç¤ºã«ãªãã¾ãã

ãããããåçã« `show` ã¯ã©ã¹ã®è¡¨ç¤ºã¨éè¡¨ç¤ºãå¤æ´ããã­ã¸ãã¯ãå®è£ãã¦ããã¾ãããã

ã¾ãã`const [attackState, setAttackState] = useState('');` ã®ç´ä¸ã«ä¸è¨ãè¿½å ãã¾ãããã

```javascript
// Arena/index.js
// æ»æãã¡ã¼ã¸ã®è¡¨ç¤ºå½¢å¼ãä¿å­ããå¤æ°ãåæåãã¾ãã
const [showToast, setShowToast] = useState(false);
```

æ¬¡ã«ãä¸è¨ã®ããã«ã`runAttackAction` é¢æ°ã« `setShowToast` ãè¨­å®ãã¦ããã¾ãããã

```javascript
// Arena/index.js
const runAttackAction = async () => {
  try {
    // ã³ã³ãã©ã¯ããå¼ã³åºããããã¨ãç¢ºèªãã¾ãã
    if (gameContract) {
      // attackState ã®ç¶æã attacking ã«è¨­å®ãã¾ãã
      setAttackState("attacking");
      console.log("Attacking boss...");

      // NFT ã­ã£ã©ã¯ã¿ã¼ããã¹ãæ»æãã¾ãã
      const attackTxn = await gameContract.attackBoss();

      // ãã©ã³ã¶ã¯ã·ã§ã³ããã¤ãã³ã°ãããã¾ã§å¾ã¡ã¾ãã
      await attackTxn.wait();
      console.log("attackTxn:", attackTxn);

      // attackState ã®ç¶æã hit ã«è¨­å®ãã¾ãã
      setAttackState("hit");

      // æ»æãã¡ã¼ã¸ã®è¡¨ç¤ºã true ã«è¨­å®ãï¼è¡¨ç¤ºï¼ã5ç§å¾ã« false ã«è¨­å®ããï¼éè¡¨ç¤ºï¼
      setShowToast(true);
      setTimeout(() => {
        setShowToast(false);
      }, 5000);
    }
  } catch (error) {
    console.error("Error attacking boss:", error);
    setAttackState("");
  }
};
```

ããã§ã¯ã`setTimeout` ãä½¿ç¨ãã¦ãæ»æã¡ãã»ã¼ã¸ã 5 ç§éè¡¨ç¤ºããå¾ã«ãéè¡¨ç¤ºã«ããã­ã¸ãã¯ãè¿½å ãã¦ãã¾ãã

ä¸è¨ã®å®è£ãæåããå ´åãWeb ã¢ããªã±ã¼ã·ã§ã³ä¸ã§ãã¹ãæ»æããã¨ãæ»æãã¡ã¼ã¸ããã­ã³ãã¨ã³ãã«è¡¨ç¤ºããã¾ãã

### ðââï¸ è³ªåãã

ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã® `#section-4` ã§è³ªåãã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã® 3 ç¹ãè¨è¼ãã¦ãã ãã â¨

```
1. è³ªåãé¢é£ãã¦ããã»ã¯ã·ã§ã³çªå·ã¨ã¬ãã¹ã³çªå·
2. ä½ããããã¨ãã¦ããã
3. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
4. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```

---

æ¬¡ã®ã¬ãã¹ã³ã«é²ãã§ãWeb ã¢ããªã±ã¼ã·ã§ã³ã Vercel ã«ããã­ã¤ãã¾ããã ð
