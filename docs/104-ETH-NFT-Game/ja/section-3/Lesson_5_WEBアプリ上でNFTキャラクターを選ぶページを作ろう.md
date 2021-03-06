### ð± NFT ã­ã£ã©ã¯ã¿ã¼ããã­ã³ãã¨ã³ãã«è¡¨ç¤ºãã

ååã®ã¬ãã¹ã³ã§ã¯ãWeb ã¢ããªã±ã¼ã·ã§ã³ããã¹ãã¼ãã³ã³ãã©ã¯ããå¼ã³åºãã³ã¼ããå®è£ãã `SelectCharacter` ã³ã³ãã¼ãã³ããä½æãã¾ããã

ãããããã¹ãã¼ãã³ã³ãã©ã¯ããã NFT ã­ã£ã©ã¯ã¿ã¼ãåå¾ãã¦ãã­ã³ãã¨ã³ãã«è¡¨ç¤ºããã¦ããã¾ãããã

### ð `deploy.js` ãæ´çãã

Web ã¢ããªã±ã¼ã·ã§ã³ã®éçºãé²ããåã«ã`epic-game/scripts` ã«ããã`deploy.js` ãã¡ã¤ã«ãæ´çãã¾ãããã

`mintCharacterNFT` ã `attackBoss` é¢æ°ãæé¤ãã¦ããã¾ãã

ãããã§ã«æé¤ããã¦ããå ´åã¯ããã®ãã­ã»ã¹ãã¹ã­ãããã¦åé¡ããã¾ããã

`deploy.js` ãä¸è¨ã®ããã«ãªã£ã¦ãããã¨ãç¢ºèªããããæ¬¡ã«é²ã¿ã¾ãããã

```javascript
// deploy.js
const main = async () => {
  const gameContractFactory = await hre.ethers.getContractFactory("MyEpicGame");

  const gameContract = await gameContractFactory.deploy(
    ["ZORO", "NAMI", "USOPP"], // ã­ã£ã©ã¯ã¿ã¼ã®åå
    [
      "https://i.imgur.com/TZEhCTX.png", // ã­ã£ã©ã¯ã¿ã¼ã®ç»å
      "https://i.imgur.com/WVAaMPA.png",
      "https://i.imgur.com/pCMZeiM.png",
    ],
    [100, 200, 300],
    [100, 50, 25],
    "CROCODILE", // Bossã®åå
    "https://i.imgur.com/BehawOh.png", // Bossã®ç»å
    10000, // Bossã®hp
    50 // Bossã®æ»æå
  );
  // ããã§ã¯ãnftGame ã³ã³ãã©ã¯ããã
  // ã­ã¼ã«ã«ã®ãã­ãã¯ãã§ã¼ã³ã«ããã­ã¤ãããã¾ã§å¾ã¤å¦çãè¡ã£ã¦ãã¾ãã
  const nftGame = await gameContract.deployed();

  console.log("Contract deployed to:", nftGame.address);
};
const runMain = async () => {
  try {
    await main();
    process.exit(0);
  } catch (error) {
    console.log(error);
    process.exit(1);
  }
};
runMain();
```

`deploy.js` ãæ´çãããã¨ã«ããããã­ã³ãã¨ã³ãã«ãããç¶æã¨ã©ã¼ãé²ããã¨ãã§ãã¾ãã

`deploy.js` ãæ´æ°ããå¾ãããä¸åº¦ã¹ãã¼ãã³ã³ãã©ã¯ããããã­ã¤ããã¨ããããã Web ã¢ããªã±ã¼ã·ã§ã³ä¸ã§ NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ãããã­ã»ã¹ãã¹ã ã¼ãºã«ãªãã¾ãã

å¾©ç¿ãå¼ã­ã¦ãä¸è¨ãå®è¡ãã¦ããã¾ãããã

**1 \. ååº¦ãã³ã³ãã©ã¯ããããã­ã¤ããã**

- `npx hardhat run scripts/deploy.js --network rinkeby` ãå®è¡ããå¿è¦ãããã¾ãã

**2 \. ãã­ã³ãã¨ã³ãï¼ `constants.js`ï¼ã® `CONTRACT_ADDRESS` ãæ´æ°ããã**

**3 \. ã® ABI ãã¡ã¤ã«ãæ´æ°ããã**

- `epic-game/artifacts/contracts/MyEpicGame.sol/MyEpicGame.json` ã®ä¸­èº«ãæ°ããä½æãã `nft-game-starter-project/src/utils/MyEpicGame.json` ã®ä¸­ã«è²¼ãä»ããå¿è¦ãããã¾ãã

### â»ï¸ `index.js` ãæ´æ°ãã

`nft-game-starter-project/src/Components/SelectCharacter` ã«ãã `index.js` ã¯ããã­ã°ã©ã ã®ä¸­ã§ä½åº¦ãç»å ´ããå¤æ°ãé¢æ°ãã¾ã¨ãã¦ãããã¡ã¤ã«ã§ãã

