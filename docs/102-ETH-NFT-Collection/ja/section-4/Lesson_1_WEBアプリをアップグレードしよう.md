### ð ã¦ã¼ã¶ã¼ ã« OpenSea/Rarible ã®ãªã³ã¯ãæä¾ãã

NFT ãçºè¡ãããå¾ãOpenSea ã Rarible ã§ NFT ã¸ã®ãªã³ã¯ãå±æã§ãã¾ãã

OpenSea ã® NFT ã¸ã®ãªã³ã¯ã¯æ¬¡ã®ããã«ãªãã¾ãã

```
https://testnets.opensea.io/assets/0x88a0e9c2F3939598c402eccb7Ae1612e45448C04/0
```

ãªã³ã¯ã«ã¯ãä¸è¨ 2 ã¤ã®å¤æ°ãçµã¿è¾¼ã¾ãã¦ãã¾ãã

```
https://testnets.opensea.io/assets/ããªãã®ã³ã³ãã©ã¯ãã¢ãã¬ã¹/tokenId
```

ã¾ããRarible ã® NFT ã®ãªã³ã¯ã¯æ¬¡ã®ããã«ãªãã¾ãã

```
https://rinkeby.rarible.com/token/0x88a0e9c2F3939598c402eccb7Ae1612e45448C04:0
```

ãªã³ã¯ã«ã¯ãä¸è¨ 2 ã¤ã®å¤æ°ãçµã¿è¾¼ã¾ãã¦ãã¾ãã

```
https://rinkeby.rarible.com/token/ããªãã®ã³ã³ãã©ã¯ãã¢ãã¬ã¹:tokenId
```

### ð ã³ã³ãã©ã¯ããæ´æ°ãã¦ tokenId ãåå¾ãã

ç¾å¨ã`App.js`ã«ã¯ã³ã³ãã©ã¯ãã¢ãã¬ã¹ãè¨è¼ããã¦ãã¾ãã

```javascript
// App.js
const CONTRACT_ADDRESS = "0x.."; â ãã¡ã
```

ã§ãããç¾å¨ `App.js` ã«ã¯ã`tokenId` ãè¨è¼ããã¦ãã¾ããã

ããããã`tokenId` ãåå¾ããã³ã¼ãã `MyEpicNFT.sol` ã«è¿½å ããååº¦ããã­ã¤ãã¦ããã¾ãã

ä¸è¨ 2 ç¹ã®å¤æ´ã `MyEpicNFT.sol` ã«åæ ããã¾ãããã

**1 \. `NewEpicNFTMinted` ã¤ãã³ããå®ç¾©ãã**

`string[] thirdWords` ãå®ç¾©ããã¦ããã³ã¼ãã®ç´ä¸ã«ãä¸è¨ã®ã³ã¼ããè¿½å ãã¦ãã ããã

```solidity
// MyEpicNFT.sol
event NewEpicNFTMinted(address sender, uint256 tokenId);
```

**2 \. `NewEpicNFTMinted` ã¤ãã³ãã `emit` ãã**

`makeAnEpicNFT` é¢æ°ã®ä¸çªä¸ã«ãä¸è¨ã®ã³ã¼ããè¿½å ãã¾ãããã

```solidity
// MyEpicNFT.sol
emit NewEpicNFTMinted(msg.sender, newItemId);
```

ãã®ã³ã¼ããã`makeAnEpicNFT` é¢æ°ã®æå¾ã®è¡ã«ãªãããã«æ³¨æãã¦ãã ãã

> **âï¸: Solidity ã§ã¯ã`event` ã¨ `emit` ãé »ç¹ã«ä½¿ç¨ããã¾ãã**

ä¸è¨ã®å®è£ã¯ã`NewEpicNFTMinted` ã¤ãã³ãã `emit` ããããã¨ã«ãã³ã³ãã©ã¯ãã«æ¸ãè¾¼ã¾ãããã¼ã¿ã Web ã¢ããªã±ã¼ã·ã§ã³ã®ãã­ã³ãã¨ã³ãã«åæ ããããã¨ãç®çã¨ãã¦ãã¾ãã

- ã³ã³ãã©ã¯ãã§ã¤ãã³ãã `emit` ãããã¨ããã­ã³ãã¨ã³ãï¼`App.js`ï¼ã§ãã®æå ±ãåãåãã¾ãã

- `NewEpicNFTMinted` ã¤ãã³ãã `emit` ãããéããã­ã³ãã¨ã³ãï¼`App.js`ï¼ã§ä½¿ç¨ããå¤æ° `msg.sender` ã¨ `newItemId` ããã­ã³ãã¨ã³ãã«éä¿¡ãã¦ãã¾ãã

