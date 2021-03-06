### ð¶ Letâs write a contract

### ð¶ ã¹ãã¼ãã³ã³ãã©ã¯ããä½æãã¦ã¿ãã

ååããããããè¨­å®ããã¦ãããã¹ãã®ã³ã³ãã©ã¯ããå®è¡ã§ãã¾ããã

ã§ã¯ããããèªåã§ã³ã³ãã©ã¯ããä½æãã¦ããã¾ãããã

`contracts` ãã£ã¬ã¯ããªã®ä¸ã« `Domains.sol` ã¨ããååã®ãã¡ã¤ã«ãä½æãã¾ãã

ã¿ã¼ããã«ä¸ã§æ°ãããã¡ã¤ã«ãä½æããå ´åã¯ãä¸è¨ã®ã³ãã³ããå½¹ç«ã¡ã¾ãã

1. `cool-domains` ãã£ã¬ã¯ããªã«ç§»å: `cd cool-domains`
2. `contracts` ãã£ã¬ã¯ããªã«ç§»å: `cd contracts`
3. `Domains.sol` ãã¡ã¤ã«ãä½æ: `touch Domains.sol`

Hardhat ãä½¿ç¨ããå ´åããã¡ã¤ã«æ§é ã¯éå¸¸ã«éè¦ã§ãã®ã§ãæ³¨æããå¿è¦ãããã¾ãããã¡ã¤ã«æ§é ãä¸è¨ã®ããã«ãªã£ã¦ããã°å¤§ä¸å¤«ã§ã ð

```bash
cool-domains
    |_ contracts
           |_  Domains.sol
```

æ¬¡ã«ãã³ã¼ãã¨ãã£ã¿ã§ãã­ã¸ã§ã¯ãã®ã³ã¼ããéãã¾ãã

