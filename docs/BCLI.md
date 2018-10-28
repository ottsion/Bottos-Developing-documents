# BCLI

### 一. Brief introduction of BCLI tools

Bottos BCLI implements a set of human-computer interaction command lines, mainly based on RESTFUL APIs to interaction with the chain and the realization of user creation, chain checking, transfer, wallet and other human-computer interaction based on the main chain function.

### 二. Installation and use of BCLI tools

Execute `go build` in the BCLI directory of BOTTOS code. After the compilation is successful, BclI executable file will be generated.

### 三. BCLI command line description

Global options specification

| Global option name | Parameter description            |
| ------------------ | -------------------------------- |
| --servaddr         | Configure global restful address |

Global help information

```
./bcli --help

NAME:
Bottos bcli tool - a tool that makes user communicate with bottos blockchain

USAGE:
bcli [global options] command [command options] [arguments...]

VERSION:
0.0.1

COMMANDS:
    getinfo      get chian info
    getblock     get block info
    gettable     get table info
    account      create or get account
    transfer     for user transfering bto
    transaction  get or push transactions
    contract     get or deploy contract
    p2p          for p2p connection
    delegate     for delegate operations
    wallet       For wallet operations
    genesis      for genesis node operations
    help, h      Shows a list of commands or help for one command

GLOBAL OPTIONS:
--servaddr value  (default: "127.0.0.1:8689")
--help, -h        show help
--version, -v     print the version
```

Command function description

| Master command line | Parameter list | Parameter description                    |
| ------------------- | -------------- | ---------------------------------------- |
| ./bcli              | getinfo        | Get bulk information                     |
| ./bcli              | getblock       | Get the specified BLOCK information      |
| ./bcli              | gettable       | Get contract form information            |
| ./bcli              | account        | Create / acquire user information, pledge / unload / recovery pledge, etc. |
| ./bcli              | transfer       | BTO transfer function                    |
| ./bcli              | transaction    | Query / initiate transaction             |
| ./bcli              | contract       | Query / deployment contracts and ABI     |
| ./bcli              | p2p            | P2P command line temporarily unsupported. |
| ./bcli              | delegate       | Register / solve registered producers, producers vote / cancel voting, etc. |
| ./bcli              | wallet         | Wallet creation / lock / unlock / query etc. |
| ./bcli              | genesis        | Creation node operation related, set the initial producer, transfer the block right, cancel the node operation permissions, etc. |

### 1. BCLI user account function command line

User account function command line is mainly responsible for creating new users, access to designated user information, pledge and unload BTO, and reclaim pledge.

General command line help information

```
./bcli account --help

NAME:
Bottos bcli tool account - create or get account

USAGE:
Bottos bcli tool account command [command options] [arguments...]

COMMANDS:
    create   create account
    get      get account info
    stake    stake of account
    unstake  unstake of account
    claim    claim of stake

OPTIONS:
--help, -h  show help
```

Command function description

| Master command line | Parameter list | Parameter description    |
| ------------------- | -------------- | ------------------------ |
| ./bcli account      | create         | Create new users         |
| ./bcli account      | get            | Getting user information |
| ./bcli account      | stake          | Pledge BTO               |
| ./bcli account      | unstake        | unload BTO               |
| ./bcli account      | claim          | Recovery part pledge BTO |

##### Create user command specification

Help information

```
./bcli account create --help

NAME:
Bottos bcli tool account create - create account
USAGE:
Bottos bcli tool account create [command options] [arguments...]

OPTIONS:
```

--username value acocunt name --pubkey value account public key (default: "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f") --referrer value account referrer

Parameter description

| Master command line | Parameter list | Parameter description                    | Required parameters |
| ------------------- | -------------- | ---------------------------------------- | ------------------- |
| bcli account create | --username     | Username created                         | Yes                 |
|                     | --pubkey       | New user's public key, If  you do not fill, use the built-in default pubkey. | No                  |
|                     | --referrer     | Referee, If you do not fill in, use the default built-in account to sign, otherwise you will use the referee to sign. | No                  |



Return information

After the command succeeds, it will return the Transaction information successfully sent by BCLI, including the user name, public key, initiator and signature (--referrer information, default to the built-in bottos user), and so on.

Examples:

```
./bcli account create --username user1 --pubkey 0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f
```

Output results

```
Create account: user1 Succeed
Trx: 
{
    "version": 1,
    "cursor_num": 1093,
    "cursor_label": 3607725829,
    "lifetime": 1536230581,
    "sender": "bottos",
    "contract": "bottos",
    "method": "newaccount",
    "param": {
        "name": "user1",
        "pubkey": "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f"
    },
    "param_bin": "dc0002da00057573657231da008230343534663163323232336435353361613665653533656131636365613862376266373862386361393966336666363232613362623365363264656463373132303839303333643630393164373732393635343762633037313032326361323833386339653836646563323936363763663734306535633965363534623631323766",
    "sig_alg": 1,
    "signature": "90936cc7c453a737ec16a70d4c63d1032b1f3d3419a3b20f428d6c98490d5934553bcf2bb5ee6c21914b1421fcbb41146fe8beafd0f0bc78d8708811769dd6db"
}
TrxHash: fc83e64f1e05fd6a78256250c6e58a782567ead312db711a6549a6675eafb696
```

##### Sample commands for getting user information

Help information

```
./bcli account get --help
NAME:
Bottos bcli tool account get - get account info

USAGE:
Bottos bcli tool account get [command options] [arguments...]

OPTIONS:
    --username value  acocunt nam
```

Parameter description

| Master command line | Parameter list | Parameter description | Required parameters |
| ------------------- | -------------- | --------------------- | ------------------- |
| bcli account get    | --username     | Username              | Yes                 |

Return information

The command will return the BTO information held by the user after the command is successful.

Examples:

```
./bcli account get --username bottos
```

Output results

```
Account: bottos
Balance: 999710000.00000000 BTO
```

##### Example of user pledge BTO command

Help information

```
./bcli account stake --help

NAME:
Bottos bcli tool account stake - stake of account

USAGE:
Bottos bcli tool account stake [command options] [arguments...]

OPTIONS:
    --account value  acocunt name
    --amount value   amount of bto
```

Parameter description

| Master command line | Parameter list | Parameter description | Required parameters |
| ------------------- | -------------- | --------------------- | ------------------- |
| bcli account stake  | --account      | Username              | Yes                 |
|                     | --amount       | BTO number of pledge  | Yes                 |

Return information

When the command is successful, it will return the Transaction message that BCLI successfully sent.

Examples

```
./bcli account stake --account lyp --amount 2
```



Output results

```
Transfer Succeed:
Trx: 
{
    "version": 1,
    "cursor_num": 3909,
    "cursor_label": 4191535575,
    "lifetime": 1536560467,
    "sender": "bottos",
    "contract": "bottos",
    "method": "stake",
    "param": "dc0001c500200000000000000000000000000000000000000000000000000000000000000002",
    "param_bin": "dc0001c500200000000000000000000000000000000000000000000000000000000000000002",
    "sig_alg": 1,
    "signature": "fcb341de3ada22108107285b511fe35d8777d31150545678eb278ad4457303c8059e1b1ff2fa39fb545a0ea743b45e830c6d1bbf86611087a4807116c5351acd"
}
TrxHash: cbea44984ca17dc640cec7bc5349b6c839229ff86462a24fa0e1196d2b73cedd
```

##### Example of user solution to unload BTO command

Help information

```
./bcli account unstake --help

NAME:
Bottos bcli tool account unstake - unstake of account

USAGE:
Bottos bcli tool account unstake [command options] [arguments...]

OPTIONS:
    --account value  acocunt name
    --amount value   amount of bto
```

Parameter description

| Master command line | Parameter list | Parameter description | Required parameters |
| ------------------- | -------------- | --------------------- | ------------------- |
| bcli account stake  | --account      | Username              | Yes                 |
|                     | --amount       | BTO number of unload  | Yes                 |

Return information

When the command is successful, it will return the Transaction message that BCLI successfully sent.

Examples

```
./bcli account unstake --account lyp --amount 2
```

Output results

```
Transfer Succeed:
Trx: 
{
    "version": 1,
    "cursor_num": 4067,
    "cursor_label": 3077673547,
    "lifetime": 1536560941,
    "sender": "bottos",
    "contract": "bottos",
    "method": "unstake",
    "param": "dc0001c500200000000000000000000000000000000000000000000000000000000000000002",
    "param_bin": "dc0001c500200000000000000000000000000000000000000000000000000000000000000002",
    "sig_alg": 1,
    "signature": "9f14f894a5dd68a7ec010e95ae9c0de52bf368964e8a539d4f2a2c68240e1e4164d4e7a0b34943399c821c81c7b5526ff96370f2cd7d175c4dab062a98f354e5"
}
TrxHash: 336b46af3a8eefbc8879cd46e91c42eb122152111c3f61c312422eb41b77e383
```



##### User unload BTO command example

Help information

```
./bcli account claim --help

NAME:
Bottos bcli tool account claim - claim of stake

USAGE:
Bottos bcli tool account claim [command options] [arguments...]

OPTIONS:
    --account value  acocunt name
    --amount value   amount of bto
```

Parameter description

| Master command line | Parameter list | Parameter description         | Required parameters |
| ------------------- | -------------- | ----------------------------- | ------------------- |
| bcli account claim  | --account      | Username                      | Yes                 |
|                     | --amount       | BTO number of recovery pledge | Yes                 |

Return information

When the command is successful, it will return the Transaction message that BCLI successfully sent.

Examples

```
./bcli account claim --account lyp --amount 2
```

Output results

