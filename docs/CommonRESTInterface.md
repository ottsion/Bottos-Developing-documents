# Common REST Interface

## Get block information

**Interface function**

> Interface Description: get block information
>
> **Interface address**
>
> URL:  /v1/block/detail
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST
>
> **Request parameters：**
>
> | Parameter  | Mandatory | Type   | Default value | Explanation      |
> | ---------- | --------- | ------ | ------------- | ---------------- |
> | block_num  | FALSE     | uint64 | empty         | Block number     |
> | block_hash | FALSE     | string | empty         | Block hash value |

Note: Block_num, block_hash must be choosed one, if all default, the default query is to block 0 information.

**Response field：**

| Parameter          | Type       | Explanation                              |
| ------------------ | ---------- | ---------------------------------------- |
| errcode            | uint32     | Error code, 0- corresponding success, other see error code Chapter |
| msg                | string     | Response description                     |
| result             | jsonObject | Response results                         |
| block_num          | uint64     | Block number                             |
| prev_block_hash    | string     | The previous Block hash value            |
| block_hash         | string     | current Block hash value                 |
| cursor_block_label | uint32     | Current block identifier                 |
| block_time         | uint64     | Block generation time                    |
| trx_merkle_root    | string     | Merkel root value, the root hash value of all transactions packaged by the block. |
| delegate           | string     | Producer name                            |
| delegate_sign      | string     | Producer signature                       |
| trxs               | jsonArray  | List of transactions packed in the current block. See the response field in the chapter "query transaction information". |

**Field change**

- None

  **Interface example**

> address：<http://127.0.0.1:8689/v1/block/detail>

- request：

```
  {
      "block_num": 32,
      "block_hash": "405a6fb8b91a055a7a4cf007451ce0b31ea6626cb2d56ec050b126701fbf093d"
  }

```

- response：

```
  HTTP/1.1 200 OK

  {
      "errcode": 0,
      "msg": "success",
      "result": {
          "prev_block_hash": "1b345401d8f859c05e37b5ccacd39ff5b4a21615b63f9b96edb59352a3e54e82",
          "block_num": 32,
          "block_hash": "405a6fb8b91a055a7a4cf007451ce0b31ea6626cb2d56ec050b126701fbf093d",
          "cursor_block_label": 532613437,
          "block_time": 1537259127,
          "trx_merkle_root": "85f9d2fbe1d3c0a217e10932899b6f73b24fafe59a006406ed65d7e4a39a7416",
          "delegate": "bottos",
          "delegate_sign": "41c25998e7d432527f07ae5c10c5c30a4873e9519c29cb02e7f46e3a8e238baf47748efe3f24db3ff3630305441b1d24c5d0ba796b3332a8b8fd3fca4efc4cfb",
          "trxs": [
              {
                  "version": 1,
                  "cursor_num": 31,
                  "cursor_label": 2749714050,
                  "lifetime": 1537259224,
                  "sender": "bottos",
                  "contract": "bottos",
                  "method": "newaccount",
                  "param": {
                      "name": "testtest",
                      "pubkey": "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f"
                  },
                  "sig_alg": 1,
                  "signature": "c85fd25af493cbb6a79870ce0fc602acc892664ca17e2c646aff0332ca6db7787beeb7e5d8553de8e4b83bdf7b227762fedf9e3674888893f18bf31f0b05d622"
              }
          ]
      }
  }

```

## Get block height information

**Interface function**

> Interface Explanation: get block height information
>
> **Interface address**
>
> URL:  /v1/block/height
>
> **Return format**
>
> JSON
>
> **Request method**
>
> GET
>
> **Request parameters：**
>
> | Parameter | Mandatory | Type | Default value | Explanation |
> | --------- | --------- | ---- | ------------- | ----------- |
> | None      |           |      |               |             |

**Response field：**

| Parameter                | Type       | Explanation                              |
| ------------------------ | ---------- | ---------------------------------------- |
| errcode                  | uint32     | Error code, 0- corresponding success, other see error code Chapter |
| msg                      | string     | Response description                     |
| result                   | jsonObject | Response results                         |
| head_block_num           | uint64     | Block number                             |
| head_block_hash          | string     | The previous Block hash value            |
| head_block_time          | uint64     | Block generation time                    |
| head_block_delegate      | string     | Block producer                           |
| cursor_label             | uint32     | Block identification                     |
| last_consensus_block_num | uint32     | Irreversible block number                |
| chain_id                 | string     | Chain ID, the Chain_id of all nodes of the same chain must be the same. |

