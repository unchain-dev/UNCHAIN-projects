### ð« Candy Machine ã¨ NFT ã devnet ã«æ¥ç¶ãã

æ¬ãã­ã¸ã§ã¯ãã®ã¡ã¤ã³ãã¼ãã§ããCandy Machine ã¨ NFT ã devnet ã«æã¡è¾¼ã¿ã¾ãã

Candy Machine v2 ã«ããããã®ãã­ã»ã¹ãå¤§å¹ã«ç°¡ç´ åããã¾ããã

1 ã¤ã®ã³ãã³ãã§ãä»¥ä¸ãå®è¡ã§ãã¾ãã

1\. NFT ã [Arweave](https://www.arweave.org) (åæ£åãã¡ã¤ã«ã¹ãã¢)ã«ã¢ããã­ã¼ãããCandy Machine ã®æ§æãåæåãã

2\. Metaplex ã®ã³ã³ãã©ã¯ãã§ Candy Machine ãä½æãã

3\. Candy Machine ããä¾¡æ ¼ãçªå·ãéå§æ¥ããã®ã»ãè«¸ãã®è¨­å®ãå®æ½ãã

### ð Solana ã­ã¼ãã¢ã®è¨­å®

ã¢ããã­ã¼ãããããã«ã¯ãã­ã¼ã«ã«ã® Solana ã­ã¼ãã¢ãè¨­å®ããå¿è¦ãããã¾ãã

â» éå»ã«ãã®ä½æ¥­ãããã¨ãããå ´åã¯ãå¼ãç¶ãä»¥ä¸ã®æé ã«å¾ã£ã¦ãã ããã

NFT ã Solana ã«ã¢ããã­ã¼ãããããã«ã¯ãã³ãã³ãã©ã¤ã³ã§ä½æ¥­ããããã®ãã­ã¼ã«ã«ã¦ã©ã¬ããããå¿è¦ã«ãªãã¾ãã

ã¦ã©ã¬ããã¯åºæ¬çã«å¬ééµã¨ç§å¯éµã®ãã­ã¼ãã¢ãã§ãããã¦ã©ã¬ããããªããã° Solana ã¨éä¿¡ã§ãã¾ããã

ããã¯ä»¥ä¸ã®ã³ãã³ããå®è¡ã§ãã¾ãã

â»ãã¹ãã¬ã¼ãºã®å¥åãæ±ããããããEnter ã­ã¼ãæ¼ãã¦ç©ºã«ãã¦ããã¨ããã§ãããã

```txt
solana-keygen new --outfile ~/.config/solana/devnet.json
```

ããããããã®ã­ã¼ãã¢ãããã©ã«ãã®ã­ã¼ãã¢ã¨ãã¦è¨­å®ã§ãã¾ãã

```txt
solana config set --keypair ~/.config/solana/devnet.json
```

ããã§ã`solana config get` ãå®è¡ããã¨ãæ¬¡ã®ããã« `devnet.json` ã `KeypairPath` ã¨ãã¦è¡¨ç¤ºããã¾ãã

```txt
Config File: /Users/ä»»æã®ãã©ã«ãå/.config/solana/cli/config.yml
RPC URL: https://api.devnet.solana.com
WebSocket URL: wss://api.devnet.solana.com/ (computed)
Keypair Path: /Users/ä»»æã®ãã©ã«ãå/.config/solana/devnet.json
Commitment: confirmed
```

ä¸è¨ã³ãã³ãã§ Solana ã®ä»®æ³éè²¨ã§ãã SOL ã®ä¿ææ°ãç¢ºèªã§ãã¾ãã

```txt
solana balance
```

`0SOL` ã¨åºåããã¾ãã

SOL ãªãã§ã¯ Solana ã«ãã¼ã¿ãããã­ã¤ã§ãã¾ããã

ãã­ãã¯ãã§ã¼ã³ã«ãã¼ã¿ãæ¸ãè¾¼ãã«ã¯ãã³ã¹ãããããã¾ãã

ç¾å¨ devnet ä¸ã«ããã®ã§ãå½ã® SOL ãèªåèªèº«ã«ä¸ãããã¨ãã§ãã¾ãã

ä¸è¨å®è¡ãã¾ãã

```txt
solana airdrop 2
```

ããä¸åº¦ `solana balance` ãå®è¡ãã¦ã2 SOL ã¨è¡¨ç¤ºãããã¯ãã§ãã

â» å½ã® SOL ãä¸è¶³ããå ´åã¯ãä¸è¨ã®ã³ãã³ããååº¦å®è¡ãã¦ãã ãã

### ð Candy Machine ãæ§ç¯ãã

`Candy Machine` ã«ã©ã®ãããªåä½ããããããä¼ããã«ã¯ãè¨­å®ãå¿è¦ã§ãã`Candy MachineV2` ã¯ãããç°¡åã«è¡ããã¨ãã§ãã¾ãã

ãã­ã¸ã§ã¯ãã®ã«ã¼ããã©ã«ãï¼`assets` ãã©ã«ãã¨åãå ´æï¼ã« `config.json` ã¨ãããã¡ã¤ã«ãä½æããä»¥ä¸ã®åå®¹ãè¿½å ãã¾ãã

```json
{
  "price": 0.1,
  "number": 3,
  "gatekeeper": null,
  "solTreasuryAccount": "<YOUR WALLET ADDRESS>",
  "splTokenAccount": null,
  "splToken": null,
  "goLiveDate": "05 Jan 2021 00:00:00 GMT",
  "endSettings": null,
  "whitelistMintSettings": null,
  "hiddenSettings": null,
  "storage": "arweave",
  "ipfsInfuraProjectId": null,
  "ipfsInfuraSecret": null,
  "awsS3Bucket": null,
  "noRetainAuthority": false,
  "noMutable": false
}
```

æåã¯å°ãé£ããããããã¾ããããå¿è¦ãªã®ã¯ãã®ãã¡ 5 ã¤ã ãã§ããæ®ãã®ãã®ã¯ä»ã®ã¨ããç¡è¦ãã¾ããããã§ã¯å¿è¦ãªé ç®ãè¦ã¦ããã¾ãããã

- `price`ï¼å NFT ã®ä¾¡æ ¼

- `number`ï¼ããã­ã¤ããã NFT ã®æ°ãã¤ã¡ã¼ã¸ã¨ json ã®ãã¢ã®æ°ã¨ä¸è´ãã¦ããªãã¨ãã°ãèµ·ãã¾ãã

- `solTreasuryAccount`ï¼ããªãã® Phantom Wallet ã®ã¢ãã¬ã¹ã§ããSOL æ¯æãããã®æç¶ããè¡ãããã¦ã©ã¬ããã«ãªãã¾ãã

- `goLiveDate`ï¼ãã³ããéå§æ¥æãè¨­å®ãã¾ãã

- `storage`ï¼ããªãã® NFT ãä¿å­ãããå ´æã§ãã

ããã§ã¯ `solTreasuryAccount` ã ãä¿®æ­£ãã¾ãã

`solTreasuryAccount` ã«ã¯ããªãã® Fantom Wallet ã®ã¢ãã¬ã¹ãå¥åãã¾ãããã

ä½è«ã§ãããdevnet ã«ã¯æå¤§ 10 åã® NFT ãããã­ã¤ã§ãã¾ãã

ä»åã¯ NFT ã 3 ã¤ããä¸ããªãã®ã§ããã3 ã¤ä»¥ä¸ããããå ´åã¯ `number` ã®æ°å­ãå¤æ´ãã¦ãã ããã

### ð NFT ãã¢ããã­ã¼ãããCandy Machine ãä½æãã

æ¬¡ã«ãMetaplex ã® `upload` ã³ãã³ããä½¿ç¨ãã¦ã`Assets` ãã£ã¬ã¯ããªã«ãã NFT ãã¢ããã­ã¼ãããCandy Machine ãä½æãã¾ãããã®ä½æ¥­ã¯ä¸åº¦ã«è¡ããã¾ãã

ãã®ã³ãã³ãã¯ `assets` ãã£ã¬ã¯ããªã® 1 ã¤ä¸ã®éå±¤ããå®è¡ããå¿è¦ãããã¾ãã

â» ã¿ã¼ããã«ãã `ls` ãå¥åãã¦ãä¸è¨ã®ãããªãã£ã¬ã¯ããªã«ãªã£ã¦ããã°å¤§ä¸å¤«ã§ãã

![ç¡é¡](/public/images/302-Solana-NFT-Drop/section2/2_3_1.png)

ããã§ã¯ä¸è¨ã³ãã³ããã¿ã¼ããã«ã«å¥åããNFT ãã¢ããã­ã¼ããã¾ãããã

```txt
ts-node ~/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts upload -e devnet -k ~/.config/solana/devnet.json -cp config.json ./assets

```

`no such file or directory, scandir './assets'` ã®ãããªã¨ã©ã¼ãåºãå ´åã¯ãã³ãã³ãã®å®è¡å ´æãééã£ã¦ãããã¨ãæå³ãã¾ããå¿ã `assets` ãã©ã«ããããã®ã¨åããã£ã¬ã¯ããªã§å®è¡ãã¦ãã ããã

`upload` ã³ãã³ãã¯ä¸è¨ãå®è¡ãã¦ãã¾ãã

- `assets` ãã©ã«ãåã®ãã¹ã¦ã® NFT ãã¢ãåå¾ãã

- Arweave ã« NFT ãã¢ããã­ã¼ããã

- ãããã® NFT ã¸ã®ãã¤ã³ã¿ãä¿æãã Candy Machine ã® config ãåæåãã

- ãã® config ã Solana ã® devnet ã«ä¿å­

ãã®ã³ãã³ããå®è¡ãããã¨ãç¾å¨ã©ã® NFT ãã¢ããã­ã¼ãããã¦ããããã¿ã¼ããã«ã«ä½ããã®åºåãè¡¨ç¤ºãããã¯ãã§ãã

```txt
wallet public key: A1AfJpXEiqiP3twp6CdZCWixpyx6p8E26zej4TNQ12GT
WARNING: The "arweave" storage option will be going away soon. Please migrate to arweave-bundle or arweave-sol for mainnet.

Beginning the upload for 3 (img+json) pairs
started at: 1641470635118
Size 3 { mediaExt: '.png', index: '0' }
Processing asset: 0
initializing candy machine
initialized config for a candy machine with publickey: 5FUh6tm4sATuCA6hth9a4JAuko9GEAhsewULrXa5zS8C
Processing asset: 0
Processing asset: 1
Processing asset: 2
Writing indices 0-2
Done. Successful = true.
ended at: 2022-01-06T12:04:38.862Z. time taken: 00:00:43
```

`initialized config for a candy machine"` ã¨è¨è¼ããã¦ããã`public key` ãåºåãã¦ããç®æãè¦ã¦ãã ããã

ãã®ã­ã¼ãã³ãã¼ãã¦ Solana ã® [Devnet Explorer](https://explorer.solana.com/?cluster=devnet) ã«è²¼ãä»ããã¨ãå®éã«ãã­ãã¯ãã§ã¼ã³ã«ããã­ã¤ããããã¨ãç¢ºèªã§ãã¾ãããã²ãã£ã¦ã¿ã¦ãã ããã

å°æ¥çã«å¿è¦ã«ãªãã®ã§ããã®ã¢ãã¬ã¹ãæåã«ç½®ãã¦ããã¾ãããã

ããã§ãNFT ãå¤æ´ãã¦ååº¦ `upload` ãå®è¡ãã¦ããå®éã«ã¯æ°ãããã®ã¯ã¢ããã­ã¼ããããªããã¨ã«æ°ä»ãã§ãããã

```txt
ts-node ~/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts upload -e devnet -k ~/.config/solana/devnet.json -cp config.json ./assets
```

ãã®çç±ã¯ããã®ãã¼ã¿ãä¿å­ãã `.cache` ãã©ã«ããä½æããã¦ããããã§ãã

å¤æ´ãããå ´åã¯ãã­ã¸ã§ã¯ãã®ã«ã¼ããã£ã¬ã¯ããªã«å­å¨ãã¦ãã `.cache` ãã©ã«ããåé¤ãã¦ã`upload` ãååº¦å®è¡ããå¿è¦ãããã¾ãã

ããã«ãããCandy Machine æ§æãåæåããã¾ãã

ã³ã¬ã¯ã·ã§ã³ãå¬éããåã«ã³ã¬ã¯ã·ã§ã³ã«å¤æ´ãå ãããå ´åã¯ãå¿ããããè¡ã£ã¦ãã ããã

### â NFT ãç¢ºèªãã

æ¬¡ã«é²ãåã«ãä¸è¨ `verify` ã³ãã³ããå®è¡ãã¦ãNFT ãå®éã«ã¢ããã­ã¼ãããããã¨ãç¢ºèªãã¾ãã

```txt
ts-node ~/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts verify_upload -e devnet -k ~/.config/solana/devnet.json
```

ãã¾ããã£ã¦ããå ´åãåºåã¯æ¬¡ã®ããã«ãªãã¾ãã

```txt
wallet public key: A1AfJpXEiqiP3twp6CdZCWixpyx6p8E26zej4TNQ12GT
Key size 3
uploaded (3) out of (3)
ready to deploy!
```

`/.cache/devnet-temp.json` ãã¡ã¤ã«ãè¦ãã¨ã3 ã¤ã® Arweave ãªã³ã¯ãããã¾ãããããã¯ NFT ã®æ ¼ç´åã§ãã

Arweave ãªã³ã¯ã® 1 ã¤ãã³ãã¼ãã¦ãã©ã¦ã¶ã«è²¼ãä»ããNFT ã®ã¡ã¿ãã¼ã¿ãç¢ºèªãã¦ãã ããã

Arweave ã¯ãã¼ã¿ã**æ°¸ç¶çã«**ä¿å­ãã¾ãã

ããã¯ãIPFS / Filecoin ã®ä¸çã¨ã¯å¤§ããç°ãªãã¾ãã

IPFS / Filecoin ã§ã¯ããã¡ã¤ã«ãä¿æãããã¨ãæ±ºå®ãããã¼ãã«ãã¨ã¥ãã¦ãã¼ã¿ããã¢ãã¼ãã¢ã§ä¿å­ããã¾ãã

Arweave ã¯ä¸åº¦æ¯æãã¨ã**æ°¸ä¹ã«**ä¿å­ãã¾ãã

Arweave ã§ã¯ããã¡ã¤ã«ã®å¤§ããã«å¿ãã¦ãä¿å­ã«å¿è¦ãªã³ã¹ããè¦ç©ãã[ ã¢ã«ã´ãªãºã  ](https://arwiki.wiki/#/en/storage-endowment#toc_Transaction_Pricing)ãä½æãããããå©ç¨ãã¦ãã¾ãã

[é»å](https://arweavefees.com/) ãä½¿ã£ã¦è¨ç®ãã§ãã¾ãããã¨ãã° 1MB ãæ°¸ä¹ã«ä¿å­ããã«ã¯ãç´ 0.0083 ãã«ã®è²»ç¨ããããã¾ããæªããªãã§ãã­ã

ãããããç§ã®ãã®ããã¹ãããã®ã«èª°ããéãæã£ã¦ãããã ã!ãã¨çåã«æãããããã¾ãããã[ãã¡ã](https://github.com/metaplex-foundation/metaplex/blob/59ab126e41e6d85b53c79ad7358964dadd12b5f4/js/packages/cli/src/helpers/upload/arweave.ts#L93)ã®ã½ã¼ã¹ã³ã¼ããè¦ãã°ãä»ã®ã¨ãã Metaplex ããéãæã£ã¦ããã¦ãããã¨ããããã¾ãã

### ð¨ Candy Machine ã®æ§æãæ´æ°ãã

Candy Machine ã®æ§æãæ´æ°ããã«ã¯ã`config.json` ãã¡ã¤ã«ãæ´æ°ãã¦ãæ¬¡ã®ã³ãã³ããå®è¡ããã ãã§ãã

```txt
ts-node ~/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts update_candy_machine -e devnet -k ~/.config/solana/devnet.json -cp config.json
```

### ð¡ æ³¨æãã¹ãã¨ã©ã¼

ä»¥ä¸ã®ãããªã¨ã©ã¼ãçºçããå ´åï¼

```txt
/Users/flynn/metaplex-foundation/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts:53
      return fs.readdirSync(`${val}`).map(file => path.join(val, file));
                      ^
TypeError: Cannot read property 'candyMachineAddress' of undefined
    at /Users/flynn/metaplex-foundation/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts:649:53
    at step (/Users/flynn/metaplex-foundation/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts:53:23)
    at Object.next (/Users/flynn/metaplex-foundation/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts:34:53)
    at fulfilled (/Users/flynn/metaplex-foundation/metaplex/js/packages/cli/src/candy-machine-v2-cli.ts:25:58)
    at processTicksAndRejections (node:internal/process/task_queues:96:5)
```

ããã¯ Candy Machine ã NFT ã«é¢ãããã¼ã¿ãå¥ã£ã `.cache` ãã©ã«ãã«ã¢ã¯ã»ã¹ã§ããªããã¨ãæå³ãã¾ãã

ãã®ã¨ã©ã¼ãçºçããå ´åã¯ãCandy Machine ã®ã³ãã³ãã `.cache` ãã©ã«ãã¨ `assets` ãã©ã«ããããåããã£ã¬ã¯ããªããå®è¡ãã¦ãããç¢ºèªãã¦ãã ãããèµ·ãããã¡ãªãã¹ãªã®ã§ååæ³¨æãã¦ãã ãã!

### ðââï¸ è³ªåãã

ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã® `#section-2` ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã® 3 ç¹ãè¨è¼ãã¦ãã ãã â¨

```
1. è³ªåãé¢é£ãã¦ããã»ã¯ã·ã§ã³çªå·ã¨ã¬ãã¹ã³çªå·
2. ä½ããããã¨ãã¦ããã
3. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
4. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```

---

ããã§ã¨ããããã¾ã!ãã»ã¯ã·ã§ã³ 2 ã¯çµäºã§ã!

ãã²ãã¿ã¼ããã«ã®åºåçµæãã³ãã¥ããã£ã«æç¨¿ãã¦ãã ãã!

ããªãã®æåãã³ãã¥ããã£ã§ç¥ãã¾ããã ð

æ¬¡ã®ã¬ãã¹ã³ã§ã¯ãWeb ã¢ããªã±ã¼ã·ã§ã³ãã Candy Machine ãå¼ã³åºãã¦ããã¾ã!
