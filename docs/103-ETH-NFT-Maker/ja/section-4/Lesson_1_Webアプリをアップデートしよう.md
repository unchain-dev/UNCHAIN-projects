### ðª MVP = Web3Mint.sol Ã NftUploader.jsx
ä»åã®ãã­ã¸ã§ã¯ãã® MVPï¼ï¼æå°éã®æ©è½ãåãããã­ãã¯ãï¼ãæ§ç¯ãã Web3Mint.sol ã¨ NftUploader.jsx ã®ã¹ã¯ãªãããå±æãã¾ãã

è¦ãããããã«å°ãæ´çæ´é ãã¦ããã¾ã ð§¹â¨
ããã³ã¼ãã«ã¨ã©ã¼ãçºçãã¦ãããã°ãå°é£ãªå ´åã¯ãä¸è¨ã®ã³ã¼ããä½¿ç¨ãã¦ã¿ã¦ãã ããã

**`Web3Mint.sol` ã¯ãã¡ã:**

```solidity
// Web3Mint.sol
// SPDX-License-Identifier: UNLICENSED
pragma solidity ^0.8.9;
import "@openzeppelin/contracts/token/ERC721/ERC721.sol";

//OpenZeppelinãæä¾ãããã«ãã¼æ©è½ãã¤ã³ãã¼ããã¾ãã
import "@openzeppelin/contracts/utils/Counters.sol";

import "./libraries/Base64.sol";
import "hardhat/console.sol";
contract Web3Mint is ERC721{
    struct NftAttributes{
        string name;
        string imageURL;
    }

    using Counters for Counters.Counter;
    // tokenIdã¯NFTã®ä¸æãªè­å¥å­ã§ã0, 1, 2, .. N ã®ããã«ä»ä¸ããã¾ãã
    Counters.Counter private _tokenIds;

    NftAttributes[] Web3Nfts;

    constructor() ERC721("NFT","nft"){
        console.log("This is my NFT contract.");
    }

    // ã¦ã¼ã¶ã¼ã NFT ãåå¾ããããã«å®è¡ããé¢æ°ã§ãã

    function mintIpfsNFT(string memory name,string memory imageURI) public{
        uint256 newItemId = _tokenIds.current();
        _safeMint(msg.sender,newItemId);
        Web3Nfts.push(NftAttributes({
            name: name,
            imageURL: imageURI
        }));
        console.log("An NFT w/ ID %s has been minted to %s", newItemId, msg.sender);
        _tokenIds.increment();
    }
    function tokenURI(uint256 _tokenId) public override view returns(string memory){
    string memory json = Base64.encode(
        bytes(
            string(
                abi.encodePacked(
                    '{"name": "',
                    Web3Nfts[_tokenId].name,
                    ' -- NFT #: ',
                    Strings.toString(_tokenId),
                    '", "description": "An epic NFT", "image": "ipfs://',
                    Web3Nfts[_tokenId].imageURL,'"}'
                )
            )
        )
    );
    string memory output = string(
        abi.encodePacked("data:application/json;base64,", json)
    );
    return output;
    }
}
```
**`NftUploader.jsx` ã¯ãã¡ã:**