```
Transfer Succeed:
Trx: 
{
    "version": 1,
    "cursor_num": 4148,
    "cursor_label": 2794796656,
    "lifetime": 1536561184,
    "sender": "bottos",
    "contract": "bottos",
    "method": "claim",
    "param": "dc0001c500200000000000000000000000000000000000000000000000000000000000000002",
    "param_bin": "dc0001c500200000000000000000000000000000000000000000000000000000000000000002",
    "sig_alg": 1,
    "signature": "e05082ecf9028bc9e1e0aa003f6f13cffabba4fc28118ad3d3e9de678525d5b049035818d14c8067b739db34408d8aee1aa50deb99a0fcd9973ad2dcd7fdc627"
}
TrxHash: fe3952e5743db0b35bf669b68e5a3d243c19836e1f5c17b970f524a9d59b8eab
```

#### 2. BCLI contract function command line

BCLI contract function command line mainly implements the user to actively deploy a contract and ABI files to the main chain, and from the main chain to obtain contract code (or files) files and ABI (or files) functions.

The overall help information is as follows

```
./bcli contract --help

NAME:
Bottos bcli tool contract - get or deploy contract

USAGE:
Bottos bcli tool contract command [command options] [arguments...]

COMMANDS:
    deploy      contract deploy
    deploycode  contract  deploycode
    deployabi   Contract  deployabi
    get         get contract

OPTIONS:
    --help, -h  show help
```

Command function description

| Master command line | Parameter list | Parameter description                    |
| ------------------- | -------------- | ---------------------------------------- |
| ./bcli contract     | deploy         | Deploying ABI files and WASM contracts   |
| ./bcli contract     | deploycode     | Deploying contract                       |
| ./bcli contract     | deployabi      | Deploying ABI files                      |
| ./bcli contract     | get            | Get the specified contract and ABI information coexist |

##### BCLI contract deployment command line

Help information

```
./bcli contract deploycode --help
NAME:
Bottos bcli tool contract deploycode - contract  deploycode

USAGE:
    Bottos bcli tool contract deploycode [command options] [arguments...]

OPTIONS:
    --name value  the contract name
    --code value  the contract's wasm file path ( includes wasm file name )
    --user value  the user account
```

Parameter description

| Master command line      | Parameter list | Parameter description                    | Required parameters |
| ------------------------ | -------------- | ---------------------------------------- | ------------------- |
| bcli contract deploycode | --name         | Contract name                            | Yes                 |
|                          | --code         | Location of contract document (.WASM)    | Yes                 |
|                          | --user         | User name who initiating contract signature | Yes                 |

Return information

When the command is successful, it will return the Transaction message that BCLI successfully sent.

Examples

```
./bcli contract deploycode --name nodeclustermng --code nodeclustermng.wasm --user bottos
```

Output results

```
Deploy contract: nodeclustermng Succeed
Trx: 
{
    "version": 1,
    "cursor_num": 4948,
    "cursor_label": 3178968225,
    "lifetime": 1536563584,
    "sender": "nodeclustermng",
    "contract": "bottos",
    "method": "deploycode",
    "param": {
        "name": "nodeclustermng",
        "vm_type": 1,
        "vm_version": 1,
        "contract_code": "0061736d0100000001290760027f7f017f60017f0060027f7f0060067f7f7f7f7f7f017f60037f7f7f017f60000060017f017f02560603656e7608676574506172616d000003656e76066d656d637079000403656e76066d656d736574000403656e7606..."
    },
    "param_bin": "dc0004da000e6e6f6465636c75737465726d6e67cc01cc01c5162f0061736d0100000001290760027f7f017f60017f0060027f7f0060067f7f7f7f7f7f017f60037f7f7f017f60000060017f017f02560603656e7608676574506172616d000003656e76...",
    "sig_alg": 1,
    "signature": "aa80b0d7ab8779f112e38cd9ae6eff759dc3997c2d852c33130baac8cf4c641d549b43d69759c3e2b1c617a7552134be5d68ff11dbb0b2fd70d51a2606b853be"
}
TrxHash: ad45ac9a840642e569f07d0a9ba7fb9331e67bc96576e157b68ee09840d430f7
```

##### BCLI ABI deployment command line

Help information

```
./bcli contract deployabi --help
NAME:
Bottos bcli tool contract deployabi - Contract  deployabi

USAGE:
    Bottos bcli tool contract deployabi [command options] [arguments...]

OPTIONS:
    --name value  the contract name
    --abi value   the contract's abi file path ( includes abi file name )
    --user value  the user account
```

Parameter description

| Master command line     | Parameter list | Parameter description                    | Required parameters |
| ----------------------- | -------------- | ---------------------------------------- | ------------------- |
| bcli contract deployabi | --name         | Contract name                            | Yes                 |
|                         | --abi          | Location of ABI describe files (.Abi)    | Yes                 |
|                         | --user         | User name who initiating contract signature | Yes                 |

Return information

When the command is successful, it will return the Transaction message that BCLI successfully sent.

Examples

```
./bcli contract deployabi --name nodeclustermng --abi nodeclustermng.abi --user bottos
```

Output results

```
{
    "errcode": 0,
    "msg": "trx receive succ",
    "result": {
        "trx": {
            "version": 1,
            "cursor_num": 5264,
            "cursor_label": 890555306,
            "lifetime": 1536564532,
            "sender": "nodeclustermng",
            "contract": "bottos",
            "method": "deployabi",
            "param": "dc0002da000e6e6f6465636c75737465726d6e67c504297b0a09227479706573223a205b5d2c0a092273747275637473223a205b0a20202020202020202020202020207b0a202020202020202020202020202009226e616d65223a20224e6f6465436c7573746572526567222c0a2020202020202020202020202020092262617365223a2022222c0a202020202020202020202020202009226669656c6473223a207b0a20202020202020202020202020200909226e6f64654950223a2022737472696e67222c0a2020202020202020202020202020090922636c75737465724950223a2022737472696e67222c0a202020202020202020202020202009092275756964223a2022737472696e67222c0a20202020202020202020202020200909226361706163697479223a2022737472696e67220a20202020202020202020202020202020202020207d0a2020202020202020202020202020097d2c0a20202020202020202020202020207b0a202020202020202020202020202009226e616d65223a20224e6f6465436c7573746572496e666f222c0a2020202020202020202020202020092262617365223a2022222c0a202020202020202020202020202009226669656c6473223a207b0a2020202020202020202020202020090922636c75737465724950223a2022737472696e67222c0a202020202020202020202020202009092275756964223a2022737472696e67222c0a20202020202020202020202020200909226361706163697479223a2022737472696e67220a20202020202020202020202020202020202020207d0a2020202020202020202020202020097d0a202020202020205d2c0a0922616374696f6e73223a205b0a20202020202020202020202020207b0a20202020202020202020202020200922616374696f6e5f6e616d65223a2022726567222c0a2020202020202020202020202020092274797065223a20224e6f6465436c7573746572526567220a20202020202020202020202020207d0a202020202020205d2c0a09227461626c6573223a205b0a20202020202020202020202020207b0a202020202020202020202020202009227461626c655f6e616d65223a20226e6f6465636c7573746572696e666f222c0a20202020202020202020202020200922696e6465785f74797065223a2022737472696e67222c0a202020202020202020202020202009226b65795f6e616d6573223a20205b0a20202020202020202020202020200909226e6f64654950220a202020202020202020202020202009205d2c0a202020202020202020202020202009226b65795f7479706573223a20205b0a2020202020202020202020202020090922737472696e67220a202020202020202020202020202009205d2c0a2020202020202020202020202020092274797065223a20224e6f6465436c7573746572496e666f220a20202020202020202020202020207d0a202020202020205d0a7d0a",
            "sig_alg": 1,
            "signature": "1807799fb6c007dff7a49641f1a84b41c083d346af300bbafa0dd1894a01ab6e51d1885b9ded14a66850b85e5ef4c38cc515bd9934f7ceaf26f2db33cfc6973f"
        },
        "trx_hash": "62472648f88eece3a959d4cc1ff6e5dca11f05b1c6fb214e49ac4a9b3458ed1e"
    }
}
```



Note: The BOTTOS ABI file is an information description of the interfaces and structures and parameters required for contract methods, such as the nodeclustermng. abi file in this example.

```
"structs" Represents all structural definitions that need to be used for all methods in this contract;
"actions" Represents all contract method names supported by all contracts in this contract and the corresponding structure names.
"tables" When the query contract is invoked(entry into force), the contract information will be written to the chain.TABLES represents the input parameters needed for a piece of information on the query chain, including keywords and corresponding structure information.

Specific examples are as follows.

{
    "types": [],
    "structs": [
            {
                "name": "NodeClusterReg",
                "base": "",
                "fields": {
                    "nodeIP": "string",
                    "clusterIP": "string",
                    "uuid": "string",
                    "capacity": "string"
                    }
                },
            {
                "name": "NodeClusterInfo",
                "base": "",
                "fields": {
                    "clusterIP": "string",
                    "uuid": "string",
                    "capacity": "string"
                    }
                }
    ],
    "actions": [
            {
                "action_name": "reg",
                "type": "NodeClusterReg"
            }
    ],
    "tables": [
            {
                "table_name": "nodeclusterinfo",
                "index_type": "string",
                "key_names":  [
                    "nodeIP"
                ],
                "key_types":  [
                    "string"
                ],
                "type": "NodeClusterInfo"
            }
    ]
}
```

##### BCLI CODE and ABI deploy command line at the same time.

Help information

```
./bcli contract deploy --help
NAME:
Bottos bcli tool contract deploy - contract deploy

USAGE:
    Bottos bcli tool contract deploy [command options] [arguments...]

OPTIONS:
    --name value  the contract name
    --code value  the contract's wasm file path ( includes wasm file name )
    --abi value   the contract's abi file path ( includes abi file name )
    --user value  the user account
```

