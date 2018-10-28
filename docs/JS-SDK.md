## Classes

- [BottosWalletSDK](http://47.74.187.9:4000/Wallet%20SDK/API.html#BottosWalletSDK)


## Objects

- [Api](http://47.74.187.9:4000/Wallet%20SDK/API.html#Api) : `object`

- [Contract](http://47.74.187.9:4000/Wallet%20SDK/API.html#Contract) : `object`

- [Tool](http://47.74.187.9:4000/Wallet%20SDK/API.html#Tool) : `object`

- [Wallet](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet) : `object`


## Typedefs

- [functionCallback](http://47.74.187.9:4000/Wallet%20SDK/API.html#functionCallback) : `function`

  This callback is displayed as a global member.

- [originFetchTemplate](http://47.74.187.9:4000/Wallet%20SDK/API.html#originFetchTemplate) : `Object`

- [originFetchTemplate](http://47.74.187.9:4000/Wallet%20SDK/API.html#originFetchTemplate) : `Object`

## BottosWalletSDK

**Kind**: global class

- BottosWalletSDK
  - [new BottosWalletSDK(config)](http://47.74.187.9:4000/Wallet%20SDK/API.html#new_BottosWalletSDK_new)
  - [.Api](http://47.74.187.9:4000/Wallet%20SDK/API.html#BottosWalletSDK+Api)
  - [.Tool](http://47.74.187.9:4000/Wallet%20SDK/API.html#BottosWalletSDK+Tool)
  - [.Wallet](http://47.74.187.9:4000/Wallet%20SDK/API.html#BottosWalletSDK+Wallet)
  - [.Contract](http://47.74.187.9:4000/Wallet%20SDK/API.html#BottosWalletSDK+Contract)
  - [.setBaseUrl(baseUrl)](http://47.74.187.9:4000/Wallet%20SDK/API.html#BottosWalletSDK+setBaseUrl)

### new BottosWalletSDK(config)

Represents the BottosWalletSDK.

| Param            | Type     | Default                           |
| ---------------- | -------- | --------------------------------- |
| config           | `Object` |                                   |
| [config.baseUrl] | `string` | `"http://localhost:8689/v1&quot;` |
| [config.version] | `number` | `1`                               |
| [config.crypto]  | `Object` | `BTCryptTool`                     |

### bottosWalletSDK.Api

See [Api](http://47.74.187.9:4000/Wallet%20SDK/API.html#Api).

**Kind**: instance property of [`BottosWalletSDK`](http://47.74.187.9:4000/Wallet%20SDK/API.html#BottosWalletSDK)

### bottosWalletSDK.Tool

See [Tool](http://47.74.187.9:4000/Wallet%20SDK/API.html#Tool).

**Kind**: instance property of [`BottosWalletSDK`](http://47.74.187.9:4000/Wallet%20SDK/API.html#BottosWalletSDK)

### bottosWalletSDK.Wallet

See [Wallet](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet).

**Kind**: instance property of [`BottosWalletSDK`](http://47.74.187.9:4000/Wallet%20SDK/API.html#BottosWalletSDK)

### bottosWalletSDK.Contract

See [Contract](http://47.74.187.9:4000/Wallet%20SDK/API.html#Contract).

**Kind**: instance property of [`BottosWalletSDK`](http://47.74.187.9:4000/Wallet%20SDK/API.html#BottosWalletSDK)

### bottosWalletSDK.setBaseUrl(baseUrl)

**Kind**: instance method of [`BottosWalletSDK`](http://47.74.187.9:4000/Wallet%20SDK/API.html#BottosWalletSDK)

| Param   | Type     | Description                  |
| ------- | -------- | ---------------------------- |
| baseUrl | `string` | The baseUrl used in request. |

## Api : `object`

**Kind**: global namespace 

- Api : object
  - [.chain_id](http://47.74.187.9:4000/Wallet%20SDK/API.html#Api.chain_id)
  - [.request(url, params, [method\])](http://47.74.187.9:4000/Wallet%20SDK/API.html#Api.request)
  - [.getAbi(contract, [callback\])](http://47.74.187.9:4000/Wallet%20SDK/API.html#Api.getAbi) ⇒ `Promise.<Object>` | `undefined`
  - [.getBlockHeader([callback\])](http://47.74.187.9:4000/Wallet%20SDK/API.html#Api.getBlockHeader) ⇒ `Promise.<Object>` | `undefined`

### Api.chain_id

Documented as Api.chain_id

**Kind**: static property of [`Api`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Api)

### Api.request(url, params, [method])

**Kind**: static method of [`Api`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Api)

| Param    | Type     | Default  |
| -------- | -------- | -------- |
| url      | `string` |          |
| params   | `Object` |          |
| [method] | `string` | `"POST"` |

### Api.getAbi(contract, [callback]) ⇒ `Promise.<Object>` | `undefined`

Returns the abi. If callback is undefined, this function will return a promise.

**Kind**: static method of [`Api`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Api)

| Param      | Type                                                         | Description            |
| ---------- | ------------------------------------------------------------ | ---------------------- |
| contract   | `string`                                                     | The contract name.     |
| [callback] | [`functionCallback`](http://47.74.187.9:4000/Wallet%20SDK/API.html#functionCallback) | The optional callback. |

### Api.getBlockHeader([callback]) ⇒ `Promise.<Object>` | `undefined`

Documented as Api.getBlockHeader.

**Kind**: static method of [`Api`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Api)
**Returns**: `Promise.<Object>` | `undefined` - If callback is undefined, a promise will be returned.

| Param      | Type                                                         |
| ---------- | ------------------------------------------------------------ |
| [callback] | [`functionCallback`](http://47.74.187.9:4000/Wallet%20SDK/API.html#functionCallback) |

## Contract : `object`

**Kind**: global namespace 

- Contract: object
  - [.deployContract(param, senderInfo)](http://47.74.187.9:4000/Wallet%20SDK/API.html#Contract.deployContract) ⇒ `Promise.<Object>`
  - [.deployABI(param, senderInfo)](http://47.74.187.9:4000/Wallet%20SDK/API.html#Contract.deployABI) ⇒ `Promise.<Object>`
  -  [.callContract(originFetchTemplate, privateKey)](http://47.74.187.9:4000/Wallet%20SDK/API.html#Contract.callContract) ⇒ `Promise.<Object>`

### Contract.deployContract(param, senderInfo) ⇒ `Promise.<Object>`

Deploy a contract.

**Kind**: static method of [`Contract`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Contract)

| Param                 | Type          | Default       | Description           |                     |
| --------------------- | ------------- | ------------- | --------------------- | ------------------- |
| param                 | `Object`      |               |                       |                     |
| [param.vm_type]       | `number`      | `1`           | vm_type, now is 1.    |                     |
| [param.vm_version]    | `number`      | `1`           | vm_version, now is 1. |                     |
| param.contract_code   | `Uint8Array`\ | `ArrayBuffer` |                       | wasm file buffer.   |
| senderInfo            | `Object`      |               | The sender            |                     |
| senderInfo.account    | `string`      |               | sender's account      |                     |
| senderInfo.privateKey | `string` \    | `Uint8Array`  |                       | sender's privateKey |

### Contract.deployABI(param, senderInfo) ⇒ `Promise.<Object>`

Deploy an abi.

**Kind**: static method of [`Contract`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Contract)

| Param                 | Type      | Description      |                     |                             |
| --------------------- | --------- | ---------------- | ------------------- | --------------------------- |
| param                 | `Object`  |                  |                     |                             |
| param.contract_abi    | `string`\ | `Uint8Array` \   | `ArrayBuffer`       | ABI content or file buffer. |
| senderInfo            | `Object`  | The sender       |                     |                             |
| senderInfo.account    | `string`  | sender's account |                     |                             |
| senderInfo.privateKey | `string`\ | `Uint8Array`     | sender's privateKey |                             |

### Contract.callContract(originFetchTemplate, privateKey) ⇒ `Promise.<Object>`

**Kind**: static method of [`Contract`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Contract)

| Param               | Type       |              |
| ------------------- | ---------- | ------------ |
| originFetchTemplate | `Object`   |              |
| privateKey          | `string` \ | `Uint8Array` |

## Tool : `object`

 **Kind**: global namespace 

- Tool : object[.buf2hex(buffer)](http://47.74.187.9:4000/Wallet%20SDK/API.html#Tool.buf2hex) ⇒ `string`
  -- [.getRequestParams(originFetchTemplate, privateKey)](http://47.74.187.9:4000/Wallet%20SDK/API.html#Tool.getRequestParams) ⇒ `Promise.<Object>`

### Tool.buf2hex(buffer) ⇒ `string`

**Kind**: static method of [`Tool`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Tool)
**Returns**: `string` - Hexadecimal string.

| Param  | Type         | Description        |
| ------ | ------------ | ------------------ |
| buffer | `Uint8Array` | Uint8Array buffer. |

### Tool.getRequestParams(originFetchTemplate, privateKey) ⇒ `Promise.<Object>`

**Kind**: static method of [`Tool`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Tool)

| Param               | Type                                                         | Description  |                   |
| ------------------- | ------------------------------------------------------------ | ------------ | ----------------- |
| originFetchTemplate | [`originFetchTemplate`](http://47.74.187.9:4000/Wallet%20SDK/API.html#originFetchTemplate) |              |                   |
| privateKey          | `string` \                                                   | `Uint8Array` | Your private key. |

## Wallet : `object`

**Kind**: global namespace

- Wallet: object
   - [.createAccountByIntro(params)](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet
   - .createAccountByIntro) ⇒ `Object`
   - [.createKeys()](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet.createKeys) ⇒ `Object` 
   - [.createAccountWithIntro(params, referrerInfo)](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet.createAccountWithIntro) ⇒ `Promise.<Object>`
   - [.recover(password, keyObject)](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet.recover) ⇒ `Uint8Array`
   - [.getAccountInfo(account_name)](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet.getAccountInfo) ⇒ `Promise.<Object>`
   - [.sendTransaction(params, privateKey)](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet.sendTransaction) ⇒ `Promise.<Object>`
   - [.stake(amount, privateKey)](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet.stake) ⇒ `Promise.<Object>`
   - [.unstake(amount, privateKey)](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet.unstake) ⇒ `Promise.<Object>`
   - [.claim(amount, privateKey)](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet.claim) ⇒ `Promise.<Object>`


### Wallet.createAccountByIntro(params) ⇒ `Object`

**Kind**: static method of [`Wallet`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet)
**Returns**: `Object` - keystore

| Param             | Type       | Description                             |            |
| ----------------- | ---------- | --------------------------------------- | ---------- |
| params            | `Object`   | the params required for create keystore |            |
| params.account    | `string`   | account                                 |            |
| params.password   | `string`   | password                                |            |
| params.privateKey | `string` \ | `Uint8Array`                            | privateKey |

### Wallet.createKeys() ⇒ `Object`

Create public and private key pair

**Kind**: static method of [`Wallet`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet)
**Returns**: `Object` - keys

### Wallet.createAccountWithIntro(params, referrerInfo) ⇒ `Promise.<Object>`

register account on chain

**Kind**: static method of [`Wallet`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet)

| Param                   | Type      | Description            |                                        |
| ----------------------- | --------- | ---------------------- | -------------------------------------- |
| params                  | `Object`  | The params             |                                        |
| params.account          | `string`  | The new user's account |                                        |
| params.publicKey        | `string`\ | `Uint8Array`           | The publicKey provided by the new user |
| referrerInfo            | `Object`  | The referrer           |                                        |
| referrerInfo.account    | `string`  | referrer's account     |                                        |
| referrerInfo.privateKey | `string`\ | `Uint8Array`           | referrer's privateKey                  |

### Wallet.recover(password, keyObject) ⇒ `Uint8Array`

**Kind**: static method of [`Wallet`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet)
**Returns**: `Uint8Array` - privateKey

| Param     | Type     | Description  |
| --------- | -------- | ------------ |
| password  | `string` | password     |
| keyObject | `Object` | the keystore |

### Wallet.getAccountInfo(account_name) ⇒ `Promise.<Object>`

**Kind**: static method of [`Wallet`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet)

| Param        | Type     |
| ------------ | -------- |
| account_name | `string` |

### Wallet.sendTransaction(params, privateKey) ⇒ `Promise.<Object>`

**Kind**: static method of [`Wallet`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet)

| Param        | Type       |          |
| ------------ | ---------- | -------- |
| params       | `Object`   |          |
| params.from  | `string`   |          |
| params.to    | `string`   |          |
| params.value | `string` \ | `number` |
| privateKey   | `string`   |          |

### Wallet.stake(amount, privateKey) ⇒ `Promise.<Object>`

**Kind**: static method of [`Wallet`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet)

| Param      | Type       |              |
| ---------- | ---------- | ------------ |
| amount     | `number`   |              |
| privateKey | `string` \ | `Uint8Array` |

### Wallet.unstake(amount, privateKey) ⇒ `Promise.<Object>`

**Kind**: static method of [`Wallet`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet)

| Param      | Type       |              |
| ---------- | ---------- | ------------ |
| amount     | `number`   |              |
| privateKey | `string` \ | `Uint8Array` |

### Wallet.claim(amount, privateKey) ⇒ `Promise.<Object>`

**Kind**: static method of [`Wallet`](http://47.74.187.9:4000/Wallet%20SDK/API.html#Wallet)

| Param      | Type       |              |
| ---------- | ---------- | ------------ |
| amount     | `number`   |              |
| privateKey | `string` \ | `Uint8Array` |

## functionCallback : `function`

This callback is displayed as a global member.

**Kind**: global typedef

| Param  | Type | Description         |
| ------ | ---- | ------------------- |
| err    | `*`  | The callback error. |
| result | `*`  | The success result. |

## originFetchTemplate : `Object`

**Kind**: global typedef
**Properties**

| Name                           | Type     | Default    | Description                            |
| ------------------------------ | -------- | ---------- | -------------------------------------- |
| [originFetchTemplate.version]  | `number` | `1`        | Default value is 1.                    |
| originFetchTemplate.sender     | `string` |            | Default value is bottos.               |
| [originFetchTemplate.contract] | `string` | `"bottos"` | The contract. Default value is bottos. |
| originFetchTemplate.method     | `string` |            |                                        |
| originFetchTemplate.param      | `Object` |            |                                        |
| [originFetchTemplate.sig_alg]  | `number` | `1`        | Default value is 1.                    |