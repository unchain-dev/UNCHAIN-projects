### ð ã­ã¼ãæã«è³¼å¥æ¸ãã©ãããç¢ºèªãã

ããã§ã¯ã`order.json` ã®ããã¼ã¿ãã¼ã¹ããä¸æãå©ç¨ãã¦ãã¹ãã¢ã«è³¼å¥æ©è½ãå®è£ãã¦ããã¾ããã!

ãããè¡ãããã®ãã­ã¼ã¯ `api.js` ã§ä½¿ç¨ãã `addOrder` ã¨ããä¼¼ã¦ãã¾ãã

ã¾ãã`lib/api.js` ã®**ãããã«ä»¥ä¸ã®ã³ã¼ããè¿½å **ãã¾ãã

```jsx
// api.js

// æå®ãããå¬ééµãéå»ã«ååãè³¼å¥ãã¦ããå ´åã¯trueãè¿ãã¾ãã
export const hasPurchased = async (publicKey, itemID) => {
  // å¬ééµããã©ã¡ã¼ã¿ã¨ãã¦GETãªã¯ã¨ã¹ããéä¿¡ãã¾ãã
  const response = await fetch(`../api/orders?buyer=${publicKey.toString()}`);
  // ã¬ã¹ãã³ã¹ã³ã¼ãã200ã®å ´åã®å¦çã§ãã
  if (response.status === 200) {
    const json = await response.json();
    console.log("Current wallet's orders are:", json);
    // æ³¨æãå­å¨ããå ´åã®å¦çã§ãã
    if (json.length > 0) {
      // ãã®è³¼å¥èã¨ã¢ã¤ãã IDã®ã¬ã³ã¼ãããããã©ãããç¢ºèªãã¾ãã
      const order = json.find((order) => order.buyer === publicKey.toString() && order.itemID === itemID);
      if (order) {
        return true;
      }
    }
  }
  return false;
};
```

ããã§ã¯ã¨ã³ããã¤ã³ãã¨ããåãããæå®ãããã¢ãã¬ã¹ãç¹å®ã®ã¢ã¤ãã ãè³¼å¥ãããã©ãããç¢ºèªãã¦ãã¾ãã

ãã®æ©è½ãå®è£ããã«ããã£ã¦ã`Buy.js` ã§ä»¥ä¸ã® 2 ã¤ã®ãã¨ãè¡ãå¿è¦ãããã¾ãã

1\. ã¤ã³ãã¼ãã« `hasPurchased` ãå«ããã

2\. useEffect ã§ãã¼ã¸ã®èª­ã¿è¾¼ã¿æã« `hasPurchased` ãã§ãã¯ãå®è¡ããã

ããããã®å¤æ´ãå ããããã«ãä»¥ä¸ã®ã¨ããæ´æ°ãã¦ããã¾ãããã

