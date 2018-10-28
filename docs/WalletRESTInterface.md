# Wallet REST Interface

## Create a wallet with one button 

**Interface function**

> Interface description：create a wallet with one button，the wallet file pack is saved by default in the Linux:/home/bottos/bot/ directory.
>
> **Interface address**
>
> URL: /v1/wallet/createwallet 
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| parameter    | mandatory | type   | defalt | explanation  |
| ------------ | --------- | ------ | ------ | ------------ |
| account_name | TRUE      | string | none   | account name |
| passwd       | TRUE      | string | none   | password     |

**Response field：**

| parameter   | type       | explanation                                                  |
| ----------- | ---------- | ------------------------------------------------------------ |
| errcode     | uint32     | Error code, 0- corresponding success, other see error code Chapter |
| msg         | string     | Response description                                         |
| result      | jsonObject | Response results                                             |
| wallet_name | string     | The name of the generated wallet file is defaults to the account name + ".Keystore" suffix. |

**Field change**

- none

  **Interface example**

> adress：<<http://127.0.0.1:6869/v1/wallet/createwallet> >

- request：

  \```

  ```
  "account_name": "testtest1",
  "passwd": "123456"    
  ```

  }

```
- response：
```

HTTP/1.1 200 OK { "errcode": 0, "msg": "success", "result": { "wallet_name": "testtest1.keystore" } }

```
## Generate public and private key pairs

**Interface function**

> Interface description： Generate public and private key pairs
>
> **Interface address**
>
> URL:  /v1/wallet/generatekeypair
>
> **Return format**
>
> JSON
>
> **Request method**
>
> GET

**Request parameters：**

| parameter | required | type | Default value | explanation |
| ---- | ---- | ---- | ------ | ---- |
| none   |      |      |        |      |

**Response field：**

|  parameter       | type       | explanation                                 |
| ----------- | ---------- | ------------------------------------ |
| errcode     | uint32     | Error code, 0- corresponding success, other see error code Chapter |
| msg         | string     | Response description                             |
| result      | jsonObject | Response results                             |
| public_key  | string     | public key                                 |
| private_key | string     | private key                                 |

**Field change**

- none

  **Interface example**

> adress：<http://127.0.0.1:6869/v1/wallet/generatekeypair  >

- request：
```

none

```
- response：
```

HTTP/1.1 200 OK { "errcode": 0, "msg": "success", "result": { "public_key": "043680ae1b81f87274d7051e6101afc8f8da3cd978bb75b22f24becb98afb456f110151644330ff6c742e44f8e9652f1ab5ea1cd3997bebe5a23a4389ff0cb6493", "private_key": "8a068d821ad8d58fe8caaa87f32ea69f889f6b8ce8c6bc3bc67ce2c68c43da3b" } }

```
## Create an account

**Interface function**

> Interface description： Create an account
>
> **Interface address**
>
> URL:  /v1/wallet/createaccount 
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| parameters         | mandatory  | type   | Default value | explanation                                   |
| ------------ | ----- | ------ | ------ | -------------------------------------- |
| account_name | TRUE  | string | none     | Account name                               |
| public_key   | TRUE  | string | none     | public key                                   |
| referrer     | FALSE | string | bottos | Referral account number, if not, default to system bottos account. |

**Response field：**

| parameters         | type       | explanation                                 |
| ------------ | ---------- | ------------------------------------ |
| errcode      | uint32     | Error code, 0- corresponding success, other see error code Chapter |
| msg          | string     | Response description                             |
| result       | jsonObject | Response results, specific data details               |
| account_name | string     | Newly registered account name                     |

**Field change**

- none

  **Interface example**

> adress：<http://127.0.0.1:6869/v1/wallet/createaccount >

- request：
```

{ "account_name": "testtest", "public_key": "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f", "referrer": "bottos"
}

```
- response：
```

HTTP/1.1 200 OK { "errcode": 0, "msg": "success", "result": { "account_name":"testtest" } }

```
## Create wallet manually

**Interface function**

> Interface description： Create wallet manually，The wallet file pack is saved by default in the Linux:/home/bottos/bot/ directory.The name of the generated wallet file is defaults to the account name + ".Keystore" suffix
>
> **Interface address**
>
> URL:  /v1/wallet/createwalletmanual 
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| parameter         | mandatory | type   | default value | explanation     |
| ------------ | ---- | ------ | ------ | -------- |
| account_name | TRUE | string | none     | account name |
| private_key  | TRUE | string | none     | private key     |
| passwd       | TRUE | string | none     | public key     |