Parameter description

| Master command line  | Parameter list | Parameter description                    | Required parameters |
| -------------------- | -------------- | ---------------------------------------- | ------------------- |
| bcli contract deploy | --name         | Contract name                            | Yes                 |
|                      | --code         | Contract bytecode after compilation      | Yes                 |
|                      | --abi          | Location of ABI describe files (.Abi)    | Yes                 |
|                      | --user         | User name who initiating contract signature | Yes                 |

Return information

When the command is successful, it will return the Transaction message that BCLI successfully sent.

Examples

```
./bcli contract deploy --name nodeclustermng --code nodeclustermng.wasm --abi nodeclustermng.wasm --user nodeclustermng
```

Output results

```
Deploy contract: nodeclustermng Succeed
Trx:
{
    "version": 1,
    "cursor_num": 5730,
    "cursor_label": 2562596760,
    "lifetime": 1536565930,
    "sender": "nodeclustermng",
    "contract": "bottos",
    "method": "deploycode",
    "param": {
        "name": "nodeclustermng",
        "vm_type": 1,
        "vm_version": 1,
        "contract_code": "0061736d0100000001290760027f7f017f60017f0060027f7f0060067f7f7f7f7f7f017f60037f7f7f017f60000060017f017f02560603656e7608676574506172616d000003656e76066d656d637079000403656e76066d656d736574000403656e7606..."
    },
    "param_bin": "dc0004da000e6e6f6465636c75737465726d6e67cc01cc01c5162f0061736d0100000001290760027f7f017f60017f0060027f7f0060067f7f7f7f7f7f017f60037f7f7f017f60000060017f017f02560603656e7608676574506172616d000003656e76...",
    "sig_alg": 1,
    "signature": "5611a1ccaa1286616e01e93517c04d4353143b5fe3d831ce9f67c48d7a19f39c505e6bd8e190f65ea74f8ade93a5db528c5299b8314cfa37243a8a66df0d900a"
}
TrxHash: 5be2a59d92486a5b9cdc9ab8197f9640d0276949d08c7f8887374a9cd5b36bdc
{
    "errcode": 0,
    "msg": "trx receive succ",
    "result": {
        "trx": {
            "version": 1,
            "cursor_num": 5730,
            "cursor_label": 2562596760,
            "lifetime": 1536565930,
            "sender": "nodeclustermng",
            "contract": "bottos",
            "method": "deployabi",
            "param": "dc0002da000e6e6f6465636c75737465726d6e67c5162f0061736d0100000001290760027f7f017f60017f0060027f7f0060067f7f7f7f7f7f017f60037f7f7f017f60000060017f017f02560603656e7608676574506172616d000003656e76066d656d637079000403656e76066d656d736574000403656e76067072696e7469000103656e76067072696e7473000203656e760b73657453747256616c75650003030504050506000404017000000503010001073d04066d656d6f7279020004696e697400070573746172740008215f474c4f42414c5f5f7375625f495f6e6f6465636c75737465726d6e672e63707000060ada2804f202004100420037028c4041004200370294404100420037029c40410042003702a440410042003702ac40410041003602b440410041003602b840410041003602bc40410041003602c040410041003602c440410041003602c840410041003602cc40410041003602d040410041003602d440410041003602d840410041003602dc40410041003602e040410041003602e440410041003602e840410041003602ec40410041003602f040410041003602f440410041003602f840410041003602fc404100410036028041410041003602844141004100360288414100410036028c414100410036029041410041003602944141004100360298414100410036029c41410041003602a041410041003602a441410041003602a841410041003602ac41410041003602b041410041003602b441410041003602b841410041003602bc41410041003602c041410041003602c441410041003602c841410041003602cc41410041003602d041410041003602d4410b02000bec1b01087f4100410028020441c0196b22083602040240024002400240024002400240200041f200470d00200841c0096a410041801010021a20084180056a410041ba0410021a200841c0096a41801010002205100302402005450d00200841c0096a210020052107034020002d00001003200041016a21002007417f6a22070d000b0b200841003a00f004200820053602f804200841003602fc042008200841c0096a3602f404200841f0046a200841306a1009450d0420082d00304106470d0120082802384104470d04200841f0046a200841306a1009450d0420082d00304105470d022008280238220641016a410a490d03200841013a00f0040c040b200841c0096a41b0c300412310011a200841c0096a4101722105410021000340200520006a2107200041016a2206210020072d00000d000b200841c0096a200610040c040b200841063a00f0040c020b200841063a00f0040c010b0240024020082802f4042207450d00200841fc046a280200220020066a200841f8046a2802004d0d010b200841043a00f0040c010b02402006450d00200720006a210020084180056a2107200621050340200720002d00003a0000200741016a2107200041016a21002005417f6a22050d000b200841fc046a28020021000b20084180056a20066a41003a0000200841fc046a200020066a360200200841f0046a200841306a1009450d000240024020082d00304105470d002008280238220641016a41c303490d01200841013a00f0040c020b200841063a00f0040c010b0240024020082802f4042207450d00200841fc046a280200220020066a200841f8046a2802004d0d010b200841043a00f0040c010b20084189056a210102402006450d00200720006a210020012107200621050340200720002d00003a0000200741016a2107200041016a21002005417f6a22050d000b200841fc046a28020021000b200841fc046a200020066a36020020084180056a20066a41096a41003a0000200841f0046a200841306a1009450d000240024020082d00304105470d002008280238220641016a41e500490d01200841013a00f0040c020b200841063a00f0040c010b0240024020082802f4042207450d00200841fc046a280200220020066a200841f8046a2802004d0d010b200841043a00f0040c010b200841cb086a210202402006450d00200720006a210020022107200621050340200720002d00003a0000200741016a2107200041016a21002005417f6a22050d000b200841fc046a28020021000b200841fc046a200020066a36020020084180056a20066a41cb036a41003a0000200841f0046a200841306a1009450d000240024020082d00304105470d002008280238220341016a410c490d01200841013a00f0040c020b200841063a00f0040c010b0240024020082802f4042205450d00200841fc046a280200220720036a200841f8046a2802004d0d010b200841043a00f0040c010b200841af096a210002402003450d00200520076a210720002105200321060340200520072d00003a0000200541016a2105200741016a21072006417f6a22060d000b200841fc046a28020021070b200841fc046a200720036a3602004100210720084180056a20036a41af046a41003a0000200841366a41002d0086423a0000200841346a41002f0084423b01002008410028008042360230200841306a41017221060340200620076a2105200741016a2203210720052d00000d000b200841306a200310044100210741002103024020082d008005450d0020084180056a4101722104410021050340200420056a2106200541016a2203210520062d00000d000b0b20084180056a20031004200841386a41002f0098423b01002008410029009042370230200841306a41017221060340200620076a2105200741016a2203210720052d00000d000b200841306a200310044100210741002103024020084189056a2d0000450d002008418a056a2104410021050340200420056a2106200541016a2203210520062d00000d000b0b200120031004200841346a41002d00a4423a0000200841002800a042360230200841306a41017221060340200620076a2105200741016a2203210720052d00000d000b200841306a2003100441002107410021030240200841cb086a2d0000450d00200841cc086a2104410021050340200420056a2106200541016a2203210520062d00000d000b0b200220031004200841386a41002d00b8423a0000200841002900b042370230200841306a41017221060340200620076a2105200741016a2203210720052d00000d000b200841306a20031004410021060240200841af096a2d0000450d00200841b0096a2103410021070340200320076a2105200741016a2206210720052d00000d000b0b200020061004200841306a410041b10410021a200841306a21070340200720012d000022053a0000200741016a2107200141016a210120050d000b200841f2036a21070340200720022d000022053a0000200741016a2107200241016a210220050d000b200841d6046a21070340200720002d000022053a0000200741016a2107200041016a210020050d000b200841f0046a41086a418010360200200841fc046a2201410336020041002105200841003a00f004200841dc013a00c00920084180063b00c1092008200841c0096a3602f404024020082d00302203450d00200841306a4101722106410021000340200620006a2107200041016a2205210020072d00000d000b0b4106210220014106360200200841da013a00c309200820053a00c50920082005410874418080fc07714110763a00c4090240024002400240200541ffff03712206450d0041052100200641066a4180104b0d01200820033a00c609024020064101460d00410120066b2105200841c0096a4107722100200841306a41017221070340200020072d00003a0000200041016a2100200741016a2107200541016a22050d000b0b200841fc046a2200200028020020066a22023602000b02400240200841f2036a2d00002201450d00200841f3036a2106410021000340200620006a2107200041016a2205210020072d00000d000c020b0b410021050b4103210020082802f4042207450d00200241016a200841f0046a41086a2802004b0d00200720026a41da013a0000200841fc046a22002000280200220741016a2206360200024020082802f4042202450d0041082100200741036a200841f0046a41086a2802004b0d01200220066a220020054118742005410874418080fc07717220054108764180fe03712005411876727222074118763a0001200020074110763a0000200841fc046a22002000280200220741026a22023602000240200541ffff03712206450d004105210020082802f4042203450d02200220066a200841f8046a2802004b0d02200320026a20013a0000024020064101460d00410120066b2105200320076a41036a2100200841f3036a21070340200020072d00003a0000200041016a2100200741016a2107200541016a22050d000b0b200841fc046a2200200028020020066a22023602000b02400240200841d6046a2d00002201450d00200841d7046a2106410021000340200620006a2107200041016a2205210020072d00000d000c020b0b410021050b4103210020082802f4042207450d01200241016a200841f0046a41086a2802004b0d01200720026a41da013a0000200841fc046a22002000280200220741016a220636020020082802f4042202450d0041082100200741036a200841f0046a41086a2802004b0d01200220066a220020054118742005410874418080fc07717220054108764180fe03712005411876727222074118763a0001200020074110763a0000200841fc046a22002000280200220741026a22023602000240200541ffff03712206450d004105210020082802f4042203450d02200220066a200841f8046a2802004b0d02200320026a20013a0000024020064101460d00410120066b2105200320076a41036a2100200841d7046a21070340200020072d00003a0000200041016a2100200741016a2107200541016a22050d000b0b200841fc046a2200200028020020066a22023602000b41002100200841002903e842370328200841002903e042370320200841206a41017221050340200520006a2107200041016a2206210020072d00000d000b20082d008005450d0220084180056a4101722101410021000340200120006a2107200041016a2205210020072d00000d000c040b0b410821000b200820003a00f00441002100200841106a41002d00d0423a0000200841002903c842370308200841002903c042370300200841017221050340200520006a2107200041016a2206210020072d00000d000b2008200610040c030b410021050b0240200841206a200620084180056a200520082802f40420021005450d0041002100200841146a41002d00a4433a0000200841106a41002802a04336020020084100290398433703082008410029039043370300200841017221050340200520006a2107200041016a2206210020072d00000d000b200820061004410021000c030b41002100200841146a41002d0084433a0000200841106a410028028043360200200841002903f842370308200841002903f042370300200841017221050340200520006a2107200041016a2206210020072d00000d000b2008200610040c010b41002100200841c4006a41002f01f4413b0100200841c0006a41002802f041360200200841002903e841370338200841002903e041370330200841306a41017221050340200520006a2107200041016a2206210020072d00000d000b200841306a200610040b410121000b4100200841c0196a36020420000bf20902047f017e0240024020002802042202450d00200028020c220341016a220420002802084d0d010b200041023a000041000f0b200220036a2d000021022000410c6a200436020002400240024002400240024002400240024002400240024002400240200241bb7e6a220241174b0d00024020020e18000101010101010203040501010101010101010101060107000b200141003a00000240200041046a2802002202450d002000410c6a2203280200220441026a2205200041086a2802004d0d080b200041073a000041000f0b200041063a000041000f0b200141013a00000240200041046a2802002202450d002000410c6a2203280200220441016a200041086a2802004d0d070b200041043a000041000f0b200141023a00000240200041046a2802002202450d002000410c6a2203280200220441026a200041086a2802004d0d070b200041043a000041000f0b200141033a00000240200041046a2802002202450d002000410c6a2203280200220441046a200041086a2802004d0d070b200041043a000041000f0b200141043a00000240200041046a2802002202450d002000410c6a2203280200220441086a200041086a2802004d0d070b200041043a000041000f0b200141053a00000240200041046a2802002202450d002000410c6a2203280200220441026a2205200041086a2802004d0d070b200041043a000041000f0b200141063a00000240200041046a2802002202450d002000410c6a2203280200220441026a2205200041086a2802004d0d070b200041043a000041000f0b200220046a22002d0000210220002d0001210020032005360200200141086a200220004108747222004118742000410874418080fc07717241107636020041010f0b200141086a200220046a2d00003a00002003200328020041016a36020041010f0b200141086a2200200220046a22022d00003a0000200141096a20022d00013a00002003200328020041026a360200200020002f010022014118742001410874418080fc0771724110763b010041010f0b200141086a2205200220046a22002d00003a0000200141096a20002d00013a00002001410a6a200041026a2d00003a00002001410b6a200041036a2d00003a00002003200328020041046a3602002005200528020022004118742000410874418080fc07717220004108764180fe03712000411876727236020041010f0b200141086a2205200220046a22002d00003a0000200141096a20002d00013a00002001410a6a200041026a2d00003a00002001410b6a200041036a2d00003a00002001410c6a200041046a2d00003a00002001410d6a200041056a2d00003a00002001410e6a200041066a2d00003a00002001410f6a200041076a2d00003a00002003200328020041086a360200200520052903002206423886200642288642808080808080c0ff0083842006421886428080808080e03f8320064208864280808080f01f838484200642088842808080f80f832006421888428080fc07838420064228884280fe0383200642388884848437030041010f0b200220046a22002d0000210220002d0001210020032005360200200141086a200220004108747222004118742000410874418080fc07717241107636020041010f0b200220046a22002d0000210220002d0001210020032005360200200141086a200220004108747222004118742000410874418080fc07717241107636020041010b0bf3010b0041040b04e06100000041e0c1000b166e6f646520636c757374657220726567206661696c00004180c2000b076e6f6465495000004190c2000b0a636c75737465724950000041a0c2000b0575756964000041b0c2000b096361706163697479000041c0c2000b117061636b20696e666f206661696c6564000041e0c2000b106e6f6465636c7573746572696e666f000041f0c2000b15736574207374722076616c7565206661696c656400004190c3000b15726567206e6f646520636c757374657220737563000041b0c3000b23696e76616c6964206d6574686f642066726f6d206e6f6465636c75737465726d6e6700",
            "sig_alg": 1,
            "signature": "fecde87d6c5cd6c53b3a4f7c79e6335c5d229bad22092db918850130163cc1bd688bfbf79b188352129ec6c1240d56f8c7c90ad16f953a8cd41a71e63aa426f2"
        },
        "trx_hash": "f55af648b151466499d19d8de3a62ab304a3ff49616e10fa12f78443ec12c4e4"
    }
}
```