**Field change**

- None

  **Interface example**

> Address:<http://127.0.0.1:8689/v1/block/height>

- Request:

```
  None

```

- Response:

```
  HTTP/1.1 200 OK
  {
      "errcode": 0,
      "msg": "",
      "result": {
          "head_block_num": 87,
          "head_block_hash": "b34806eefc77b88743ab447f43658bf229fd4e5cd9452340e21f3995a5d2054b",
          "head_block_time": 1534213225,
          "head_block_delegate": "alsephina",
          "cursor_label": 2782004555,
          "last_consensus_block_num": 64,
          "chain_id": "4b97b92d2c78bcffe95ebd3067565c73a2931b39d5eb7234b11816dcec54761a"
      }
  }

```

## Sending transaction information

**Interface function**

> Interface Explanation: sending transaction information
>
> **Interface address**
>
> URL:  /v1/transaction/send
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| Parameter    | Mandatory | Type   | Default value | Explanation                                                  |
| ------------ | --------- | ------ | ------------- | ------------------------------------------------------------ |
| version      | TRUE      | uint32 | 1             | Chain version number                                         |
| cursor_num   | TRUE      | uint64 | None          | The most new area Block number, get the access block to get. |
| cursor_label | TRUE      | uint32 | None          | The most new area Block identification, get the access block to get. |
| lifetime     | TRUE      | uint64 | None          | Transaction expiration time, calling the zone block, plus a certain delay, recommended delay of 100 seconds. |
| sender       | TRUE      | string | None          | sender                                                       |
| contract     | TRUE      | string | None          | Contract name                                                |
| method       | TRUE      | string | None          | Contract method                                              |
| param        | TRUE      | string | None          | Business Parameter, sixteen binary string                    |
| sig_alg      | TRUE      | uint32 | 1             | signature algorithm                                          |
| signature    | TRUE      | string | None          | Signature value                                              |

**Response field：**

| Parameter    | Type       | Explanation                                                  |
| ------------ | ---------- | ------------------------------------------------------------ |
| errcode      | uint32     | Error code, 0- corresponding success, other see error code Chapter |
| msg          | string     | Response description                                         |
| result       | jsonObject | Response results                                             |
| trx_hash     | string     | Transaction hash value                                       |
| trx          | jsonObject | transaction details                                          |
| version      | uint32     | Chain version number                                         |
| cursor_num   | uint64     | The most new area Block number, get the access block to get. |
| cursor_label | uint32     | The latest block label is called the capture block.          |
| lifetime     | uint64     | The expiration date of the transaction is to call the access block and add a certain delay. |
| sender       | string     | sender                                                       |
| contract     | string     | Contract name                                                |
| method       | string     | Contract method                                              |
| param        | string     | Business Parameter, sixteen binary string                    |
| sig_alg      | uint32     | signature algorithm                                          |
| signature    | string     | Signature value                                              |

**Field change**

- None

  **Interface example**

> Address:<http://127.0.0.1:8689/v1/transaction/send>

- Request:

```
  {
      "version": 1,
      "cursor_num": 719,
      "cursor_label": 2997806499,
      "lifetime": 1534143531,
      "sender": "bottos",
      "contract": "bottos",
      "method": "newaccount",
      "param": "dc0002da0009757365727465737431da008230346430373538383030353634383861393864613365643234623766613265633061623864383464343764623534366333663138316137363462613366613165383237396637363434303963343164653031623030383065623161616565623935303966373932333535323061373565333432343432393134346234336331303462",
      "sig_alg": 1,
      "signature": "f0069bc363a55dc22207c75d15cc75524bf4950159130c6bf385f6f1ca877177362ad5ab51108e7f396043e3aee7058f1ca6a40fd6c79a8483e439d2e2bccf2c"
  }

```

- Response:

```
  HTTP/1.1 200 OK
  {
      "errcode": 0,
      "msg": "trx receive succ",
      "result": {
          "trx": {
              "version": 1,
              "cursor_num": 719,
              "cursor_label": 2997806499,
              "lifetime": 1534143531,
              "sender": "delta",
              "contract": "bottos",
              "method": "newaccount",
              "param": "dc0002da0009757365727465737431da008230346430373538383030353634383861393864613365643234623766613265633061623864383464343764623534366333663138316137363462613366613165383237396637363434303963343164653031623030383065623161616565623935303966373932333535323061373565333432343432393134346234336331303462",
              "sig_alg": 1,
              "signature": "f0069bc363a55dc22207c75d15cc75524bf4950159130c6bf385f6f1ca877177362ad5ab51108e7f396043e3aee7058f1ca6a40fd6c79a8483e439d2e2bccf2c"
          },
          "trx_hash": "1815f4d4dfb52b88fb445efc255a5be6275fc3ad694f802c01c40644f09b651f"
      }
  }

```