ããããã`index.js` ã®ä¸­èº«ãæ´æ°ãã¦ããã¾ãã

ã¾ãã`index.js` ã® `import` ã®é¨åãä¸è¨ã®ããã«æ´æ°ãã¦ãã ããã

```javascript
// index.js
import React, { useEffect, useState } from "react";
import "./SelectCharacter.css";
import { ethers } from "ethers";
import { CONTRACT_ADDRESS, transformCharacterData } from "../../constants";
import myEpicGame from "../../utils/MyEpicGame.json";
```

æ¬¡ã«ã`SelectCharacter` ãä¸è¨ã®ããã«æ´æ°ãã¾ãããã

```javascript
// index.js
// SelectCharacter ã³ã³ãã¼ãã³ããå®ç¾©ãã¦ãã¾ãã
const SelectCharacter = ({ setCharacterNFT }) => {
  const [characters, setCharacters] = useState([]);
  const [gameContract, setGameContract] = useState(null);

  // ãã¼ã¸ãã­ã¼ããããç¬éã«ä¸è¨ãå®è¡ãã¾ãã
  useEffect(() => {
    const { ethereum } = window;
    if (ethereum) {
      const provider = new ethers.providers.Web3Provider(ethereum);
      const signer = provider.getSigner();
      const gameContract = new ethers.Contract(
        CONTRACT_ADDRESS,
        myEpicGame.abi,
        signer
      );

      // gameContract ã®ç¶æãæ´æ°ãã¾ãã
      setGameContract(gameContract);
    } else {
      console.log("Ethereum object not found");
    }
  }, []);

  return (
    <div className="select-character-container">
      <h2>â¬ ä¸ç·ã«æ¦ã NFT ã­ã£ã©ã¯ã¿ã¼ãé¸æ â¬</h2>
    </div>
  );
};
export default SelectCharacter;
```

è¿½å ããã³ã¼ããè©³ããè¦ã¦ããã¾ãããã

```javascript
// index.js
const [characters, setCharacters] = useState([]);
const [gameContract, setGameContract] = useState(null);
```

ããã§ã¯ãããã¤ãã®ç¶æå¤æ°ãè¨­å®ãã¦ããã¾ãã

- `characters` : ã³ã³ãã©ã¯ãããè¿ããã NFT ã­ã£ã©ã¯ã¿ã¼ã®ã¡ã¿ãã¼ã¿ãä¿æãããã­ããã£ã

- `setCharacters` : `characters` ã®ç¶æãæ´æ°ãããã­ããã£ã

- `gameContract` : ã³ã³ãã©ã¯ãã®ç¶æãåæåãã¦ä¿å­ãããã­ããã£ã

  ãã­ã°ã©ã ã®ä¸­ã§ã³ã³ãã©ã¯ãã¯è¤æ°åå¼ã³åºãããã®ã§ããã£ããåæåããç¶æã§ä¿å­ããã³ã³ãã©ã¯ãå¨ä½ã§ä½¿ç¨ã§ããããã«ãã¾ãã

- `setGameContract` : `gameContract` ã®ç¶æãæ´æ°ãããã­ããã£ã

æ¬¡ã«ãä¸è¨ã®ã³ã¼ããè¦ã¦ããã¾ãããã

```javascript
// index.js
// ãã¼ã¸ãã­ã¼ããããç¬éã«ä¸è¨ãå®è¡ãã¾ãã
useEffect(() => {
  const { ethereum } = window;
  if (ethereum) {
    const provider = new ethers.providers.Web3Provider(ethereum);
    const signer = provider.getSigner();
    const gameContract = new ethers.Contract(
      CONTRACT_ADDRESS,
      myEpicGame.abi,
      signer
    );
    // gameContract ã®ç¶æãæ´æ°ãã¾ãã
    setGameContract(gameContract);
  } else {
    console.log("Ethereum object not found");
  }
}, []);
```

ããã§ã¯ `useEffect` ãä½¿ã£ã¦ã`SelectCharacter` ã³ã³ãã¼ãã³ããå¼ã³åºãããããããã« `gameContract` ãä½æãã¦ãä½¿ç¨ã§ããããã«ãã¦ãã¾ãã

ãã®å¦çã«ããããã­ã³ãã¨ã³ãã§ NFT ã­ã£ã©ã¯ã¿ã¼ãè¡¨ç¤ºããæºåãæ´ãã¾ãã

### ð NFT ã­ã£ã©ã¯ã¿ã¼ã®ãã¼ã¿ãåå¾ãã

NFT ã­ã£ã©ã¯ã¿ã¼ã®ãã¼ã¿ãã¹ãã¼ãã³ã³ãã©ã¯ãããåå¾ããããã«ã`getCharacters` é¢æ°ãä½æãã¾ãã