```javascript
// NftUploader.jsx
import { ethers } from "ethers";
import Web3Mint from "../../utils/Web3Mint.json";
import { Button } from "@mui/material";
import React from "react";
import { useEffect, useState } from 'react'
import ImageLogo from "./image.svg";
import "./NftUploader.css";
import { Web3Storage } from 'web3.storage'

const NftUploader = () => {
  /*
   * ã¦ã¼ã¶ã¼ã®ã¦ã©ã¬ããã¢ãã¬ã¹ãæ ¼ç´ããããã«ä½¿ç¨ããç¶æå¤æ°ãå®ç¾©ãã¾ãã
   */
  const [currentAccount, setCurrentAccount] = useState("");
  /*ãã®æ®µéã§currentAccountã®ä¸­èº«ã¯ç©º*/
  console.log("currentAccount: ", currentAccount);
  const checkIfWalletIsConnected = async () => {
    const { ethereum } = window;
    if (!ethereum) {
      console.log("Make sure you have MetaMask!");
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
  const connectWallet = async () =>{
    try {
      const { ethereum } = window;
      if (!ethereum) {
        alert("Get MetaMask!");
        return;
      }
      /*
       * ã¦ã©ã¬ããã¢ãã¬ã¹ã«å¯¾ãã¦ã¢ã¯ã»ã¹ããªã¯ã¨ã¹ããã¦ãã¾ãã
       */
      const accounts = await ethereum.request({
        method: "eth_requestAccounts",
      });
      console.log("Connected", accounts[0]);
      /*
       * ã¦ã©ã¬ããã¢ãã¬ã¹ã currentAccount ã«ç´ä»ãã¾ãã
       */
      setCurrentAccount(accounts[0]);
    } catch (error) {
      console.log(error);
    }
  };

  const askContractToMintNft = async (ipfs) => {
    const CONTRACT_ADDRESS =
      "0x35558364D864EAAcE19c10d84437969F133eDf12";
    try {
      const { ethereum } = window;
      if (ethereum) {
        const provider = new ethers.providers.Web3Provider(ethereum);
        const signer = provider.getSigner();
        const connectedContract = new ethers.Contract(
          CONTRACT_ADDRESS,
          Web3Mint.abi,
          signer
        );
        console.log("Going to pop wallet now to pay gas...");
        let nftTxn = await connectedContract.mintIpfsNFT("sample",ipfs);
        console.log("Mining...please wait.");
        await nftTxn.wait();
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


  const renderNotConnectedContainer = () => (
      <button onClick={connectWallet} className="cta-button connect-wallet-button">
        Connect to Wallet
      </button>
    );
  /*
   * ãã¼ã¸ãã­ã¼ããããã¨ãã« useEffect()åã®é¢æ°ãå¼ã³åºããã¾ãã
   */
  useEffect(() => {
    checkIfWalletIsConnected();
  }, []);

  const API_KEY = "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJkaWQ6ZXRocjoweGU4MTQxMmVkYTk5NUI5NjMzMDIwNTYxRDkzMTRhNGE5NEQyMDIyNTQiLCJpc3MiOiJ3ZWIzLXN0b3JhZ2UiLCJpYXQiOjE2NDkzMTE5NzIxNjYsIm5hbWUiOiJzYW1wbGUifQ.1q2qbS-4FgjREAr_wVE0QtRI68QLEfPQdPO-B-7ixjg";

  const imageToNFT = async (e) => {
    const client = new Web3Storage({ token: API_KEY })
    const image = e.target
    console.log(image)

    const rootCid = await client.put(image.files, {
        name: 'experiment',
        maxRetries: 3
    })
    const res = await client.get(rootCid) // Web3Response
    const files = await res.files() // Web3File[]
    for (const file of files) {
      console.log("file.cid:",file.cid)
      askContractToMintNft(file.cid)
    }
}

  return (
    <div className="outerBox">
      {currentAccount === "" ? (
        renderNotConnectedContainer()
      ) : (
        <p>If you choose image, you can mint your NFT</p>
      )}
      <div className="title">
        <h2>NFTã¢ããã­ã¼ãã¼</h2>
      </div>
      <div className="nftUplodeBox">
        <div className="imageLogoAndText">
          <img src={ImageLogo} alt="imagelogo" />
          <p>ããã«ãã©ãã°ï¼ãã­ãããã¦ã­</p>
        </div>
        <input className="nftUploadInput" multiple name="imageURL" type="file" accept=".jpg , .jpeg , .png" onChange={imageToNFT}  />
      </div>
      <p>ã¾ãã¯</p>
      <Button variant="contained">
        ãã¡ã¤ã«ãé¸æ
        <input className="nftUploadInput" type="file" accept=".jpg , .jpeg , .png" onChange={imageToNFT} />
      </Button>
    </div>
  );
};

export default NftUploader;
```

### ð Web ã¢ããªã±ã¼ã·ã§ã³ãã¢ããã°ã¬ã¼ããã

MVP ãèµ·ç¹ã« Web ã¢ããªã±ã¼ã·ã§ã³ãèªåã®å¥½ããªããã«ã¢ããã°ã¬ã¼ããã¾ãããã

**1\. ãã³ãããã NFT ã®æ°ã«å¶éãè¨­å®ãã**

- `Web3Mint.sol` ãå¤æ´ãã¦ããããããè¨­å®ãããæ°ã® NFT ã®ã¿ããã³ãã§ããããã«ãããã¨ããå§ããã¾ãã
- `NftUploader.jsx` ãæ´æ°ãã¦ãWeb ã¢ããªã±ã¼ã·ã§ã³ä¸ã§ Mint ã«ã¦ã³ã¿ãè¡¨ç¤ºãã¦ã¿ã¾ããã!ï¼ä¾ããããã¾ã§ã«ä½æããã 4/50 NFTãï¼

**2\. ã¦ã¼ã¶ã¼ãééã£ããããã¯ã¼ã¯ä¸ã«ããã¨ãã¢ã©ã¼ããåºã**

- ããªãã® Web ãµã¤ãã¯ Rinkeby Test Network ã§**ã®ã¿**æ©è½ãã¾ãã
- ã¦ã¼ã¶ã¼ããRinkeby ä»¥å¤ã®ãããã¯ã¼ã¯ã«ã­ã°ã¤ã³ãã¦ããç¶æã§ãããªãã® Web ãµã¤ãã«æ¥ç¶ãããã¨ãããããããç¥ãããã¢ã©ã¼ããåºãã¾ãããã
- `ethereum.request` ã¨ `eth_accounts` ã¨ `eth_requestAccounts` ã¨ããã¡ã½ãããä½¿ç¨ãã¦ãã¢ã©ã¼ããä½æã§ãã¾ãã
- `eth_chainId` ãä½¿ã£ã¦ãã­ãã¯ãã§ã¼ã³ãè­å¥ãã ID ãåå¾ãã¾ãã

ä¸è¨ã®ã³ã¼ãã `NftUploader.jsx` ã«çµã¿è¾¼ãã§ã¿ã¾ãããã

```javascript
// NftUploader.jsx
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
- Rarible ã¸ã®ãªã³ã¯ã¯ `NftUploader.jsx` ã«ãã¼ãã³ã¼ãã£ã³ã°ããå¿è¦ãããã¾ãã

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