### ð© ããä¸åº¦ããã­ã¤ãã

ã³ã³ãã©ã¯ããæ´æ°ããã®ã§ãä¸è¨ãå®è¡ããå¿è¦ãããã¾ãã

1\. ååº¦ã³ã³ãã©ã¯ããããã­ã¤ãã

2\. ãã­ã³ãã¨ã³ãã®ã³ã³ãã©ã¯ãã¢ãã¬ã¹ãæ´æ°ããï¼æ´æ°ãããã¡ã¤ã«: `App.js`ï¼

3\. ãã­ã³ãã¨ã³ãã® ABI ãã¡ã¤ã«ãæ´æ°ããï¼æ´æ°ãããã¡ã¤ã«: `nft-collection-starter-project/src/utils/MyEpicNFT.json`ï¼

**ã³ã³ãã©ã¯ããæ´æ°ãããã³ããããã® 3 ã¤ã®ã¹ããããå®è¡ããå¿è¦ãããã¾ãã**

å¾©ç¿ããã­ã¦ãä¸å¯§ã«å®è¡ãã¦ããã¾ãããã

**1\. ã¿ã¼ããã«ä¸ã§ `epic-nfts` ã«ç§»åãã¾ãã**

ä¸è¨ãå®è¡ããã³ã³ãã©ã¯ããååº¦ããã­ã¤ãã¾ãããã

```
npx hardhat run scripts/deploy.js --network rinkeby
```

ä¸è¨ã®ããã«ãã¿ã¼ããã«ã«åºåãããã³ã³ãã©ã¯ãã¢ãã¬ã¹ï¼`0x..`ï¼ãã³ãã¼ãã¾ãããã

```
Contract deployed to: 0x... â ããªãã®ã³ã³ãã©ã¯ãã¢ãã¬ã¹ãã³ãã¼
```

**2\. ã³ãã¼ããã¢ãã¬ã¹ã `App.js` ã® `const CONTRACT_ADDRESS = "ãã¡ã"` ã«è²¼ãä»ãã¾ãããã**

**3\. ä»¥åã¨åãããã« `artifacts` ãã ABI ãã¡ã¤ã«ãåå¾ãã¾ããä¸è¨ã®ã¹ããããå®è¡ãã¦ãã ããã**

1\. ã¿ã¼ããã«ä¸ã§ `epic-nfts` ã«ãããã¨ãç¢ºèªããï¼ãããã¯ç§»åããï¼ã

2\. ã¿ã¼ããã«ä¸ã§ä¸è¨ãå®è¡ããã

> ```
> code artifacts/contracts/MyEpicNFT.sol/MyEpicNFT.json
> ```

3\. VS Code ã§ `MyEpicNFT.json` ãã¡ã¤ã«ãéãããã®ã§ãä¸­èº«ããã¹ã¦ã³ãã¼ãããâ» VS Code ã®ãã¡ã¤ã³ãã¼ãä½¿ã£ã¦ãç´æ¥ `MyEpicNFT.json` ãéããã¨ãå¯è½ã§ãã

4\. ã³ãã¼ãã `epic-nfts/artifacts/contracts/MyEpicNFT.sol/MyEpicNFT.json` ã®ä¸­èº«ã `nft-collection-starter-project/src/utils/MyEpicNFT.json` ã®ä¸­èº«ã¨äº¤æããã

**ç¹°ãè¿ãã¾ãããã³ã³ãã©ã¯ããæ´æ°ãããã³ã«ãããè¡ãå¿è¦ãããã¾ãã**

### ðª ãã­ã³ãã¨ã³ããæ´æ°ãã

ä¸è¨ã®ããã«ã`App.js` ãæ´æ°ãã¦ãã ããã

ã¾ãã`const TWITTER_HANDLE = 'ãã¡ã'` ã«ãããªãã® Twitter ãã³ãã«ãè²¼ãä»ãã¦ã¿ã¦ãã ãããããªãã® Web ãµã¤ãããããªãã® Twitter ã¢ã«ã¦ã³ãããªã³ã¯ããããã¨ãã§ãã¾ãã

æ¬¡ã«ãä¸è¨ 2 ã¤ã®ã³ã¼ããã­ãã¯ã« `setupEventListener()` ãè¨­å®ãã¾ãããã

1 ã¤ç®ã®ã¤ãã³ããªã¹ããè¨­å®ã