`gameContract` ãä½¿ç¨ããæºåãã§ããããããã« `getCharacters` é¢æ°ãå¼ã³åºãããã®ã§ãããã§ã `useEffect` ãä½¿ç¨ãã¦ããã¾ãã

ããã§ã¯ã`SelectCharacter` ã®ä¸­ã«è¨è¼ãã `useEffect` é¢æ°ãç¢ºèªãã¾ãããã


```javascript
// index.js
useEffect(() => {
	const { ethereum } = window;

	if (ethereum) {
	  const provider = new ethers.providers.Web3Provider(ethereum);
	  const signer = provider.getSigner();
	  const gameContract = new ethers.Contract(
		CONTRACT_ADDRESS,
		myEpicGame.abi,
		signer
	  );
	  // gameContract ã®ç¶æãæ´æ°ãã¾ãã
	  setGameContract(gameContract);
	} else {
	  console.log('Ethereum object not found');
	}
  	}, []);
```

ãã®é¢æ°ã®ç´ä¸ã«ãä¸è¨ãè¿½å ãã¦ããã¾ãããã

```javascript
// index.js
useEffect(() => {
  // NFT ã­ã£ã©ã¯ã¿ã¼ã®ãã¼ã¿ãã¹ãã¼ãã³ã³ãã©ã¯ãããåå¾ãã¾ãã
  const getCharacters = async () => {
    try {
      console.log("Getting contract characters to mint");
      // ãã³ãå¯è½ãªå¨ NFT ã­ã£ã©ã¯ã¿ã¼ ãã³ã³ãã©ã¯ããããå¼ã³åºãã¾ãã
      const charactersTxn = await gameContract.getAllDefaultCharacters();

      console.log("charactersTxn:", charactersTxn);

      // ãã¹ã¦ã®NFTã­ã£ã©ã¯ã¿ã¼ã®ãã¼ã¿ãå¤æãã¾ãã
      const characters = charactersTxn.map((characterData) =>
        transformCharacterData(characterData)
      );

      // ãã³ãå¯è½ãªãã¹ã¦ã®NFTã­ã£ã©ã¯ã¿ã¼ã®ç¶æãè¨­å®ãã¾ãã
      setCharacters(characters);
    } catch (error) {
      console.error("Something went wrong fetching characters:", error);
    }
  };
  // gameContractã®æºåãã§ããããNFT ã­ã£ã©ã¯ã¿ã¼ãèª­ã¿è¾¼ã¿ã¾ãã
  if (gameContract) {
    getCharacters();
  }
}, [gameContract]);
```

ã³ã¼ãã®ä¸­èº«ãè¦ã¦ããã¾ãããã

```javascript
// index.js
// ãã³ãå¯è½ãªå¨ NFT ã­ã£ã©ã¯ã¿ã¼ ãã³ã³ãã©ã¯ããããå¼ã³åºãã¾ãã
const charactersTxn = await gameContract.getAllDefaultCharacters();
```

ããã§ã¯ã`gameContract` ãä½¿ç¨ãã¦ã`MyEpicGame.sol` ã«è¨è¼ãã`getAllDefaultCharacters` é¢æ°ãå¼ã³åºãã¦ãã¾ãã

> âï¸: `getAllDefaultCharacters` ã¯ã3 ä½ã® NFT ã­ã£ã©ã¯ã¿ã¼ã®ããã©ã«ãæå ±ãåå¾ããé¢æ°ã§ãã

æ¬¡ã«ãä¸è¨ã®ã³ã¼ããè¦ã¦ããã¾ãããã

```javascript
// index.js
// ãã¹ã¦ã®NFTã­ã£ã©ã¯ã¿ã¼ã®ãã¼ã¿ãå¤æãã¾ãã
const characters = charactersTxn.map((characterData) =>
  transformCharacterData(characterData)
);
```

ããã§ã¯ã`transformCharacterData` ãä½¿ç¨ãã¦ãNFT ã­ã£ã©ã¯ã¿ã¼ã®ãã¼ã¿ã Web ã¢ããªã±ã¼ã·ã§ã³ã§æ±ãããªãã¸ã§ã¯ãã«å¤æãã¦ãã¾ãã

> âï¸: `map()` ã®ä½¿ãæ¹
> `map()` ã¯éåãã¼ã¿ã«ä½¿ãã¡ã½ããã§ãã
> `map()` ã¡ã½ãããä½¿ã£ã¦ãéåã«å¥ã£ã¦ãã NFT ã­ã£ã©ã¯ã¿ã¼ããããã®å±æ§æå ±ï¼ HP ãªã©ï¼ã«å¯¾ãã¦ `transformCharacterData` ãå®è¡ãããã®çµæãæ°ããéåï¼ `characters` ï¼ã¨ãã¦è¿ãã¦ãã¾ãã

æ¬¡ã«ä¸è¨ã®ã³ã¼ããè¦ã¦ããã¾ãããã

```javascript
// index.js
// ãã³ãå¯è½ãªãã¹ã¦ã®NFTã­ã£ã©ã¯ã¿ã¼ã®ç¶æãè¨­å®ãã¾ãã
setCharacters(characters);
```

