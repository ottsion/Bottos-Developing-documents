# Development and deployment of intelligent contracts



We are now using C++ to develop a smart contract for mobile phone contacts, first to write user information to the chain, and then to read out the information.

## Intelligent contract development Example

The code is as follows

> The function of the following contract is to store and read `userName` and `userInfo`.

- testRegUser.hpp

```
#define USER_NAME_LEN (20)
#define USER_INFO_LEN (20)


//@abi action reguser
struct UserInfo {
    char userName[USER_NAME_LEN];
    char userInfo[USER_INFO_LEN];
};


//@abi table userinfo:[index_type:string, key_names:userName, key_types:string]
struct UserBaseInfo {
    char userInfo[USER_INFO_LEN];
};
```

- testRegUser.cpp

```
#include "contractcomm.hpp"
#include "string.hpp"
#include "testRegUser.hpp"


#define PARAM_MAX_LEN (2048)

#define ERROR_PACK_FAIL (-1)
#define ERROR_UNPACK_FAIL (-2)
#define ERROR_SAVE_DB_FAIL (-3)
#define ERROR_METHOD_INVALID (-4)



static bool unpack_struct(MsgPackCtx *ctx, UserInfo *info)
{ 
    uint32_t size = 0;
    UNPACK_ARRAY(2)

    UNPACK_STR(info, userName, (USER_NAME_LEN+1))
    UNPACK_STR(info, userInfo, (USER_INFO_LEN+1))

    return 1;
}

static bool pack_struct(MsgPackCtx *ctx, UserBaseInfo *info)
{   
    PACK_ARRAY16(1)
    PACK_STR16(info, userInfo )

    return 1;
}

void init()
{
}

int start(char* method) 
{
    if (0 == strcmp("reguser", method))
    {
        char param[PARAM_MAX_LEN] = {0};
        uint32_t paramLen = 0;
        UserInfo userinfo = {{0}};       

        paramLen = getParam(param, PARAM_MAX_LEN);

        MsgPackCtx ctx;
        msgpack_init(&ctx, (char*)param, paramLen);
        bool unpackSuc = unpack_struct(&ctx, &userinfo);
        if (!unpackSuc)
        {
            char pstr[] = "unpack userinfo failed";
            myprints(pstr);

            return ERROR_UNPACK_FAIL;
        }

        UserBaseInfo userBaseInfo = {{0}};

        strcpy(userBaseInfo.userInfo, userinfo.userInfo);

        msgpack_init(&ctx, (char*)param, paramLen);

        bool packSuc = pack_struct(&ctx, &userBaseInfo);
        if (!packSuc)
        {
            char pstr[] = "pack userbaseinfo failed";
            myprints(pstr);

            return ERROR_PACK_FAIL;
        }

        char objname[] = "userreginfo";       

        uint32_t saveLen = setBinValue(objname, strlen(objname), userinfo.userName, strlen(userinfo.userName), ctx.buf, ctx.pos);
        if (0 == saveLen)
        {
            char pstr[] = "save db failed";
            myprints(pstr);

            return ERROR_SAVE_DB_FAIL;
        }  

        return 0;      

    }    
    else 
    {
        char pstr[] = "invalid method";
        prints(pstr, strlen(pstr));
        return ERROR_METHOD_INVALID;
    }
}
```

## Compiling intelligent contracts

Our smart contracts need to be compiled into`.Wasm` format files before they can be executed normally. So, the first step we need to compile is our intelligent contract code into `.Wasm` file.

- Download compiler tools

```
git clone https://github.com/bottos-project/contract-tool-cpp.git
```

- Compiling contract
- Enter the contract directory `testRegUser`, then run the following command to compile the contract.

```
python ../gentool.py wasm testRegUser.cpp
```

At this time, the `testRegUser.wast` and `testRegUser.wasm` files will be generated in the contract directory.

2. Then run the following command to generate `testRegUser.abi`

```
python ../gentool.py testRegUser.hpp
```

At this point, the contract directory generates `testRegUser.abi` files.

## Deploying smart contracts and ABI files

After we compile the intelligent contract, we need the BclI tool to deploy the.Wasm file to the Bottos chain.

**Use of BCLI tools**

- Enter the bottos project and deploy the compiled `wasm` file using the BclI tool.

Copy the `BclI` tool to the directory where `wasm` and `ABI` files are located. Execute the following commands

See how bclI is used.

```
bcli --help
```