**Response field：**

| parameter        | type       | explanation                                               |
| ----------- | ---------- | -------------------------------------------------- |
| errcode     | uint32     | Error code, 0- corresponding success, other see error code Chapter               |
| msg         | string     | Response description                             |
| result      | jsonObject | Response result                                    |
| wallet_name | string     | The name of the generated wallet file is defaults to the account name + ".Keystore" suffix. |

**Field change**

- none

  **Interface example**

> adress：<http://127.0.0.1:6869/v1/wallet/createwalletmanual  >

- request：
```

{ "account_name": "testtest1", "private_key": "b799ef616830cd7b8599ae7958fbee56d4c8168ffd5421a16025a398b8a4be45", "passwd": "123456" }

```
- response：
```

HTTP/1.1 200 OK { "errcode": 0, "msg": "success", "result": { "wallet_name": "testtest1.keystore" } }

```
##Open /Unlock Wallet

**Interface function**

> Interface Description: open /Unlock Wallet
>
> **interface address**
>
> URL:  /v1/wallet/unlockaccount
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| parameter         | mandatory |type   | default value | explanation     |
| ------------ | ---- | ------ | ------ | -------- |
| account_name | TRUE | string | none     | account name |
| passwd       | TRUE | string | none     | password     |

**Response field：**

| parameter    | type       | explanation                                 |
| ------- | ---------- | ------------------------------------ |
| errcode | uint32     | Error code, 0- corresponding success, other see error code Chapter |
| msg     | string     | Response description                             |
| result  | jsonObject | Response result                             |
| unlock  | bool       | Operation result                             |

**Field change**

- none

  **Interface example**

> adress：<http://127.0.0.1:6869/v1/wallet/unlockaccount  >

- request：
```

{ "account_name": "testtest1", "passwd": "123456" }

```
- response：
```

HTTP/1.1 200 OK { "errcode": 0, "msg": "success", "result": { "unlock": true } }

```
## Close /Lock Wallet

**Interface function**

> Interface description： Close /Lock Wallet
>
> **Interface address**
>
> URL:  /v1/wallet/lockaccount 
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| parameters         | mandatory | type   |default value | explanation     |
| ------------ | ---- | ------ | ------ | -------- |
| account_name | TRUE | string | none     | account name |

**Response field：**

| parameters    | type       | explanation                                 |
| ------- | ---------- | ------------------------------------ |
| errcode | uint32     | Error code, 0- corresponding success, other see error code Chapter  |
| msg     | string     | Response description                             |
| result  | jsonObject | Response results                             |
| lock    | bool       | Operation resultS |

**Field change**

- none

  **Interface example**

> adress：<http://127.0.0.1:6869/v1/wallet/lockaccount  >

- request：
```

{ "account_name": "testtest1" }

```
-response：
```

HTTP/1.1 200 OK { "errcode": 0, "msg": "success", "result": { "lock": true } }

```
## Query wallet list

**Interface function**

> Interface description： Query wallet list
>
> **Interface address**
>
> URL:  /v1/wallet/list
>
> **Return format**
>
> JSON
>
> **Request method**
>
> GET

**Request parameters：**

| Parameters | Mandatory | Type | Default value | Explanation |
| ---- | ---- | ---- | ------ | ---- |
| none   |      |      |        |      |

**Response field：**

| Parameters         | Type       | Explanation                                       |
| ------------ | ---------- | ------------------------------------------ |
| errcode      | uint32     | Error code, 0- corresponding success, other see error code Chapter        |
| msg          | string     | Response description                                   |
| result       | jsonObject | Response results                                   |
| wallet_path  | string     | Wallet path + file name                         |
| account_name | string     | Account name                                   |
| public_key   | string     | Public key value, if the account is not registered on the chain, then the query can not be reached |

**Field change**

- none

  **Interface example**

> adress：<http://127.0.0.1:6869/v1/wallet/list >

- request：
```

none

```
- Response:
```

HTTP/1.1 200 OK { "errcode": 0, "msg": "success", "result": [{ "wallet_path": "C:\Users\jim\AppData\Roaming\bot\testtest12.keystore", "account_name": "testtest12", "public_key": "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f" }, { "wallet_path": "C:\Users\jim\AppData\Roaming\bot\testtest2.keystore", "account_name": "testtest2", "public_key": "not found on Chain" }] }

```
## Query public and private key pair