ããã§ã¯ãã³ã³ãã©ã¯ãããåå¾ãã NFT ã­ã£ã©ã¯ã¿ã¼ã®ãã¼ã¿ãç¶æã¨ãã¦ä¿å­ãã¦ãã¾ãã

ãã®å¦çã«ãããNFT ã­ã£ã©ã¯ã¿ã¼ã®ãã¼ã¿ããã­ã³ãã¨ã³ãã§ä½¿ãå§ãããã¨ãã§ãã¾ãã

æå¾ã«ãä¸è¨ã®ã³ã¼ããè¦ã¦ããã¾ãããã

```javascript
// index.js
// gameContractã®æºåãã§ããããNFT ã­ã£ã©ã¯ã¿ã¼ãèª­ã¿è¾¼ã¿ã¾ãã
if (gameContract) {
  getCharacters();
}
```

ããã§ã¯ã`gameContract` ãæ´æ°ããããã³ã«ãä¸­èº«ã `null` ã§ãªããã¨ãç¢ºèªãã`getCharacters` é¢æ°ãå¼ã³åºãå¦çãå®è£ãã¦ãã¾ãã

ãã®å¦çã«ãããNFT ã­ã£ã©ã¯ã¿ã¼ã®ãã¼ã¿ãæ´æ°ããããã³ã«ãã­ã£ã©ã¯ã¿ã¼ã®ç¶æãæ´æ°ã¦ããã­ã³ãã¨ã³ãã«åæ ããããã¨ãã§ãã¾ãã

### â¡ï¸ Web ã¢ããªã±ã¼ã·ã§ã³ä¸ã§ãã¹ããè¡ã

Web ã¢ããªã±ã¼ã·ã§ã³ä¸ã§ãNFT ã­ã£ã©ã¯ã¿ã¼ã®æå ±ãåå¾ã§ãã¦ããããç¢ºèªãã¦ã¿ã¾ãããã

ã­ã¼ã«ã«ç°å¢ã§ãã¹ãããã¦ãã Web ã¢ããªã±ã¼ã·ã§ã³ä¸ã§ã`Inspect` ãå®è¡ããConsole ã«åããã¾ãããã

Web ã¢ããªã±ã¼ã·ã§ã³ããªãã¬ãã·ã¥ãã¦ãã¦ã©ã¬ããæ¥ç¶ãå®äºããããä¸è¨ã®ãããªçµæã Console ã«åºåããã¦ãããç¢ºèªãã¦ãã ããã

```
charactersTxn:
(3) [Array(6), Array(6), Array(6)]
0: (6) [BigNumber, 'ZORO', 'https://i.imgur.com/TZEhCTX.png', BigNumber, BigNumber, BigNumber, characterIndex: BigNumber, name: 'ZORO', imageURI: 'https://i.imgur.com/TZEhCTX.png', hp: BigNumber, maxHp: BigNumber, â¦]
1: (6) [BigNumber, 'NAMI', 'https://i.imgur.com/WVAaMPA.png', BigNumber, BigNumber, BigNumber, characterIndex: BigNumber, name: 'NAMI', imageURI: 'https://i.imgur.com/WVAaMPA.png', hp: BigNumber, maxHp: BigNumber, â¦]
2: (6) [BigNumber, 'USOPP', 'https://i.imgur.com/pCMZeiM.png', BigNumber, BigNumber, BigNumber, characterIndex: BigNumber, name: 'USOPP', imageURI: 'https://i.imgur.com/pCMZeiM.png', hp: BigNumber, maxHp: BigNumber, â¦]
length: 3
[[Prototype]]: Array(0)
```

ä¸è¨ã®ãããªçµæã Console ã«è¡¨ç¤ºããã¦ããã°ãã¹ãã¯æåã§ãã

### ð NFT ã­ã£ã©ã¯ã¿ã¼ ã Web ã¢ããªã±ã¼ã·ã§ã³ã«ã¬ã³ããªã³ã°ãã

ããã§ã¯ãNFT ã­ã£ã©ã¯ã¿ã¼ã®æå ±ã Web ã¢ããªã±ã¼ã·ã§ã³ã«åæ ããã¦ããã¾ãããã

ã¾ãã`index.js` ãéãã`SelectCharacter` ã³ã³ãã¼ãã³ãã®ä¸­ã«ã`renderCharacters` ã¡ã½ãããè¿½å ãã¾ãããã

- 2 ã¤ç®ã«ä½æããã`useEffect` é¢æ°ã®ç´ä¸ã«ãä¸è¨ãè²¼ãä»ãã¦ãã ããã