##### BCLI gets contract CODE files and ABI files

Help information

```
./bcli contract get --help
NAME:
Bottos bcli tool contract get - get contract

USAGE:
Bottos bcli tool contract get [command options] [arguments...]

OPTIONS:
    --name value  the contract name
    --code value  the contract's wasm file path ( includes wasm file name )
    --abi value   the contract's abi file path ( includes abi file name )
```

Parameter description   

| Master command line  | Parameter list | Parameter description                    | Required parameters |
| -------------------- | -------------- | ---------------------------------------- | ------------------- |
| bcli contract deploy | --name         | Contract name                            | Yes                 |
|                      | --code         | Contract bytecode after compilation      | Yes                 |
|                      | --abi          | The ABI description file (.Abi) path to be saved | Yes                 |


Return information

When this command succeeds, it returns the contract file stream and ABI file information, and saves the corresponding content to the destination contract file path and the ABI file path.

Examples

```
./bcli contract get --name nodeclustermng --code ~/nodeclustermng.wasm --abi ~/nodeclustermng.abi
```

Output results

============CONTRACTCODE===============

"0061736d0100000001290760027f7f017f60017f0060027f7f0060067f7f7f7f7f7f017f60037f7f7f017f60000060017f017f02560603656e7608676574506172616d000003656e76066d656d637079000403656e76066d656d736574000403656e76067072696e7469000103656e76067072696e7473000203656e760b73657453747256616c75650003030504050506000404017000000503010001073d04066d656d6f7279020004696e697400070573746172740008215f474c4f42414c5f5f7375625f495f6e6f6465636c75737465726d6e672e63707000060ada2804f202004100420037028c4041004200370294404100420037029c40410042003702a440410042003702ac40410041003602b440410041003602b840410041003602bc40410041003602c040410041003602c440410041003602c840410041003602cc40410041003602d040410041003602d440410041003602d840410041003602dc40410041003602e040410041003602e440410041003602e840410041003602ec40410041003602f040410041003602f440410041003602f840410041003602fc404100410036028041410041003602844141004100360288414100410036028c414100410036029041410041003602944141004100360298414100410036029c41410041003602a041410041003602a441410041003602a841410041003602ac41410041003602b041410041003602b441410041003602b841410041003602bc41410041003602c041410041003602c441410041003602c841410041003602cc41410041003602d041410041003602d4410b02000bec1b01087f4100410028020441c0196b22083602040240024002400240024002400240200041f200470d00200841c0096a410041801010021a20084180056a410041ba0410021a200841c0096a41801010002205100302402005450d00200841c0096a210020052107034020002d00001003200041016a21002007417f6a22070d000b0b200841003a00f004200820053602f804200841003602fc042008200841c0096a3602f404200841f0046a200841306a1009450d0420082d00304106470d0120082802384104470d04200841f0046a200841306a1009450d0420082d00304105470d022008280238220641016a410a490d03200841013a00f0040c040b200841c0096a41b0c300412310011a200841c0096a4101722105410021000340200520006a2107200041016a2206210020072d00000d000b200841c0096a200610040c040b200841063a00f0040c020b200841063a00f0040c010b0240024020082802f4042207450d00200841fc046a280200220020066a200841f8046a2802004d0d010b200841043a00f0040c010b02402006450d00200720006a210020084180056a2107200621050340200720002d00003a0000200741016a2107200041016a21002005417f6a22050d000b200841fc046a28020021000b20084180056a20066a41003a0000200841fc046a200020066a360200200841f0046a200841306a1009450d000240024020082d00304105470d002008280238220641016a41c303490d01200841013a00f0040c020b200841063a00f0040c010b0240024020082802f4042207450d00200841fc046a280200220020066a200841f8046a2802004d0d010b200841043a00f0040c010b20084189056a210102402006450d00200720006a210020012107200621050340200720002d00003a0000200741016a2107200041016a21002005417f6a22050d000b200841fc046a28020021000b200841fc046a200020066a36020020084180056a20066a41096a41003a0000200841f0046a200841306a1009450d000240024020082d00304105470d002008280238220641016a41e500490d01200841013a00f0040c020b200841063a00f0040c010b0240024020082802f4042207450d00200841fc046a280200220020066a200841f8046a2802004d0d010b200841043a00f0040c010b200841cb086a210202402006450d00200720006a210020022107200621050340200720002d00003a0000200741016a2107200041016a21002005417f6a22050d000b200841fc046a28020021000b200841fc046a200020066a36020020084180056a20066a41cb036a41003a0000200841f0046a200841306a1009450d000240024020082d00304105470d002008280238220341016a410c490d01200841013a00f0040c020b200841063a00f0040c010b0240024020082802f4042205450d00200841fc046a280200220720036a200841f8046a2802004d0d010b200841043a00f0040c010b200841af096a210002402003450d00200520076a210720002105200321060340200520072d00003a0000200541016a2105200741016a21072006417f6a22060d000b200841fc046a28020021070b200841fc046a200720036a3602004100210720084180056a20036a41af046a41003a0000200841366a41002d0086423a0000200841346a41002f0084423b01002008410028008042360230200841306a41017221060340200620076a2105200741016a2203210720052d00000d000b200841306a200310044100210741002103024020082d008005450d0020084180056a4101722104410021050340200420056a2106200541016a2203210520062d00000d000b0b20084180056a20031004200841386a41002f0098423b01002008410029009042370230200841306a41017221060340200620076a2105200741016a2203210720052d00000d000b200841306a200310044100210741002103024020084189056a2d0000450d002008418a056a2104410021050340200420056a2106200541016a2203210520062d00000d000b0b200120031004200841346a41002d00a4423a0000200841002800a042360230200841306a41017221060340200620076a2105200741016a2203210720052d00000d000b200841306a2003100441002107410021030240200841cb086a2d0000450d00200841cc086a2104410021050340200420056a2106200541016a2203210520062d00000d000b0b200220031004200841386a41002d00b8423a0000200841002900b042370230200841306a41017221060340200620076a2105200741016a2203210720052d00000d000b200841306a20031004410021060240200841af096a2d0000450d00200841b0096a2103410021070340200320076a2105200741016a2206210720052d00000d000b0b200020061004200841306a410041b10410021a200841306a21070340200720012d000022053a0000200741016a2107200141016a210120050d000b200841f2036a21070340200720022d000022053a0000200741016a2107200241016a210220050d000b200841d6046a21070340200720002d000022053a0000200741016a2107200041016a210020050d000b200841f0046a41086a418010360200200841fc046a2201410336020041002105200841003a00f004200841dc013a00c00920084180063b00c1092008200841c0096a3602f404024020082d00302203450d00200841306a4101722106410021000340200620006a2107200041016a2205210020072d00000d000b0b4106210220014106360200200841da013a00c309200820053a00c50920082005410874418080fc07714110763a00c4090240024002400240200541ffff03712206450d0041052100200641066a4180104b0d01200820033a00c609024020064101460d00410120066b2105200841c0096a4107722100200841306a41017221070340200020072d00003a0000200041016a2100200741016a2107200541016a22050d000b0b200841fc046a2200200028020020066a22023602000b02400240200841f2036a2d00002201450d00200841f3036a2106410021000340200620006a2107200041016a2205210020072d00000d000c020b0b410021050b4103210020082802f4042207450d00200241016a200841f0046a41086a2802004b0d00200720026a41da013a0000200841fc046a22002000280200220741016a2206360200024020082802f4042202450d0041082100200741036a200841f0046a41086a2802004b0d01200220066a220020054118742005410874418080fc07717220054108764180fe03712005411876727222074118763a0001200020074110763a0000200841fc046a22002000280200220741026a22023602000240200541ffff03712206450d004105210020082802f4042203450d02200220066a200841f8046a2802004b0d02200320026a20013a0000024020064101460d00410120066b2105200320076a41036a2100200841f3036a21070340200020072d00003a0000200041016a2100200741016a2107200541016a22050d000b0b200841fc046a2200200028020020066a22023602000b02400240200841d6046a2d00002201450d00200841d7046a2106410021000340200620006a2107200041016a2205210020072d00000d000c020b0b410021050b4103210020082802f4042207450d01200241016a200841f0046a41086a2802004b0d01200720026a41da013a0000200841fc046a22002000280200220741016a220636020020082802f4042202450d0041082100200741036a200841f0046a41086a2802004b0d01200220066a220020054118742005410874418080fc07717220054108764180fe03712005411876727222074118763a0001200020074110763a0000200841fc046a22002000280200220741026a22023602000240200541ffff03712206450d004105210020082802f4042203450d02200220066a200841f8046a2802004b0d02200320026a20013a0000024020064101460d00410120066b2105200320076a41036a2100200841d7046a21070340200020072d00003a0000200041016a2100200741016a2107200541016a22050d000b0b200841fc046a2200200028020020066a22023602000b41002100200841002903e842370328200841002903e042370320200841206a41017221050340200520006a2107200041016a2206210020072d00000d000b20082d008005450d0220084180056a4101722101410021000340200120006a2107200041016a2205210020072d00000d000c040b0b410821000b200820003a00f00441002100200841106a41002d00d0423a0000200841002903c842370308200841002903c042370300200841017221050340200520006a2107200041016a2206210020072d00000d000b2008200610040c030b410021050b0240200841206a200620084180056a200520082802f40420021005450d0041002100200841146a41002d00a4433a0000200841106a41002802a04336020020084100290398433703082008410029039043370300200841017221050340200520006a2107200041016a2206210020072d00000d000b200820061004410021000c030b41002100200841146a41002d0084433a0000200841106a410028028043360200200841002903f842370308200841002903f042370300200841017221050340200520006a2107200041016a2206210020072d00000d000b2008200610040c010b41002100200841c4006a41002f01f4413b0100200841c0006a41002802f041360200200841002903e841370338200841002903e041370330200841306a41017221050340200520006a2107200041016a2206210020072d00000d000b200841306a200610040b410121000b4100200841c0196a36020420000bf20902047f017e0240024020002802042202450d00200028020c220341016a220420002802084d0d010b200041023a000041000f0b200220036a2d000021022000410c6a200436020002400240024002400240024002400240024002400240024002400240200241bb7e6a220241174b0d00024020020e18000101010101010203040501010101010101010101060107000b200141003a00000240200041046a2802002202450d002000410c6a2203280200220441026a2205200041086a2802004d0d080b200041073a000041000f0b200041063a000041000f0b200141013a00000240200041046a2802002202450d002000410c6a2203280200220441016a200041086a2802004d0d070b200041043a000041000f0b200141023a00000240200041046a2802002202450d002000410c6a2203280200220441026a200041086a2802004d0d070b200041043a000041000f0b200141033a00000240200041046a2802002202450d002000410c6a2203280200220441046a200041086a2802004d0d070b200041043a000041000f0b200141043a00000240200041046a2802002202450d002000410c6a2203280200220441086a200041086a2802004d0d070b200041043a000041000f0b200141053a00000240200041046a2802002202450d002000410c6a2203280200220441026a2205200041086a2802004d0d070b200041043a000041000f0b200141063a00000240200041046a2802002202450d002000410c6a2203280200220441026a2205200041086a2802004d0d070b200041043a000041000f0b200220046a22002d0000210220002d0001210020032005360200200141086a200220004108747222004118742000410874418080fc07717241107636020041010f0b200141086a200220046a2d00003a00002003200328020041016a36020041010f0b200141086a2200200220046a22022d00003a0000200141096a20022d00013a00002003200328020041026a360200200020002f010022014118742001410874418080fc0771724110763b010041010f0b200141086a2205200220046a22002d00003a0000200141096a20002d00013a00002001410a6a200041026a2d00003a00002001410b6a200041036a2d00003a00002003200328020041046a3602002005200528020022004118742000410874418080fc07717220004108764180fe03712000411876727236020041010f0b200141086a2205200220046a22002d00003a0000200141096a20002d00013a00002001410a6a200041026a2d00003a00002001410b6a200041036a2d00003a00002001410c6a200041046a2d00003a00002001410d6a200041056a2d00003a00002001410e6a200041066a2d00003a00002001410f6a200041076a2d00003a00002003200328020041086a360200200520052903002206423886200642288642808080808080c0ff0083842006421886428080808080e03f8320064208864280808080f01f838484200642088842808080f80f832006421888428080fc07838420064228884280fe0383200642388884848437030041010f0b200220046a22002d0000210220002d0001210020032005360200200141086a200220004108747222004118742000410874418080fc07717241107636020041010f0b200220046a22002d0000210220002d0001210020032005360200200141086a200220004108747222004118742000410874418080fc07717241107636020041010b0bf3010b0041040b04e06100000041e0c1000b166e6f646520636c757374657220726567206661696c00004180c2000b076e6f6465495000004190c2000b0a636c75737465724950000041a0c2000b0575756964000041b0c2000b096361706163697479000041c0c2000b117061636b20696e666f206661696c6564000041e0c2000b106e6f6465636c7573746572696e666f000041f0c2000b15736574207374722076616c7565206661696c656400004190c3000b15726567206e6f646520636c757374657220737563000041b0c3000b23696e76616c6964206d6574686f642066726f6d206e6f6465636c75737465726d6e6700"