```jsx
// Buy.js

import React, { useState, useEffect, useMemo } from 'react';
import { Keypair, Transaction } from '@solana/web3.js';
import { findReference, FindReferenceError } from '@solana/pay';
import { useConnection, useWallet } from '@solana/wallet-adapter-react';
import { InfinitySpin } from 'react-loader-spinner';
import IPFSDownload from './IpfsDownload';
import { addOrder, hasPurchased } from '../lib/api';

const STATUS = {
  Initial: 'Initial',
  Submitted: 'Submitted',
  Paid: 'Paid',
};

export default function Buy({ itemID }) {
  const { connection } = useConnection();
  const { publicKey, sendTransaction } = useWallet();
  const orderID = useMemo(() => Keypair.generate().publicKey, []); // æ³¨æãè­å¥ããããã«ä½¿ç¨ããå¬ééµãç¨æãã¾ãã

  const [loading, setLoading] = useState(false);
  const [status, setStatus] = useState(STATUS.Initial); // ãã©ã³ã¶ã¯ã·ã§ã³ã¹ãã¼ã¿ã¹è¿½è·¡ç¨ã®stateãå®ç¾©ãã¾ãã

  const order = useMemo(
    () => ({
      buyer: publicKey.toString(),
      orderID: orderID.toString(),
      itemID: itemID,
    }),
    [publicKey, orderID, itemID]
  );

  const processTransaction = async () => {
    setLoading(true);
    const txResponse = await fetch('../api/createTransaction', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify(order),
    });
    const txData = await txResponse.json();

    const tx = Transaction.from(Buffer.from(txData.transaction, 'base64'));
    console.log('Tx data is', tx);

    try {
      const txHash = await sendTransaction(tx, connection);
      console.log(
        `Transaction sent: https://solscan.io/tx/${txHash}?cluster=devnet`
      );
      setStatus(STATUS.Submitted);
    } catch (error) {
      console.error(error);
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => {
    // ãã®ã¢ãã¬ã¹ããã§ã«å¯¾è±¡ã®ååãè³¼å¥ãã¦ãããç¢ºèªããè³¼å¥ãã¦ããå ´åã¯ååãã¼ã¿ãåå¾ãã¦Paidãtrueã«è¨­å®ãã¾ãã
    async function checkPurchased() {
      const purchased = await hasPurchased(publicKey, itemID);
      if (purchased) {
        setStatus(STATUS.Paid);
        console.log("Address has already purchased this item!");
      }
    }
    checkPurchased();
  }, [publicKey, itemID]);


  useEffect(() => {
    if (status === STATUS.Submitted) {
      setLoading(true);
      const interval = setInterval(async () => {
        try {
          const result = await findReference(connection, orderID);
          console.log('Finding tx reference', result.confirmationStatus);
          if (
            result.confirmationStatus === 'confirmed' ||
            result.confirmationStatus === 'finalized'
          ) {
            clearInterval(interval);
            setStatus(STATUS.Paid);
            setLoading(false);
            addOrder(order);
            alert('Thank you for your purchase!');
          }
        } catch (e) {
          if (e instanceof FindReferenceError) {
            return null;
          }
          console.error('Unknown error', e);
        } finally {
          setLoading(false);
        }
      }, 1000);
      return () => {
        clearInterval(interval);
      };
    }
  }, [status]);

  if (!publicKey) {
    return (
      <div>
        <p>You need to connect your wallet to make transactions</p>
      </div>
    );
  }

  if (loading) {
    return <InfinitySpin color="gray" />;
  }

  return (
    <div>
      {status === STATUS.Paid ? (
        <IPFSDownload filename="anya" hash="QmcJPLeiXBwA17WASSXs5GPWJs1n1HEmEmrtcmDgWjApjm" cta="Download goods"/>
      ) : (
        <button
          disabled={loading}
          className="buy-button"
          onClick={processTransaction}
        >
          Buy now ð 
        </button>
      )}
    </div>
  );
}
```

ä»¥ä¸ãä»åè¿½å ããé¨åã«ãªãã¾ãã

ã³ã¡ã³ãã®ã¨ããåä½ãã¾ãã

```jsx
  useEffect(() => {
    // ãã®ã¢ãã¬ã¹ããã§ã«å¯¾è±¡ã®ååãè³¼å¥ãã¦ãããç¢ºèªããè³¼å¥ãã¦ããå ´åã¯ååãã¼ã¿ãåå¾ãã¦Paidãtrueã«è¨­å®ãã¾ãã
    async function checkPurchased() {
      const purchased = await hasPurchased(publicKey, itemID);
      if (purchased) {
        setStatus(STATUS.Paid);
        console.log("Address has already purchased this item!");
      }
    }
    checkPurchased();
  }, [publicKey, itemID]);
