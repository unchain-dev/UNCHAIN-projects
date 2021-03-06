### ðª IPFS ãä½¿ãã

IPFS ã«åçãã¢ããã­ã¼ãã§ããã¨ããã§ããã®åçãä½¿ã£ã¦NFTãä½ã£ã¦ã¿ã¾ãããã

`Web3Mint.sol` ãä¸è¨ã®ããã«æ´æ°ãã¦ã¿ã¾ãããã

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

    NftAttributes[] Web3Nfts;

    using Counters for Counters.Counter;
    // tokenIdã¯NFTã®ä¸æãªè­å¥å­ã§ã0, 1, 2, .. N ã®ããã«ä»ä¸ããã¾ãã
    Counters.Counter private _tokenIds;

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

è§£èª¬ãã¦ããã¾ããã

```solidity
// Web3Mint.sol
import "./libraries/Base64.sol";
```
`tokenURI` ã«ã¯ãNFTãã¼ã¿ã JSON å½¢å¼ã§æ¸¡ããªããã°ããã¾ããã
Base64 ã®ããæ¹ã¯ã[project3](https://unchain-portal.netlify.app/projects/104-ETH-NFT-game/section-1-Lesson-5) ã®ããæ¹ãåèã«ãã¦ãã¾ãã

ãªããBase64 ã§æ¸¡ãå¿è¦ãããã®ããèª¿ã¹ã¦ã¿ã¦ãã ãã!

`libraries` ãã£ã¬ã¯ããªã®ä¸ã« `Base64.sol` ãã¡ã¤ã«ãä½æãã¦ãä¸è¨ã®ã³ã¼ããè²¼ãä»ãã¦ãã ãã

```solidity
// Base64.sol
// SPDX-License-Identifier: MIT

pragma solidity ^0.8.9;

/// [MIT License]
/// @title Base64
/// @notice Provides a function for encoding some bytes in base64
/// @author Brecht Devos <brecht@loopring.org>
library Base64 {
    bytes internal constant TABLE =
        "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/";

    /// @notice Encodes some bytes to the base64 representation
    function encode(bytes memory data) internal pure returns (string memory) {
        uint256 len = data.length;
        if (len == 0) return "";

        // multiply by 4/3 rounded up
        uint256 encodedLen = 4 * ((len + 2) / 3);

        // Add some extra buffer at the end
        bytes memory result = new bytes(encodedLen + 32);

        bytes memory table = TABLE;

        assembly {
            let tablePtr := add(table, 1)
            let resultPtr := add(result, 32)

            for {
                let i := 0
            } lt(i, len) {

            } {
                i := add(i, 3)
                let input := and(mload(add(data, i)), 0xffffff)

                let out := mload(add(tablePtr, and(shr(18, input), 0x3F)))
                out := shl(8, out)
                out := add(
                    out,
                    and(mload(add(tablePtr, and(shr(12, input), 0x3F))), 0xFF)
                )
                out := shl(8, out)
                out := add(
                    out,
                    and(mload(add(tablePtr, and(shr(6, input), 0x3F))), 0xFF)
                )
                out := shl(8, out)
                out := add(
                    out,
                    and(mload(add(tablePtr, and(input, 0x3F))), 0xFF)
                )
                out := shl(224, out)

                mstore(resultPtr, out)

                resultPtr := add(resultPtr, 4)
            }

            switch mod(len, 3)
            case 1 {
                mstore(sub(resultPtr, 2), shl(240, 0x3d3d))
            }
            case 2 {
                mstore(sub(resultPtr, 1), shl(248, 0x3d))
            }

            mstore(result, encodedLen)
        }

        return string(result);
    }
}
```

æ¬¡ã¯ãä¸è¨ã®ã³ã¼ããè§£èª¬ãã¾ãã

```solidity
struct NftAttributes{
        string name;
        string imageURL;
    }

    NftAttributes[] Web3Nfts;
```
æåã«æ¸ãã¦ãã NFT ã®ãã¼ã¿ãä¿å­ããããã®éåãããã§ãã
ãã®éåã®çªå·ã¨ãNFT  ã®è­å¥å­ã®çªå·ãæãã¾ãã

ä¾ãã°ã0 çªç®ã®è­å¥å­ã®NFTã®ãã¼ã¿ã¯ã`Web3Nfts` ã®éåã® 0 çªç®ã«å¥ãããã«ããã¨ãã£ããããªæãã§ãã

æ¬¡ã¯ mintIpfsNFT é¢æ°ã§ãã

```solidity
// Base64.sol
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
```

åç¨ã®ã³ã¼ããã `setTokenURI` é¢æ°ãæ¶ããä»£ããã«ä¸è¨ã®ã³ã¼ããè¿½å ããã¦ãã¾ãã

```solidity
// Base64.sol
Web3Nfts.push(NftAttributes({
            name: name,
            imageURL: imageURI
        }));
```
`mintIpfsNFT` é¢æ°ãå¼æ°ã§ãNFTã«ããããã®ã®ãã¼ã¿ãåãåããããã§éåã«å ãã¾ãã`tokenId` ã®å¤ã¨ãéåã®çªå·ã¯åãã«ãªã£ã¦ãã¾ãã

æ¬¡ã¯ `tokenURI` é¢æ°ã§ãã
```solidity
// Base64.sol
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
```
opensea ãªã©ã® NFT ãã¼ã±ãããµã¼ãã¹ã¯ããã® `tokenURI` é¢æ°ã®ãã¼ã¿ãã¿ã¦ãã¾ãã
è©³ããç¥ãããæ¹ã¯ [ãã¡ã](https://docs.opensea.io/docs/metadata-standards#implementing-token-uri) ãããããã ããã

>For OpenSea to pull in off-chain metadata for ERC721 and ERC1155 assets, your contract will need to return a URI where we can find the metadata. > To find this URI, we use the tokenURI method in ERC721 and the uri method in ERC1155

`tokenURI` é¢æ°ã¯ ERC721 ãã override ãã¦ããé¢æ°ã§ãå¤é¨ããã§ã `_tokenId` ããããã° return ãè¿ãã¦ãããé¢æ°ã§ãªãã¨ãããªãã®ã§ãå¼æ°ãªã©ãã NFT ã®ã¡ã¿ãã¼ã¿ãéããã¨ã¯ã§ãã¾ããããªã®ã§ã`tokenId` ã ããä¸ãããã¦ãNFT ã® metadata ãè¿ããããã«ããªããã°ãªããªãã§ãã
ããã§ãéåãä½¿ããã¨ããçºæ³ã«ãªã£ã¦ãã¾ãã

æ¬¡ã¯ããã®ã³ã¼ãããã£ããã¨åãã¦ãããç¢ºèªããããã«ãã¹ãã³ã¼ããæ¸ãã¦ã¿ã¾ãããã

`ipfs-nfts/test` ã®ãã£ã¬ã¯ããªã« `Web3Mint.js` ã®ãã¡ã¤ã«ãè¿½å ãã¦ãä¸è¨ã®ã³ã¼ããã³ãã¼ãã¦ãã ããã

`scripts/run.js` ã§ãã¹ããè¡ã£ã¦ãããã®ã§ãããããã¯ã­ã¼ã«ã«ç°å¢ã«ããã­ã¤ãã¦ãããããã¯ãå°ãæéãæããã®ã§ãèªåã§ãã¹ãã³ã¼ããæ¸ãã¨ãã«ã¯ããã¹ããããã¨ãå¤ãã§ãããããä¸è¨ã®ããã«ãã¹ããè¡ããã¨ããããããã¾ãã

```javascript
// Web3Mint.js
const { expect } = require("chai");
const { ethers } = require("hardhat");


describe("Web3Mint",  () => {
    it("Should return the nft", async () => {
      const Mint = await ethers.getContractFactory("Web3Mint");
      const mintContract = await Mint.deploy();
      await mintContract.deployed();

      const [owner, addr1] = await ethers.getSigners();

      let nftName = 'poker'
      let ipfsCID = 'bafkreievxssucnete4vpthh3klylkv2ctll2sk2ib24jvgozyg62zdtm2y'

      await mintContract.connect(owner).mintIpfsNFT(nftName,ipfsCID) //0
      await mintContract.connect(addr1).mintIpfsNFT(nftName,ipfsCID) //1

      console.log(await mintContract.tokenURI(0))
      console.log(await mintContract.tokenURI(1))


    });
  });
```

ãã®ãã¹ãã³ã¼ãã®æ¸ãæ¹ã«é¢ãã¦ã¯ã[hardhatãç¨æãã¦ãããã­ã¥ã¡ã³ã](https://hardhat.org/guides/waffle-testing.html)ãéå¸¸ã«åèã«ãªãã¾ãã
ethers.jsãä½¿ã£ãæ¸ãæ¹ã¯ä»ã¾ã§ããã¦ãã¦ããã®ã§ããã®èª¬æã¯çãã¾ãã

ä»åå®ã¯ã`expect` ã¨ããè¨æ³ãä½¿ã£ã¦ããªãã®ã§ã

```javascript
const { expect } = require("chai");
```
ãã®ããã« `chai` ãèª­ã¿è¾¼ãå¿è¦ã¯ãªãã®ã§ãããã¹ãã¼ãã³ã³ãã©ã¯ãã®ãã¹ããè¡ãä¸ã§ãå¿ã `expect` ãä½¿ãæ©ä¼ã¯æ¥ãã¯ããªã®ã§èå³ã®ããæ¹ã¯èª¿ã¹ã¦ã¿ã¦ãã ããã

ä»åãã®ãã¹ãã§ã¯ã`mintIpfsNFT` é¢æ°ã§ãã£ããã¨NFTãçºè¡ãã`tokenURI` ã®è¿ãå¤ãæå¾éãã«ãªã£ã¦ããããç¢ºããã¾ãã

å¤æ° `nftName` ã«ã¯å¥½ããªååãã`ipfsCID` ã«ã¯åç¨ã¤ãã£ã `IpfsCID` ãå¥ãã¦ã¿ã¾ããã!

ããã¾ã§ã®ä½æ¥­ãã§ããã`npx hardhat test`ããã¦ã¿ã¾ããã
```
Web3Mint
This is my NFT contract.
An NFT w/ ID 0 has been minted to 0xf39fd6e51aad88f6f4ce6ab8827279cfffb92266
An NFT w/ ID 1 has been minted to 0x70997970c51812dc3a010c7d01b50e0d17dc79c8
data:application/json;base64,eyJuYW1lIjogInBva2VyIC0tIE5GVCAjOiAwIiwgImRlc2NyaXB0aW9uIjogIkFuIGVwaWMgTkZUIiwgImltYWdlIjogImlwZnM6Ly9iYWZrcmVpZXZ4c3N1Y25ldGU0dnB0aGgza2x5bGt2MmN0bGwyc2syaWIyNGp2Z296eWc2MnpkdG0yeSJ9
data:application/json;base64,eyJuYW1lIjogInBva2VyIC0tIE5GVCAjOiAxIiwgImRlc2NyaXB0aW9uIjogIkFuIGVwaWMgTkZUIiwgImltYWdlIjogImlwZnM6Ly9iYWZrcmVpZXZ4c3N1Y25ldGU0dnB0aGgza2x5bGt2MmN0bGwyc2syaWIyNGp2Z296eWc2MnpkdG0yeSJ9
    â Should return the nft
```
ãã®ãããªã­ã°ãè¡¨ç¤ºãããã¯ãã§ãã
```
data:application/json;base64,eyJuYW1lIjogInBva2VyIC0tIE5GVCAjOiAwIiwgImRlc2NyaXB0aW9uIjogIkFuIGVwaWMgTkZUIiwgImltYWdlIjogImlwZnM6Ly9iYWZrcmVpZXZ4c3N1Y25ldGU0dnB0aGgza2x5bGt2MmN0bGwyc2syaWIyNGp2Z296eWc2MnpkdG0yeSJ9
```
ããããã©ã¦ã¶ã§è¡¨ç¤ºãã¦ãã ããã
```
{"name": "poker -- NFT #: 0", "description": "An epic NFT", "image": "ipfs://bafkreievxssucnete4vpthh3klylkv2ctll2sk2ib24jvgozyg62zdtm2y"}
```
ãã®ããã«è¡¨ç¤ºããã¦ãããæåã§ããimageã®ipfsããã£ããã¨ç»åãè¡¨ç¤ºããããã¦ããããç¢ºèªãã¦ã¿ã¦ãã ããã

**brave**ãã©ã¦ã¶ã§ã¯ã`ipfs://bafkreievxssucnete4vpthh3klylkv2ctll2sk2ib24jvgozyg62zdtm2y`ã®ã¾ã¾ãã©ã¦ã¶ã«è²¼ãã°è¡¨ç¤ºãããä»ã®ãã©ã¦ã¶ã®å ´åã¯`https:// ipfs.io/ipfs/èªåã®CID`ã®ããã«ãã¦ãç»åãç¢ºèªãã¦ã¿ã¾ããã!


æçµç¢ºèªã¨ãã¦ `run.js` ã§ãç¢ºèªãã¦ã¿ã¾ãããã

`run.js` ãä¸è¨ã«æ´æ°ãã¦ãã ããã

```javascript
// run.js
const main = async () => {
    // ã³ã³ãã©ã¯ããã³ã³ãã¤ã«ãã¾ã
    // ã³ã³ãã©ã¯ããæ±ãããã«å¿è¦ãªãã¡ã¤ã«ã `artifacts` ãã£ã¬ã¯ããªã®ç´ä¸ã«çæããã¾ãã
    const nftContractFactory = await hre.ethers.getContractFactory("Web3Mint");
    // Hardhat ãã­ã¼ã«ã«ã® Ethereum ãããã¯ã¼ã¯ãä½æãã¾ãã
    const nftContract = await nftContractFactory.deploy();
    // ã³ã³ãã©ã¯ãã Mint ãããã­ã¼ã«ã«ã®ãã­ãã¯ãã§ã¼ã³ã«ããã­ã¤ãããã¾ã§å¾ã¡ã¾ãã
    await nftContract.deployed();
    console.log("Contract deployed to:", nftContract.address);

    let txn = await nftContract.mintIpfsNFT("poker","bafybeibewfzz7w7lhm33k2rmdrk3vdvi5hfrp6ol5vhklzzepfoac37lry");
    await txn.wait();
    let returnedTokenUri = await nftContract.tokenURI(0);
    console.log("tokenURI:",returnedTokenUri);
  };
  // ã¨ã©ã¼å¦çãè¡ã£ã¦ãã¾ãã
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
`mintIpfsNft` é¢æ°ã¨ `tokenURI` é¢æ°ããã£ããã¨ã§ãã¦ããããç¢ºèªãã¾ãããã


ã¹ãã¼ãã³ã³ãã©ã¯ãã®é¢æ°ããã£ããã¨æ©è½ãã¦ãããã¨ãããã£ãã®ã§ããã¹ããããã«ããã­ã¤ãã¾ãããã

`deploy.js` ãä¸è¨ã®ããã«æ´æ°ãã¦ `npx hardhat run scripts/deploy.js` ããã¦ãã ããã

```javascript
// deploy.js
const main = async () => {
    // ã³ã³ãã©ã¯ããã³ã³ãã¤ã«ãã¾ã
    // ã³ã³ãã©ã¯ããæ±ãããã«å¿è¦ãªãã¡ã¤ã«ã `artifacts` ãã£ã¬ã¯ããªã®ç´ä¸ã«çæããã¾ãã
    const nftContractFactory = await hre.ethers.getContractFactory("Web3Mint");
    // Hardhat ãã­ã¼ã«ã«ã® Ethereum ãããã¯ã¼ã¯ãä½æãã¾ãã
    const nftContract = await nftContractFactory.deploy();
    // ã³ã³ãã©ã¯ãã Mint ãããã­ã¼ã«ã«ã®ãã­ãã¯ãã§ã¼ã³ã«ããã­ã¤ãããã¾ã§å¾ã¡ã¾ãã
    await nftContract.deployed();
    console.log("Contract deployed to:", nftContract.address);
    };
  // ã¨ã©ã¼å¦çãè¡ã£ã¦ãã¾ãã
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

ãã®ã³ã³ãã©ã¯ãã¢ãã¬ã¹ã¯ä»å¾ãä½¿ç¨ããã®ã§ä¿å­ãã¦ããã¦ãã ããã

### ðââï¸ è³ªåãã

ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã® `#section-1` ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã® 3 ç¹ãè¨è¼ãã¦ãã ãã â¨

```
1. è³ªåãé¢é£ãã¦ããã»ã¯ã·ã§ã³çªå·ã¨ã¬ãã¹ã³çªå·
2. ä½ããããã¨ãã¦ããã
3. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
4. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```

ããã§ã¨ããããã¾ã!Lesson2ã¯çµäºã§ããããªãã®IPFSã«ãããç»åãã³ãã¥ããã£ã§å±æãã¦ã¿ã¾ããã!