```javascript
// index.js
// NFT ã­ã£ã©ã¯ã¿ã¼ããã­ã³ãã¨ã³ãã«ã¬ã³ããªã³ã°ããã¡ã½ããã§ãã
const renderCharacters = () =>
  characters.map((character, index) => (
    <div className="character-item" key={character.name}>
      <div className="name-container">
        <p>{character.name}</p>
      </div>
      <img src={character.imageURI} alt={character.name} />
      <button
        type="button"
        className="character-mint-button"
        //onClick={mintCharacterNFTAction(index)}
      >{`Mint ${character.name}`}</button>
    </div>
  ));
```

> â ï¸: æ³¨æ
>
> ã¨ã©ã¼å¦çãåæ»ã«ããããã`onClick={mintCharacterNFTAction(index)}` ã¯ã³ã¡ã³ãã¢ã¦ãããã¾ã¾ã«ãã¦ãã ããã
> å¾ã§è§£é¤ãã¾ãã

æ¬¡ã«ã`index.js` ã®ä¸­ã® `return();` ã®ä¸­èº«ãä¸è¨ã®ããã«æ´æ°ãã¦ãã ããã

```javascript
// index.js
return (
  <div className="select-character-container">
    <h2>â¬ ä¸ç·ã«æ¦ã NFT ã­ã£ã©ã¯ã¿ã¼ãé¸æ â¬</h2>
    {/* ã­ã£ã©ã¯ã¿ã¼NFTããã­ã³ãã¨ã³ãä¸ã§èª­ã¿è¾¼ãã¦ããéã«ãä¸è¨ãè¡¨ç¤ºãã¾ã*/}
    {characters.length > 0 && (
      <div className="character-grid">{renderCharacters()}</div>
    )}
  </div>
);
```

ããã§ã¯ãWeb ã¢ããªã±ã¼ã·ã§ã³ããªãã¬ãã·ã¥ãã¦ãä¸è¨ã®ããã« NFT ã­ã£ã©ã¯ã¿ã¼ããã­ã³ãã¨ã³ãã«åæ ããã¦ãããã¨ãç¢ºèªãã¦ãã ããã

![](/public/images/104-ETH-NFT-Game/section-3/3_5_1.png)

### â¨ Web ã¢ããªã±ã¼ã·ã§ã³ãã NFT ã­ã£ã©ã¯ã¿ã¼ ã Mint ãã

ãããããNFT ã­ã£ã©ã¯ã¿ã¼ã Mint ãã `mintCharacterNFTAction` é¢æ°ãä½æãã¦ããã¾ãã

`index.js` ãéãã`const [gameContract, setGameContract] = useState(null);` ã®ç´ä¸ã«ä¸è¨ãè¿½å ãã¾ãããã

```javascript
// index.js
// NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ãã¾ãã
const mintCharacterNFTAction = (characterId) => async () => {
  try {
    if (gameContract) {
      console.log("Minting character in progress...");
      const mintTxn = await gameContract.mintCharacterNFT(characterId);
      await mintTxn.wait();
      console.log("mintTxn:", mintTxn);
    }
  } catch (error) {
    console.warn("MintCharacterAction Error:", error);
  }
};
```

> â ï¸: æ³¨æ
>
> `renderCharacters` é¢æ°ã®ä¸­ã«ãã `onClick = {mintCharacterNFTAction(index)}` ã®ã³ã¡ã³ãã¢ã¦ããè§£é¤ãã¦ãã ããã

`mintCharacterNFTAction` é¢æ°ã¯ã`MyEpicGame.sol` ã«è¨è¼ããã¦ãã `mintCharacterNFT` é¢æ°ãå¼ã³åºãã¾ãã

- ã©ã® NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ãããã³ã³ãã©ã¯ãã«ä¼ããããã«ããã®ã­ã£ã©ã¯ã¿ã¼ã®ã¤ã³ããã¯ã¹ï¼`characterId`ï¼ãå¼æ°ã¨ãã¦åãå·»ãã

- `onClick = {mintCharacterNFTAction(index)}` ã® `index` ã NFT ã­ã£ã©ã¯ã¿ã¼ã®ã¤ã³ããã¯ã¹ã§ãã

### ð ã³ã³ãã©ã¯ãã§ `emit` ããã `event` ããã­ã³ãã¨ã³ãã§åãåã

NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ããããã¨ããã­ã³ãã¨ã³ãã«ä¼ãã `event` ãã³ã³ãã©ã¯ãä¸ã«ä½æãããã¨ãè¦ãã¦ã¾ããï¼

ãããããWeb ã¢ããªã±ã¼ã·ã§ã³ä¸ã§ `event` ã®æå ±ããã­ã£ãããããã³ã¼ããå®è£ãã¦ããã¾ãã

`index.js` åã§ `getCharacters` é¢æ°ãå®ç¾©ãã `useEffect` ã®ã³ã¼ããã­ãã¯ãä¸è¨ã®ããã«ç·¨éãã¦ãã ããã