## Query transaction information

**Interface function**

> Interface Explanation: query transaction information
>
> **Interface address**
>
> URL:  /v1/transaction/get
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| Parameter | Mandatory | Type   | Default value | Explanation            |
| --------- | --------- | ------ | ------------- | ---------------------- |
| trx_hash  | TRUE      | string | None          | Transaction hash value |

**Response field：**

| Parameter  | Type       | Explanation                                                  |
| ---------- | ---------- | ------------------------------------------------------------ |
| errcode    | uint32     | Error code, 0- corresponding success, other see error code Chapter |
| msg        | string     | Response description                                         |
| result     | jsonObject | Response results                                             |
| version    | uint32     | Chain version number                                         |
| cursor_num | uint64     | The most new area Block number, get the access block to get. |
| cursor_lab | uint32     | The latest block label is called the capture block.          |
| lifetime   | uint64     | The expiration date of the transaction is to call the access block and add a certain delay. |
| sender     | string     | sender                                                       |
| contract   | string     | Contract name                                                |
| method     | string     | Contract method                                              |
| param      | jsonObject | business Parameter                                           |
| sig_alg    | uint32     | signature algorithm                                          |
| signature  | string     | Signature value                                              |

**Field change**

- None

  **Interface example**

> Address:<http://127.0.0.1:8689/v1/transaction/get>

- Request:

```
  {
      "trx_hash": "85f9d2fbe1d3c0a217e10932899b6f73b24fafe59a006406ed65d7e4a39a7416"
  }

```

- Response:

```
   HTTP/1.1 200 OK
  {
      "errcode": 0,
      "msg": "success",
      "result": {
          "version": 1,
          "cursor_num": 31,
          "cursor_label": 2749714050,
          "lifetime": 1537259224,
          "sender": "bottos",
          "contract": "bottos",
          "method": "newaccount",
          "param": {
              "name": "testtest",
              "pubkey": "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f"
          },
          "sig_alg": 1,
          "signature": "c85fd25af493cbb6a79870ce0fc602acc892664ca17e2c646aff0332ca6db7787beeb7e5d8553de8e4b83bdf7b227762fedf9e3674888893f18bf31f0b05d622"
      }
  }

```

## Query data based on keywords

**Interface function**

> Interface Explanation: querying data based on keywords
>
> **Interface address**
>
> URL:  /v1/common/query
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| Parameter | Mandatory | Type   | Default value | Explanation         |
| --------- | --------- | ------ | ------------- | ------------------- |
| contract  | TRUE      | string | None          | Contract name       |
| object    | TRUE      | string | None          | Contract table name |
| key       | TRUE      | string | None          | Query key           |

**Response field：**

| Parameter | Type       | Explanation                                                  |
| --------- | ---------- | ------------------------------------------------------------ |
| errcode   | uint32     | Error code, 0- corresponding success, other see error code Chapter |
| msg       | string     | Response description                                         |
| result    | jsonObject | Response results                                             |
| contract  | string     | Contract name                                                |
| object    | string     | Contract table name                                          |
| key       | string     | Query key                                                    |
| value     | uint32     | Query value                                                  |

**Field change**

- None

  **Interface example**

> Address:<http://127.0.0.1:8689/v1/common/query>

- Request:

```
  {
      "contract":"bottostoken",
      "object":"DTO",
      "key":"aaa"
  }

```

- Response:

```
   HTTP/1.1 200 OK
  {
    "errcode": 0,
    "msg": "",
    "result": {
          "contract": "bottostoken",
          "object": "DTO",
          "key": "aaa",
          "value": "dc0001cf000000ba43b74000"
    }
  }

```

## Serializing business data

**Interface function**

> Interface Explanation: Serializes business data, JSON converts to a hexadecimal string as the ParM field value in the Send Transaction Information request.
>
> **Interface address**
>
> URL:  /v1/common/jsontobin
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| Parameter | Mandatory | Type   | Default value | Explanation         |
| --------- | --------- | ------ | ------------- | ------------------- |
| contract  | TRUE      | string | None          | Contract name       |
| object    | TRUE      | string | None          | Contract table name |
| key       | TRUE      | string | None          | Query key           |

