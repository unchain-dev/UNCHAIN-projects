### ð  è³éãå¼ãåºãæ©è½ãå®è£ãã

ååã¾ã§ã§ã¹ãã¼ãã³ã³ãã©ã¯ããããã­ã¤ããã¦ã¼ã¶ã¼ããã¡ã¤ã³ãä½æã§ããããã«ããReactãã¼ã¹ã®Webã¢ããªã±ã¼ã·ã§ã³ãä½æãã¦ãã¾ããã

ããã§ãã®æåãª Bored Ape ãè³¼å¥ãããã¼ã ã 1 æ¥ä¸­ Twitter ã«æç¨¿ãããã¨ãã§ãã¾ãã

ãããã¾ã ã§ããªããã¨ãããã¾ãã

ã¾ã **è³éãå¼ãåºã**æ¹æ³ãä½æã§ãã¦ããªãããã§ãã

ã§ã¯ãäººãããã¡ã¤ã³ã«æ¯æã£ã¦ããããã¼ã¯ã³ã«ã©ã®ããã«ã¢ã¯ã»ã¹ã§ããã§ããããï¼

### ð» é¢æ°ä¿®é£¾å­ã¨æ¤åé¢æ°

ãã®æ©è½ãè¿½å ããããã«ã³ã³ãã©ã¯ãï¼ã¤ã¾ãããã¯ã¨ã³ãå´ã§ãï¼ãä¿®æ­£ãã¦ããã¾ãããã

`Domains.sol`ã«ä»¥ä¸ãè¿½å ãã¾ãã

```solidity
// Domains.sol
modifier onlyOwner() {
  require(isOwner());
  _;
}

function isOwner() public view returns (bool) {
  return msg.sender == owner;
}

function withdraw() public onlyOwner {
  uint amount = address(this).balance;

  (bool success, ) = msg.sender.call{value: amount}("");
  require(success, "Failed to withdraw Matic");
}
```

ç¾å¨ãã¨ã©ã¼ãçºçãã¦ããå¯è½æ§ãããã¾ãã

ã§ãå¿éããªãã§ãã ãããäºæ³éãã§ãã

åã«é²ãã§ããããå°ãåè§£ãã¾ãããï¼

æåã«ä½æããã®ã¯é¢æ°`modifier`ã§ãã ããã«ãããé¢æ°ã®åä½ãå¤æ´ã§ãã¾ãã

`require`ã¹ãã¼ãã¡ã³ããå®è£ããããã®ä¾¿å©ãªææ³ã§ãã

ãã®ä¿®é£¾å­ãè¡ãã®ã¯ã `isOwner()`é¢æ°ã`true`ãè¿ããã¨ã ãã§ãã `true`ã§ãªãå ´åããã®ä¿®é£¾å­ã§å®£è¨ãããé¢æ°ã¯å®è¡ã§ãã¾ããã

åè¦ã§ä¸æè­°ã«æããé¨åã¯æå¾ã®`_;`ã§ããããmodifierä¿®é£¾å­ãä½¿ç¨ããé¢æ°ã¯ãrequireã®**å¾ã«**å®è¡ããå¿è¦ãããã¾ãã`_;`ãrequireã®åã«ããå ´åãwithdrawé¢æ°ãæåã«å¼ã³åºãããæ¬¡ã«requireãå¼ã³åºããããã¨ã«ãªãã¾ããããã§ã¯requireãå½¹ã«ç«ã¡ã¾ããã

`_;`ãè¨è¼ãããã¨ã§ããã®å¾ã®å¦çãç¶è¡ããã¨ããæå³ã«ãªãã¾ãã

`withdraw()`é¢æ°ã«é¢ãã¦ã¯ãã³ã³ãã©ã¯ãã®æ®é«ãåå¾ããããããªã¯ã¨ã¹ã¿ã¼ï¼é¢æ°ãå®è¡ããããã«ã¯ææèã§ããå¿è¦ãããã¾ãï¼ã«éä¿¡ãããã¨ã ãã§ãã ããã¯è³éãå¼ãåºãã®ã«ç°¡åãªææ³ã§ãã `msg.sender.call {valueï¼amount}(" ")`ã¯ãééããããã®æ¸ãæ¹ã§ãã æ§æã¯å°ãå¥å¦ã§ãã `amount`ãæ¸¡ãæ¹æ³ã«æ³¨ç®ãã¦ãã ããã `require(success`ã¯ããã©ã³ã¶ã¯ã·ã§ã³ãæåãããã¨ãæ³å®ãããã¨ããã§ãã æåããªãå ´åã¯ããã©ã³ã¶ã¯ã·ã§ã³ãã¨ã©ã¼ã¨ãã¦èªè­ãã`"Failed to withdraw Matic"`ã¨è¡¨ç¤ºãã¾ãã

### ð¤  ã³ã³ãã©ã¯ããªã¼ãã¼ã®è¨­å®