```javascript
// index.js
useEffect(() => {
  // NFT ã­ã£ã©ã¯ã¿ã¼ã®ãã¼ã¿ãã¹ãã¼ãã³ã³ãã©ã¯ãããåå¾ãã¾ãã
  const getCharacters = async () => {
    try {
      console.log("Getting contract characters to mint");

      // ãã³ãå¯è½ãªå¨ NFT ã­ã£ã©ã¯ã¿ã¼ ãã³ã³ãã©ã¯ããããå¼ã³åºãã¾ãã
      const charactersTxn = await gameContract.getAllDefaultCharacters();

      console.log("charactersTxn:", charactersTxn);

      // ãã¹ã¦ã®NFTã­ã£ã©ã¯ã¿ã¼ã®ãã¼ã¿ãå¤æãã¾ãã
      const characters = charactersTxn.map((characterData) =>
        transformCharacterData(characterData)
      );

      // ãã³ãå¯è½ãªãã¹ã¦ã®NFTã­ã£ã©ã¯ã¿ã¼ã®ç¶æãè¨­å®ãã¾ãã
      setCharacters(characters);
    } catch (error) {
      console.error("Something went wrong fetching characters:", error);
    }
  };

  // ã¤ãã³ããåä¿¡ããã¨ãã«èµ·åããã³ã¼ã«ããã¯ã¡ã½ãã onCharacterMint ãè¿½å ãã¾ãã
  const onCharacterMint = async (sender, tokenId, characterIndex) => {
    console.log(
      `CharacterNFTMinted - sender: ${sender} tokenId: ${tokenId.toNumber()} characterIndex: ${characterIndex.toNumber()}`
    );
    // NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ãããããã³ã³ãã©ã¯ãããã¡ã¿ãã¼ã¿ãåãåããã¢ãªã¼ãï¼ãã¹ã¨ã®ããã«ãã£ã¼ã«ãï¼ã«ç§»åããããã®ç¶æã«è¨­å®ãã¾ãã
    if (gameContract) {
      const characterNFT = await gameContract.checkIfUserHasNFT();
      console.log("CharacterNFT: ", characterNFT);
      setCharacterNFT(transformCharacterData(characterNFT));
    }
  };

  if (gameContract) {
    getCharacters();
    // ãªã¹ãã¼ã®è¨­å®ï¼NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ãããéç¥ãåãåãã¾ãã
    gameContract.on("CharacterNFTMinted", onCharacterMint);
  }

  return () => {
    // ã³ã³ãã¼ãã³ãããã¦ã³ãããããããªã¹ãã¼ãåæ­¢ããã

    if (gameContract) {
      gameContract.off("CharacterNFTMinted", onCharacterMint);
    }
  };
}, [gameContract]);
```

æ°ããè¿½å ããã³ã¼ããè©³ããè¦ã¦ããã¾ãããã

```javascript
//index.js
// ã¤ãã³ããåä¿¡ããã¨ãã«èµ·åããã³ã¼ã«ããã¯ã¡ã½ãã onCharacterMint ãè¿½å ãã¾ãã
const onCharacterMint = async (sender, tokenId, characterIndex) => {
  console.log(
    `CharacterNFTMinted - sender: ${sender} tokenId: ${tokenId.toNumber()} characterIndex: ${characterIndex.toNumber()}`
  );
  // NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ãããããã³ã³ãã©ã¯ãããã¡ã¿ãã¼ã¿ãåãåããã¢ãªã¼ãï¼ãã¹ã¨ã®ããã«ãã£ã¼ã«ãï¼ã«ç§»åããããã®ç¶æã«è¨­å®ãã¾ãã
  if (gameContract) {
    const characterNFT = await gameContract.checkIfUserHasNFT();
    console.log("CharacterNFT: ", characterNFT);
    setCharacterNFT(transformCharacterData(characterNFT));
  }
};
```

ä¸è¨ã¯ã`MyEpicGame.sol` ã«è¨è¼ãã NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ããã `event` ããã­ã³ãã¨ã³ãã«ç¥ãããï¼`emit`ï¼ã³ã¼ãã§ãã

> ```solidity
> // MyEpicGame.sol
> // ã¦ã¼ã¶ã¼ã NFT ã Mint ãããã¨ç¤ºãã¤ãã³ã
> event CharacterNFTMinted(address sender, uint256 tokenId, uint256 characterIndex);
> // ã¦ã¼ã¶ã¼ã NFT ã Mint ãããã¨ããã­ã³ãã¨ã³ãã«ä¼ãã¾ãã
> emit CharacterNFTMinted(msg.sender, newItemId, _characterIndex);
> ```

`onCharacterMint` ã¡ã½ããã¯ããã®ã¤ãã³ããã­ã£ããããã®ã§ãæ°ãã NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ããããã³ã«å¼ã³åºããã¾ãã

æ¬¡ã«ãä¸è¨ã®ã³ã¼ããè©³ããè¦ã¦ããã¾ãããã