**Response field：**

| Parameter | Type       | Explanation                                                  |
| --------- | ---------- | ------------------------------------------------------------ |
| errcode   | uint32     | Error code, 0- corresponding success, other see error code Chapter |
| msg       | string     | Response description                                         |
| result    | jsonObject | Response results                                             |
| contract  | string     | Contract name                                                |
| object    | string     | Contract table name                                          |
| key       | string     | Query key                                                    |
| value     | uint32     | Query value                                                  |

**Field change**

- None

  **Interface example**

> Address:<<http://127.0.0.1:8689/v1/common/jsontobin>

- Request:

```
  {
      "account_name": "testtest",
      "public_key": "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f"
  }

```

- Response:

```
   HTTP/1.1 200 OK
  {
    "errcode": 0,
    "msg": "",
    "result": {
          "contract": "bottostoken",
          "object": "DTO",
          "key": "aaa",
          "value": "dc0001cf000000ba43b74000"
    }
  }

```

## Query account information 

**Interface function**

> Interface Explanation: query account information
>
> **Interface address**
>
> URL:  /v1/account/info
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| Parameter    | Mandatory | Type   | Default value | Explanation             |
| ------------ | --------- | ------ | ------------- | ----------------------- |
| account_name | TRUE      | string | None          | the name on the account |

**Response field：**

| Parameter         | Type       | Explanation                                                  |
| ----------------- | ---------- | ------------------------------------------------------------ |
| errcode           | uint32     | Error code, 0- corresponding success, other see error code Chapter |
| msg               | string     | Response description                                         |
| result            | jsonObject | Response results                                             |
| account_name      | string     | Account name                                                 |
| pubkey            | string     | public key                                                   |
| balance           | string     | Token value，                                                |
| staked_balance    | string     | Token value of pledge                                        |
| unStaking_balance | string     | current Token value of unpledge                              |
| unStaking_time    | uint64     | The time to unpledge (Unix timestamp)                        |

Remarks：balance、staked_balance、unStaking_balance, the sum of the three is to change the total Token value of the account.

**Field change**

- None

  **Interface example**

> Address:<http://127.0.0.1:8689/v1/account/info>

- Request:

```
  {
      "account_name":"delta"
  }

```

- Response:

```
   HTTP/1.1 200 OK
  {
      "errcode": 0,
      "msg": "success",
      "result": {
          "account_name": "testtest",
          "pubkey": "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f",
          "balance": "0",
          "staked_balance": "0",
          "unStaking_balance": "0",
          "unStaking_time": 0
      }
  }

```

## Query contract ABI

**Interface function**

> Interface Explanation： Query contract ABI
>
> **Interface address**
>
> URL:  /v1/contract/abi 
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| Parameter | Mandatory | Type   | Default value | Explanation   |
| --------- | --------- | ------ | ------------- | ------------- |
| contract  | TRUE      | string | None          | Contract name |

**Response field：**

| Parameter   | Type       | Explanation                                                  |
| ----------- | ---------- | ------------------------------------------------------------ |
| errcode     | uint32     | Error code, 0- corresponding success, other see error code Chapter |
| msg         | string     | Response description                                         |
| result      | jsonObject | Response results                                             |
| types       | jsonObject | Reserved field                                               |
| structs     | jsonArray  | List of methods and structures included in contracts         |
| name        | string     | The structure name is usually a custom Contract method name alias. |
| base        | string     | The parent method is usually empty.                          |
| fields      | jsonObject | Method input parameter structure                             |
| name        | string     | Parameter-1，Take registered accounts as an example.：Account name |
| pubkey      | string     | Parameter-2，Take registered accounts as an example.：public key |
| actions     | jsonArray  | Method of contract                                           |
| action_name | string     | The name of Contract method corresponds to the method value of "send transaction information" Request parameters. |
| type        | string     | With name, the structure name,  is generally the custom Contract method name alias. |
| tables      | jsonArray  | The storage mode of the contract data defines the table name, Type, Key value, Type, Value Type. The built-in contract is empty. |
| table_name  | string     | Table name for contract storage                              |
| index_type  | string     | Index Type, defaults to string.                              |
| key_names   | jsonArray  | Key value for contract data storage                          |
| key_types   | jsonArray  | The Type of the key value is string by default.              |
| type        | string     | The value value corresponding to the contract data key is usually a structure. |