```javascript
// App.js
//ã¦ã¼ã¶ã¼ãèªè¨¼å¯è½ãªã¦ã©ã¬ããã¢ãã¬ã¹ãæã£ã¦ããå ´åã¯ãã¦ã¼ã¶ã¼ã«å¯¾ãã¦ã¦ã©ã¬ããã¸ã®ã¢ã¯ã»ã¹è¨±å¯ãæ±ãããè¨±å¯ãããã°ãã¦ã¼ã¶ã¼ã®æåã®ã¦ã©ã¬ããã¢ãã¬ã¹ã accounts ã«æ ¼ç´ããã
const accounts = await ethereum.request({ method: "eth_accounts" });

if (accounts.length !== 0) {
  const account = accounts[0];
  console.log("Found an authorized account:", account);
  setCurrentAccount(account);

  // **** ã¤ãã³ããªã¹ãã¼ãããã§è¨­å® ****
  // ãã®æç¹ã§ãã¦ã¼ã¶ã¼ã¯ã¦ã©ã¬ããæ¥ç¶ãæ¸ãã§ãã¾ãã
  setupEventListener();
} else {
  console.log("No authorized account found");
}
```

2 ã¤ç®ã®ã¤ãã³ããªã¹ããè¨­å®ã

```javascript
// App.js
// connectWallet ã¡ã½ãããå®è£ãã¾ãã
const connectWallet = async () => {
  try {
    const { ethereum } = window;
    if (!ethereum) {
      alert("Get MetaMask!");
      return;
    }
    // ã¦ã©ã¬ããã¢ãã¬ã¹ã«å¯¾ãã¦ã¢ã¯ã»ã¹ããªã¯ã¨ã¹ããã¦ãã¾ãã
    const accounts = await ethereum.request({ method: "eth_requestAccounts" });

    console.log("Connected", accounts[0]);

    // ã¦ã©ã¬ããã¢ãã¬ã¹ã currentAccount ã«ç´ä»ãã¾ãã
    setCurrentAccount(accounts[0]);

    // **** ã¤ãã³ããªã¹ãã¼ãããã§è¨­å® ****
    setupEventListener();
  } catch (error) {
    console.log(error);
  }
};
```

æ¬¡ã«ã`connectWallet` é¢æ°ã®ç´ä¸ã«ãä¸è¨ã® `setupEventListener` é¢æ°ãè¿½å ãã¦ãã ããã

```javascript
// App.js
// setupEventListener é¢æ°ãå®ç¾©ãã¾ãã
// MyEpicNFT.sol ã®ä¸­ã§ event ããemit ãããæã«ã
// æå ±ãåãåãã¾ãã
const setupEventListener = async () => {
  try {
    const { ethereum } = window;
    if (ethereum) {
      const provider = new ethers.providers.Web3Provider(ethereum);
      const signer = provider.getSigner();
      // NFT ãçºè¡ããã¾ãã
      const connectedContract = new ethers.Contract(
        CONTRACT_ADDRESS,
        myEpicNft.abi,
        signer
      );
      // Event ããemit ãããéã«ãã³ã³ãã©ã¯ãããéä¿¡ãããæå ±ãåãåã£ã¦ãã¾ãã
      connectedContract.on("NewEpicNFTMinted", (from, tokenId) => {
        console.log(from, tokenId.toNumber());
        alert(
          `ããªãã®ã¦ã©ã¬ããã« NFT ãéä¿¡ãã¾ãããOpenSea ã«è¡¨ç¤ºãããã¾ã§æå¤§ã§10åããããã¨ãããã¾ããNFT ã¸ã®ãªã³ã¯ã¯ãã¡ãã§ã: https://testnets.opensea.io/assets/${CONTRACT_ADDRESS}/${tokenId.toNumber()}`
        );
      });
      console.log("Setup event listener!");
    } else {
      console.log("Ethereum object doesn't exist!");
    }
  } catch (error) {
    console.log(error);
  }
};
```

`setupEventListener` é¢æ°ã¯ãNFT ãçºè¡ãããéã« `emit` ããã `NewEpicNFTMinted` ã¤ãã³ããåä¿¡ãã¾ãã

- `tokenId` ãåå¾ãã¦ãæ°ãããã³ãããã NFT ã¸ã® OpenSea ãªã³ã¯ãã¦ã¼ã¶ã¼ã«æä¾ãã¦ãã¾ãã

### ðª MVP = `MyEpicNFT.sol` Ã `App.js`

ä»åã®ãã­ã¸ã§ã¯ãã® MVPï¼ï¼æå°éã®æ©è½ãåãããã­ãã¯ãï¼ãæ§ç¯ãã `MyEpicNFT.sol` ã¨ `App.js` ã®ã¹ã¯ãªãããå±æãã¾ãã

- è¦ãããããã«å°ãæ´çæ´é ãã¦ããã¾ã ð§¹â¨

ããã³ã¼ãã«ã¨ã©ã¼ãçºçãã¦ãããã°ãå°é£ãªå ´åã¯ãä¸è¨ã®ã³ã¼ããä½¿ç¨ãã¦ã¿ã¦ãã ããã

**`MyEpicNFT.sol` ã¯ãã¡ã:**

```solidity
// MyEpicNFT.sol
// SPDX-License-Identifier: MIT