ããã§ã¯ãVS Code ã®ä½¿ç¨ããå§ããã¾ãããã¦ã³ã­ã¼ãã¯ [ãã¡ã](https://azure.microsoft.com/ja-jp/products/visual-studio-code/) ããã

VS Code ãã¿ã¼ããã«ããèµ·åããæ¹æ³ã¯ [ãã¡ã](https://maku.blog/p/f5iv9kx/) ããè¦§ãã ããã

- ã¿ã¼ããã«ä¸ã§ã`code .` ã³ãã³ããå®è¡

ä»å¾ VS Code ãèµ·åããã®ãä¸æ®µã¨æ¥½ã«ãªãã®ã§ããã²å°å¥ãã¦ã¿ã¦ãã ããã

ã³ã¼ãã£ã³ã°ã®ãµãã¼ããã¼ã«ã¨ãã¦ãVS Code ä¸ã§ Solidity ã®æ¡å¼µæ©è½ããã¦ã³ã­ã¼ããããã¨ããå§ããã¾ãã

ãã¦ã³ã­ã¼ãã¯ [ãã¡ã](https://marketplace.visualstudio.com/items?itemName=JuanBlanco.solidity) ããã

ããã§ã¯ããããã `Domains.sol` ã®ä¸­èº«ã®ä½æãã¦ããã¾ãã

`Domains.sol` ã VS Code ã§éããä¸è¨ãå¥åãã¾ãã

```solidity
// Domains.sol
// SPDX-License-Identifier: UNLICENSED

pragma solidity ^0.8.9;

import "hardhat/console.sol";

contract Domains {
  constructor() {
    console.log("THIS IS MY DOMAINS CONTRACT. NICE.");
  }
}
```
ã³ã¼ããè©³ããã¿ã¦ããã¾ãããã

```solidity
// Domains.sol
// SPDX-License-Identifier: UNLICENSED
```

ããã¯ãSPDX ã©ã¤ã»ã³ã¹è­å¥å­ãã¨å¼ã°ããã½ããã¦ã§ã¢ã»ã©ã¤ã»ã³ã¹ã®ç¨®é¡ãä¸ç®ã§ãããããã«ããããã®è­å¥å­ã§ãã

è©³ç´°ã«ã¤ãã¦ã¯ã[ãã¡ã](https://www.skyarch.net/blog/?p=15940) ãåç§ãã¦ã¿ã¦ãã ããã

```solidity
// Domains.sol
pragma solidity ^0.8.9;
```

ããã¯ãã³ã³ãã©ã¯ãã§ä½¿ç¨ãã Solidity ã³ã³ãã¤ã©ã®ãã¼ã¸ã§ã³ã§ãã

ä¸è¨ã®ã³ã¼ãã§ã¯ããã®ã³ã³ãã©ã¯ããå®è¡ããã¨ãã¯ Solidity ã³ã³ãã¤ã©ã®ãã¼ã¸ã§ã³ `0.8.9` ã®ã¿ãä½¿ç¨ãããä»¥ä¸ã®ãã®ã¯ä½¿ç¨ãã¾ãããã¨ããå®£è¨ããã¦ãã¾ãã

ã³ã³ãã¤ã©ã®ãã¼ã¸ã§ã³ã `hardhat.config.js` ã§åãã§ãããã¨ãç¢ºèªãã¦ãã ããã

ããè¨è¼ããã¦ãã Solidity ã®ãã¼ã¸ã§ã³ã`0.8.9` ã§ãªãã£ãå ´åã¯ã`Domains.sol`ã®ä¸­èº«ã`hardhat.config.js` ã«è¨è¼ããã¦ãããã¼ã¸ã§ã³ã«å¤æ´ãã¾ãããã

```solidity
// Domains.sol
import "hardhat/console.sol";
```
ã³ã³ãã©ã¯ããå®è¡ããéãã³ã³ã½ã¼ã«ã­ã°ãã¿ã¼ããã«ã«åºåããããã« Hardhat ã® `console.sol` ã®ãã¡ã¤ã«ãã¤ã³ãã¼ããã¦ãã¾ãã

ããã¯ãä»å¾ã¹ãã¼ãã³ã³ãã©ã¯ãã®ãããã°ãçºçããå ´åã«ãã¨ã¦ãå½¹ç«ã¤ãã¼ã«ã§ãã


```solidity
// Domains.sol
contract Domains{
    constructor() {
        console.log("THIS IS MY DOMAIN CONTRACT. NICE.");
    }
}

```

`contract` ã¯ãã»ãã®è¨èªã§ããã¨ããã®ã[class](https://wa3.i-3-i.info/word1120.html)ãã®ãããªãã®ãªã®ã§ãã

ãã® `contract` ãåæåããã¨ã`constructor` ãå®è¡ããã¦ `console.log` ã®ä¸­èº«ãã¿ã¼ããã«ä¸ã«è¡¨ç¤ºããã¾ãã

class ã®æ¦å¿µã«ã¤ãã¦ã¯ã[ãã¡ã](https://aiacademy.jp/media/?p=131) ãåç§ãã¦ãã ããã

### ð© constructor ã¨ã¯

`constructor` ã¯ãªãã·ã§ã³ã®é¢æ°ã§ã`contract` ã®ç¶æå¤æ°ãåæåããããã«ä½¿ç¨ããã¾ãã

ããããè©³ããèª¬æãã¦ããã®ã§ã`constructor` ã«é¢ãã¦ã¯ãã¾ãä»¥ä¸ã®ç¹å¾´ãçè§£ãã¦ãã ããã

- `contract` ã¯ 1 ã¤ã® `constructor` ããæã¤ãã¨ãã§ãã¾ããã
- `constructor` ã¯ãã¹ãã¼ãã³ã³ãã©ã¯ãã®ä½ææã«ä¸åº¦ã ãå®è¡ããã`contract` ã®ç¶æãåæåããããã«ä½¿ç¨ããã¾ãã
- `constructor` ãå®è¡ãããå¾ãã³ã¼ãããã­ãã¯ãã§ã¼ã³ã«ããã­ã¤ããã¾ãã
### ð²Â ã³ã³ãã©ã¯ããå®è¡ãã¾ããã

ãããã¹ãã¼ãã³ã³ãã©ã¯ããä½æãã¾ããã

ããããã¾ã ãããæ©è½ãããã©ããã¯ãããã¾ããã

å®éã«å®è¡ãã¦ã¿ã¾ããããæ¬¡ã®ãããªæé ã¨ãªãã¾ãã

1. `Domains.sol` ãã³ã³ãã¤ã«ãã¾ãã
2. `Domains.sol` ãã­ã¼ã«ã«ç°å¢ã§ãã­ãã¯ãã§ã¼ã³ä¸ã«ããã­ã¤ãã¾ãã
3. ä¸è¨ãå®äºãããã`console.log` ã®ä¸­èº«ãã¿ã¼ããã«ä¸ã«è¡¨ç¤ºããããã¨ãç¢ºèªãã¾ãã
### ð ã³ã³ãã©ã¯ããå®è¡ããããã®ãã­ã°ã©ã ãä½æãã

åã«æãã3ã¤ã®ã¹ããããå¦çããã¹ã¯ãªãããä½æãã¾ãã

`scripts` ãã£ã¬ã¯ããªã«ç§»åãã`run.js` ã¨ããååã®ãã¡ã¤ã«ãä½æãã¦ãã ããã

**`run.js` ã¯ã­ã¼ã«ã«ç°å¢ã§ã¹ãã¼ãã³ã³ãã©ã¯ãã®ãã¹ããè¡ãããã®ãã­ã°ã©ã ã§ãã**

`run.js` ã®ä¸­èº«ã«ãä»¥ä¸ãè¨å¥ãã¾ãããã

```javascript
// run.js
const main = async () => {
  const domainContractFactory = await hre.ethers.getContractFactory('Domains');
  const domainContract = await domainContractFactory.deploy();
  await domainContract.deployed();
  console.log("Contract deployed to:", domainContract.address);
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

ããã§ã¯ã1 è¡ãã¤ã³ã¼ãã®çè§£ãæ·±ãã¾ãããã

```javascript
// run.js
const domainContractFactory = await hre.ethers.getContractFactory('Domains');
```

ããã«ããã`Domains` ã³ã³ãã©ã¯ããã³ã³ãã¤ã«ããã¾ãã

ã³ã³ãã©ã¯ããã³ã³ãã¤ã«ãããããã³ã³ãã©ã¯ããæ±ãããã«å¿è¦ãªãã¡ã¤ã«ã `artifacts` ãã£ã¬ã¯ããªã®ç´ä¸ã«çæããã¾ãã

> âï¸: `hre.ethers.getContractFactory` ã«ã¤ãã¦
> `getContractFactory` é¢æ°ã¯ãããã­ã¤ããµãã¼ãããã©ã¤ãã©ãªã®ã¢ãã¬ã¹ã¨ `Domains` ã³ã³ãã©ã¯ãã®é£æºãè¡ã£ã¦ãã¾ãã
>
> `hre.ethers` ã¯ãHardhat ãã©ã°ã¤ã³ã®ä»æ§ã§ãã

> âï¸: `const main = async ()` ã¨ `await` ã«ã¤ãã¦
> Javascript ã§ã³ã¼ããæ¸ãã¦ããã¨ãã³ã¼ãã®ä¸ããé ã«å®è¡ãããªãã¦å°ããã¨ãããã¾ãããããéåæå¦çã«é¢ããåé¡ã¨ããã¾ãã
>
> è§£æ±ºæ³ã®ä¸ã¤ã¨ãã¦ãããã§ã¯ `async` / `await` ãä½¿ç¨ãã¾ãã
>
> ãããä½¿ãã¨ã`await` ãåé ­ã«ã¤ãã¦ããå¦çãçµããã¾ã§ã`main` é¢æ°ã®ä»ã®å¦çã¯è¡ããã¾ããã
>
> ã¤ã¾ãã`hre.ethers.getContractFactory("Domains")` ã®å¦çãçµããã¾ã§ã`main` é¢æ°ã®ä¸­ã«è¨è¼ããã¦ããä»ã®å¦çã¯å®è¡ãããªãã¨ãããã¨ã§ãã

æ¬¡ã«ãä¸è¨ã®å¦çãè¦ã¦ããã¾ãããã

```javascript
// run.js
const domainContract = await domainContractFactory.deploy();
```

Hardhat ãã­ã¼ã«ã«ã® Ethereum ãããã¯ã¼ã¯ããã³ã³ãã©ã¯ãã®ããã ãã«ä½æãã¾ãã

ããã¦ãã¹ã¯ãªããã®å®è¡ãå®äºããå¾ããã®ã­ã¼ã«ã«ã»ãããã¯ã¼ã¯ãç ´æ£ãã¾ãã

ã¤ã¾ããã³ã³ãã©ã¯ããå®è¡ãããã³ã«ãæ¯åã­ã¼ã«ã«ãµã¼ããæ´æ°ãããã®ããã«ãã­ãã¯ãã§ã¼ã³ãæ°ãããªãã¾ãã

- å¸¸ã«ã¼ã­ãªã»ããã¨ãªãã®ã§ãã¨ã©ã¼ã®ãããã°ããããããªãã¾ãã

æ¬¡ã«ä¸è¨ã®å¦çãè¦ã¦ããã¾ãããã

```javascript
// run.js
await domainContract.deployed();
```

ããã§ã¯ã`Domains` ã³ã³ãã©ã¯ãããã­ã¼ã«ã«ã®ãã­ãã¯ãã§ã¼ã³ã«ããã­ã¤ãããã¾ã§å¾ã¤å¦çãè¡ã£ã¦ãã¾ãã

Hardhat ã¯å®éã«ããªãã®ãã·ã³ä¸ã«ããã¤ãã¼ããä½æãããã­ãã¯ãã§ã¼ã³ãæ§ç¯ãã¦ããã¾ãã

`constructor` ã¯ãã¹ãã¼ãã³ã³ãã©ã¯ããããã­ã¤ãããã¨ãã«åãã¦å®è¡ããã¾ãã

```javascript
// run.js
console.log("Contract deployed to:", domainContract.address);
```

æå¾ã«ãããã­ã¤ãããã¨ã`domainContract.address` ã¯ããã­ã¤ãããã¹ãã¼ãã³ã³ãã©ã¯ãã®ã¢ãã¬ã¹ãåºåãã¾ãã

ãã®ã¢ãã¬ã¹ããããã­ãã¯ãã§ã¼ã³ä¸ã§ã¹ãã¼ãã³ã³ãã©ã¯ããè¦ã¤ãããã¨ãã§ãã¾ãããä»åã¯ã­ã¼ã«ã«ã®ã¤ã¼ãµãªã¢ã ãããã¯ã¼ã¯ï¼ï¼ãã­ãã¯ãã§ã¼ã³ï¼ã«å®è£ãã¦ãããããä¸çä¸­ã®äººãã¢ã¯ã»ã¹ã§ããããã§ããã¾ããã

ä¸æ¹ãã¤ã¼ãµãªã¢ã ãããªã´ã³ã®ãã­ãã¯ãã§ã¼ã³ã«ããã­ã¤ãã¦ããã°ãä¸çä¸­ã®èª°ã§ãã³ã³ãã©ã¯ãã«ã¢ã¯ã»ã¹ã§ãã¾ãã

å®éã®ãã­ãã¯ãã§ã¼ã³ä¸ã«ã¯ããã§ã«ä½ç¾ä¸ãã®ã¹ãã¼ãã³ã³ãã©ã¯ããããã­ã¤ããã¦ãã¾ãã

ã¢ãã¬ã¹ãããããã°ãä¸çä¸­ã©ãã«ãã¦ããç§ãã¡ãèå³ãæã£ã¦ããã¹ãã¼ãã³ã³ãã©ã¯ãã«ç°¡åã«ã¢ã¯ã»ã¹ã§ãã¾ãã

### ð¨Â å®è¡ãã¦ã¿ãã

ã¿ã¼ããã«ä¸ã§ãä¸è¨ãå®è¡ãã¦ã¿ã¾ãããã

```bash
npx hardhat run scripts/run.js
```

ã¿ã¼ããã«ä¸ã§ `console.log` ã®ä¸­èº«ã¨ã³ã³ãã©ã¯ãã¢ãã¬ã¹ãè¡¨ç¤ºããã¦ãããã¨ãç¢ºèªãã¦ãã ããã

ä¾ï¼ã¿ã¼ããã«ä¸ã§ã®ã¢ã¦ãããã:

```bash
Compiled 1 Solidity file successfully
THIS IS MY DOMAINS CONTRACT. NICE.
Contract deployed to: 0x5FbDB2315678afecb367f032d93F642f64180aa3
```

### ð© Hardhat Runtime Environment ã«ã¤ãã¦

`run.js` ã®ä¸­ã§ã`hre.ethers` ãç»å ´ãã¾ãã

ãããã`hre` ã¯ã©ãã«ãã¤ã³ãã¼ãããã¦ãã¾ãããããã¯ãªãã§ããããï¼

ããã¯ããã°ããHardhat ã Hardhat Runtime Environmentï¼HREï¼ãå¼ã³åºãã¦ããããã§ãã

HRE ã¯ãHardhat ãç¨æãããã¹ã¦ã®æ©è½ãå«ããªãã¸ã§ã¯ãï¼ï¼ã³ã¼ãã®æï¼ã§ãã

`hardhat` ã§å§ã¾ãã¿ã¼ããã«ã³ãã³ããå®è¡ãããã³ã«ãHRE ã«ã¢ã¯ã»ã¹ãã¦ããã®ã§ã`hre` ã `run.js` ã«ã¤ã³ãã¼ãããå¿è¦ã¯ããã¾ããã

è©³ããã¯ã[Hardhat å¬å¼ãã­ã¥ã¡ã³ãï¼è±èªï¼](https://hardhat.org/advanced/hardhat-runtime-environment.html) ã«ã¦ç¢ºèªã§ãã¾ãã

### ðââï¸ è³ªåãã

ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã® `#section-1` ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã® 3 ç¹ãè¨è¼ãã¦ãã ãã â¨

```
1. è³ªåãé¢é£ãã¦ããã»ã¯ã·ã§ã³çªå·ã¨ã¬ãã¹ã³çªå·
2. ä½ããããã¨ãã¦ããã
3. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
4. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```

---

ã¿ã¼ããã«ä¸ã« `console.log` ã®ä¸­èº«ã¨ã³ã³ãã©ã¯ãã¢ãã¬ã¹ãåºåã§ããããæ¬¡ã®ã¬ãã¹ã³ã«é²ãã§ãã ãã ð