**Field change**

- None

  **Interface example**

> Address:<<http://127.0.0.1:8689/v1/contract/abi> >

- Request:

```
  {
      "contract":"bottos"
  }

```

- Response:

```
   HTTP/1.1 200 OK
  {
      "errcode": 0,
      "msg": "success",
      "result": {
          "actions": [
              {
                  "action_name": "newaccount",
                  "type": "NewAccount"
              },
              {
                  "action_name": "transfer",
                  "type": "Transfer"
              },
              {
                  "action_name": "grantcredit",
                  "type": "GrantCredit"
              },
              {
                  "action_name": "cancelcredit",
                  "type": "CancelCredit"
              },
              {
                  "action_name": "transferfrom",
                  "type": "TransferFrom"
              },
              {
                  "action_name": "deploycode",
                  "type": "DeployCode"
              },
              {
                  "action_name": "deployabi",
                  "type": "DeployABI"
              },
              {
                  "action_name": "regdelegate",
                  "type": "RegDelegate"
              },
              {
                  "action_name": "unregdelegate",
                  "type": "UnregDelegate"
              },
              {
                  "action_name": "votedelegate",
                  "type": "VoteDelegate"
              },
              {
                  "action_name": "stake",
                  "type": "Stake"
              },
              {
                  "action_name": "unstake",
                  "type": "Unstake"
              },
              {
                  "action_name": "claim",
                  "type": "Claim"
              },
              {
                  "action_name": "setdelegate",
                  "type": "SetDelegate"
              },
              {
                  "action_name": "blkprodtrans",
                  "type": "BlkProdTrans"
              }
          ],
          "structs": [
              {
                  "base": "",
                  "fields": {
                      "name": "string",
                      "pubkey": "string"
                  },
                  "name": "NewAccount"
              },
              {
                  "base": "",
                  "fields": {
                      "from": "string",
                      "to": "string",
                      "value": "uint256"
                  },
                  "name": "Transfer"
              },
              {
                  "base": "",
                  "fields": {
                      "description": "string",
                      "location": "string",
                      "name": "string",
                      "pubkey": "string"
                  },
                  "name": "SetDelegate"
              },
              {
                  "base": "",
                  "fields": {
                      "limit": "uint256",
                      "name": "string",
                      "spender": "string"
                  },
                  "name": "GrantCredit"
              },
              {
                  "base": "",
                  "fields": {
                      "name": "string",
                      "spender": "string"
                  },
                  "name": "CancelCredit"
              },
              {
                  "base": "",
                  "fields": {
                      "from": "string",
                      "to": "string",
                      "value": "uint256"
                  },
                  "name": "TransferFrom"
              },
              {
                  "base": "",
                  "fields": {
                      "contract": "string",
                      "contract_code": "bytes",
                      "vm_type": "uint8",
                      "vm_version": "uint8"
                  },
                  "name": "DeployCode"
              },
              {
                  "base": "",
                  "fields": {
                      "contract": "string",
                      "contract_abi": "bytes"
                  },
                  "name": "DeployABI"
              },
              {
                  "base": "",
                  "fields": {
                      "description": "string",
                      "location": "string",
                      "name": "string",
                      "pubkey": "string"
                  },
                  "name": "RegDelegate"
              },
              {
                  "base": "",
                  "fields": {
                      "name": "string"
                  },
                  "name": "UnregDelegate"
              },
              {
                  "base": "",
                  "fields": {
                      "delegate": "string",
                      "voteop": "uint8",
                      "voter": "string"
                  },
                  "name": "VoteDelegate"
              },
              {
                  "base": "",
                  "fields": {
                      "amount": "uint256"
                  },
                  "name": "Stake"
              },
              {
                  "base": "",
                  "fields": {
                      "amount": "uint256"
                  },
                  "name": "Unstake"
              },
              {
                  "base": "",
                  "fields": {
                      "amount": "uint256"
                  },
                  "name": "Claim"
              },
              {
                  "base": "",
                  "fields": {
                      "actblknum": "uint64"
                  },
                  "name": "BlkProdTrans"
              }
          ],
          "tables": null,
          "types": null
      }
  }

```

## Query contract code

**Interface function**

