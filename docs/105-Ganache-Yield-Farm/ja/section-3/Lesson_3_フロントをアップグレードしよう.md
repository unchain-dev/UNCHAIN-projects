###  ð¥ ãã®ã¬ãã¹ã³ã®åèåç»URL
[Dapp University](https://youtu.be/CgXQC4dbGUE?t=7594)

### ð¥ ããã¯ã¨ã³ãã¨ãã­ã³ãã¨ã³ãã®æ¥ç¶é¨åã®æ®ããå®æããã

åã®ã¬ãã¹ã³ã§ä½æããããã®ã«å ãã¦ä»ä¸ãããã¦ããã¯ã¨ã³ãã¨ãã­ã³ãã¨ã³ãã®æ¥ç¶é¨åãå®æããã¾ããã!

`App.js` ãä»¥ä¸ã®ããã«æ´æ°ãã¦ãã ããã

```javascript
// App.js
// ãã­ã³ãã¨ã³ããæ§ç¯ããä¸ã§å¿è¦ãªãã¡ã¤ã«ãã©ã¤ãã©ãªãã¤ã³ãã¼ããã
import React, { Component } from 'react'
import Web3 from 'web3'
import DaiToken from '../abis/DaiToken.json'
import DappToken from '../abis/DappToken.json'
import TokenFarm from '../abis/TokenFarm.json'
import Navbar from './Navbar'
import Main from './Main'
import './App.css'

class App extends Component {
  // componentWillMount(): ä¸»ã«ãµã¼ãã¼ã¸ã®APIã³ã¼ã«ãè¡ããªã©ãå®éã®ã¬ã³ããªã³ã°ãè¡ãããåã«ãµã¼ãã¼ãµã¤ãã®ã­ã¸ãã¯ãå®è£ããããã«ä½¿ç¨ã
  async componentWillMount() {
    await this.loadWeb3()
    await this.loadBlockchainData()
  }
  // loadBlockchainData(): ãã­ãã¯ãã§ã¼ã³ä¸ã®ãã¼ã¿ã¨ããåãããããã®é¢æ°
  // MetaMask ã¨ã®æ¥ç¶ã«ãã£ã¦å¾ãããæå ±ã¨ã³ã³ãã©ã¯ãã¨ã®æå ±ãä½¿ã£ã¦æç»ã«ä½¿ãæå ±ãåå¾ã
  async loadBlockchainData() {
    const web3 = window.web3
    // ã¦ã¼ã¶ã¼ã® Metamask ã®ä¸çªæåã®ã¢ã«ã¦ã³ãï¼è¤æ°ã¢ã«ã¦ã³ããå­å¨ããå ´åï¼åå¾
    const accounts = await web3.eth.getAccounts()
    // ã¦ã¼ã¶ã¼ã® Metamask ã¢ã«ã¦ã³ããè¨­å®
    // ãã®æ©è½ã«ãããApp.js ã«è¨è¼ããã¦ãã constructor() åã® accountï¼ããã©ã«ã: '0x0'ï¼ãæ´æ°ããã
    this.setState({ account: accounts[0]})
    // ã¦ã¼ã¶ã¼ã Metamask ãä»ãã¦æ¥ç¶ãã¦ãããããã¯ã¼ã¯IDãåå¾
    const networkId = await web3.eth.net.getId()

    // DaiToken ã®ãã¼ã¿ãåå¾
    const daiTokenData = DaiToken.networks[networkId]
    if(daiTokenData){
      // DaiToken ã®æå ±ã daiToken ã«æ ¼ç´ãã
      const daiToken = new web3.eth.Contract(DaiToken.abi, daiTokenData.address)
      // constructor() åã® daiToken ã®æå ±ãæ´æ°ãã
      this.setState({daiToken})
      // ã¦ã¼ã¶ã¼ã® Dai ãã¼ã¯ã³ã®æ®é«ãåå¾ãã
      let daiTokenBalance = await daiToken.methods.balanceOf(this.state.account).call()
      // daiTokenBalanceï¼ã¦ã¼ã¶ã¼ã® Dai ãã¼ã¯ã³ã®æ®é«ï¼ãã¹ããªã³ã°åã«å¤æ´ãã
      this.setState({daiTokenBalance: daiTokenBalance.toString()})
      // ã¦ã¼ã¶ã¼ã® Dai ãã¼ã¯ã³ã®æ®é«ããã­ã³ãã¨ã³ãã® Console ã«åºåãã
      console.log(daiTokenBalance.toString())
    }else{
      window.alert('DaiToken contract not deployed to detected network.')
    }
    // â --- 1. è¿½å ããã³ã¼ã ---- â
    // DappToken ã®ãã¼ã¿ãåå¾
    const dappTokenData = DappToken.networks[networkId]
    if(dappTokenData){
      // DappToken ã®æå ±ã dappToken ã«æ ¼ç´ãã
      const dappToken = new web3.eth.Contract(DappToken.abi, dappTokenData.address)
      // constructor() åã® dappToken ã®æå ±ãæ´æ°ãã
      this.setState({dappToken})
      // ã¦ã¼ã¶ã¼ã® Dapp ãã¼ã¯ã³ã®æ®é«ãåå¾ãã
      let dappTokenBalance = await dappToken.methods.balanceOf(this.state.account).call()
      // dappTokenBalanceï¼ã¦ã¼ã¶ã¼ã® Dapp ãã¼ã¯ã³ã®æ®é«ï¼ãã¹ããªã³ã°åã«å¤æ´ãã
      this.setState({dappTokenBalance: dappTokenBalance.toString()})
      // ã¦ã¼ã¶ã¼ã® Dapp ãã¼ã¯ã³ã®æ®é«ããã­ã³ãã¨ã³ãã® Console ã«åºåãã
      console.log(dappTokenBalance.toString())
    }else{
      window.alert('DappToken contract not deployed to detected network.')
    }

    // tokenFarmData ã®ãã¼ã¿ãåå¾
    const tokenFarmData = TokenFarm.networks[networkId]
    if(tokenFarmData){
      // TokenFarm ã®æå ±ã tokenFarm ã«æ ¼ç´ãã
      const tokenFarm = new web3.eth.Contract(TokenFarm.abi, tokenFarmData.address)
      // constructor() åã® tokenFarm ã®æå ±ãæ´æ°ãã
      this.setState({tokenFarm})
      // tokenFarm åã«ã¹ãã¼ã­ã³ã°ããã¦ãã Dai ãã¼ã¯ã³ã®æ®é«ãåå¾ãã
      let tokenFarmBalance = await tokenFarm.methods.stakingBalance(this.state.account).call()
      // tokenFarmBalance ãã¹ããªã³ã°åã«å¤æ´ãã
      this.setState({stakingBalance: tokenFarmBalance.toString()})
      // ã¦ã¼ã¶ã¼ã® tokenFarmBalance ããã­ã³ãã¨ã³ãã® Console ã«åºåãã
      console.log(tokenFarmBalance.toString())
    }else{
      window.alert('TokenFarm contract not deployed to detected network.')
    }
    // â --- 1. è¿½å ããã³ã¼ã ---- â
  }
  // loadWeb3(): ã¦ã¼ã¶ã¼ã Metamask ã¢ã«ã¦ã³ããæã£ã¦ãããç¢ºèªããé¢æ°
  async loadWeb3() {
    // ã¦ã¼ã¶ã¼ã Metamask ã®ã¢ã«ã¦ã³ããæã£ã¦ããå ´åã¯ãã¢ãã¬ã¹ãåå¾
    if (window.ethereum) {
      window.web3 = new Web3(window.ethereum)
      await window.ethereum.enable()
    }
    else if (window.web3) {
      window.web3 = new Web3(window.web3.currentProvider)
    }
    // ã¦ã¼ã¶ã¼ã Metamask ã®ã¢ã«ã¦ã³ããæã£ã¦ããªãã£ãå ´åã¯ãã¨ã©ã¼ãè¿ã
    else {
      window.alert('Non ethereum browser detected. You should consider trying to install metamask')
    }

    this.setState({ loading: false})
  }
  // â --- 2. è¿½å ããã³ã¼ã ---- â
  // TokenFarm.sol ã«è¨è¼ãããã¹ãã¼ã­ã³ã°æ©è½ãå¼ã³åºã
  stakeTokens = (amount) => {
    this.setState({loading: true})
    this.state.daiToken.methods.approve(this.state.tokenFarm._address, amount).send({from: this.state.account}).on('transactionHash', (hash)=> {
      this.state.tokenFarm.methods.stakeTokens(amount).send({from: this.state.account}).on('transactionHash', (hash) => {
        this.setState({loading: false})
      })
    })
  }
  // TokenFarm.sol ã«è¨è¼ãããã¢ã³ã¹ãã¼ã­ã³ã°æ©è½ãå¼ã³åºã
  unstakeTokens = (amount) => {
    this.setState({loading: true})
    this.state.tokenFarm.methods.unstakeTokens().send({from: this.state.account}).on('transactionHash', (hash) => {
      this.setState({loading: false})
    })
  }
  // â --- 2. è¿½å ããã³ã¼ã ---- â

  // constructor(): ãã­ãã¯ãã§ã¼ã³ããèª­ã¿è¾¼ãã ãã¼ã¿ + ã¦ã¼ã¶ã¼ã®ç¶æãæ´æ°ããé¢æ°
  constructor(props) {
    super(props)
    this.state = {
      account: '0x0',
      daiToken: {},
      dappToken: {},
      tokenFarm: {},
      daiTokenBalance: '0',
      dappTokenBalance: '0',
      stakingBalance: '0',
      loading: true
    }
  }

  // ãã­ã³ãã¨ã³ãã®ã¬ã³ããªã³ã°ãä»¥ä¸ã§å®è¡ããã
  render() {
    let content
    if(this.state.loading){
      content = <p id='loader' className='text-center'>Loading...</p>
    }else{
      content = <Main
        daiTokenBalance = {this.state.daiTokenBalance}
        dappTokenBalance = {this.state.dappTokenBalance}
        stakingBalance = {this.state.stakingBalance}
        stakeTokens = {this.stakeTokens}
        unstakeTokens={this.unstakeTokens}
      />
    }
    return (
      <div>
        <Navbar account={this.state.account} />
        <div className="container-fluid mt-5">
          <div className="row">
            <main role="main" className="col-lg-12 ml-auto mr-auto" style={{ maxWidth: '600px' }}>
              <div className="content mr-auto ml-auto">
                <a
                  href="http://www.dappuniversity.com/bootcamp"
                  target="_blank"
                  rel="noopener noreferrer"
                >
                </a>

                {content}

              </div>
            </main>
          </div>
        </div>
      </div>
    );
  }
}

export default App;

```

ã¾ãã¯ä»¥ä¸ã®ã¤ã³ãã¼ãé¨åãè¦ã¦ããã¾ãããã

```javascript
// App.js
import React, { Component } from 'react'
import Web3 from 'web3'
import DaiToken from '../abis/DaiToken.json'
import DappToken from '../abis/DappToken.json'
import TokenFarm from '../abis/TokenFarm.json'
import Navbar from './Navbar'
import Main from './Main'
import './App.css'
```

ããã§æ³¨ç®ãã¦ããã ãããã®ã¯ã`DappToken.json`ã`TokenFarm.json`ã`Main.js` ãã¤ã³ãã¼ããã¦ããç¹ã§ãã

`Main.js` ã¯ãã¦ã¼ã¶ã¼ã®ç¶æã«å¿ãã¦ãã­ã³ãã¨ã³ãã®è¡¨ç¤ºï¼UIï¼ãå¤ãããã¨ãã«ãifæãå¤ããã¦ã³ã¼ããèª­ã¿ã¥ãããªããªãããã«ãã³ã¼ããåå²ãã¦ä¿å­ããããã«ä½¿ããã¡ã¤ã«ã§ãããã®ã¬ãã¹ã³ã®æå¾ã«ä½æãã¾ãð¥

ã¤ã¾ããã­ã¼ãæä»¥å¤ã®ãã­ã³ãã¨ã³ãã§ã¬ã³ããªã³ã°ããããã¶ã¤ã³ã¯ã`Main.js`ã«ããã®ã§ã!

æ¬¡ã«ã`dappTokenData` ã¨ `tokenFarmData` ãä½¿ç¨ããã¹ãã¼ãã³ã³ãã©ã¯ãã®ãã¼ã¿ãWEBã¢ããªã«èª­ã¿è¾¼ãã³ã¼ããè¦ã¦ããã¾ãããã

```javascript
// App.js
// â --- 1. è¿½å ããã³ã¼ã ---- â
// DappToken ã®ãã¼ã¿ãåå¾
const dappTokenData = DappToken.networks[networkId]
if(dappTokenData){
  // DappToken ã®æå ±ã dappToken ã«æ ¼ç´ãã
  const dappToken = new web3.eth.Contract(DappToken.abi, dappTokenData.address)
  // constructor() åã® dappToken ã®æå ±ãæ´æ°ãã
  this.setState({dappToken})
  // ã¦ã¼ã¶ã¼ã® Dapp ãã¼ã¯ã³ã®æ®é«ãåå¾ãã
  let dappTokenBalance = await dappToken.methods.balanceOf(this.state.account).call()
  // dappTokenBalanceï¼ã¦ã¼ã¶ã¼ã® Dapp ãã¼ã¯ã³ã®æ®é«ï¼ãã¹ããªã³ã°åã«å¤æ´ãã
  this.setState({dappTokenBalance: dappTokenBalance.toString()})
  // ã¦ã¼ã¶ã¼ã® Dapp ãã¼ã¯ã³ã®æ®é«ããã­ã³ãã¨ã³ãã® Console ã«åºåãã
  console.log(dappTokenBalance.toString())
}else{
  window.alert('DappToken contract not deployed to detected network.')
}

// tokenFarmData ã®ãã¼ã¿ãåå¾
const tokenFarmData = TokenFarm.networks[networkId]
if(tokenFarmData){
  // TokenFarm ã®æå ±ã tokenFarm ã«æ ¼ç´ãã
  const tokenFarm = new web3.eth.Contract(TokenFarm.abi, tokenFarmData.address)
  // constructor() åã® tokenFarm ã®æå ±ãæ´æ°ãã
  this.setState({tokenFarm})
  // tokenFarm åã«ã¹ãã¼ã­ã³ã°ããã¦ãã Dai ãã¼ã¯ã³ã®æ®é«ãåå¾ãã
  let tokenFarmBalance = await tokenFarm.methods.stakingBalance(this.state.account).call()
  // tokenFarmBalance ãã¹ããªã³ã°åã«å¤æ´ãã
  this.setState({stakingBalance: tokenFarmBalance.toString()})
  // ã¦ã¼ã¶ã¼ã® tokenFarmBalance ããã­ã³ãã¨ã³ãã® Console ã«åºåãã
  console.log(tokenFarmBalance.toString())
}else{
  window.alert('TokenFarm contract not deployed to detected network.')
}
// â --- 1. è¿½å ããã³ã¼ã ---- â
```

å®éã«ããã­ã³ãã¨ã³ãããã©ã¦ã¶ã§ç¢ºèªããéã«ãå³ã¯ãªãã¯ â `Inspect` â `Console` ãé¸æãã¦ã`console.log` ã§åºåãããçµæãç¢ºèªãã¦ã¿ã¦ãã ããã

æ¬¡ã« `stakeTokens`ã`unstakeTokens` ã¡ã½ããã«ã¤ãã¦æ¸ãããé¨åãè¦ã¦ããã¾ãããã

```javascript
// App.js
// â --- 2. è¿½å ããã³ã¼ã ---- â
// TokenFarm.sol ã«è¨è¼ãããã¹ãã¼ã­ã³ã°æ©è½ãå¼ã³åºã
stakeTokens = (amount) => {
  this.setState({loading: true})
  this.state.daiToken.methods.approve(this.state.tokenFarm._address, amount).send({from: this.state.account}).on('transactionHash', (hash)=> {
    this.state.tokenFarm.methods.stakeTokens(amount).send({from: this.state.account}).on('transactionHash', (hash) => {
      this.setState({loading: false})
    })
  })
}
// TokenFarm.sol ã«è¨è¼ãããã¢ã³ã¹ãã¼ã­ã³ã°æ©è½ãå¼ã³åºã
unstakeTokens = (amount) => {
  this.setState({loading: true})
  this.state.tokenFarm.methods.unstakeTokens().send({from: this.state.account}).on('transactionHash', (hash) => {
    this.setState({loading: false})
  })
}
// â --- 2. è¿½å ããã³ã¼ã ---- â
```

ããã§ã¯ `TokenFarm.sol` ã§ä½æãããã¡ã½ãããå¼ã³åºãã¦ããã­ã³ãã¨ã³ãä¸ã§ã¦ã¼ã¶ã¼ãã¹ãã¼ã­ã³ã°ã¨ã¢ã³ã¹ãã¼ã­ã³ã°ãè¡ãããã®å¦çãè¨è¿°ããã¦ãã¾ãã

æå¾ã« `render` ã¡ã½ããã®ä¸­ã§ `return` ã®åã«æ¸ããã¦ããå¦çãè¦ã¦ããã¾ãããã

```javascript
// App.js
let content
    if(this.state.loading){
      content = <p id='loader' className='text-center'>Loading...</p>
    }else{
      content = <Main
        daiTokenBalance = {this.state.daiTokenBalance}
        dappTokenBalance = {this.state.dappTokenBalance}
        stakingBalance = {this.state.stakingBalance}
        stakeTokens = {this.stakeTokens}
        unstakeTokens={this.unstakeTokens}
      />
    }
```

ããã§ã¯ã`render` ã¡ã½ãããä½¿ç¨ãããã¨ã§ããã­ã³ãã¨ã³ãã®ç¶æã«ãããæç»ããã³ã³ãã¼ãã³ããåãæ¿ããå¦çãè¨è¼ããã¦ãã¾ãã

`App.js` ã®ä¸­ã«ä»¥ä¸ã®ãããªã³ã¼ããè¨è¼ããã¦ãããã¨ã«ãæ°ã¥ãã§ããããï¼

```javascript
// App.js
this.setState({loading: true})
```
```javascript
// App.js
this.setState({loading: false})
```

`this.setState()` ã¯ããã­ã³ãã¨ã³ããã­ã¼ãã£ã³ã°ç¶æã§ãããå¦ãè¨­å®ããé¢æ°ã§ãããã®é¢æ°ã«ããããã­ã³ãã¨ã³ãã«ç°ãªãã³ã³ãã¼ãã³ããè¡¨ç¤ºããã¾ãã
- `loading` ã `true` ã®å ´åã«ã¯ãã­ã³ãã¨ã³ãç»é¢ã« `loading` ã¨è¡¨ç¤ºããã¾ãã
- `loading` ã `false` ã®å ´åã¯ `Main` ã³ã³ãã¼ãã³ãã«å¤æ°ãåãæ¸¡ãã¦ã`Main` ã³ã³ãã¼ãã³ãã«æ¸ããã¦ãããã¶ã¤ã³ããã­ã³ãã¨ã³ãã«æç»ããã¾ãã

### ð¨âð¨ `Main.js` ãä½æãã

ããã§ã¯ãä»ä¸ãã« `Main.js` ã `Components` ãã£ã¬ã¯ããªã«ä½æãã¦ããã¾ãã

ã¿ã¼ããã«ãéãã¦ `yield-farm-starter-project` ã«ãããã¨ãç¢ºèªããããä¸è¨ã®ã³ã¼ããå®è¡ãã¦ãã ããã

```bash
touch src/components/Main.js
```

ãã¡ã¤ã«ãå®æããã `Main.js` ã«ä»¥ä¸ã®ã³ã¼ããè¨è¿°ãã¦ãã ããã

```javascript
// Main.js
import React, { Component } from 'react'
import dai from '../dai.png'
class Main extends Component {
  render() {
    return (
      <div id='content' className='mt-3'>
       <table className='table table-borderless text-muted text-center'>
           <thead>
               <tr>
                   <th scope='col'>Staking Balance</th>
                   <th scope='col'>Reward Balance</th>
               </tr>
           </thead>
           <tbody>
               <tr>
                   <td>{window.web3.utils.fromWei(this.props.stakingBalance, 'Ether')} mDAI</td>
                   <td>{window.web3.utils.fromWei(this.props.dappTokenBalance, 'Ether')} DAPP</td>
               </tr>
           </tbody>
       </table>
       <div className='card mb-4'>
           <div className='card-body'>
               <form className='mb-3' onSubmit={(event) => {
                   event.preventDefault()
                   let amount
                   amount = this.input.value.toString()
                   amount = window.web3.utils.toWei(amount, 'Ether')
                   this.props.stakeTokens(amount)
               }}>
                   <div>
                       <label className='float-left'><b>Stake Tokens</b></label>
                       <span className='float-right text-muted'>
                       Balance: {window.web3.utils.fromWei(this.props.daiTokenBalance, 'Ether')}
                       </span>
                   </div>
                   <div className='input-group mb-4'>
                       <input
                        type="text"
                        ref = {(input) => {this.input = input}}
                        className="form-control form-control-lg"
                        placeholder='0'
                        required
                       />
                       <div className='input-group-append'>
                           <img src={dai} height='32' alt=""/>
                           &nbsp;&nbsp;&nbsp; mDai
                       </div>
                   </div>
                   <button type='submit' className='btn btn-primary btn-block btn-lg'>STAKE!</button>
               </form>
               <button
                type='submit'
                className='btn btn-link btn-block btn-sm'
                onClick={(event) => {
                    event.preventDefault()
                    this.props.unstakeTokens()
                }}
                >
                    UN-STAKE...
                </button>
           </div>
       </div>
      </div>
    );
  }
}

export default Main;
```

`Main.js` ã«ã¯ãToken Farm ã®ã¢ããªã®æ¨æºã®UIãè¨è¿°ããã¦ãã¾ãã

ããã§ãã­ã³ãã¨ã³ãã¨ããã¯ã¨ã³ãããã®æ¥ç¶é¨åã¯å®æã«ãªãã¾ã!

ã§ã¯æ©éãåããã¦ããã¾ãããã

ã¿ã¼ããã«ãéãã¦ `yield-farm-starter-project` ã«ãããã¨ãç¢ºèªãã¦ããä¸è¨ã®ã³ã¼ããé çªã«å®è¡ãã¦ã¿ã¾ãããã

```bash
npm run start
```

ããã¨ããã®ãããªç»é¢ãåºã¦ããã¯ãã§ãã
![](/public/images/105-Ganache-Yield-Farm/section-1/12_3_9.png)

ããã§å¥åæ¬ã«100ä»¥ä¸ã®æ°å­ãæã¡è¾¼ãã§ `STAKE!` ãã¿ã³ãæ¼ãã¦ã¿ã¦ãã ããã

ãã®å¾ä¸ã®ç»åã®ããã« MetaMask ã®ç»é¢ã2ååºã¦ããã®ã§ãã®äºã¤ãæ¿èªãã¾ãã
![](/public/images/105-Ganache-Yield-Farm/section-1/12_3_10.png)
![](/public/images/105-Ganache-Yield-Farm/section-1/12_3_11.png)

æå¾ã«ãã¼ã¸ããªã­ã¼ãããããä¸ã®ç»åã®ããã« Staking Balance ãå¢ãã¦ãBalance ãæ¸ã£ã¦ããã¯ãã§ãã

![](/public/images/105-Ganache-Yield-Farm/section-1/12_3_12.png)

ããã§ã¹ãã¼ã­ã³ã°ãæåãã¾ããð

ä¸æ¹ã§ãã¼ã¯ã³ã®çºè¡ã¯ã©ãã§ããããï¼

Reward Balance ã¯å¤ãã£ã¦ãã¾ããã­ã

ããããã®ã¯ãã§ãð ãã¼ã¯ã³ã®çºè¡ã¯æåã§è¡ããã¨ã«ãã¦ããã®ã§ããªããæä½ããå¿è¦ãããã¾ãã

ã¨ãããã¨ã§ `npm run start` ãå®è¡ããã¿ã¼ããã«ã¨ã¯å¥ã®ã¿ã¼ããã«ãéãã¦ã`yield-farm-starter-project` ã«ãããã¨ãç¢ºèªãã¦ããä¸è¨ã®ã³ã¼ããå®è¡ãã¦ã¿ã¾ãããã

```bash
truffle exec scripts/issue-token.js
```

ã¿ã¼ããã«ã«ä»¥ä¸ã®ãããªçµæãè¿ã£ã¦ããã° `issue` ã¡ã½ããã®å®è¡ã¯æåã§ã!

```bash
Using network 'development'.

Tokens issued!
```

ã§ã¯æå¾ã« `Dapp Token Farm` ã®ç»é¢ã«ç§»ã£ã¦ã¿ã¾ãããã
ä¸ã®ããã«å ±é¬ã¨ãã¦ `Reward Balance` ã `Staking Balance` ã¨åãæ°ã«ãªã£ã¦ããã¯ãã§ãã

![](/public/images/105-Ganache-Yield-Farm/section-1/12_3_13.png)

ã¾ãã`unstake` æ©è½ãã¹ãã¼ã­ã³ã°æ©è½åæ§ã« `UN-STAKE...` ãã¿ã³ãæ¼ãã°å®è¡ã§ããã®ã§è©¦ãã¦ã¿ã¦ãã ãã!

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
ããã§ãã­ã³ãã¨ã³ããå®æãã¾ãã!ããªãã®ãã­ã³ãã¨ã³ãã®ã¹ã¯ãªã¼ã³ã·ã§ããã `#section-3` ã«ã·ã§ã¢ãã¦ãã ããð

æ¬¡ã®ã¬ãã¹ã³ã§ä½ã£ãWEBã¢ããªã±ã¼ã·ã§ã³ããããä¸ã«ä¸ãã¾ããã!