**Interface function**

> Interface description： To query the public private key pair, the premise of calling the interface is that the account is in the open or Unlock state
>
> **Interface address**
>
> URL:  /v1/wallet/getkeypair
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| Parameters         | Mandatory | Type   | Default value | Explanation     |
| ------------ | ---- | ------ | ------ | -------- |
| account_name | TRUE | string | none     | Account name |

**Response field：**

| Parameters         | Type       | Explanation                                 |
| ------------ | ---------- | ------------------------------------ |
| errcode      | uint32     | Error code, 0- corresponding success, other see error code Chapter |
| msg          | string     | Response description                             |
| result       | jsonObject | Response results                             |
| account_name | string     | Account name                             |
| private_key  | string     | Private key value                               |
| public_key   | string     | Public key value                               |

**Field change**

- none

  **Interface example**

> Adress：<http://127.0.0.1:6869/v1/wallet/getkeypair>

- Request：
```

{ "account_name":"testtest" }

```
- Response：
```

{ "errcode": 0, "msg": "success", "result": { "account_name": "testtest", "private_key": "8a068d821ad8d58fe8caaa87f32ea69f889f6b8ce8c6bc3bc67ce2c68c43da3b", "public_key": "043680ae1b81f87274d7051e6101afc8f8da3cd978bb75b22f24becb98afb456f110151644330ff6c742e44f8e9652f1ab5ea1cd3997bebe5a23a4389ff0cb6493" } }

```
## Signature for transactions

**Interface function**

> Interface description： Signature for transactions
>
> **Interface address**
>
> URL:  /v1/wallet/signtransaction
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| Parameters     | Mandatory | Type   | Default value | Explanation                                            |
| -------- | ---- | ------ | ------ | ----------------------------------------------- |
| sender   | TRUE | string | none     | Name of account to send transaction              |
| contract | TRUE | string | none     | Contract name                                    |
| method   | TRUE | string | none     | Contract method name                             |
| param    | TRUE | string | none     | The data of the business structure is serialized by BPL, and then converted to a sixteen string string |

**Response field：**

| Parameters     | Type       | Explanation                                     |
| ------- | ---------- | ---------------------------------------- |
| errcode | uint32     | Error code, 0- corresponding success, other see error code Chapter     |
| msg     | string     | Response description                                 |
| result  | jsonObject | Response results，see "send transaction information" request field specifically |

**Field change**

- none

  **Interface example**

> Adress：<http://127.0.0.1:6869/v1/wallet/signtransaction>

- Request：
```

{ "sender": "bottos", "contract": "bottos", "method": "newaccount", "param": "" }

```
-Response：
```

HTTP/1.1 200 OK { "errcode": 0, "msg": "success", "result": { "version": 1, "cursor_num": 26, "cursor_label": 1948301132, "lifetime": 1537330126, "sender": "bottos", "contract": "bottos", "method": "newaccount", "param": "", "sig_alg": 1, "signature": "aa249f7c0e5a5564b48ada5e9f0ffa4665d955b08e08c43906a156fa5bf30272547f2e4cde31fa8d5d303f36a4de0718ec3284b2e82f93fa7da50a54cbdcf86a" } }

```
## Data signature

**Interface function**

> Interface description： Data signature
>
> **Interface address**
>
> URL:  /v1/wallet/signhash
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| Parameters         | Mandatory | Type   | Default value | Explanation         |
| ------------ | ---- | ------ | ------ | ------------ |
| account_name | TRUE | string | none     | Account name     |
| param        | TRUE | []byte | none     | Array to be signed |

**Response field：**

|  Parameters       | Type        | Explanation                                 |
| ---------- | ---------- | ------------------------------------ |
| errcode    | uint32     | Error code, 0- corresponding success, other see error code Chapter  |
| msg        | string     | Response description                             |
| result     | jsonObject | Response results                             |
| hash_value | string     | Signature value                               |

**Field change**

- none

  **Interface example**

> adress：<http://127.0.0.1:6869/v1/wallet/signhash

- request：
```

{ "account_name": "bottos", "param": [11] }

```
- response：
```

HTTP/1.1 200 OK { "errcode": 0, "msg": "success", "result": { "hash_value": "ed6b57fa91ee369af925e4c0545c06f5829ce3d2825949931a2b8816039f53f47160701c779b528abe84f5d6acdb2d9c46de6958e42606d2e4d7b9b072991729" } } ```