============ABI===============

{ "types": [], "structs": [ { "name": "NodeClusterReg", "base": "", "fields": { "nodeIP": "string", "clusterIP": "string", "uuid": "string", "capacity": "string" } }, { "name": "NodeClusterInfo", "base": "", "fields": { "clusterIP": "string", "uuid": "string", "capacity": "string" } } ], "actions": [ { "action_name": "reg", "type": "NodeClusterReg" } ], "tables": [ { "table_name": "nodeclusterinfo", "index_type": "string", "key_names": [ "nodeIP" ], "key_types": [ "string" ], "type": "NodeClusterInfo" } ] }

##### BCLI gets contract TABLE information

Help information

```
./bcli gettable --help
NAME:
bcli gettable - get table info

USAGE:
    bcli gettable [command options] [arguments...]

OPTIONS:
    --contract value  contract name (default: "usermng")
    --table value     table name
    --key value       Key value
```

Parameter description

| Master command line | Parameter list | Parameter description                    | Required parameters |
| ------------------- | -------------- | ---------------------------------------- | ------------------- |
| bcli gettable       | --contract     | Contract name                            | Yes                 |
|                     | --table        | The TABLE name to be querying on the chain (refer to ABI file TABLE description). | Yes                 |
|                     | --key          | The key key value to be querying on the chain (refer to ABI file TABLE description). | Yes                 |