```javascript
// index.js, onCharacterMint()
// NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ãããããã³ã³ãã©ã¯ãããã¡ã¿ãã¼ã¿ãåãåããã¢ãªã¼ãï¼ãã¹ã¨ã®ããã«ãã£ã¼ã«ãï¼ã«ç§»åããããã®ç¶æã«è¨­å®ãã¾ãã
if (gameContract) {
  const characterNFT = await gameContract.checkIfUserHasNFT();
  console.log("CharacterNFT: ", characterNFT);
  setCharacterNFT(transformCharacterData(characterNFT));
}
```

ã¾ãã`if (gameContract)` ã§ NFT ã­ã£ã©ã¯ã¿ã¼ããã§ã« Mint ããã¦ãããã¨ãç¢ºèªãã¦ãã¾ãã

ã¦ã¼ã¶ã¼ããã§ã« NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ãã¦ããå ´åã¯ã`checkIfUserHasNFT` é¢æ°ãä½¿ã£ã¦ãã³ã³ãã©ã¯ãï¼`gameContract`ï¼ã«ä¿å­ããã¦ãããã® NFT ã­ã£ã©ã¯ã¿ã¼ã®ã¡ã¿ãã¼ã¿ï¼HP ãªã©ï¼ã `characterNFT` ã«æ ¼ç´ãã¾ãã

`setCharacterNFT(transformCharacterData(characterNFT));` ã¯ãã³ã³ãã©ã¯ãã«ä¿å­ããã¦ããã¡ã¿ãã¼ã¿ããã­ã³ãã¨ã³ãã§æ±ãããªãã¸ã§ã¯ãå½¢å¼ã«å¤æããå¦çã§ãã

**ãããããã¹ã¦å®äºããã¨ãNFT ã­ã£ã©ã¯ã¿ã¼ããã¹ã¨ããã«ãããã¨ã«ãªã `Area` ã³ã³ãã¼ãã³ãã§ã¡ã¿ãã¼ã¿ãä½¿ç¨ã§ãã¾ãã**

æ¬¡ã«ãä¸è¨ã®ã³ã¼ããè¦ã¦ããã¾ãããã

```javascript
// index.js
if (gameContract) {
  getCharacters();
  // ãªã¹ãã¼ã®è¨­å®ï¼NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ãããéç¥ãåãåãã¾ãã
  gameContract.on("CharacterNFTMinted", onCharacterMint);
}
```

`gameContract.on('CharacterNFTMinted', onCharacterMint)` ã«ããããã­ã³ãã¨ã³ãã¯ã`CharacterNFtMinted` ã¤ãã³ããã³ã³ãã©ã¯ãããçºä¿¡ãããã¨ãã«ãæå ±ãåãåãã¾ããããã«ãããæå ±ããã­ã³ãã¨ã³ãã«åæ ããã¾ãã

- ãã®ãã¨ãã**ã³ã³ãã¼ãã³ãï¼æå ±ï¼ããã¦ã³ãï¼ãã­ã³ãã¨ã³ãã«åæ ï¼ããã**ã¨è¨ãã¾ãã

- ã¾ãããã­ã³ãã¨ã³ãã§ã¤ãã³ããåä¿¡ããæ©è½ã®ãã¨ãããªã¹ããã¨å¼ã³ã¾ãã

ãã­ã³ãã¨ã³ãã§ `CharacterNFtMinted` ã¤ãã³ããåä¿¡ãããã¨ã`onCharacterMint` ã¡ã½ãããå®è¡ããã¾ãã

æå¾ã«ãä¸è¨ã®ã³ã¼ããè¦ã¦ããã¾ãããã

```javascript
// index.js
return () => {
  // ã³ã³ãã¼ãã³ãããã¦ã³ãããããããªã¹ãã¼ãåæ­¢ããã
  if (gameContract) {
    gameContract.off("CharacterNFTMinted", onCharacterMint);
  }
};
```

ããã§ã¯ãNFT ã­ã£ã©ã¯ã¿ã¼ãä¸åº¦ Mint ãããå¾ã`CharacterNFTMinted` ã®åä¿¡ãåæ­¢ããå¦çãè¡ã£ã¦ãã¾ãã

ã³ã³ãã¼ãã³ãããã¦ã³ããããç¶æããã®ã¾ã¾ã«ãã¦ããã¨ãã¡ã¢ãªãªã¼ã¯ï¼ã³ã³ãã¥ã¼ã¿ãåä½ããã¦ããåã«ãä½¿ç¨å¯è½ãªã¡ã¢ãªã®å®¹éãæ¸ã£ã¦ãã£ã¦ãã¾ãç¾è±¡ï¼ãçºçããå¯è½æ§ãããã¾ãã

ã¡ã¢ãªãªã¼ã¯ãé²ãããã«ã`gameContract.off('CharacterNFTMinted', onCharacterMint)` ã§ã¯ã`onCharacterMint` é¢æ°ã®ç¨¼åãããã¦ãã¾ããããã¯ãã¤ãã³ããªã¹ããããããã¨ãæå³ãã¦ãã¾ãã