pragma solidity 0.8.9;

// ããã¤ãã® OpenZeppelin ã®ã³ã³ãã©ã¯ããã¤ã³ãã¼ããã¾ãã
import "@openzeppelin/contracts/utils/Strings.sol";
import "@openzeppelin/contracts/token/ERC721/extensions/ERC721URIStorage.sol";
// utils ã©ã¤ãã©ãªãã¤ã³ãã¼ããã¦æå­åã®å¦çãè¡ãã¾ãã
import "@openzeppelin/contracts/utils/Counters.sol";
import "hardhat/console.sol";

// Base64.solã³ã³ãã©ã¯ãããSVGã¨JSONãBase64ã«å¤æããé¢æ°ãã¤ã³ãã¼ããã¾ãã
import { Base64 } from "./libraries/Base64.sol";

// ã¤ã³ãã¼ããã OpenZeppelin ã®ã³ã³ãã©ã¯ããç¶æ¿ãã¦ãã¾ãã
// ç¶æ¿ããã³ã³ãã©ã¯ãã®ã¡ã½ããã«ã¢ã¯ã»ã¹ã§ããããã«ãªãã¾ãã
contract MyEpicNFT is ERC721URIStorage {
  // OpenZeppelinãããtokenIdsããç°¡åã«è¿½è·¡ããããã«æä¾ããã©ã¤ãã©ãªãå¼ã³åºãã¦ãã¾ã
  using Counters for Counters.Counter;
  // _tokenIdsãåæåï¼_tokenIds = 0ï¼
  Counters.Counter private _tokenIds;

  // SVGã³ã¼ããä½æãã¾ãã
  // å¤æ´ãããã®ã¯ãè¡¨ç¤ºãããåèªã ãã§ãã
  // ãã¹ã¦ã®NFTã«SVGã³ã¼ããé©ç¨ããããã«ãbaseSvgå¤æ°ãä½æãã¾ãã
  string baseSvg = "<svg xmlns='http://www.w3.org/2000/svg' preserveAspectRatio='xMinYMin meet' viewBox='0 0 350 350'><style>.base { fill: white; font-family: serif; font-size: 24px; }</style><rect width='100%' height='100%' fill='black' /><text x='50%' y='50%' class='base' dominant-baseline='middle' text-anchor='middle'>";

  // 3ã¤ã®éå string[] ã«ãããããã©ã³ãã ãªåèªãè¨­å®ãã¾ãããã
  string[] firstWords = ["Epic", "Fantastic", "Crude", "Crazy", "Hysterical", "Grand"];
  string[] secondWords = ["Meta", "Live", "Pop", "Cute", "Sweet", "Hot"];
  string[] thirdWords = ["Kitten", "Puppy", "Monkey", "Bird", "Panda", "Elephant"];

  // NewEpicNFTMinted ã¤ãã³ããå®ç¾©ãã¾ãã
  event NewEpicNFTMinted(address sender, uint256 tokenId);

  // NFT ãã¼ã¯ã³ã®ååã¨ãã®ã·ã³ãã«ãæ¸¡ãã¾ãã
  constructor() ERC721 ("SquareNFT", "SQUARE") {
    console.log("This is my NFT contract.");
  }

  // ã·ã¼ããçæããé¢æ°ãä½æãã¾ãã
  function random(string memory input) internal pure returns (uint256) {
      return uint256(keccak256(abi.encodePacked(input)));
  }

  // åéåããã©ã³ãã ã«åèªãé¸ã¶é¢æ°ã3ã¤ä½æãã¾ãã
  // pickRandomFirstWordé¢æ°ã¯ãæåã®åèªãé¸ã³ã¾ãã
  function pickRandomFirstWord(uint256 tokenId) public view returns (string memory) {
    // pickRandomFirstWord é¢æ°ã®ã·ã¼ãã¨ãªã rand ãä½æãã¾ãã
    uint256 rand = random(string(abi.encodePacked("FIRST_WORD", Strings.toString(tokenId))));
    // seed rand ãã¿ã¼ããã«ã«åºåããã
	console.log("rand - seed: ", rand);
	// firstWordséåã®é·ããåºæºã«ãrand çªç®ã®åèªãé¸ã³ã¾ãã
    rand = rand % firstWords.length;
	// firstWordséåããä½çªç®ã®åèªãé¸ã°ãããã¿ã¼ããã«ã«åºåããã
	console.log("rand - first word: ", rand);
    return firstWords[rand];
  }

  // pickRandomSecondWordé¢æ°ã¯ã2çªç®ã«è¡¨ç¤ºãããã®åèªãé¸ã³ã¾ãã
  function pickRandomSecondWord(uint256 tokenId) public view returns (string memory) {
    // pickRandomSecondWord é¢æ°ã®ã·ã¼ãã¨ãªã rand ãä½æãã¾ãã
    uint256 rand = random(string(abi.encodePacked("SECOND_WORD", Strings.toString(tokenId))));
    rand = rand % secondWords.length;
    return secondWords[rand];
  }

  // pickRandomThirdWordé¢æ°ã¯ã3çªç®ã«è¡¨ç¤ºãããã®åèªãé¸ã³ã¾ãã
  function pickRandomThirdWord(uint256 tokenId) public view returns (string memory) {
    // pickRandomThirdWord é¢æ°ã®ã·ã¼ãã¨ãªã rand ãä½æãã¾ãã
    uint256 rand = random(string(abi.encodePacked("THIRD_WORD", Strings.toString(tokenId))));
    rand = rand % thirdWords.length;
    return thirdWords[rand];
  }

  // ã¦ã¼ã¶ã¼ã NFT ãåå¾ããããã«å®è¡ããé¢æ°ã§ãã
  function makeAnEpicNFT() public {
    // ç¾å¨ã®tokenIdãåå¾ãã¾ããtokenIdã¯0ããå§ã¾ãã¾ãã
    uint256 newItemId = _tokenIds.current();

    // 3ã¤ã®éåãããããã1ã¤ã®åèªãã©ã³ãã ã«åãåºãã¾ãã
    string memory first = pickRandomFirstWord(newItemId);
    string memory second = pickRandomSecondWord(newItemId);
    string memory third = pickRandomThirdWord(newItemId);

	// 3ã¤ã®åèªãçµã¿åãããè¨èï¼ä¾: GrandCuteBirdï¼ã combinedWord ã«æ ¼ç´ãã¦ãã¾ãã
    string memory combinedWord = string(abi.encodePacked(first, second, third));

    // 3ã¤ã®åèªãé£çµãã¦ã<text>ã¿ã°ã¨<svg>ã¿ã°ã§éãã¾ãã
    string memory finalSvg = string(abi.encodePacked(baseSvg, first, second, third, "</text></svg>"));

	// NFTã«åºåããããã­ã¹ããã¿ã¼ããã«ã«åºåãã¾ãã
	console.log("\n----- SVG data -----");
    console.log(finalSvg);
    console.log("--------------------\n");

    // JSONãã¡ã¤ã«ãæå®ã®ä½ç½®ã«åå¾ããbase64ã¨ãã¦ã¨ã³ã³ã¼ããã¾ãã
    string memory json = Base64.encode(
        bytes(
            string(
                abi.encodePacked(
                    '{"name": "',
                    // NFTã®ã¿ã¤ãã«ãçæãããè¨èï¼ä¾: GrandCuteBirdï¼ã«è¨­å®ãã¾ãã
                    combinedWord,
                    '", "description": "A highly acclaimed collection of squares.", "image": "data:image/svg+xml;base64,',
                    //  data:image/svg+xml;base64 ãè¿½å ããSVG ã base64 ã§ã¨ã³ã³ã¼ãããçµæãè¿½å ãã¾ãã
                    Base64.encode(bytes(finalSvg)),
                    '"}'
                )
            )
        )
    );

    // ãã¼ã¿ã®åé ­ã« data:application/json;base64 ãè¿½å ãã¾ãã
    string memory finalTokenUri = string(
        abi.encodePacked("data:application/json;base64,", json)
    );

	console.log("\n----- Token URI ----");
    console.log(finalTokenUri);
    console.log("--------------------\n");

   // msg.sender ãä½¿ã£ã¦ NFT ãéä¿¡èã« Mint ãã¾ãã
    _safeMint(msg.sender, newItemId);

    // tokenURIãæ´æ°ãã¾ãã
    _setTokenURI(newItemId, finalTokenUri);

 	// NFTããã¤èª°ã«ä½æãããããç¢ºèªãã¾ãã
	console.log("An NFT w/ ID %s has been minted to %s", newItemId, msg.sender);

    // æ¬¡ã® NFT ã Mint ãããã¨ãã®ã«ã¦ã³ã¿ã¼ãã¤ã³ã¯ãªã¡ã³ãããã
    _tokenIds.increment();

    // ã¤ãã³ãã emit ãã¾ãã
    emit NewEpicNFTMinted(msg.sender, newItemId);
  }
}
```

**`App.js` ã¯ãã¡ã:**

```javascript
// App.js
import "./styles/App.css";

