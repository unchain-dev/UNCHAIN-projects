### ð¸ IPFS ã¸ãã¡ã¤ã«ãã¢ããã­ã¼ããã

æ¬¡ã®ã¹ãããã¯ãWeb ã¢ããªã±ã¼ã·ã§ã³ã¸ã®ååã®è¿½å ã§ãã

ååãã¼ã¿ããµã¼ãã¼ãã¯ã©ã¦ãã¹ãã¬ã¼ã¸ã«ä¿å­ãã¦ãããã¨ãã§ãã¾ãããä»åã¯[IPFS](https://en.wikipedia.org/wiki/InterPlanetary_File_System)ãå©ç¨ãã¾ãã

IPFS ã¯ InterPlanetary File System ã®ç¥ã§ããã¼ã¿ãåæ£çã«ä¿å­ãã¦ãããåæ£åã¹ãã¬ã¼ã¸ã§ãã

IPFS ã«ä¿å­ããããã¼ã¿ã¯ä¸å®æéåã«ã¢ã¯ã»ã¹ããªãã¨æ¶ãã¦ãã¾ãå¯è½æ§ãããã®ã§ãã¦ã¼ã¶ã¼ã¯å®æçã«ã¹ãã¬ã¼ã¸ã«ã¢ã¯ã»ã¹ï¼[ãã³](https://docs.ipfs.io/how-to/pin-files/)ï¼ããå¿è¦ãããã¾ãã ï¼ä»åã®ãã¥ã¼ããªã¢ã«ã§ã¯å®æ½ãã¾ãããï¼

â»IPFS ã®è©³ç´°ã«ã¤ãã¦ã¯ [ãã](https://decrypt.co/resources/how-to-use-ipfs-the-backbone-of-web3) ãåç§ãã¦ã¿ã¦ãã ããã

ä»åã¯ IPFS pinning service ã®[Pinata](https://www.pinata.cloud/?utm_source=buildspace)ãå©ç¨ãã¾ãã

ããã§ã¯ãPinata ãå©ç¨ãã¦ IPFS ã«ç»åãã¢ããã­ã¼ããã¦ãã ããã

â»ã¢ããã­ã¼ãããããã«ã¯ `+ Upload` ãã¿ã³ãæ¼ä¸ãã¦é²ãã¾ãã

![pinata](/public/images/303-Solana-Online-Store/section-1/1_3_1.png)

ã¤ã¥ãã¦ãã¢ããã­ã¼ãããç»åã®ã CID ï¼ã³ã³ãã³ã ID ï¼ãã®æ¬ã«è¨è¼ããã ID ããã·ã¥ãã³ãã¼ãã¦ããã¾ãããã

CID ã¯ IPFS ä¸ã§ã³ã³ãã³ãã«ã¢ã¯ã»ã¹ããããã®ã¢ãã¬ã¹ã§ãä»¥ä¸ã®ãããªãªã³ã¯ãä½æãã¦ã¢ã¯ã»ã¹ãããã¨ãã§ãã¾ãã

```html
https://cloudflare-ipfs.com/ipfs/"ããªãã®ç»åãã¡ã¤ã«ã®CID"
```


### ð IPFSãããã¡ã¤ã«ããã¦ã³ã­ã¼ããã

`hooks` ãã©ã«ãåã« IPFS ã²ã¼ãã¦ã§ã¤ã® URL ã«ããã·ã¥ã¨ãã¡ã¤ã«åãè¿½å ãã `useIPFS.js` ãã¡ã¤ã«ãããã¾ãã

ããã¯ããã­ã³ãã¨ã³ãå´ã§ IPFS ããã®ãã¦ã³ã­ã¼ãã®åä½ãæããã®ã§ãã

`useIPFS()` ãä½¿ãããã`components` ãã©ã«ãã®ä¸­ã« `IpfsDownload.js` ãã¡ã¤ã«ãä½æãã`useIPFS()` ãå¼ã³åºãã³ã³ãã¼ãã³ããä½æãã¦ããã¾ãã

```jsx
// IpfsDownload.js

import React  from 'react';
import useIPFS from '../hooks/useIPFS';

const IPFSDownload = ({ hash, filename }) => {

  const file = useIPFS(hash, filename);

  return (
    <div>
      {file ? (
        <div className="download-component">
          <a className="download-button" href={file} download={filename}>Download</a>
        </div>
      ) : (
        <p>Downloading file...</p>
      )}
    </div>
  );
};

export default IPFSDownload;
```

ãã¦ã³ã­ã¼ããªã³ã¯ãæç»ããã ãã®ã·ã³ãã«ãªã³ã³ãã¼ãã³ãã§ãã


### ð ãã¦ã³ã­ã¼ãæ©è½ã®å®è£

ç¶ãã¦ããã¦ã³ã­ã¼ãæ©è½ãå®è£ãã¾ãããã

`pages` ãã£ã¬ã¯ããªã« `api` ãã©ã«ããè¿½å ãããã®ä¸­ã« `products.json` ãã¡ã¤ã«ãä½æãã¦ä»¥ä¸ã®ã³ã¼ããè²¼ãä»ãã¦ãã ããã

ãã® `products.json` ãã¡ã¤ã«ã¯ååã®ã¢ãã¯ãã¼ã¿ãã¼ã¹ã§ããï¼ãµã³ãã«ã® `image_url` ã¯éå¸¸ã«é·ãã§ããæ°ã«ããé²ãã¦ãã ãããï¼

`name` åã³ `hash` ãã£ã¼ã«ãã«ã¯ã Pinata ã¸ã¢ããã­ã¼ããããã¡ã¤ã«ã®åååã³çæããã CID ãå¥ãã¦ããã¾ãããã

```json
// products.json

[
  {
    "id": 1,
    "name": "ANYA WAKUWAKU PACK",
    "price": "0.09",
    "description": "Get this hot Anya pack for only $0.09! Includes 2 hot Anyas!",
    "image_url": "data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iMjM3LjY4NzVweCIgaGVpZ2h0PSIxMjJweCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB2aWV3Qm94PSIxMzEuMTU2MjUgMTQgMjM3LjY4NzUgMTIyIiBzdHlsZT0iYmFja2dyb3VuZDojNTk2ODg2IiBwcmVzZXJ2ZUFzcGVjdFJhdGlvPSJ4TWlkWU1pZCI+PGRlZnM+PGZpbHRlciBpZD0iZWRpdGluZy1ob3ZlciIgeD0iLTEwMCUiIHk9Ii0xMDAlIiB3aWR0aD0iMzAwJSIgaGVpZ2h0PSIzMDAlIj48ZmVGbG9vZCBmbG9vZC1jb2xvcj0iIzA1MmI0YSIgcmVzdWx0PSJmbG9vZCI+PC9mZUZsb29kPjxmZUNvbXBvc2l0ZSBvcGVyYXRvcj0iaW4iIGluMj0iU291cmNlQWxwaGEiIGluPSJmbG9vZCIgcmVzdWx0PSJzaGFkb3ciPjwvZmVDb21wb3NpdGU+PGZlT2Zmc2V0IGR4PSItNCIgZHk9Ii00IiBpbj0iU291cmNlR3JhcGhpYyIgcmVzdWx0PSJvZmZzZXQtMSI+PC9mZU9mZnNldD48ZmVPZmZzZXQgZHg9IjQiIGR5PSI0IiBpbj0ic2hhZG93IiByZXN1bHQ9Im9mZnNldC0yIj48L2ZlT2Zmc2V0PjxmZU1lcmdlPjxmZU1lcmdlTm9kZSBpbj0ib2Zmc2V0LTIiPjwvZmVNZXJnZU5vZGU+PGZlTWVyZ2VOb2RlIGluPSJvZmZzZXQtMSI+PC9mZU1lcmdlTm9kZT48L2ZlTWVyZ2U+PC9maWx0ZXI+PC9kZWZzPjxnIGZpbHRlcj0idXJsKCNlZGl0aW5nLWhvdmVyKSI+PGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMTcwLjY0MDAxMTMxMDU3NzQsIDk4LjM4OTk5OTM4OTY0ODQ0KSI+PHBhdGggZD0iTTMuODctMS45MkwzLjg3LTEuOTJMMy44Ny0xLjkyUTIuMzctMy41OCAxLjcwLTYuMjFMMS43MC02LjIxTDEuNzAtNi4yMVExLjAyLTguODMgMS4wMi0xMy4xMkwxLjAyLTEzLjEyTDEuMDItMTMuMTJRMS4wMi0xNy40MSAyLjUwLTIxLjMxTDIuNTAtMjEuMzFMMi41MC0yMS4zMVEzLjk3LTI1LjIyIDYuNjYtMjguMDNMNi42Ni0yOC4wM0w2LjY2LTI4LjAzUTEyLjE2LTMzLjkyIDIxLjI1LTMzLjkyTDIxLjI1LTMzLjkyTDIxLjI1LTMzLjkyUTI0LjUxLTMzLjkyIDI2Ljg4LTMyLjgzTDI2Ljg4LTMyLjgzTDM3LjgyLTMzLjkyTDMzLjA5LTguOTZMMzMuMDktOC45NlEzMi45MC04LjE5IDMyLjkwLTYuNzhMMzIuOTAtNi43OEwzMi45MC02Ljc4UTMyLjkwLTUuMzggMzMuNzYtNC40OEwzMy43Ni00LjQ4TDMzLjc2LTQuNDhRMzQuNjItMy41OCAzNS45MC0zLjQ2TDM1LjkwLTMuNDZMMzUuOTAtMy40NlEzNS4yNi0xLjI4IDMyLjkzIDBMMzIuOTMgMEwzMi45MyAwUTMwLjU5IDEuMjggMjcuOTcgMS4yOEwyNy45NyAxLjI4TDI3Ljk3IDEuMjhRMjUuMzQgMS4yOCAyMy41OCAwLjI5TDIzLjU4IDAuMjlMMjMuNTggMC4yOVEyMS44Mi0wLjcwIDIxLjMxLTIuMzdMMjEuMzEtMi4zN0wyMS4zMS0yLjM3UTIwLjI5LTAuNzcgMTguMTEgMC4yNkwxOC4xMSAwLjI2TDE4LjExIDAuMjZRMTUuOTQgMS4yOCAxMy4wMiAxLjI4TDEzLjAyIDEuMjhMMTMuMDIgMS4yOFExMC4xMSAxLjI4IDcuNzQgMC41MUw3Ljc0IDAuNTFMNy43NCAwLjUxUTUuMzgtMC4yNiAzLjg3LTEuOTJaTTE3LjM4LTI3LjkwTDE3LjM4LTI3LjkwTDE3LjM4LTI3LjkwUTE2LjY0LTI2Ljc1IDE2LTI0LjgwTDE2LTI0LjgwTDE2LTI0LjgwUTE1LjM2LTIyLjg1IDE0LjMwLTE3LjYzTDE0LjMwLTE3LjYzTDE0LjMwLTE3LjYzUTEzLjI1LTEyLjQyIDEzLjI1LTguNzBMMTMuMjUtOC43MEwxMy4yNS04LjcwUTEzLjI1LTQuOTkgMTMuODItMy45MEwxMy44Mi0zLjkwTDEzLjgyLTMuOTBRMTQuNDAtMi44MiAxNS40Mi0yLjgyTDE1LjQyLTIuODJMMTUuNDItMi44MlExNy40Ny0yLjgyIDE4Ljk4LTQuNzdMMTguOTgtNC43N0wxOC45OC00Ljc3UTIwLjQ4LTYuNzIgMjEuMDYtMTAuMThMMjEuMDYtMTAuMThMMjQuNDUtMjguOTNMMjQuNDUtMjguOTNRMjMuMTAtMzAuMDggMjEuNTQtMzAuMDhMMjEuNTQtMzAuMDhMMjEuNTQtMzAuMDhRMTkuOTctMzAuMDggMTkuMDQtMjkuNTdMMTkuMDQtMjkuNTdMMTkuMDQtMjkuNTdRMTguMTEtMjkuMDYgMTcuMzgtMjcuOTBaTTY4LjM1IDEuMjhMNjguMzUgMS4yOEw2OC4zNSAxLjI4UTYwLjYxIDEuMjggNjAuNjEtNC43NEw2MC42MS00Ljc0TDYwLjYxLTQuNzRRNjAuNjctNi40MCA2MS4xOC05LjIyTDYxLjE4LTkuMjJMNjIuMzQtMTUuMTBMNjIuMzQtMTUuMTBRNjQuMDYtMjMuNDIgNjQuMDYtMjUuMjhMNjQuMDYtMjUuMjhMNjQuMDYtMjUuMjhRNjQuMDYtMjguOTkgNjEuODktMjguOTlMNjEuODktMjguOTlMNjEuODktMjguOTlRNTguMjQtMjguOTkgNTYuMzItMTkuNDZMNTYuMzItMTkuNDZMNTIuNTQgMEwzOS42OCAxLjI4TDQ2LjM0LTMyLjcwTDU2LjgzLTMzLjkyTDU1LjgxLTI3LjY1TDU1LjgxLTI3LjY1UTU4LjgyLTMzLjkyIDY4LjAzLTMzLjkyTDY4LjAzLTMzLjkyTDY4LjAzLTMzLjkyUTcyLjUxLTMzLjkyIDc0LjQwLTMyLjAzTDc0LjQwLTMyLjAzTDc0LjQwLTMyLjAzUTc2LjI5LTMwLjE0IDc2LjI5LTI1LjkyTDc2LjI5LTI1LjkyTDc2LjI5LTI1LjkyUTc2LjI5LTIxLjk1IDc0LjI0LTEyLjY3TDc0LjI0LTEyLjY3TDc0LjI0LTEyLjY3UTczLjI4LTguNTEgNzMuMjgtNi45NEw3My4yOC02Ljk0TDczLjI4LTYuOTRRNzMuMjgtNS4zOCA3NC4xNC00LjQ4TDc0LjE0LTQuNDhMNzQuMTQtNC40OFE3NS4wMS0zLjU4IDc2LjI5LTMuNDZMNzYuMjktMy40Nkw3Ni4yOS0zLjQ2UTc1LjY1LTEuMjggNzMuNDQgMEw3My40NCAwTDczLjQ0IDBRNzEuMjMgMS4yOCA2OC4zNSAxLjI4Wk0xMDEuNzYtNy4yM0wxMDEuNzYtNy4yM0wxMDEuNzYtNy4yM1E5OC40My0zLjc4IDkyLjM1LTMuNzhMOTIuMzUtMy43OEw5Mi4zNS0zLjc4UTg0Ljc0LTMuNzggODMuMTQtOS4zNEw4My4xNC05LjM0TDgzLjE0LTkuMzRRODIuNjItMTEuMDEgODIuNjItMTIuODZMODIuNjItMTIuODZMODIuNjItMTIuODZRODIuNjItMTQuNzIgODMuMDEtMTYuNjRMODMuMDEtMTYuNjRMODYuMDItMzIuNjRMOTkuMDEtMzMuOTJMOTUuNDktMTUuMzBMOTUuNDktMTUuMzBROTUuMzYtMTQuNDYgOTUuMTctMTMuNTdMOTUuMTctMTMuNTdMOTUuMTctMTMuNTdROTQuOTgtMTIuNjcgOTQuOTgtMTEuNzRMOTQuOTgtMTEuNzRMOTQuOTgtMTEuNzRROTQuOTgtMTAuODIgOTUuMzAtMTAuMjFMOTUuMzAtMTAuMjFMOTUuMzAtMTAuMjFROTUuNjItOS42MCA5Ni4wNi05LjIyTDk2LjA2LTkuMjJMOTYuMDYtOS4yMlE5Ni44My04LjcwIDk4LjIxLTguNzBMOTguMjEtOC43MEw5OC4yMS04LjcwUTk5LjU4LTguNzAgMTAwLjc3LTEwLjM3TDEwMC43Ny0xMC4zN0wxMDAuNzctMTAuMzdRMTAxLjk1LTEyLjAzIDEwMi41My0xNC45MUwxMDIuNTMtMTQuOTFMMTA2LjA1LTMyLjY0TDExOC42Ni0zMy45MkwxMTMuODYtOC43N0wxMTMuODYtOC43N1ExMTEuNDkgMy41MiAxMDYuNjIgOC4zOEwxMDYuNjIgOC4zOEwxMDYuNjIgOC4zOFExMDQuMTMgMTAuODggMTAwLjkwIDExLjg3TDEwMC45MCAxMS44N0wxMDAuOTAgMTEuODdROTcuNjYgMTIuODYgOTMuNTAgMTIuODZMOTMuNTAgMTIuODZMOTMuNTAgMTIuODZRODYuNzggMTIuODYgODIuOTQgMTAuNzVMODIuOTQgMTAuNzVMODIuOTQgMTAuNzVRNzkuMTAgOC42NCA3OS4xMCA1LjEyTDc5LjEwIDUuMTJMNzkuMTAgNS4xMlE3OS4xMCAyLjUwIDgxLjA5IDAuOTlMODEuMDkgMC45OUw4MS4wOSAwLjk5UTgzLjA3LTAuNTEgODYuMTQtMC41MUw4Ni4xNC0wLjUxTDg2LjE0LTAuNTFRODguODMtMC41MSA5MC44OCAwLjY0TDkwLjg4IDAuNjRMOTAuODggMC42NFE5Mi4xMCAxLjM0IDkyLjY3IDIuMjRMOTIuNjcgMi4yNEw5Mi42NyAyLjI0UTkxLjIwIDMuNTIgOTEuMjAgNS42M0w5MS4yMCA1LjYzTDkxLjIwIDUuNjNROTEuMjAgOC40NSA5My43NiA4LjQ1TDkzLjc2IDguNDVMOTMuNzYgOC40NVE5Ny45OCA4LjQ1IDEwMC40Mi0xLjI4TDEwMC40Mi0xLjI4TDEwMC40Mi0xLjI4UTEwMS4xMi00LjE2IDEwMS43Ni03LjIzWk0xMjMuNzQtMS45MkwxMjMuNzQtMS45MkwxMjMuNzQtMS45MlExMjIuMjQtMy41OCAxMjEuNTctNi4yMUwxMjEuNTctNi4yMUwxMjEuNTctNi4yMVExMjAuOTAtOC44MyAxMjAuOTAtMTMuMTJMMTIwLjkwLTEzLjEyTDEyMC45MC0xMy4xMlExMjAuOTAtMTcuNDEgMTIyLjM3LTIxLjMxTDEyMi4zNy0yMS4zMUwxMjIuMzctMjEuMzFRMTIzLjg0LTI1LjIyIDEyNi41My0yOC4wM0wxMjYuNTMtMjguMDNMMTI2LjUzLTI4LjAzUTEzMi4wMy0zMy45MiAxNDEuMTItMzMuOTJMMTQxLjEyLTMzLjkyTDE0MS4xMi0zMy45MlExNDQuMzgtMzMuOTIgMTQ2Ljc1LTMyLjgzTDE0Ni43NS0zMi44M0wxNTcuNzAtMzMuOTJMMTUyLjk2LTguOTZMMTUyLjk2LTguOTZRMTUyLjc3LTguMTkgMTUyLjc3LTYuNzhMMTUyLjc3LTYuNzhMMTUyLjc3LTYuNzhRMTUyLjc3LTUuMzggMTUzLjYzLTQuNDhMMTUzLjYzLTQuNDhMMTUzLjYzLTQuNDhRMTU0LjUwLTMuNTggMTU1Ljc4LTMuNDZMMTU1Ljc4LTMuNDZMMTU1Ljc4LTMuNDZRMTU1LjE0LTEuMjggMTUyLjgwIDBMMTUyLjgwIDBMMTUyLjgwIDBRMTUwLjQ2IDEuMjggMTQ3Ljg0IDEuMjhMMTQ3Ljg0IDEuMjhMMTQ3Ljg0IDEuMjhRMTQ1LjIyIDEuMjggMTQzLjQ2IDAuMjlMMTQzLjQ2IDAuMjlMMTQzLjQ2IDAuMjlRMTQxLjcwLTAuNzAgMTQxLjE4LTIuMzdMMTQxLjE4LTIuMzdMMTQxLjE4LTIuMzdRMTQwLjE2LTAuNzcgMTM3Ljk4IDAuMjZMMTM3Ljk4IDAuMjZMMTM3Ljk4IDAuMjZRMTM1LjgxIDEuMjggMTMyLjkwIDEuMjhMMTMyLjkwIDEuMjhMMTMyLjkwIDEuMjhRMTI5Ljk4IDEuMjggMTI3LjYyIDAuNTFMMTI3LjYyIDAuNTFMMTI3LjYyIDAuNTFRMTI1LjI1LTAuMjYgMTIzLjc0LTEuOTJaTTEzNy4yNS0yNy45MEwxMzcuMjUtMjcuOTBMMTM3LjI1LTI3LjkwUTEzNi41MS0yNi43NSAxMzUuODctMjQuODBMMTM1Ljg3LTI0LjgwTDEzNS44Ny0yNC44MFExMzUuMjMtMjIuODUgMTM0LjE4LTE3LjYzTDEzNC4xOC0xNy42M0wxMzQuMTgtMTcuNjNRMTMzLjEyLTEyLjQyIDEzMy4xMi04LjcwTDEzMy4xMi04LjcwTDEzMy4xMi04LjcwUTEzMy4xMi00Ljk5IDEzMy43MC0zLjkwTDEzMy43MC0zLjkwTDEzMy43MC0zLjkwUTEzNC4yNy0yLjgyIDEzNS4zMC0yLjgyTDEzNS4zMC0yLjgyTDEzNS4zMC0yLjgyUTEzNy4zNC0yLjgyIDEzOC44NS00Ljc3TDEzOC44NS00Ljc3TDEzOC44NS00Ljc3UTE0MC4zNS02LjcyIDE0MC45My0xMC4xOEwxNDAuOTMtMTAuMThMMTQ0LjMyLTI4LjkzTDE0NC4zMi0yOC45M1ExNDIuOTgtMzAuMDggMTQxLjQxLTMwLjA4TDE0MS40MS0zMC4wOEwxNDEuNDEtMzAuMDhRMTM5Ljg0LTMwLjA4IDEzOC45MS0yOS41N0wxMzguOTEtMjkuNTdMMTM4LjkxLTI5LjU3UTEzNy45OC0yOS4wNiAxMzcuMjUtMjcuOTBaIiBmaWxsPSIjZmZkNWFmIj48L3BhdGg+PC9nPjwvZz48c3R5bGU+dGV4dCB7CiAgZm9udC1zaXplOiA2NHB4OwogIGZvbnQtZmFtaWx5OiBBcmlhbCBCbGFjazsKICBkb21pbmFudC1iYXNlbGluZTogY2VudHJhbDsKICB0ZXh0LWFuY2hvcjogbWlkZGxlOwp9PC9zdHlsZT48L3N2Zz4=",
    "filename": "anya",
    "hash": "QmcJPLeiXBwA17WASSXs5GPWJs1n1HEmEmrtcmDgWjApjm"
  }
]
```

æ¬¡ã«ã`components` ãã©ã«ãã« `Product.js` ãã¡ã¤ã«ãä½æãã¦ä»¥ä¸ã®ã³ã¼ããè²¼ãä»ãã¦ãã ããã

```jsx
// Product.js

import React from "react";
import styles from "../styles/Product.module.css";
import IPFSDownload from './IpfsDownload';

export default function Product({ product }) {
  const { id, name, price, description, image_url } = product;

  return (
    <div className={styles.product_container}>
      <div >
        <img className={styles.product_image}src={image_url} alt={name} />
      </div>

      <div className={styles.product_details}>
        <div className={styles.product_text}>
          <div className={styles.product_title}>{name}</div>
          <div className={styles.product_description}>{description}</div>
        </div>

        <div className={styles.product_action}>
          <div className={styles.product_price}>{price} USDC</div>
          {/* ä»¥ä¸ã®é¨åã¯å¾ã»ã©APIããããã·ã¥ãåå¾ããå¦çã«å¤æ´ãã¾ãã */}
          <IPFSDownload filename="anya" hash="QmcJPLeiXBwA17WASSXs5GPWJs1n1HEmEmrtcmDgWjApjm" cta="Download goods"/>
        </div>
      </div>
    </div>
  );
}
```

ç¶ãã¦ããã¼ã¿ãã¼ã¹ããè£½åããã§ããã§ãã API ã¨ã³ããã¤ã³ããä½æãã¾ãã

`pages/api` ãã©ã«ãåã« `fetchProducts.js` ãã¡ã¤ã«ãä½æãã¦ä»¥ä¸ã®ã³ã¼ããè²¼ãä»ãã¦ãã ããã

```jsx
// fetchProducts.js

import products from "./products.json"

export default function handler(req, res) {
  if (req.method === "GET") {
    // ãªã¯ã¨ã¹ããåãåã£ãå ´åãããã·ã¥ã¨ãã¡ã¤ã«åãé¤ããè£½åã®ã³ãã¼ãä½æãã¾ããï¼éåï¼
    const productsNoHashes = products.map((product) => {

      const { hash, filename, ...rest } = product;
      return rest;
    });

    res.status(200).json(productsNoHashes);
  }
  else {
    res.status(405).send(`Method ${req.method} not allowed`);
  }
}
```

ããã§ããã·ã¥ããã§ããããªãçç±ã¯ããã® Web ã¢ããªã±ã¼ã·ã§ã³ãé²è¦§ããäººãæ¯æããå®äºããåã«ããã·ã¥ãæ¸¡ããããªãããã§ãã

ãã¦ãããã¾ã§ã®ä½æ¥­ããã­ã³ãã¨ã³ãã«åæ ãããããã« `index.js` ãä»¥ä¸ã®ããã«æ´æ°ãã¾ãããã

```jsx
// index.js

import React, { useEffect, useState } from 'react';
import Product from "../components/Product";
import HeadComponent from '../components/Head';

import { useWallet } from '@solana/wallet-adapter-react';
import { WalletMultiButton } from '@solana/wallet-adapter-react-ui';

// å®æ°ãå®£è¨ãã¾ãã
const TWITTER_HANDLE = "ããªãã®Twitterãã³ãã«";
const TWITTER_LINK = `https://twitter.com/${TWITTER_HANDLE}`;

const App = () => {
  const { publicKey } = useWallet();
  const [products, setProducts] = useState([]);

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

  const renderNotConnectedContainer = () => (
    <div>
      <img src="https://media.giphy.com/media/FWAcpJsFT9mvrv0e7a/giphy.gif" alt="anya" />
      <div className="button-container">
        <WalletMultiButton className="cta-button connect-wallet-button" />
      </div>
    </div>
  );

  const renderItemBuyContainer = () => (
    <div className="products-container">
      {products.map((product) => (
        <Product key={product.id} product={product} />
      ))}
    </div>
  );

  return (
    <div className="App">
      <div className="container">
        <header className="header-container">
          <p className="header"> ð³ UNCHAIN Image Store ð</p>
          <p className="sub-text">The only Image store that accepts shitcoins</p>
        </header>

        <main>
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

ããã§ãã¦ã©ã¬ãããæ¥ç¶ããã¨ Web ã¢ããªã±ã¼ã·ã§ã³ã« `Download` ãã¿ã³ãè¡¨ç¤ºãããããã«ãªãã¾ããã

`Download` ãã¿ã³ãã¯ãªãã¯ããã¨ã IPFS ããè©²å½ã®ãã¡ã¤ã«ããã¦ã³ã­ã¼ããããã¨ãã§ãã¾ãã

IPFS ä¸ã®ãã¡ã¤ã«ã¯è¤æ°ã®ãã¼ãã«ã­ã£ãã·ã¥ããããããã¢ããã­ã¼ãããã°ããã®ãã¡ã¤ã«ã¯å°æ°ã®ãã¼ãã«ããå­å¨ããããã¦ã³ã­ã¼ãã«å°ãæéãããããã¨ãããã¾ãã

éã«ãã¡ã¤ã«ã¸ã®ã¢ã¯ã»ã¹ãå¤ãã»ã©ãã­ã£ãã·ã¥ããããã¼ããå¤ããªãããããã¦ã³ã­ã¼ããéããªãã¾ãã


### ð ããªãã ãã®ååæ£ã¸!

ä»¥ä¸ã®ã³ãã³ãã§ Web ã¢ããªã±ã¼ã·ã§ã³ãåããã¦ã¿ã¾ãããã

```bash
npx next dev
```

ã¦ã©ã¬ããæ¥ç¶å¾ã®ç»é¢ã§ããããåä»ããããååãä¸¦ã¹ããã¦ããã¯ãã§ãã

ä½åã®ããäººã¯ã`products.json` ã«æ°ããååãè¿½å ãã¦ã¿ã¾ããã!


### ðââï¸ è³ªåãã

ããã¾ã§ã®ä½æ¥­ã§ä½ãããããªããã¨ãããå ´åã¯ãDiscord ã® `#section-1` ã§è³ªåããã¦ãã ããã

ãã«ããããã¨ãã®ãã­ã¼ãåæ»ã«ãªãã®ã§ãã¨ã©ã¼ã¬ãã¼ãã«ã¯ä¸è¨ã® 4 ç¹ãè¨è¼ãã¦ãã ãã â¨

```
1. è³ªåãé¢é£ãã¦ããã»ã¯ã·ã§ã³çªå·ã¨ã¬ãã¹ã³çªå·
2. ä½ããããã¨ãã¦ããã
3. ã¨ã©ã¼æãã³ãã¼&ãã¼ã¹ã
4. ã¨ã©ã¼ç»é¢ã®ã¹ã¯ãªã¼ã³ã·ã§ãã
```

---

ããã§ã¨ããããã¾ã!

ã»ã¯ã·ã§ã³ 1 ã¯çµäºã§ã!

ãã²ãããªãã®ãæ°ã«å¥ãã®ååãè¡¨ç¤ºããããã­ã³ãã¨ã³ãã®ã¹ã¯ãªã¼ã³ã·ã§ããã `#section-1` ã«æç¨¿ãã¦ãã ãã ð

ããªãã®æåãã³ãã¥ããã£ã§ç¥ãã¾ããã ð

æ¬¡ã®ã»ã¯ã·ã§ã³ã§ã¯ãæ±ºæ¸æ©è½ãå®è£ãã¦ããã¾ã!