### ð Rarible ã§ Mint ãã NFT ã­ã£ã©ã¯ã¿ã¼ãç¢ºèªãã

ããã§ã¯ãWeb ã¢ããªã±ã¼ã·ã§ã³ãããã­ã£ã©ã¯ã¿ã¼ããã£ãã Mint ãã¦ã[rinkeby.rarible.com](https://rinkeby.rarible.com/) ã«åæ ããããç¢ºèªãã¦ããã¾ãããã

**1ï¸â£ NFT ã­ã£ã©ã¯ã¿ã¼ã Mint ãã**

Web ã¢ããªã±ã¼ã·ã§ã³ä¸ã§ã`Mint` ãã¿ã³ãæ¼ããããMetaMask ä¸ã§æ¿èªä½æ¥­ï¼`Confirm`ï¼ãè¡ã£ã¦ãã ããã

Mint ãæåããå¾ã«ãWeb ã¢ããªã±ã¼ã·ã§ã³ããªãã¬ãã·ã¥ããã¨ä¸è¨ã®ãããªçµæããConsole ã«è¡¨ç¤ºããã¾ãã

```
Checking for Character NFT on address: 0x3a0a49fb3cf930e599f0fa7abe554dc18bd1f135

Getting contract characters to mint

User has character NFT
```

ãã®ãããªçµæãè¡¨ç¤ºããã¦ããã¨ãããã¨ã¯ãããªãã®ã¦ã©ã¬ããã¢ãã¬ã¹ã« NFT ã­ã£ã©ã¯ã¿ã¼ãå­å¨ãã¦ãããã¨ã«ãªãã¾ãã

**2ï¸â£ Rarible ã§ NFT ã­ã£ã©ã¯ã¿ã¼ãç¢ºèªãã**

[rinkeby.rarible.com](https://rinkeby.rarible.com/) ã§ãNFT ã­ã£ã©ã¯ã¿ã¼ãåç§ãã¦ã¿ã¾ãããã

ããªãã® `CONTACT_ADDRESS` ã¨ `TOKEN_ID` ãåå¾ãã¦ãä¸è¨ã®ã¢ãã¬ã¹ãæ´æ°ãããããã©ã¦ã¶ã«è²¼ãä»ãã¦ã¿ã¦ãã ããã

```
https://rinkeby.rarible.com/token/CONTRACT_ADDRES:TOKEN_ID?table=details
```

ä¸è¨ã¯ãRarible ã®ãªã³ã¯ã®ãµã³ãã«ã«ãªãã¾ãã

[https://rinkeby.rarible.com/token/0xec4d62e631c4fdc9c293772b3897c64a07874b06:1?tab=details](https://rinkeby.rarible.com/token/0xec4d62e631c4fdc9c293772b3897c64a07874b06:1?tab=details)

OpenSea ã§ NFT ã­ã£ã©ã¯ã¿ã¼ãç¢ºèªãããå ´åã¯ãä¸è¨ã®ãªã³ã¯ãã©ã¼ããããä½¿ç¨ãã¦ãã ããã

```
https://testnets.opensea.io/assets/CONTRACT_ADDRES/TOKEN_ID
```

ä¸è¨ã®ããã«ããªã³ã©ã¤ã³ä¸ã§ãããªãã® NFT ã­ã£ã©ã¯ã¿ã¼ãè¡¨ç¤ºããããã¨ãç¢ºèªãã¾ãããã

![](/public/images/104-ETH-NFT-Game/section-3/3_5_2.png)

### ðª ãã¾ã

ã¦ã¼ã¶ã¼ã« NFT ã­ã£ã©ã¯ã¿ã¼ãç¢ºèªãã Rarible ãªã³ã¯ãçºè¡ãã¾ãããã

`index.js` ãéãã¦ã`onCharacterMint` é¢æ°ã®ä¸­èº«ãå¤æ´ãã¾ãã

- `setCharacterNFT(transformCharacterData(characterNFT));` ã®ç´ä¸ã«ä¸è¨ãè¿½å ãã¾ãããã

```javascript
// index.js
alert(
  `NFT ã­ã£ã©ã¯ã¼ã Mint ããã¾ãã -- ãªã³ã¯ã¯ãã¡ãã§ã: https://rinkeby.rarible.com/token/${
    gameContract.address
  }:${tokenId.toNumber()}?tab=details`
);
```

### ðââï¸ è³ªåãã

ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã® `#section-3` ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã® 3 ç¹ãè¨è¼ãã¦ãã ãã â¨

```
1. è³ªåãé¢é£ãã¦ããã»ã¯ã·ã§ã³çªå·ã¨ã¬ãã¹ã³çªå·
2. ä½ããããã¨ãã¦ããã
3. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
4. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```

---

æ¬¡ã®ã¬ãã¹ã³ã«é²ãã§ããã¹ã¨ã®ããã«ãã£ã¼ã«ããå®è£ãã¾ããã ð