- Create public and private key

```
./bcli --servaddr 192.168.52.130:8689 wallet generatekey
```

The command will return the public private key pair.

```
{
    "private_key": "773df18f6d7e1fa3fda1f2c36806bc40b20bbdd61ab59d00a2b47ecc4f9718e6",
    "public_key": "04daec4f6b166ea21f5a3c4f8d50ef638ad0312cb01def711ba0ab350c10abeba8a137e5b5c4fffcbfdae4d747595bb33f24fa2174abf8f631610d253977dfed23"
}
```

- Creating account with public key

```
./bcli --servaddr 192.168.52.130:8689 account create --username john --pubkey 04daec4f6b166ea21f5a3c4f8d50ef638ad0312cb01def711ba0ab350c10abeba8a137e5b5c4fffcbfdae4d747595bb33f24fa2174abf8f631610d253977dfed23
```

If you return the following information, account creation is successful.

```
Create account: john Succeed
Trx: 
{
    "version": 1,
    "cursor_num": 1071,
    "cursor_label": 1597958457,
    "lifetime": 1537171186,
    "sender": "bottos",
    "contract": "bottos",
    "method": "newaccount",
    "param": {
        "name": "john",
        "pubkey": "04daec4f6b166ea21f5a3c4f8d50ef638ad0312cb01def711ba0ab350c10abeba8a137e5b5c4fffcbfdae4d747595bb33f24fa2174abf8f631610d253977dfed23"
    },
    "param_bin": "dc0002da00046a6f686eda008230346461656334663662313636656132316635613363346638643530656636333861643033313263623031646566373131626130616233353063313061626562613861313337653562356334666666636266646165346437343735393562623333663234666132313734616266386636333136313064323533393737646665643233",
    "sig_alg": 1,
    "signature": "fe62ac036c193a870ef1667f264b62c6c17c9d09f00958a9f6971931a187bbbf6b5c6129a162765cfcc02b5da23d602bf4e19b84036bb88e58ce29ad38715117"
}
```

- See if accounts create results

```
./bcli --servaddr 192.168.52.130:8689 account get --username john
```

If returns a description, the creation is successful.

```
Account: john
Balance: 0.00000000 BTO
```

- Deploy `wasm` files to the chain

```
./bcli --servaddr 192.168.52.130:8689 contract deploy --name john --code ./testRegUser.wasm -abi testRegUser.abi
```

Note: the contract name here is the account name we created above.

If the following information is returned, the contract is successfully deployed.