Return information

When the command is successful, it will return the Transaction message sent by BCLI.

Examples

```
（No, the contract is being debugged for the time being.）
```

#### 3. BCLI candidate node election function command line

The BCLI candidate node functions to elect the main line of the command line to achieve the candidate nodes: registered nodes are production nodes, unregistered production nodes, enumerate all (part) of the production node information, vote (cast a node to become a production node), cancel voting, etc.

The overall help information is as follows

```
./bcli delegate --help
NAME:
Bottos bcli tool delegate - for delegate operations

USAGE:
    Bottos bcli tool delegate command [command options] [arguments...]

COMMANDS:
    reg         reg delegate
    unreg       unreg delegate
    list        list delegates
    vote        Vote for producers
    cancelvote  cancel vote for producers

OPTIONS:
    --help, -h  show help
```

Command function description

| Master command line | Parameter list | Parameter description  |
| ------------------- | -------------- | ---------------------- |
| ./bcli delegate     | reg            | Register as producer   |
| ./bcli delegate     | unreg          | unregister as producer |
| ./bcli delegate     | list           | View producer list     |
| ./bcli delegate     | vote           | Election producer      |
| ./bcli delegate     | cancelvote     | Cancel the election    |

##### BCLI register production node command line

Help information

```
./bcli delegate reg --help
NAME:
Bottos bcli tool delegate reg - reg delegate

USAGE:
    Bottos bcli tool delegate reg [command options] [arguments...]

OPTIONS:
    --account value      account name
    --signkey value      public sign key (default: "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f")
    --location value     location
    --description value  description
```

Parameter description

| Master command line | Parameter list | Parameter description                    | Required parameters |
| ------------------- | -------------- | ---------------------------------------- | ------------------- |
| bcli delegate reg   | --account      | Username                                 | Yes                 |
|                     | --signkey      | User defined public key (default is built in default value) | Yes                 |
|                     | --location     | Vote geographical city name              | No                  |
|                     | --description  | User defined description                 | No                  |

Return information

When the command is successful, it will return the Transaction message sent by BCLI.

Examples

```
./bcli delegate reg --account lyp --location "SHANGHAI" --description "Reg lyp as a producer"
```

Output results

```
Transfer Succeed:
Trx:
{
    "version": 1,
    "cursor_num": 6115,
    "cursor_label": 789697330,
    "lifetime": 1536567085,
    "sender": "bottos",
    "contract": "bottos",
    "method": "regdelegate",
    "param": "dc0004da00036c7970da008230343534663163323232336435353361613665653533656131636365613862376266373862386361393966336666363232613362623365363264656463373132303839303333643630393164373732393635343762633037313032326361323833386339653836646563323936363763663734306535633965363534623631323766da00085348414e47484149da0015526567206c797020617320612070726f6475636572",
    "param_bin": "dc0004da00036c7970da008230343534663163323232336435353361613665653533656131636365613862376266373862386361393966336666363232613362623365363264656463373132303839303333643630393164373732393635343762633037313032326361323833386339653836646563323936363763663734306535633965363534623631323766da00085348414e47484149da0015526567206c797020617320612070726f6475636572",
    "sig_alg": 1,
    "signature": "eb0f741d4466c8d650c867dd3da988d2b81fc7c035018a461c01b9adab0767177239a041c9e6835e0952d2a95ab48900255a97ef8145a61115b286f1bbbfd3bb"
}
TrxHash: 816dc08c5cb3c4e059d04ac4842ceb583b34c58c865311c889d2d9d9acf9658b
```

Note: this command performs the premise that the creation node must successfully transfer the block rights. Reference command`./bcli genesis blkprodtrans --sender lyp --actblknum 10`

##### BCLI unregister production node command line

Help information

```
./bcli  delegate unreg  --help

NAME:
Bottos bcli tool delegate unreg - unreg delegate

USAGE:
    Bottos bcli tool delegate unreg [command options] [arguments...]

OPTIONS:
    --account value  account
```

Parameter description

| Master command line | Parameter list | Parameter description | Required parameters |
| ------------------- | -------------- | --------------------- | ------------------- |
| bcli delegate unreg | --account      | Username              | Yes                 |

Return information

When the command is successful, it will return the Transaction message sent by BCLI.

Examples

```
./bcli delegate unreg --account lyp
```

Output results

```
Transfer Succeed: Trx: { "version": 1, "cursor_num": 6237, "cursor_label": 2162498930, "lifetime": 1536567466, "sender": "bottos", "contract": "bottos", "method": "unregdelegate", "param": "dc0001da00036c7970", "param_bin": "dc0001da00036c7970", "sig_alg": 1, "signature": "48e3f949527851c13e9a82e5eb5bd605548ca4491ea05f3afed8405cab6985c037b6d59175d7880658da9bad33ab61e14da77b846305913d1b9326afd0b326dd" } TrxHash: 8eacc1d64d722565b0033ca7afbd090ab73ae56f6ab2bf10fe934a3d305ffd6f
```

##### BCLI lists the current production node list

Help information

```
./bcli delegate list --help
NAME:
Bottos bcli tool delegate list - list delegates

USAGE:
    Bottos bcli tool delegate list [command options] [arguments...]

OPTIONS:
    --limit value  (default: 100)
    --start value  (default: 0)
```

Parameter description

| Master command line | Parameter list | Parameter description                    | Required parameters |
| ------------------- | -------------- | ---------------------------------------- | ------------------- |
| bcli delegate list  | --limit        | Output top N record                      | No                  |
|                     | --limit        | From where to output and statistics numbers | No                  |

Return information

When the command is successful, it will return the Transaction message sent by BCLI.

Examples

```
./bcli delegate list
```

Output results

```
[
    {
        "account_name": "adhil",
        "active": false,
        "desc": "",
        "last_confirmed_block_num": 6358,
        "last_slot": 1147647,
        "location": "",
        "report_key": "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f",
        "total_missed": 0
    },
    {
        "account_name": "albireo",
        "active": false,
        "desc": "",
        "last_confirmed_block_num": 6377,
        "last_slot": 1147667,
        "location": "",
        "report_key": "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f",
        "total_missed": 0
    },
    .....
    ....
    .... (etc.)
```

##### BCLI producer voting command line

Help information

```
./bcli delegate vote --help
NAME:
Bottos bcli tool delegate vote - Vote for producers

USAGE:
    Bottos bcli tool delegate vote [command options] [arguments...]

OPTIONS:
    --voter value     voter account
    --delegate value  delegate account
```

Parameter description

| Master command line | Parameter list | Parameter description                    | Required parameters |
| ------------------- | -------------- | ---------------------------------------- | ------------------- |
| bcli delegate vote  | --voter        | Voter                                    | Yes                 |
|                     | --delegate     | Which production node should be put to (must be registered to the node of the production node) | Yes                 |

Return information

When the command is successful, it will return the Transaction message sent by BCLI.

Examples

```
./bcli delegate vote --voter bottos --delegate lyp
```

Output results

```
Transfer Succeed:
Trx: 
{
    "version": 1,
    "cursor_num": 6616,
    "cursor_label": 1568844234,
    "lifetime": 1536568645,
    "sender": "bottos",
    "contract": "bottos",
    "method": "votedelegate",
    "param": "dc0003cc01da0006626f74746f73da00036c7970",
    "param_bin": "dc0003cc01da0006626f74746f73da00036c7970",
    "sig_alg": 1,
    "signature": "86968717552104084b995c8ac46aca0f20fde5535daaf6f634af3cef9ecef804508577ee0c4c5c41f33e10feec45c22fccb5569e712fa62149f38d816d76ce35"
}
```

##### BCLI producer cancels voting command line

Help information

```
./bcli delegate cancelvote --help
NAME:
Bottos bcli tool delegate cancelvote - cancel vote for producers

USAGE:
    Bottos bcli tool delegate cancelvote [command options] [arguments...]

OPTIONS:
    --voter value     voter account
    --delegate value  delegate account
```

Parameter description

| Master command line      | Parameter list | Parameter description                    | Required parameters |
| ------------------------ | -------------- | ---------------------------------------- | ------------------- |
| bcli delegate cancelvote | --voter        | Voter                                    | Yes                 |
|                          | --delegate     | To cancel which production node should be thrown (must fill in the node registered as the production node). | Yes                 |

Return information

When the command is successful, it will return the Transaction message sent by BCLI.

Examples

```
./bcli delegate cancelvote --voter bottos --delegate lyp
```

Output results

```
Transfer Succeed:
Trx:
{
    "version": 1,
    "cursor_num": 6690,
    "cursor_label": 482796464,
    "lifetime": 1536568876,
    "sender": "bottos",
    "contract": "bottos",
    "method": "votedelegate",
    "param": "dc0003cc00da0006626f74746f73da00036c7970",
    "param_bin": "dc0003cc00da0006626f74746f73da00036c7970",
    "sig_alg": 1,
    "signature": "946291c599105d2906d004b73fbec002e4ae2d8e113a4d71bbc17fa7129affb324ee6b6e1a101f9da217eee14ff1bac697f55bb29e634cdd4eda20b33801d116"
}
TrxHash: f90e5cb5c6e5990c6bceb6e0fd7ec5a2f629760dd809b7fbd9c2832f916319ee
```

#### 4. BCLI block information access command line

BCLI block information acquisition mainly includes: obtaining the current block information, bulk information.