// ãã­ã³ãã¨ã³ãã¨ã³ã³ãã©ã¯ããé£æºããã©ã¤ãã©ãªãã¤ã³ãã¼ããã¾ãã
import { ethers } from "ethers";
// useEffect ã¨ useState é¢æ°ã React.js ããã¤ã³ãã¼ããã¦ãã¾ãã
import React, { useEffect, useState } from "react";

import twitterLogo from "./assets/twitter-logo.svg";
import myEpicNft from "./utils/MyEpicNFT.json";

const TWITTER_HANDLE = "ããªãã®Twitterãã³ãã«";
const TWITTER_LINK = `https://twitter.com/${TWITTER_HANDLE}`;
const OPENSEA_LINK = "";
const TOTAL_MINT_COUNT = 50;

// ã³ãã³ãã©ã¯ãã¢ãã¬ã¹ãCONTRACT_ADDRESSå¤æ°ã«æ ¼ç´
const CONTRACT_ADDRESS = "ããªãã®ã³ã³ãã©ã¯ãã¢ãã¬ã¹";

const App = () => {
  // ã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¢ãã¬ã¹ãæ ¼ç´ããããã«ä½¿ç¨ããç¶æå¤æ°ãå®ç¾©ãã¾ãã
  const [currentAccount, setCurrentAccount] = useState("");

  // setupEventListener é¢æ°ãå®ç¾©ãã¾ãã
  // MyEpicNFT.sol ã®ä¸­ã§ event ããemit ãããæã«ã
  // æå ±ãåãåãã¾ãã
  const setupEventListener = async () => {
    try {
      const { ethereum } = window;

      if (ethereum) {
        const provider = new ethers.providers.Web3Provider(ethereum);
        const signer = provider.getSigner();
        const connectedContract = new ethers.Contract(
          CONTRACT_ADDRESS,
          myEpicNft.abi,
          signer
        );

        // Event ããemit ãããéã«ãã³ã³ãã©ã¯ãããéä¿¡ãããæå ±ãåãåã£ã¦ãã¾ãã
        connectedContract.on("NewEpicNFTMinted", (from, tokenId) => {
          console.log(from, tokenId.toNumber());
          alert(
            `ããªãã®ã¦ã©ã¬ããã« NFT ãéä¿¡ãã¾ãããOpenSea ã«è¡¨ç¤ºãããã¾ã§æå¤§ã§10åããããã¨ãããã¾ããNFT ã¸ã®ãªã³ã¯ã¯ãã¡ãã§ã: https://testnets.opensea.io/assets/${CONTRACT_ADDRESS}/${tokenId.toNumber()}`
          );
        });

        console.log("Setup event listener!");
      } else {
        console.log("Ethereum object doesn't exist!");
      }
    } catch (error) {
      console.log(error);
    }
  };

  // ã¦ã¼ã¶ã¼ãèªè¨¼å¯è½ãªã¦ã©ã¬ããã¢ãã¬ã¹ãæã£ã¦ãããç¢ºèªãã¾ãã
  const checkIfWalletIsConnected = async () => {
    const { ethereum } = window;

    if (!ethereum) {
      console.log("Make sure you have MetaMask!");
      return;
    } else {
      console.log("We have the ethereum object", ethereum);
    }

    // ã¦ã¼ã¶ã¼ãèªè¨¼å¯è½ãªã¦ã©ã¬ããã¢ãã¬ã¹ãæã£ã¦ããå ´åã¯ãã¦ã¼ã¶ã¼ã«å¯¾ãã¦ã¦ã©ã¬ããã¸ã®ã¢ã¯ã»ã¹è¨±å¯ãæ±ãããè¨±å¯ãããã°ãã¦ã¼ã¶ã¼ã®æåã®ã¦ã©ã¬ããã¢ãã¬ã¹ã accounts ã«æ ¼ç´ããã
    const accounts = await ethereum.request({ method: "eth_accounts" });

    if (accounts.length !== 0) {
      const account = accounts[0];
      console.log("Found an authorized account:", account);
      setCurrentAccount(account);

      // ã¤ãã³ããªã¹ãã¼ãè¨­å®
      // ãã®æç¹ã§ãã¦ã¼ã¶ã¼ã¯ã¦ã©ã¬ããæ¥ç¶ãæ¸ãã§ãã¾ãã
      setupEventListener();
    } else {
      console.log("No authorized account found");
    }
  };

  // connectWallet ã¡ã½ãããå®è£ãã¾ãã
  const connectWallet = async () => {
    try {
      const { ethereum } = window;

      if (!ethereum) {
        alert("Get MetaMask!");
        return;
      }

      // ã¦ã©ã¬ããã¢ãã¬ã¹ã«å¯¾ãã¦ã¢ã¯ã»ã¹ããªã¯ã¨ã¹ããã¦ãã¾ãã
      const accounts = await ethereum.request({
        method: "eth_requestAccounts",
      });

      console.log("Connected", accounts[0]);

      // ã¦ã©ã¬ããã¢ãã¬ã¹ã currentAccount ã«ç´ä»ãã¾ãã
      setCurrentAccount(accounts[0]);

      // ã¤ãã³ããªã¹ãã¼ãè¨­å®
      setupEventListener();
    } catch (error) {
      console.log(error);
    }
  };

  // NFT ã Mint ããé¢æ°ãå®ç¾©ãã¦ãã¾ãã
  const askContractToMintNft = async () => {
    try {
      const { ethereum } = window;

      if (ethereum) {
        const provider = new ethers.providers.Web3Provider(ethereum);
        const signer = provider.getSigner();
        const connectedContract = new ethers.Contract(
          CONTRACT_ADDRESS,
          myEpicNft.abi,
          signer
        );

        console.log("Going to pop wallet now to pay gas...");
        let nftTxn = await connectedContract.makeAnEpicNFT();

        console.log("Mining...please wait.");
        await nftTxn.wait();
        console.log(nftTxn);
        console.log(
          `Mined, see transaction: https://rinkeby.etherscan.io/tx/${nftTxn.hash}`
        );
      } else {
        console.log("Ethereum object doesn't exist!");
      }
    } catch (error) {
      console.log(error);
    }
  };

  // ãã¼ã¸ãã­ã¼ããããéã«ä¸è¨ãå®è¡ããã¾ãã
  useEffect(() => {
    checkIfWalletIsConnected();
  }, []);

  // renderNotConnectedContainer ã¡ã½ããï¼ Connect to Wallet ãè¡¨ç¤ºããé¢æ°ï¼ãå®ç¾©ãã¾ãã
  const renderNotConnectedContainer = () => (
    <button
      onClick={connectWallet}
      className="cta-button connect-wallet-button"
    >
      Connect to Wallet
    </button>
  );

  // Mint NFT ãã¿ã³ãã¬ã³ããªã³ã°ããã¡ã½ãããå®ç¾©ãã¾ãã
  const renderMintUI = () => (
    <button
      onClick={askContractToMintNft}
      className="cta-button connect-wallet-button"
    >
      Mint NFT
    </button>
  );

  return (
    <div className="App">
      <div className="container">
        <div className="header-container">
          <p className="header gradient-text">My NFT Collection</p>
          <p className="sub-text">ããªãã ãã®ç¹å¥ãª NFT ã Mint ãããð«</p>
          {/*æ¡ä»¶ä»ãã¬ã³ããªã³ã°ã
          // ãã§ã«ã¦ã©ã¬ããæ¥ç¶ããã¦ããå ´åã¯ã
          // Mint NFT ãè¡¨ç¤ºããã*/}
          {currentAccount === ""
            ? renderNotConnectedContainer()
            : renderMintUI()}
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

### ð Web ã¢ããªã±ã¼ã·ã§ã³ãã¢ããã°ã¬ã¼ããã

MVP ãèµ·ç¹ã« Web ã¢ããªã±ã¼ã·ã§ã³ãèªåã®å¥½ããªããã«ã¢ããã°ã¬ã¼ããã¾ãããã

**1\. ãã³ãããã NFT ã®æ°ã«å¶éãè¨­å®ãã**

- `MyEpicNFT.sol` ãå¤æ´ãã¦ããããããè¨­å®ãããæ°ã® NFT ã®ã¿ããã³ãã§ããããã«ãããã¨ããå§ããã¾ãã
- `App.js` ãæ´æ°ãã¦ãWeb ã¢ããªã±ã¼ã·ã§ã³ä¸ã§ Mint ã«ã¦ã³ã¿ãè¡¨ç¤ºãã¦ã¿ã¾ããã!ï¼ä¾ããããã¾ã§ã«ä½æããã 4/50 NFTãï¼

**2\. ã¦ã¼ã¶ã¼ãééã£ããããã¯ã¼ã¯ä¸ã«ããã¨ãã¢ã©ã¼ããåºã**

- ããªãã® Web ãµã¤ãã¯ Rinkeby Test Network ã§**ã®ã¿**æ©è½ãã¾ãã
- ã¦ã¼ã¶ã¼ããRinkeby ä»¥å¤ã®ãããã¯ã¼ã¯ã«ã­ã°ã¤ã³ãã¦ããç¶æã§ãããªãã® Web ãµã¤ãã«æ¥ç¶ãããã¨ãããããããç¥ãããã¢ã©ã¼ããåºãã¾ãããã
- `methereum.request` ã¨ `eth_accounts` ã¨ `eth_requestAccounts` ã¨ããã¡ã½ãããä½¿ç¨ãã¦ãã¢ã©ã¼ããä½æã§ãã¾ãã
- `eth_chainId` ãä½¿ã£ã¦ãã­ãã¯ãã§ã¼ã³ãè­å¥ãã ID ãåå¾ãã¾ãã

ä¸è¨ã®ã³ã¼ãã `App.js` ã«çµã¿è¾¼ãã§ã¿ã¾ãããã

```javascript
// App.js
let chainId = await ethereum.request({ method: "eth_chainId" });
console.log("Connected to chain " + chainId);
// 0x4 ã¯ãRinkeby ã® ID ã§ãã
const rinkebyChainId = "0x4";
if (chainId !== rinkebyChainId) {
  alert("You are not connected to the Rinkeby Test Network!");
}
```

ä»ã®ãã­ãã¯ãã§ã¼ã³ ID ã¯ [ãã¡ã](https://docs.MetaMask.io/guide/ethereum-provider.html#chain-ids) ããè¦ã¤ãããã¨ãã§ãã¾ãã

**3\. ãã¤ãã³ã°ã¢ãã¡ã¼ã·ã§ã³ãä½æãã**

- ä¸é¨ã®ã¦ã¼ã¶ã¼ã¯ãMint ãã¯ãªãã¯ããå¾ã15 ç§ä»¥ä¸ä½ãèµ·ãããªãã¨ãæ··ä¹±ãã¦ãã¾ãå¯è½æ§ãããã§ãããã
- "Loading ..." ã®ãããªã¢ãã¡ã¼ã·ã§ã³ãè¿½å ãã¦ãã¦ã¼ã¶ã¼ã«å®å¿ãã¦ãããã¾ãããã

**4\. ããªãã®ã³ã¬ã¯ã·ã§ã³ Web ã¢ããªã±ã¼ã·ã§ã³ããªã³ã¯ããã**

- ããªãã®ã³ã¬ã¯ã·ã§ã³ãè¦ã«ããããã¿ã³ã Web ã¢ããªã±ã¼ã·ã§ã³ä¸ã«ä½æãã¦ãã¦ã¼ã¶ã¼ããã¤ã§ãããªãã® NFT ã³ã¬ã¯ã·ã§ã³ãè¦ã«è¡ããããã«ãã¾ãããã
- ããªãã® Web ãµã¤ãã«ããRarible ã§ã³ã¬ã¯ã·ã§ã³ãè¡¨ç¤ºãã¨ããå°ããªãã¿ã³ãè¿½å ãã¾ãã
- ã¦ã¼ã¶ã¼ããããã¯ãªãã¯ããã¨ãã³ã¬ã¯ã·ã§ã³ã®ãã¼ã¸ã«è¡ããããã«ãã¾ãããã
- Rarible ã¸ã®ãªã³ã¯ã¯ `App.js` ã«ãã¼ãã³ã¼ãã£ã³ã°ããå¿è¦ãããã¾ãã

### ðââï¸ è³ªåãã

ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã®`#section-4`ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã® 3 ç¹ãè¨è¼ãã¦ãã ãã â¨

```
1. è³ªåãé¢é£ãã¦ããã»ã¯ã·ã§ã³çªå·ã¨ã¬ãã¹ã³çªå·
2. ä½ããããã¨ãã¦ããã
3. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
4. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```

---

ããã§ã¯ãæå¾ã®ã¬ãã¹ã³ã«é²ã¿ã¾ããã ð