```


### ð API ãä½¿ã£ã¦ãã¼ã¿ãã¼ã¹ããã¢ã¤ãã æå ±ãåå¾ãã

ä»ã¾ã§ãã¢ã¤ãã ã®ä¸è¦§ããã¼ãã³ã¼ãã£ã³ã°ãã¦ãã¾ããããããã§ãã®é¨åãä¿®æ­£ãã¦ããã¾ãã

ã¾ãæå§ãã«ã`pages/api` ãã£ã¬ã¯ããªã« `fetchItem.js` ã¨ãããã¡ã¤ã«ãä½æãã¦ä»¥ä¸ã®ã³ã¼ããè²¼ãä»ãã¦ãã ããã

```jsx
// fetchItem.js

// ãã®ã¨ã³ããã¤ã³ãã¯ã¦ã¼ã¶ã¼ã«å¯¾ãã¦ IPFS ãããã¡ã¤ã«ããã·ã¥ãéä¿¡ãã¾ãã
import products from "./products.json"

export default async function handler(req, res) {
  if (req.method === "POST") {
    const { itemID } = req.body;

    if (!itemID) {
      return res.status(400).send('Missing itemID');
    }

    const product = products.find((p) => p.id === itemID);

    if (product) {
      const { hash, filename } = product;
      return res.status(200).send({ hash, filename });
    } else {
      return res.status(404).send("Item not found");
    }
  } else {
    return res.status(405).send(`Method ${req.method} not allowed`);
  }
}
```

ãã®æ®µéã§ã¯ãããã·ã¥ãåé¤ãã¦ããããã`fetchProducts` ãä½¿ããªããªã£ã¦ãã¾ãã

ãã®ããã`lib/api.js` ã®**ãããã«ä»¥ä¸ã®ã³ã¼ããè¿½å **ãã¾ãã

```jsx
// api.js

export const fetchItem = async (itemID) => {
  const response = await fetch("../api/fetchItem", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({ itemID }),
  });
  const item = await response.json();
  return item;
}
```

ãããã«ã`Buy.js` ãä»¥ä¸ã®ã¨ããæ´æ°ãã¾ãã

```jsx
// Buy.js

import React, { useEffect, useState, useMemo } from "react";
import { Keypair, Transaction } from "@solana/web3.js";
import { findReference, FindReferenceError } from "@solana/pay";
import { useConnection, useWallet } from "@solana/wallet-adapter-react";
import { InfinitySpin } from "react-loader-spinner";
import IPFSDownload from "./IpfsDownload";
import { addOrder, hasPurchased, fetchItem } from "../lib/api";

const STATUS = {
  Initial: "Initial",
  Submitted: "Submitted",
  Paid: "Paid",
};