##### BCLI bulk information access command line

Help information

```
./bcli getinfo --help
NAME:
    bcli getinfo - get chian info

USAGE:
    bcli getinfo [arguments...]
```

Parameter description

| Master command line | Parameter list | Parameter description | Required parameters |
| ------------------- | -------------- | --------------------- | ------------------- |
| ./bcli getinfo      | (None)         | (None)                | (None)              |
|                     | (None)         | (None)                | (None)              |

Return information

When the command is successful, it will return the latest block information in real time.

Examples

```
./bcli getinfo
```

Output results

```
==Chain Info==

{
    "head_block_num": 7047,
    "head_block_hash": "34460313889fc988137e42394009df8880e5e82118fcae4579fc0e33d913309e",
    "head_block_time": 1536569883,
    "head_block_delegate": "sulafat",
    "cursor_label": 3641913502,
    "last_consensus_block_num": 7026,
    "chain_id": "5c7c2ea85df042747b38b183c84c8313b499177ed4abbf29d0947f4908934941"
}
```

##### BCLI latest block information access command line

Help information

```
./bcli getblock --help
NAME:
    bcli getblock - get block info

USAGE:
    bcli getblock [command options] [arguments...]

OPTIONS:
    --num value   get block by number (default: 100)
    --hash value  get block by hash
```

Parameter description

| Master command line | Parameter list | Parameter description | Required parameters |
| ------------------- | -------------- | --------------------- | ------------------- |
| ./bcli getblock     | (None)         | (None)                | (None)              |
|                     | (None)         | (None)                | (None)              |

Return information

```
When the command is successful, it will return the latest block information in real time.
```

Examples

```
./bcli getblock
```
Output results
```
==Block Info==

{
    "prev_block_hash": "6de5f9fb40511d307a55f5838e936a4d8c211177a0750287010bc7e67935954f",
    "block_num": 100,
    "block_hash": "e97df19ae9b73ba46b5f5681b159f87a56a4aa8426dc0407f6ea4ed12fb1857d",
    "cursor_block_label": 800163197,
    "block_time": 1536548940,
    "trx_merkle_root": "0000000000000000000000000000000000000000000000000000000000000000",
    "delegate": "vega",
    "delegate_sign": "fa3504d657168fb9b16ae9ee3d281ead80adb43fbb3859213198f856732b12c33459b2ff820af6fdf15c9dce7dde9a29fe0446a09568b1a34a3909cd64a73815",
    "trxs": null
}
```

#### 5. BCLI creation node function command line

The BCLI creation node function command line mainly includes: adding the initial producer, handing over the block rights, revoking the privileged operation privileges of the Genesis node.

The overall help information is as follows

```
./bcli genesis --help

NAME:
Bottos bcli tool genesis - for genesis node operations

USAGE:
    Bottos bcli tool genesis command [command options] [arguments...]

COMMANDS:
    setdelegate      set delegate
    blkprodtrans     for genesis node transfering the permission of producing blocks
    cancelprevilige  cancel genesis node permission

OPTIONS:
    --help, -h  show help
```

Command function description

| Master command line | Parameter list  | Parameter description                    |
| ------------------- | --------------- | ---------------------------------------- |
| ./bcli genesis      | setdelegate     | Designated initial producer on creation node |
| ./bcli genesis      | blkprodtrans    | The creation node transfers the right to block. |
| ./bcli genesis      | cancelprevilige | Creation node cancels operation privileges |

##### BCLI creation node adds initial producer function command line.

Help information

```
./bcli genesis setdelegate --help
NAME:
Bottos bcli tool genesis setdelegate - set delegate

USAGE:
    Bottos bcli tool genesis setdelegate [command options] [arguments...]

OPTIONS:
    --sender value       sender account
    --account value      account name
    --signkey value      public sign key (default: "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f")
    --location value     location
    --description value  description
```

Parameter description

| Master command line        | Parameter list | Parameter description                    | Required parameters |
| -------------------------- | -------------- | ---------------------------------------- | ------------------- |
| ./bcli genesis setdelegate | --sender       | Initiating signer (must be a registered user name, default to the built-in bottos user). | No                  |
|                            | --account      | The initial producer user name to be added. | Yes                 |
|                            | --signkey      | User's public key                        | No                  |
|                            | --location     | User specified city name                 | No                  |
|                            | --description  | User specified description               | No                  |

Return information

When the command is successful, it will return the Transaction information submitted by BCLI.

Examples

```
./bcli genesis setdelegate --sender bottos --account lyp
```

Output results

```
Transfer Succeed:
Trx: 
{
    "version": 1,
    "cursor_num": 7356,
    "cursor_label": 2458267119,
    "lifetime": 1536570943,
    "sender": "bottos",
    "contract": "bottos",
    "method": "setdelegate",
    "param": "",
    "param_bin": "",
    "sig_alg": 1,
    "signature": "fe901957f6b55a41aef893ec6c285bd8f3c6624a1a0950d96cea4dab5896fe3d4476f602b910cdd7d51e9f74ee69af9c17b126ca37a85c040d6aee0827e33e3d"
}
TrxHash: ec4654e3edb61c661ed63cf6b02d44cd255ca7a604c463074fb1307f70025181
```

##### BCLI creation node transfer block right function command line

Help information

```
./bcli genesis blkprodtrans --help
NAME:
Bottos bcli tool genesis blkprodtrans - for genesis node transfering the permission of producing blocks

USAGE:
    Bottos bcli tool genesis blkprodtrans [command options] [arguments...]

OPTIONS:
    --sender value     sender account
    --actblknum value  the threshold number of active block for which genesis node transfering the permission of producing blocks after exceeding it (default: 0)
```

Parameter description

| Master command line         | Parameter list | Parameter description                    | Required parameters |
| --------------------------- | -------------- | ---------------------------------------- | ------------------- |
| ./bcli genesis blkprodtrans | --sender       | Initiating signer (must be a registered user name, default to the built-in bottos user). | No                  |

Return information

When the command is successful, it will return the Transaction information submitted by BCLI.

Examples

```
 ./bcli genesis blkprodtrans --sender lyp
```

Output results

```
Transfer Succeed:
Trx: 
{
    "version": 1,
    "cursor_num": 7431,
    "cursor_label": 974139076,
    "lifetime": 1536571174,
    "sender": "lyp",
    "contract": "bottos",
    "method": "blkprodtrans",
    "param": "",
    "param_bin": "",
    "sig_alg": 1,
    "signature": "393abd00bc0c7bb2da1bec6fb03d755e553e17cddfd7b4e40daecdf372d188854517d099a5d166057e6e85e7b4edae98d5e75d48ec09f891d1f6eca3c94b979f"
}
TrxHash: 2e25dd5f8bc7c598a3c6b81f245b6413143973ab9c9bc46f695a9ef6b33b4507
```

##### BCLI revocation of creation node privileges operation permission function command line

Help information

```
./bcli genesis cancelprevilige --help
NAME:
Bottos bcli tool genesis cancelprevilige - cancel genesis node permission

USAGE:
    Bottos bcli tool genesis cancelprevilige [command options] [arguments...]

OPTIONS:
    --sender value  sender account
```

Parameter description

| Master command line            | Parameter list | Parameter description                    | Required parameters |
| ------------------------------ | -------------- | ---------------------------------------- | ------------------- |
| ./bcli genesis cancelprevilige | --sender       | Initiating signer (must be a registered user name, default to the built-in bottos user). | No                  |

Return information

When the command is successful, it will return the Transaction information submitted by BCLI.

Examples

```
 ./bcli genesis cancelprevilige --sender lyp
```

Output results

```
Transfer Succeed:
Trx: 
{
    "version": 1,
    "cursor_num": 7479,
    "cursor_label": 4050849039,
    "lifetime": 1536571324,
    "sender": "lyp",
    "contract": "bottos",
    "method": "cancelprevilige",
    "param": "",
    "param_bin": "",
    "sig_alg": 1,
    "signature": "bb88393a4d1b526c079f2c3d0d38bbbc90f46084fb0c3e21cde9a5eaed5e0ce140a7a5dd30192ae63df489b46fa54d0ad4ff077c5f7286e559221e64c5d1ee9f"
}
TrxHash: 794fb7f03c8d9ae0545660d66394f45e5cc261966fc66342dab72a70a6bbd2ea
```

#### 6. BCLI transfer function command line

The BCLI transfer function is responsible for BTO transfers from FROM users to TO users.

##### BCLI transfer order line

Help information

```
./bcli transfer --help
NAME:
bcli transfer - for user transfering bto

USAGE:
    bcli transfer [command options] [arguments...]

OPTIONS:
    --from value    the from user account (default: "bottos")
    --to value      the [to] user account (default: "bottos")
    --amount value  the amount of bto (default: "0")
```

Parameter description

| Master command line | Parameter list | Parameter description                    | Required parameters |
| ------------------- | -------------- | ---------------------------------------- | ------------------- |
| ./bcli transfer     | --from         | Transfer                                 | No                  |
|                     | --to           | Transfer target person                   | No                  |
|                     | --amount       | Number of transfers BTO                  | No                  |
|                     | --sign         | User defined public key (default is built in default value) | No                  |

Return information

When the command is successful, it will return the Transaction information submitted by BCLI.

Examples

```
./bcli transfer --from bottos --to lyp --amount 2
```

Output results