```
Deploy contract: john Succeed
Trx: 
{
    "version": 1,
    "cursor_num": 45,
    "cursor_label": 3016045512,
    "lifetime": 1537497253,
    "sender": "john",
    "contract": "bottos",
    "method": "deploycode",
    "param": {
        "name": "john",
        "vm_type": 1,
        "vm_version": 1,
        "contract_code": "0061736d0100000001250660027f7f017f60027f7f0060067f7f7f7f7f7f017f60037f7f7f017f60000060017f017f023c0403656e7608676574506172616d000003656e76066d656d736574000303656e76067072696e7473000103656e760b73657442..."
    },
    "param_bin": "dc0004da00046a6f686ecc01cc01c50ea40061736d0100000001250660027f7f017f60027f7f0060067f7f7f7f7f7f017f60037f7f7f017f60000060017f017f023c0403656e7608676574506172616d000003656e76066d656d736574000303656e7606...",
    "sig_alg": 1,
    "signature": "f2f96610b5ede1975359fd962b447264da4b1fa492869350a2a93540122dfd1d2b10f1bfe722ce484ea054b59e2f8bd7120fa3ce17cc2e0de893997a2dcc18a5"
}
TrxHash: 7d3bea7da59d3a74b2d9625505bd64099efd2a509c20387ff28c924a12619250
signTrx: [183 153 239 97 104 48 205 123 133 153 174 121 88 251 238 86 212 200 22 143 253 84 33 161 96 37 163 152 184 164 190 69]
trx :%!(EXTRA *api.Transaction=version:1 cursor_num:45 cursor_label:3016045512 lifetime:1537497253 sender:"john" contract:"bottos" method:"deployabi" param:"dc0002da00046a6f686ec503867b0a09227479706573223a205b5d2c0a092273747275637473223a205b0a20202020202020202020202020207b0a202020202020202020202020202009226e616d65223a202255736572496e666f222c0a2020202020202020202020202020092262617365223a2022222c0a202020202020202020202020202009226669656c6473223a207b0a2020202020202020202020202020090922757365724e616d65223a2022737472696e67222c0a202020202020202020202020202009092275736572496e666f223a2022737472696e67220a20202020202020202020202020202020202020207d0a2020202020202020202020202020097d2c0a20202020202020202020202020207b0a202020202020202020202020202009226e616d65223a20225573657242617365496e666f222c0a2020202020202020202020202020092262617365223a2022222c0a202020202020202020202020202009226669656c6473223a207b0a202020202020202020202020202009092275736572496e666f223a2022737472696e67220a20202020202020202020202020202020202020207d0a2020202020202020202020202020097d0a202020202020205d2c0a0922616374696f6e73223a205b0a20202020202020202020202020207b0a20202020202020202020202020200922616374696f6e5f6e616d65223a202272656775736572222c0a2020202020202020202020202020092274797065223a202255736572496e666f220a20202020202020202020202020207d0a202020202020205d2c0a09227461626c6573223a205b0a20202020202020202020202020207b0a202020202020202020202020202009227461626c655f6e616d65223a202275736572696e666f222c0a20202020202020202020202020200922696e6465785f74797065223a2022737472696e67222c0a202020202020202020202020202009226b65795f6e616d6573223a20205b0a2020202020202020202020202020090922757365724e616d65220a202020202020202020202020202009205d2c0a202020202020202020202020202009226b65795f7479706573223a20205b0a2020202020202020202020202020090922737472696e67220a202020202020202020202020202009205d2c0a2020202020202020202020202020092274797065223a20225573657242617365496e666f220a20202020202020202020202020207d0a202020202020205d0a7d0a" sig_alg:1 ){
    "errcode": 0,
    "msg": "trx receive succ",
    "result": {
        "trx": {
            "version": 1,
            "cursor_num": 45,
            "cursor_label": 3016045512,
            "lifetime": 1537497253,
            "sender": "john",
            "contract": "bottos",
            "method": "deployabi",
            "param": "dc0002da00046a6f686ec503867b0a09227479706573223a205b5d2c0a092273747275637473223a205b0a20202020202020202020202020207b0a202020202020202020202020202009226e616d65223a202255736572496e666f222c0a2020202020202020202020202020092262617365223a2022222c0a202020202020202020202020202009226669656c6473223a207b0a2020202020202020202020202020090922757365724e616d65223a2022737472696e67222c0a202020202020202020202020202009092275736572496e666f223a2022737472696e67220a20202020202020202020202020202020202020207d0a2020202020202020202020202020097d2c0a20202020202020202020202020207b0a202020202020202020202020202009226e616d65223a20225573657242617365496e666f222c0a2020202020202020202020202020092262617365223a2022222c0a202020202020202020202020202009226669656c6473223a207b0a202020202020202020202020202009092275736572496e666f223a2022737472696e67220a20202020202020202020202020202020202020207d0a2020202020202020202020202020097d0a202020202020205d2c0a0922616374696f6e73223a205b0a20202020202020202020202020207b0a20202020202020202020202020200922616374696f6e5f6e616d65223a202272656775736572222c0a2020202020202020202020202020092274797065223a202255736572496e666f220a20202020202020202020202020207d0a202020202020205d2c0a09227461626c6573223a205b0a20202020202020202020202020207b0a202020202020202020202020202009227461626c655f6e616d65223a202275736572696e666f222c0a20202020202020202020202020200922696e6465785f74797065223a2022737472696e67222c0a202020202020202020202020202009226b65795f6e616d6573223a20205b0a2020202020202020202020202020090922757365724e616d65220a202020202020202020202020202009205d2c0a202020202020202020202020202009226b65795f7479706573223a20205b0a2020202020202020202020202020090922737472696e67220a202020202020202020202020202009205d2c0a2020202020202020202020202020092274797065223a20225573657242617365496e666f220a20202020202020202020202020207d0a202020202020205d0a7d0a",
            "sig_alg": 1,
            "signature": "7d7ab2051ac3e2c419614849e036678e996a65999be556d5259087ff930c1c1a716d529c7062371e57a0fd44894247b8e183b6cb1273dc517d8f5d8e64eaf8c5"
        },
        "trx_hash": "bfbeed13120730d77a9c3ea8aa0bb1f6bc8b4df78dc8fd306581ca8f59853617"
    }
}
```