export default function Buy({ itemID }) {
  const { connection } = useConnection();
  const { publicKey, sendTransaction } = useWallet();
  const orderID = useMemo(() => Keypair.generate().publicKey, []); // æ³¨æãè­å¥ããããã«ä½¿ç¨ããå¬ééµãç¨æãã¾ãã

  const [item, setItem] = useState(null); // è³¼å¥ããã¢ã¤ãã ã®IPFSããã·ã¥ã¨ãã¡ã¤ã«åãè¨­å®ãã¾ãã
  const [loading, setLoading] = useState(false); // ä¸è¨ã®ãã¹ã¦ã®ã­ã¼ãç¶æãè¨­å®ãã¾ãã
  const [status, setStatus] = useState(STATUS.Initial); // ãã©ã³ã¶ã¯ã·ã§ã³ã¹ãã¼ã¿ã¹è¿½è·¡ç¨ã®stateãå®ç¾©ãã¾ãã

  const order = useMemo(
    () => ({
      buyer: publicKey.toString(),
      orderID: orderID.toString(),
      itemID: itemID,
    }),
    [publicKey, orderID, itemID]
  );

  // ãµã¼ãã¼ãããã©ã³ã¶ã¯ã·ã§ã³ãªãã¸ã§ã¯ããåå¾ãã¾ããï¼æ¹ãããåé¿ããããã«å®è¡ããã¾ããï¼
  const processTransaction = async () => {
    setLoading(true);
    const txResponse = await fetch("../api/createTransaction", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify(order),
    });
    const txData = await txResponse.json();

    const tx = Transaction.from(Buffer.from(txData.transaction, "base64"));
    console.log("Tx data is", tx);
    // ãã©ã³ã¶ã¯ã·ã§ã³ããããã¯ã¼ã¯ã«éä¿¡ãã¾ãã
    try {
      const txHash = await sendTransaction(tx, connection);
      console.log(`Transaction sent: https://solscan.io/tx/${txHash}?cluster=devnet`);
      setStatus(STATUS.Submitted);
    } catch (error) {
      console.error(error);
    } finally {
      setLoading(false);
    }
  };

  useEffect(() => {
    // ãã®ã¢ãã¬ã¹ããã§ã«å¯¾è±¡ã®ååãè³¼å¥ãã¦ãããç¢ºèªããè³¼å¥ãã¦ããå ´åã¯ååãã¼ã¿ãåå¾ãã¦Paidãtrueã«è¨­å®ãã¾ãã
    async function checkPurchased() {
      const purchased = await hasPurchased(publicKey, itemID);
      if (purchased) {
        setStatus(STATUS.Paid);
        const item = await fetchItem(itemID);
        setItem(item);
      }
    }
    checkPurchased();
  }, [publicKey, itemID]);

  useEffect(() => {
    // ãã©ã³ã¶ã¯ã·ã§ã³ãç¢ºèªããã¦ããããã§ãã¯ãã¾ãã
    if (status === STATUS.Submitted) {
      setLoading(true);
      const interval = setInterval(async () => {
        try {
          const result = await findReference(connection, orderID);
          console.log("Finding tx reference", result.confirmationStatus);
          if (result.confirmationStatus === "confirmed" || result.confirmationStatus === "finalized") {
            clearInterval(interval);
            setStatus(STATUS.Paid);
            addOrder(order);
            setLoading(false);
            alert("Thank you for your purchase!");
          }
        } catch (e) {
          if (e instanceof FindReferenceError) {
            return null;
          }
          console.error("Unknown error", e);
        } finally {
          setLoading(false);
        }
      }, 1000);
      return () => {
        clearInterval(interval);
      };
    }

    async function getItem(itemID) {
      const item = await fetchItem(itemID);
      setItem(item);
    }

    if (status === STATUS.Paid) {
      getItem(itemID);
    }
  }, [status]);

  if (!publicKey) {
    return (
      <div>
        <p>You need to connect your wallet to make transactions</p>
      </div>
    );
  }

  if (loading) {
    return <InfinitySpin color="gray" />;
  }

  return (
    <div>
      {/* ããã·ã¥ãå­å¨ãããã©ããã«åºã¥ãã¦è³¼å¥ãã¿ã³ã¾ãã¯IPFS Downloadã³ã³ãã¼ãã³ãã®ãããããè¡¨ç¤ºãã¾ãã */}
      {item ? (
        <IPFSDownload hash={item.hash} filename={item.filename} />
      ) : (
        <button disabled={loading} className="buy-button" onClick={processTransaction}>
          Buy now ð 
        </button>
      )}
    </div>
  );
}
```

ããã§ã¨ããããã¾ã!

ããã§è³¼å¥ãã¿ã³ã¨ååãã¼ã¿ãæ³¨ææå ±ãªã©ããã¹ã¦ãªã³ã¯ããããã¨ãã§ãã¾ããð¤£ð¤£ð¤£


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

ããã§ã¨ããããã¾ã!

ã»ã¯ã·ã§ã³ 2 ã¯çµäºã§ã!

ãã²ãWeb ã¢ããªã±ã¼ã·ã§ã³ã®ååè³¼å¥æã®ã­ã¼ãã£ã³ã°ç»é¢ãã³ãã¥ããã£ã«æç¨¿ãã¦ãã ãã!

ããªãã®æåãã³ãã¥ããã£ã§ç¥ãã¾ããã ð

æ¬¡ã®ã»ã¯ã·ã§ã³ã§ã¯ãååã®è¿½å ãè¡ã£ã¦ããã¾ã!
