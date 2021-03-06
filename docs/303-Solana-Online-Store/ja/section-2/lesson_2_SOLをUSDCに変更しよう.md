### ð¤ SOL ãã USDC ã«å¤æ´ãã

USDC ã®ãã©ã³ã¶ã¯ã·ã§ã³ã¯ SOL ã®ãã©ã³ã¶ã¯ã·ã§ã³ã¨éå¸¸ã«ããä¼¼ã¦ãã¾ãã

ããã§ã®å¤æ´ç¹ã¯ããã©ã³ã¶ã¯ã·ã§ã³é¢æ°ã§å¥ã®ã¿ã¤ãã®å½ä»¤ãå¼ã³åºããã¨ã§ãã

ã¾ãã[ãã](https://spl-token-faucet.com/?token-name=USDC)ã§ãSolana ä¸ã§å±éããã¦ãã devnet ç¨ã® USDC ãã¼ã¯ã³åãåã£ã¦ãã ããã

ã¦ã©ã¬ãããæ¥ç¶ãã¦ããNetwork selectionããããDEVNETããé¸æãããAddress for airdropãã«èªåã®ã¢ãã¬ã¹ãå¥ãããUSDC airdropãã®`GET USDC` ãã¿ã³ãæ¼ãã¨ USDC ã Airdrop ããã¾ãã

![USDC TOKEN FAUCET](/public/images/303-Solana-Online-Store/section-2/2_2_1.jpg)

USDC ãæã«å¥ãããã`pages/api` ãã©ã«ãåã® `createTransaction.js` ãä»¥ä¸ã®ã¨ããæ´æ°ãã¾ãã

**â» ã³ãã¼&ãã¼ã¹ãããå¾ã`sellerAddress` ã®å¤ãèªåã®ã¦ã©ã¬ããã¢ãã¬ã¹ã«å¤æ´ããã®ãå¿ããªãã§ãã ãã!**

```jsx
// createTransaction.js

import { WalletAdapterNetwork } from "@solana/wallet-adapter-base";
import { clusterApiUrl, Connection, PublicKey, Transaction } from "@solana/web3.js";
import { createTransferCheckedInstruction, getAssociatedTokenAddress, getMint } from "@solana/spl-token";
import BigNumber from "bignumber.js";
import products from "./products.json";

// devãããä¸ã®USDCãã¼ã¯ã³ã®ã¢ãã¬ã¹ãè¨­å®ãã¾ãã
const usdcAddress = new PublicKey("Gh9ZwEmdLJ8DscKNTkTqPbNwLNNBjuSzaG9Vp2KGtKJr");
// ãã®ã¦ã©ã¬ããã¢ãã¬ã¹ãæ¸ãæãã¾ããã!
const sellerAddress = "ããªãã®ã¦ã©ã¬ããã¢ãã¬ã¹";
const sellerPublicKey = new PublicKey(sellerAddress);

const createTransaction = async (req, res) => {
  try {
    const { buyer, orderID, itemID } = req.body;
    if (!buyer) {
      res.status(400).json({
        message: "Missing buyer address",
      });
    }

    if (!orderID) {
      res.status(400).json({
        message: "Missing order ID",
      });
    }

    const itemPrice = products.find((item) => item.id === itemID).price;

    if (!itemPrice) {
      res.status(404).json({
        message: "Item not found. please check item ID",
      });
    }

    const bigAmount = BigNumber(itemPrice);
    const buyerPublicKey = new PublicKey(buyer);

    const network = WalletAdapterNetwork.Devnet;
    const endpoint = clusterApiUrl(network);
    const connection = new Connection(endpoint);

    const buyerUsdcAddress = await getAssociatedTokenAddress(usdcAddress, buyerPublicKey);
    const shopUsdcAddress = await getAssociatedTokenAddress(usdcAddress, sellerPublicKey);
    const { blockhash } = await connection.getLatestBlockhash("finalized");

    // è»¢éãããã¼ã¯ã³ã®ãã³ãã¢ãã¬ã¹ãåå¾ãã¦ãã¾ãã
    const usdcMint = await getMint(connection, usdcAddress);

    const tx = new Transaction({
      recentBlockhash: blockhash,
      feePayer: buyerPublicKey,
    });

    // SOLã¨ã¯ç°ãªãã¿ã¤ãã®å½ä»¤ãä½æãã¦ãã¾ãã
    const transferInstruction = createTransferCheckedInstruction(
      buyerUsdcAddress,
      usdcAddress,     // è»¢éãããã¼ã¯ã³ã®ã¢ãã¬ã¹ã§ãã
      shopUsdcAddress,
      buyerPublicKey,
      bigAmount.toNumber() * 10 ** (await usdcMint).decimals,
      usdcMint.decimals // ãã¼ã¯ã³ã«ã¯ä»»æã®æ°ã®å°æ°ãå«ãããã¨ãã§ãã¾ãã
    );

    // ä»¥ä¸ã®å¤æ´ã¯ãªãã§ãã
    transferInstruction.keys.push({
      pubkey: new PublicKey(orderID),
      isSigner: false,
      isWritable: false,
    });

    tx.add(transferInstruction);

    const serializedTransaction = tx.serialize({
      requireAllSignatures: false,
    });

    const base64 = serializedTransaction.toString("base64");

    res.status(200).json({
      transaction: base64,
    });
  } catch (err) {
    console.error(err);

    res.status(500).json({ error: "error creating transaction" });
    return;
  }
};

export default function handler(req, res) {
  if (req.method === "POST") {
    createTransaction(req, res);
  } else {
    res.status(405).end();
  }
}
```

æåã«è¿½å ããã®ã¯ faucet ããåå¾ï¼è¨è¼ã®ããï¼ãã devnet ä¸ã«å­å¨ãã USDC ãã¼ã¯ã³ã®ãã¼ã¯ã³ã¢ãã¬ã¹ã§ãã

```jsx
const usdcAddress = new PublicKey("Gh9ZwEmdLJ8DscKNTkTqPbNwLNNBjuSzaG9Vp2KGtKJr");
```

ãã®ã¢ãã¬ã¹ãä½¿ç¨ãã¦ãUSDC ãã¼ã¯ã³ã¢ã«ã¦ã³ãã®ã¢ãã¬ã¹ãæ¢ãã¦æ±ããããã«ãã¾ãã

Solana ä¸ã®ä»£æ¿å¯è½ãªãã¼ã¯ã³ã¯ã[ãã¼ã¯ã³ãã­ã°ã©ã ](https://spl.solana.com/token)ã«ããä½æããã¾ãã

ããã¯ãåãã¼ã¯ã³ãç¬èªã®ã¢ã«ã¦ã³ãï¼ã¢ãã¬ã¹ï¼ãæã¤ãã¨ãæå³ãã¾ãã

Solana ã¢ã«ã¦ã³ããããã«ãåãã¼ã¯ã³ã®ã¢ã«ã¦ã³ããããã«ã®é¨å±ã¨èããã¨ãããã«ã®é¨å±ã®ä¸­ãè¦ãããã«ã¯é¨å±çªå·ãå¿è¦ã«ãªãã¾ãã

ã¤ã¾ãããã¼ã¯ã³ã¢ã«ã¦ã³ããããã¼ã¯ã³ãéä¿¡ããããã«ã¯ããã®ãã¼ã¯ã³ã®ã¢ãã¬ã¹ãç¥ãå¿è¦ãããã¨ãããã¨ã§ãã

â»ã¦ã¼ã¶ã¼ã¢ã«ã¦ã³ãã« USDC ãå¥ã£ã¦ããªãå ´åãUSDC ãã¼ã¯ã³ã¢ãã¬ã¹ãå­å¨ããªãã¨èªè­ããã¦ãã¾ããããéä¿¡åã»éä¿¡åã®ä¸¡æ¹ã®ã¦ã¼ã¶ã¼ã¢ã«ã¦ã³ãã« USDC ãå¿è¦ã¨ãªãã¾ãã

```jsx
    const transferInstruction = createTransferCheckedInstruction(
      buyerUsdcAddress,
      usdcAddress,
      shopUsdcAddress,
      buyerPublicKey,
      bigAmount.toNumber() * 10 ** (await usdcMint).decimals,
      usdcMint.decimals
    );
```

ã¡ãªã¿ã«ãä¸è¨ã®é¨åãä»»æã®[SPLãã¼ã¯ã³](https://spl.solana.com/)ã«ç½®ãæãã¦ãæ©è½ãã¾ãã

`Buy now â` ãã¿ã³ãã¯ãªãã¯ããã¨ããã¼ã¯ã³åï¼ã¢ãã¬ã¹ã§è¡¨ç¤ºãããï¼ãGh9ZwEmdLJ8DscKNTkTqPbNwLNNBjuSzaG9Vp2KGtKJrãã®ãªã¯ã¨ã¹ããè¡¨ç¤ºãããã¯ãã§ãã

ããã¯**å½ã® USDC ãã¼ã¯ã³ã®ã¢ãã¬ã¹**ã§ãããã¡ã¤ã³ãããã§ã¯ããã USDC ã¨ãªãããã§ãã

èª¬æã ãã§ã¯åããã¥ããã¨ãããããã®ã§ã`sellerAddress` ã«è¨­å®ããã¢ãã¬ã¹ A ã¨ã¯å¥ã®ã¢ãã¬ã¹ B ã§ Web ã¢ããªã±ã¼ã·ã§ã³ã«æ¥ç¶ããå®éã« `Buy now â` ãã¿ã³ãæ¼ãã¦è³¼å¥ãã¦ã¿ã¦ãã ããã

ã¢ãã¬ã¹ B ãããæå®ã®éé¡ãã¢ãã¬ã¹ A ã«ééããã¦ãããã¨ãåããã¯ãã§ããï¼åæè¨­å®ã§ã¯éé¡ã 0.09 USDC ã¨ãªã£ã¦ããã®ã§ãåãããããããã« 10.00 USDC ã«å¤æ´ãã¦è©¦ãã¦ã¿ã¦ãã ãããï¼

ä»¥ä¸ã§ãUSDC ã§ã®æ¯æãã®æºåãæ´ãã¾ãã!


### ðââï¸ è³ªåãã

ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã® `#section-2` ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã® 4 ç¹ãè¨è¼ãã¦ãã ãã â¨

```
1. è³ªåãé¢é£ãã¦ããã»ã¯ã·ã§ã³çªå·ã¨ã¬ãã¹ã³çªå·
2. ä½ããããã¨ãã¦ããã
3. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
4. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```

---

æ¬¡ã®ã¬ãã¹ã³ã§ã¯ãæ³¨ææå ±ã®ä¿å­æ©è½ãå®è£ãã¾ã!