> Interface Explanation: query contract code
>
> **Interface address**
>
> URL:  /v1/contract/code
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| Parameter | Mandatory | Type   | Default value | Explanation   |
| --------- | --------- | ------ | ------------- | ------------- |
| contract  | TRUE      | string | None          | Contract name |

**Response field：**

| Parameter | Type       | Explanation                              |
| --------- | ---------- | ---------------------------------------- |
| errcode   | uint32     | Error code, 0- corresponding success, other see error code Chapter |
| msg       | string     | Response description                     |
| result    | jsonObject | Response results                         |

**Field change**

- None

  **Interface example**

> Address:<<http://127.0.0.1:8689/v1/contract/code> >

- Request:

```
  {
      "contract":"usermng"
  }

```

- Response:

```
   HTTP/1.1 200 OK
  {
      "errcode": 0,
      "msg": "",
      "result": "7b0a2020227479706573223a205b5d2c0a20202273747275637473223a205b7b0a202020202020226e616d65223a202255736572496e666f222c0a2020202020202262617365223a2022222c0a202020202020226669656c6473223a207b0a20202020202020202020226469646964223a2022737472696e67222c0a2020202020202020202022696e666f223a2022737472696e67220a20202020202020207d0a202020207d2c7b0a202020202020226e616d65223a2022557365724c6f67696e222c0a2020202020202262617365223a2022222c0a202020202020226669656c6473223a207b0a2020202020202020202022757365724e616d65223a2022737472696e67222c0a202020202020202020202272616e646f6d4e756d223a202275696e743332220a20202020202020207d0a202020207d2c7b0a202020202020226e616d65223a20225573657242617365496e666f222c0a2020202020202262617365223a2022222c0a202020202020226669656c6473223a207b0a2020202020202020202022696e666f223a2022737472696e67220a20202020202020207d0a202020207d0a20205d2c0a202022616374696f6e73223a205b7b0a20202020202022616374696f6e5f6e616d65223a202272656775736572222c0a2020202020202274797065223a202255736572496e666f220a202020207d2c7b0a20202020202022616374696f6e5f6e616d65223a2022757365726c6f67696e222c0a2020202020202274797065223a2022557365724c6f67696e220a202020207d0a20205d2c0a2020227461626c6573223a205b7b0a202020202020227461626c655f6e616d65223a202275736572726567696e666f222c0a20202020202022696e6465785f74797065223a2022737472696e67222c0a202020202020226b65795f6e616d6573223a205b0a2020202020202020226469646964220a2020202020205d2c0a202020202020226b65795f7479706573223a205b0a202020202020202022737472696e67220a2020202020205d2c0a2020202020202274797065223a20225573657242617365496e666f220a202020207d0a20205d0a7d0a"
  }

```

## Query all producers

**Interface function**

> Interface  Explanation： Query all producers
>
> **Interface address**
>
> URL:  /v1/delegate/getall
>
> **Return format**
>
> JSON
>
> **Request method**
>
> POST

**Request parameters：**

| Parameter | Mandatory | Type   | Default value | Explanation           |
| --------- | --------- | ------ | ------------- | --------------------- |
| limit     | TRUE      | uint32 | None          | Query number          |
| start     | TRUE      | uint32 | 0             | Query start subscript |

**Response field：**

| Parameter    | Type      | Explanation                                                  |
| ------------ | --------- | ------------------------------------------------------------ |
| errcode      | uint32    | Error code, 0- corresponding success, other see error code Chapter |
| msg          | string    | Response description                                         |
| result       | jsonArray | Response results                                             |
| account_name | string    | Account name                                                 |
| public_key   | string    | public key                                                   |
| location     | string    | Node location information, such as "Shanghai, China"         |
| desc         | string    | Node description information                                 |

**Field change**

- None

  **Interface example**

> Address:<<http://127.0.0.1:8689/v1/delegate/getall> >

- Request:

```
  {
      "limit": 10,
      "start": 0
  }

```

- Response:

```
   HTTP/1.1 200 OK
  {
      "errcode": 0,
      "msg": "success",
      "result":  [
          {
              "account_name": "adhil",
              "report_key": "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f",
              "location": "shanghai,china",
              "desc": "",
              "last_slot": 1029945,
              "total_missed": 0,
              "last_confirmed_block_num": 32,
              "active": true
          },
          {
              "account_name": "albireo",
              "report_key": "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f",
              "location": "",
              "desc": "",
              "last_slot": 1026356,
              "total_missed": 123,
              "last_confirmed_block_num": 10,
              "active": false
          }
      ]
  }

```