åä»ãª`owner`ã¨ã©ã¼ãä¿®æ­£ããã«ã¯ãã³ã³ãã©ã¯ãã®åé ­ã«ã°ã­ã¼ãã«ãª`owner`å¤æ°ãä½æããæ¬¡ã®ããã«ã³ã³ã¹ãã©ã¯ã¿ã¼ã«è¨­å®ããã ãã§ãã

```solidity
// Domains.sol
address payable public owner;

constructor(string memory _tld) ERC721 ("Ninja Name Service", "NNS") payable {
  owner = payable(msg.sender);
  tld = _tld;
  console.log("%s name service deployed", _tld);
}
```

éè¦ãªç¹ã¯ã`payable`ã¿ã¤ãã¨ãã¦è¨­å®ãããã¨ã§ãã ããã¯ãææèã®`address`ãæ¯æããåãåããã¨ãã§ãããã¨ãæå³ããæç¤ºçã«å®£è¨ããå¿è¦ãããã¾ãã è©³ç´°ã«ã¤ãã¦ã¯ã[ãã¡ã](https://solidity-by-example.org/payable/)ããåç§ãã ããã

ããã§ã³ã³ãã©ã¯ãã«ããè³éãå¼ãåºããã¨ãã§ãã¾ãã


### ð¦ ãã¹ããã¦ã¿ã¾ããã

`run.js`ã¹ã¯ãªãããè¨­å®ãã¾ãã

```javascript
// run.js
const main = async () => {
  const [owner, superCoder] = await hre.ethers.getSigners();
  const domainContractFactory = await hre.ethers.getContractFactory('Domains');
  const domainContract = await domainContractFactory.deploy("ninja");
  await domainContract.deployed();

  console.log("Contract owner:", owner.address);

  // ä»åã¯å¤é¡ãè¨­å®ãã¦ãã¾ãã
  let txn = await domainContract.register("a16z",  {value: hre.ethers.utils.parseEther('1234')});
  await txn.wait();

  // ã³ã³ãã©ã¯ãã«ãããããããç¢ºèªãã¦ãã¾ãã
  const balance = await hre.ethers.provider.getBalance(domainContract.address);
  console.log("Contract balance:", hre.ethers.utils.formatEther(balance));

  // ã¹ã¼ãã¼ã³ã¼ãã¼ã¨ãã¦ã³ã³ãã©ã¯ãããè³éãå¥ªããã¨ãã¾ãã
  try {
    txn = await domainContract.connect(superCoder).withdraw();
    await txn.wait();
  } catch(error){
    console.log("Could not rob contract");
  }

  // å¼ãåºãåã®ã¦ã©ã¬ããã®æ®é«ãç¢ºèªãã¾ãããã¨ã§æ¯è¼ãã¾ãã
  let ownerBalance = await hre.ethers.provider.getBalance(owner.address);
  console.log("Balance of owner before withdrawal:", hre.ethers.utils.formatEther(ownerBalance));

  // ãªã¼ãã¼ãªãå¼ãåºããã§ãããã
  txn = await domainContract.connect(owner).withdraw();
  await txn.wait();

  // contract ã¨ owner ã®æ®é«ãç¢ºèªãã¾ãã
  const contractBalance = await hre.ethers.provider.getBalance(domainContract.address);
  ownerBalance = await hre.ethers.provider.getBalance(owner.address);

  console.log("Contract balance after withdrawal:", hre.ethers.utils.formatEther(contractBalance));
  console.log("Balance of owner after withdrawal:", hre.ethers.utils.formatEther(ownerBalance));
}

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

ãã®ã¹ã¯ãªããã`npx hardhat run scripts/run.js`ã§å®è¡ããã¨ãçã¿åããã¨ãããã¨ããã­ãã¯ããã¦catch errorãä½ç¨ãããã¨ããããã¨æãã¾ãã

```
% npx hardhat run scripts/run.js
Compiled 1 Solidity file successfully
ninja name service deployed
Contract owner: 0x---------
Registering a16z.ninja on the contract with tokenID 0

Contract balance: 1234.0
Could not rob contract
Balance of owner before withdrawal: 8765.98283853524900992
Contract balance after withdrawal: 0.0
Balance of owner after withdrawal: 9999.982788363651247088
```

ããã§ä½ãèµ·ãã£ã¦ããã®ãã¨ããã¨ã `withdraw()`é¢æ°ãã©ã³ãã ãªäººç©`superCoder`ã¨ãã¦å¼ã³åºãã¨ã`modifier`ã¯ç§ãã¡ãææèã§ã¯ãªããã¨ãç¢ºèªãããã©ã³ã¶ã¯ã·ã§ã³ãåã«æ»ãã¾ãã

ããããç§ãã¡ã`owner`ã¨ãã¦è¡ãã¨æ¯æããããã¾ãã

ãã®ããã«å¿è¦ã«å¿ãã¦ãtry catchãä½¿ã£ã¦ã³ã³ãã©ã¯ãã®åå®¹ãç¢ºèªã§ãã¾ãã

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
ãç²ãæ§ã§ãã!! ä¸ä¼ã¿ãã¦ããã§ãæ¬¡ã®ã¬ãã¹ã³ã«é²ã¿ã¾ãããð