```
Transfer Succeed
    From: bottos
    To: lyp
    Amount: 200000000
Trx: 
{
    "version": 1,
    "cursor_num": 7762,
    "cursor_label": 117036287,
    "lifetime": 1536572206,
    "sender": "bottos",
    "contract": "bottos",
    "method": "transfer",
    "param": {
        "from": "bottos",
        "to": "lyp",
        "value": 2
    },
    "param_bin": "dc0003da0006626f74746f73da00036c7970c50020000000000000000000000000000000000000000000000000000000000bebc200",
    "sig_alg": 1,
    "signature": "3aa45652b368827fd5480721de1588ed08c2289de2cfa97ce352d65c8f1acc6e4f04b2c8492caacedb61097dea2728019d4c40c932d763ed7e26d051ca27a188"
}
TrxHash: 86cbc8bd54d85fc817f3675103e62c5693fe7ef1520f2218f57c6406be05b46b
```

#### 7. BCLI Transaction submit and query command line

The BCLI Transaction submission and query command line is responsible for submitting a user-defined Transaction to the chain or querying an existing contract information based on the TrxHash value.

The overall help information is as follows

```
./bcli transaction --help

NAME:
Bottos bcli tool transaction - get or push transactions

USAGE:
Bottos bcli tool transaction command [command options] [arguments...]

COMMANDS:
    get   get tx details
    push  push transaction

OPTIONS:
--help, -h  show help
```

Command function description

| Master command line | Parameter list | Parameter description                    |
| ------------------- | -------------- | ---------------------------------------- |
| ./bcli transaction  | get            | Gets the transaction information corresponding to the specified TRXHASH. |
| ./bcli transaction  | push           | Submit a Transaction                     |

##### BCLI Transaction query command line

Help information

```
./bcli transaction get --help

NAME:
    Bottos bcli tool transaction get - get tx details

USAGE:
    Bottos bcli tool transaction get [command options] [arguments...]

OPTIONS:
    --trxhash value 
```

Parameter description

| Master command line    | Parameter list | Parameter description        | Required parameters |
| ---------------------- | -------------- | ---------------------------- | ------------------- |
| ./bcli transaction get | --trxhash      | Transaction hash index value | Yes                 |

Return information

After the command is successful, the Transaction information corresponding to the specified Trxhash will be returned.

Examples

```
./bcli transaction get --trxhash 86cbc8bd54d85fc817f3675103e62c5693fe7ef1520f2218f57c6406be05b46b
```

Output results

```
{
    "contract": "bottos",
    "cursor_label": 117036287,
    "cursor_num": 7762,
    "lifetime": 1536572206,
    "method": "transfer",
    "param": null,
    "sender": "bottos",
    "sig_alg": 1,
    "signature": "3aa45652b368827fd5480721de1588ed08c2289de2cfa97ce352d65c8f1acc6e4f04b2c8492caacedb61097dea2728019d4c40c932d763ed7e26d051ca27a188",
    "version": 1
}
```

##### BCLI Transaction submits command line

Help information

```
./bcli transaction push --help
NAME:
    Bottos bcli tool transaction push - push transaction

USAGE:
    Bottos bcli tool transaction push [command options] [arguments...]

OPTIONS:
    --sender value    acocunt name
    --contract value  contract name
    --method value    method name
    --param value     param value
    --sign value      sign value
```

Parameter description

| Master command line     | Parameter list | Parameter description                    | Required parameters |
| ----------------------- | -------------- | ---------------------------------------- | ------------------- |
| ./bcli transaction push | --sender       | Signature initiator (default for built-in bottos user) | No                  |
| ./bcli transaction push | --contract     | Contract name                            | Yes                 |
| ./bcli transaction push | --method       | Contract method name                     | Yes                 |
| ./bcli transaction push | --param        | Parameter key pair                       | Yes                 |
| ./bcli transaction push | --sign         | User defined public key (default is built in default value) | No                  |

Return information

After the command is successful, the Transaction information corresponding to the specified Trxhash will be returned.

Examples

```
（etc.）
```

#### 8. BCLI wallet command line

The wallet function mainly provides wallet creation, binding, unlocking, locking and querying functions for user submitting Transaction.

Help information

```
./bcli wallet --help

NAME:
Bottos bcli tool wallet - For wallet operations

USAGE:
Bottos bcli tool wallet command [command options] [arguments...]

COMMANDS:
    generatekey  generate key pairs
    create       create wallet
    lock         lock wallet
    unlock       unlock wallet
    list         list wallet
    listkey      listkey of wallet

OPTIONS:
--help, -h  show help
```

Command function description

| Master command line | Parameter list | Parameter description                    |
| ------------------- | -------------- | ---------------------------------------- |
| ./bcli wallet       | generatekey    | Create a pair of new public and private key pairs |
| ./bcli wallet       | create         | Create a wallet                          |
| ./bcli wallet       | lock           | Lock the wallet                          |
| ./bcli wallet       | unlock         | Unlock the wallet                        |
| ./bcli wallet       | list           | List all purses.                         |
| ./bcli wallet       | listkey        | List the corresponding public and private key pairs of the purse (which must be used after the purse is unlocked). |

##### BCLI create purse public and private key command line

Help information ./bcli wallet generatekey --help

```
NAME:
    Bottos bcli tool wallet generatekey - generate key pairs

USAGE:
    Bottos bcli tool wallet generatekey [arguments...]
```

Parameter description

| Master command line       | Parameter list | Parameter description | Required parameters |
| ------------------------- | -------------- | --------------------- | ------------------- |
| ./bcli wallet generatekey | (None)         | （None）                | （None）              |

Return information

After the command is successful, a pair of newly generated public and private key pairs will be returned.

Examples

```
 ./bcli wallet generatekey
```

Output results { "private_key": "b8b890ebc315a8e1c3a6f7b78977d68ca1e9274c986314ccbe967b964cf68b66", "public_key": "0485fccecf8c8e6260d8558e1a61adca3a888127e34ba0d052dfeb1c31d419bf0494482e7e8a447d63394cff713fc00aa8e64c24b73a8173661a91884b71407bce" }

##### BCLI create wallet command line

Help information

```
./bcli wallet create --help

NAME:
Bottos bcli tool wallet create - create wallet

USAGE:
Bottos bcli tool wallet create [command options] [arguments...]

OPTIONS:
--account value  account name
```

Parameter description

| Master command line  | Parameter list | Parameter description       | Required parameters |
| -------------------- | -------------- | --------------------------- | ------------------- |
| ./bcli wallet create | --account      | User name of wallet binding | Yes                 |

Return information

When this command succeeds, it returns the user's wallet file keystore information. The path is under / home / bottos / bot, and the file format is the user. keystore file.

Examples

```
 ./bcli wallet create --account lyp
```

Output results

Please input your password for your wallet:

Please input your private key for your wallet:

{ "wallet_name": "lyp.keystore" }

Note: in this case, users are required to manually enter the purse password and the private key used.

##### BCLI lock wallet command line

Help information

```
./bcli wallet lock --help

NAME:
Bottos bcli tool wallet lock - lock wallet

USAGE:
Bottos bcli tool wallet lock [command options] [arguments...]

OPTIONS:
--account value  account name
```

Parameter description

| Master command line | Parameter list | Parameter description       | Required parameters |
| ------------------- | -------------- | --------------------------- | ------------------- |
| ./bcli wallet lock  | --account      | User name of wallet binding | Yes                 |

Return information

BCLI unlocks the purse command line. After the command is successful, the wallet lock status flag will be returned.

Examples

./bcli wallet lock --account lyp

Output results

./bcli wallet lock --account lyp { "lock": true }

##### BCLI unlock wallet command line

Help information

```
./bcli wallet unlock --help

NAME:
Bottos bcli tool wallet unlock - unlock wallet

USAGE:
Bottos bcli tool wallet unlock [command options] [arguments...]

OPTIONS:
--account value  account name
```

Parameter description

| Master command line  | Parameter list | Parameter description       | Required parameters |
| -------------------- | -------------- | --------------------------- | ------------------- |
| ./bcli wallet unlock | --account      | User name of wallet binding | Yes                 |

Return information

The command will return to the wallet lock status flag after the command is successful.

Examples

```
 ./bcli wallet unlock --account lyp
```

Output results

```
Please input your password for your wallet: 

{
    "unlock": true
}
```

Note: this example requires the user to enter the password when creating the wallet at that time.

##### BCLI view all wallet command lines

Help information

```
./bcli wallet list --help

NAME:
Bottos bcli tool wallet list - list wallet

USAGE:
Bottos bcli tool wallet list [arguments...]
```

Parameter description

| Master command line | Parameter list | Parameter description | Required parameters |
| ------------------- | -------------- | --------------------- | ------------------- |
| ./bcli wallet list  | (None)         | （None）                | （None）              |

Return information

The command will return to the wallet lock status flag after the command is successful.

Examples

```
 ./bcli wallet list
```

Output results

```
[
    {
        "account_name": "lyp",
        "public_key": "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f",
        "wallet_path": "/home/bottos/bot/lyp.keystore"
    }
]
```

##### BCLI to view all purse public and private key command lines

Note: this command must be executed in the purse unlock state.

Help information

```
./bcli wallet listkey --help

NAME:
Bottos bcli tool wallet listkey - listkey of wallet

USAGE:
    Bottos bcli tool wallet listkey [command options] [arguments...]

OPTIONS:
    --account value  account name
```

Parameter description

| Master command line   | Parameter list | Parameter description | Required parameters |
| --------------------- | -------------- | --------------------- | ------------------- |
| ./bcli wallet listkey | --account      | Wallet binding users  | （None）              |

Return information

After the command is successful, it will return the wallet account corresponding to the public and private key pair.

Examples

```
./bcli wallet listkey --account lyp
```

Output results

{ "account_name": "lyp", "private_key": "b799ef616830cd7b8599ae7958fbee56d4c8168ffd5421a16025a398b8a4be45", "public_key": "0454f1c2223d553aa6ee53ea1ccea8b7bf78b8ca99f3ff622a3bb3e62dedc712089033d6091d77296547bc071022ca2838c9e86dec29667cf740e5c9e654b6127f" }