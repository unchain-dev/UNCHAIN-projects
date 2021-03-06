### ð± ååãè¿½å ããã!

ãªã³ã©ã¤ã³ã·ã§ããã®å®æã¯éè¿ã§ã!

ãããã«ãã·ã§ããã®ãªã¼ãã¼ã§ããããªãã **ãã­ã³ãã¨ã³ããã** ã·ã§ããã«ã¢ã¤ãã ãè¿½å ã§ããæ©è½ãè¿½å ãã¾ãã

ã¾ãããã­ã¸ã§ã¯ãã®ã«ã¼ããã£ã¬ã¯ããªã« `.env` ãã¡ã¤ã«ãä½æããããã«ã¢ãã¬ã¹ãè¿½å ãã¾ãã

ç§ã®å ´åã`.env` ãã¡ã¤ã«ã¯ä»¥ä¸ã®ããã«ãªãã¾ãã

```code
// .env
NEXT_PUBLIC_OWNER_PUBLIC_KEY=2TmQsWGFh5vhqJdDrG6uA2MRstGrUwUCiiThyHL9HaMe
```

> â ï¸ æ³¨æ
>
> Next.js ã«ã¯ [dotenv](https://www.dotenv.org/) ãçµã¿è¾¼ã¾ãã¦ãã¾ãããenv å¤æ°åã `NEXT_PUBLIC` ããã¯ãããå¿è¦ãããã¾ãã
>
> ã¾ãã`.env` ã¸ã®å¤æ´ãåæ ãããããã«ã¯ãNext.js ãåèµ·åï¼`CTR + C` ã§ä¸æ¦åæ­¢ããã`npx next dev` ã§åã³ç«ã¡ä¸ããï¼ããå¿è¦ããããã¨ã«æ³¨æãã¦ãã ããã

ããã§ã¯ã`components` ãã©ã«ãã« `CreateProduct.js` ãã¡ã¤ã«ãä½æãã¦ä»¥ä¸ã®ã³ã¼ããè²¼ãä»ãã¦ãã ããã

```jsx
// CreateProduct.js

import React, { useState } from "react";
import { create } from "ipfs-http-client";
import styles from "../styles/CreateProduct.module.css";

const client = create("https://ipfs.infura.io:5001/api/v0");

const CreateProduct = () => {

  const [newProduct, setNewProduct] = useState({
    name: "",
    price: "",
    image_url: "",
    description: "",
  });
  const [file, setFile] = useState({});
  const [uploading, setUploading] = useState(false);

  async function onChange(e) {
    setUploading(true);
    const files = e.target.files;
    try {
      console.log(files[0]);
      const added = await client.add(files[0]);
      setFile({ filename: files[0].name, hash: added.path });
    } catch (error) {
      console.log("Error uploading file: ", error);
    }
    setUploading(false);
  }

  const createProduct = async () => {
    try {
      // ååãã¼ã¿ã¨file.nameãçµåãã¾ãã
      const product = { ...newProduct, ...file };
      console.log("Sending product to api",product);
      const response = await fetch("../api/addProduct", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify(product),
      });
      const data = await response.json();
      if (response.status === 200) {
        alert("Product added!");
      }
      else{
        alert("Unable to add product: ", data.error);
      }

    } catch (error) {
      console.log(error);
    }
  };

  return (
    <div className={styles.background_blur}>
      <div className={styles.create_product_container}>
        <div className={styles.create_product_form}>
          <header className={styles.header}>
            <h1>Create Product</h1>
          </header>

          <div className={styles.form_container}>
            <input
              type="file"
              className={styles.input}
              accept=".jpg,.png"
              placeholder="Images"
              onChange={onChange}
            />
            {file.name != null && <p className="file-name">{file.filename}</p>}
            <div className={styles.flex_row}>
              <input
                className={styles.input}
                type="text"
                placeholder="Product Name"
                onChange={(e) => {
                  setNewProduct({ ...newProduct, name: e.target.value });
                }}
              />
              <input
                className={styles.input}
                type="text"
                placeholder="0.01 USDC"
                onChange={(e) => {
                  setNewProduct({ ...newProduct, price: e.target.value });
                }}
              />
            </div>

            <div className={styles.flex_row}>
              <input
                className={styles.input}
                type="url"
                placeholder="Image URL ex: https://media.giphy.com/media/FWAcpJsFT9mvrv0e7a/giphy.gif"
                onChange={(e) => {
                  setNewProduct({ ...newProduct, image_url: e.target.value });
                }}
              />
            </div>
            <textarea
              className={styles.text_area}
              placeholder="Description here..."
              onChange={(e) => {
                setNewProduct({ ...newProduct, description: e.target.value });
              }}
            />

            <button
              className={styles.button}
              onClick={() => {
                createProduct();
              }}
              disabled={uploading}
            >
              Create Product
            </button>
          </div>
        </div>
      </div>
    </div>
  );
};

export default CreateProduct;
```

æ¬¡ã«ã`index.js` ãä»¥ä¸ã®ã¨ããæ´æ°ãã¦ãç»é²ããã¢ãã¬ã¹ã¨ã¡ãã»ã¼ã¸éä¿¡èã®ã¢ãã¬ã¹ãä¸è´ããã®ãç¢ºèªã§ããããã«ãã¾ããããï¼ããã§ã·ã§ããã®ãªã¼ãã¼ãç¢ºèªãã¾ããï¼

```jsx
// index.js

import React, { useState, useEffect} from "react";
import CreateProduct from "../components/CreateProduct";
import Product from "../components/Product";
import HeadComponent from '../components/Head';

import { useWallet } from "@solana/wallet-adapter-react";
import { WalletMultiButton } from "@solana/wallet-adapter-react-ui";

// å®æ°ãå®£è¨ãã¾ãã
const TWITTER_HANDLE = "ããªãã®Twitterãã³ãã«";
const TWITTER_LINK = `https://twitter.com/${TWITTER_HANDLE}`;

const App = () => {
  const { publicKey } = useWallet();
  const isOwner = ( publicKey ? publicKey.toString() === process.env.NEXT_PUBLIC_OWNER_PUBLIC_KEY : false );
  const [creating, setCreating] = useState(false);
  const [products, setProducts] = useState([]);

  const renderNotConnectedContainer = () => (
    <div>
      <img src="https://media.giphy.com/media/FWAcpJsFT9mvrv0e7a/giphy.gif" alt="anya" />

      <div className="button-container">
        <WalletMultiButton className="cta-button connect-wallet-button" />
      </div>
    </div>
  );

  useEffect(() => {
    if (publicKey) {
      fetch(`/api/fetchProducts`)
        .then(response => response.json())
        .then(data => {
          setProducts(data);
          console.log("Products", data);
        });
    }
  }, [publicKey]);

  const renderItemBuyContainer = () => (
    <div className="products-container">
      {products.map((product) => (
        <Product key={product.id} product={product} />
      ))}
    </div>
  );

  return (
    <div className="App">
      <HeadComponent/>
      <div className="container">
        <header className="header-container">
          <p className="header"> ð³ UNCHAIN Image Store ð</p>
          <p className="sub-text">The only Image store that accepts shitcoins</p>

          {isOwner && (
            <button className="create-product-button" onClick={() => setCreating(!creating)}>
              {creating ? "Close" : "Create Product"}
            </button>
          )}
        </header>

        <main>
          {creating && <CreateProduct />}
          {publicKey ? renderItemBuyContainer() : renderNotConnectedContainer()}
        </main>

        <div className="footer-container">
          <img alt="Twitter Logo" className="twitter-logo" src="twitter-logo.svg" />
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

ããã§ããªã¼ãã¼ã¨åãã¦ã©ã¬ããã§æ¥ç¶ããã¨ãå³ä¸ã« `Create Product` ãã¿ã³ãè¡¨ç¤ºãããã¯ãã§ãã

æå¾ã«ããã¼ã¿ãã¼ã¹ã« API ã¨ã³ããã¤ã³ããè¿½å ãã¾ãããã

`pages/api` ãã©ã«ãã« `addProduct.js` ãã¡ã¤ã«ãä½æãã¦ä»¥ä¸ã®ã³ã¼ããè²¼ãä»ãã¦ãã ããã

```jsx
// addProduct.js

import products from './products.json';
import fs from "fs";

export default function handler(req, res){
  if (req.method === "POST"){
    try {
      console.log("body is ", req.body)
      const { name, price, image_url, description, filename, hash } = req.body;

      // ååã®ãã­ãã¯ãIDãåã«æ°ãããã­ãã¯ãIDãä½æãã¾ãã
      const maxID = products.reduce((max, product) => Math.max(max, product.id), 0);
      products.push({
        id: maxID + 1,
        name,
        price,
        image_url,
        description,
        filename,
        hash,
      });
      fs.writeFileSync("./pages/api/products.json", JSON.stringify(products, null, 2));
      res.status(200).send({ status: "ok" });
    } catch (error) {
      console.error(error);
      res.status(500).json({error: "error adding product"});
      return;
    }
  }
  else {
    res.status(405).send(`Method ${req.method} not allowed`);
  }
}
```

ããã§ã¢ã¤ãã ãè¿½å ãããã¨ãã§ããããã«ãªãã¾ãã!

â»å¤æ®µã®æ¬ã«ã¯æ°å­ã ããå¥ãããããæ³¨æãã¦ãã ããã

![Create Product](/public/images/303-Solana-Online-Store/section-3/3_1_1.jpg)


### ðââï¸ è³ªåãã

ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã® `#section-3` ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã® 4 ç¹ãè¨è¼ãã¦ãã ãã â¨

```
1. è³ªåãé¢é£ãã¦ããã»ã¯ã·ã§ã³çªå·ã¨ã¬ãã¹ã³çªå·
2. ä½ããããã¨ãã¦ããã
3. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
4. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```

---

ããã§ã¨ããããã¾ã!

ã»ã¯ã·ã§ã³ 3 ã¯çµäºã§ã!

ãã²ãæ°ããè¿½å ããååãè¡¨ç¤ºããã¦ããç¶æã® Web ã¢ããªã±ã¼ã·ã§ã³ã®ç»é¢ãã³ãã¥ããã£ã«æç¨¿ãã¦ãã ãã!

ããªãã®æåãã³ãã¥ããã£ã§ç¥ãã¾ããã ð

æ¬¡ã®ã»ã¯ã·ã§ã³ã§ã¯ãæå¾ã®ä»ä¸ããè¡ã£ã¦ããã¾ã!
