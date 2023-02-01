---
layout: post
title: Metahub Protocol
categories: test
description: Metahub 协议的初次尝试
keywords: Cryprto,protocol,web3,Test
---
# Metahub Protocol
>好早就接触到这个Metahub这个项目，但是一直没有太深入的去研究过，正好明天余冬良老师还在上海，今晚走一遍流程了解下，明天向他请教应该能有更加深入的认知！！！！

## 准备步骤
### 1. 目前Metahub是跑在goerli测试网上,所以要先领取代币。   
网址： `https://goerlifaucet.com/`

### 2. 通过safe创建测试账号：  
 `https://gnosis-safe.io/`(app/welcome)   

![test1](/images/test/2023.02.02/301c444505905b0d46a017dc291cb51.png)  
<font size=2 color=orange>Tips:请检查一步url是否是gnosis-safe.io，我因为这个没注意后面抓耳挠腮好久。(~这个色儿应该明显点~)
</font>  
* 点击 `Create new Safe` 创建一个新的多签钱包。  

![test2](/images/test/2023.02.02/b47b3b33115bad2d8b09755693ecafa.png)
* 输入多签账号名字 点击 `Continue`  
* 输入多签人 `Owner Name`  点击 `Continue`


## 开始正题！！GOGOGOGO  
![test3](/images/test/2023.02.02/230aa3da72c9a838ddba59f0aff8f05.png)  
<font size=2 color=orange>Tips:后续合约的交互都是通过这里进行两步操作！(~显眼显眼~)    
</font>  

*  先点击 `New Transition`  ，在点击 `Contract interaction`。
 
### 3. 通过USDT合约的mint接口领取测试支付代币USDT。   
 USDT测试合约： `0x63B702e9C5B05ceA963962fb4fE8B2B72d731F2d` 。  

 ![test4](/images/test/2023.02.02/7bbf0b044bcff7e402bdc7bd209c18a.png)    
 把USDT的合约地址复制到 `Contract address`中，下方接口选择 `mint`。  

 ### 4. 将USDT授权给Pass合约，用于铸造Pass NFT扣款（授权数量+6个0）。  
 pass合约： `0x98A9325419cA136a454a8fF12Ac1D3a088062bfC` 。 
 ![test5](/images/test/2023.02.02/e1a17873b917ef66108dfb12c2db884.png)
 * 重复上面的合约交互动作
 * 分别将图上的地址复制进去，接口选择approve，授权数量+6个0，点击 `Review` 。  
 
 ### 5. 通过Pass合约mint接口，给将要铸造PassNFT取名，是该Pass发布的社区名称。

<details>  
<summary>点我点我</summary>
<pre><code>
         [
            {
              "inputs": [
                {
                  "internalType": "string",
                  "name": "name_",
                  "type": "string"
                },
                {
                  "internalType": "string",
                  "name": "symbol_",
                  "type": "string"
                },
                {
                  "internalType": "uint256",
                  "name": "minDelay",
                  "type": "uint256"
                },
                {
                  "internalType": "contract IIdentityHub",
                  "name": "identityHub_",
                  "type": "address"
                },
                {
                  "internalType": "address",
                  "name": "safe_",
                  "type": "address"
                },
                {
                  "internalType": "address",
                  "name": "currency_",
                  "type": "address"
                },
                {
                  "internalType": "address",
                  "name": "metahubCoin_",
                  "type": "address"
                },
                {
                  "internalType": "address",
                  "name": "LPTreasury_",
                  "type": "address"
                },
                {
                  "internalType": "address",
                  "name": "alchemistTreasury_",
                  "type": "address"
                },
                {
                  "internalType": "address",
                  "name": "XTreasury_",
                  "type": "address"
                }
              ],
              "stateMutability": "nonpayable",
              "type": "constructor"
            },
            {
              "inputs": [],
              "name": "NotOwnerOrApproved",
              "type": "error"
            },
            {
              "inputs": [],
              "name": "SignatureExpired",
              "type": "error"
            },
            {
              "inputs": [],
              "name": "SignatureInvalid",
              "type": "error"
            },
            {
              "inputs": [],
              "name": "TokenTransferWhilePaused",
              "type": "error"
            },
            {
              "inputs": [],
              "name": "ZeroSpender",
              "type": "error"
            },
            {
              "anonymous": false,
              "inputs": [
                {
                  "indexed": true,
                  "internalType": "address",
                  "name": "owner",
                  "type": "address"
                },
                {
                  "indexed": true,
                  "internalType": "address",
                  "name": "approved",
                  "type": "address"
                },
                {
                  "indexed": true,
                  "internalType": "uint256",
                  "name": "tokenId",
                  "type": "uint256"
                }
              ],
              "name": "Approval",
              "type": "event"
            },
            {
              "anonymous": false,
              "inputs": [
                {
                  "indexed": true,
                  "internalType": "address",
                  "name": "owner",
                  "type": "address"
                },
                {
                  "indexed": true,
                  "internalType": "address",
                  "name": "operator",
                  "type": "address"
                },
                {
                  "indexed": false,
                  "internalType": "bool",
                  "name": "approved",
                  "type": "bool"
                }
              ],
              "name": "ApprovalForAll",
              "type": "event"
            },
            {
              "anonymous": false,
              "inputs": [
                {
                  "indexed": false,
                  "internalType": "address",
                  "name": "account",
                  "type": "address"
                }
              ],
              "name": "Paused",
              "type": "event"
            },
            {
              "anonymous": false,
              "inputs": [
                {
                  "indexed": true,
                  "internalType": "bytes32",
                  "name": "role",
                  "type": "bytes32"
                },
                {
                  "indexed": true,
                  "internalType": "bytes32",
                  "name": "previousAdminRole",
                  "type": "bytes32"
                },
                {
                  "indexed": true,
                  "internalType": "bytes32",
                  "name": "newAdminRole",
                  "type": "bytes32"
                }
              ],
              "name": "RoleAdminChanged",
              "type": "event"
            },
            {
              "anonymous": false,
              "inputs": [
                {
                  "indexed": true,
                  "internalType": "bytes32",
                  "name": "role",
                  "type": "bytes32"
                },
                {
                  "indexed": true,
                  "internalType": "address",
                  "name": "account",
                  "type": "address"
                },
                {
                  "indexed": true,
                  "internalType": "address",
                  "name": "sender",
                  "type": "address"
                }
              ],
              "name": "RoleGranted",
              "type": "event"
            },
            {
              "anonymous": false,
              "inputs": [
                {
                  "indexed": true,
                  "internalType": "bytes32",
                  "name": "role",
                  "type": "bytes32"
                },
                {
                  "indexed": true,
                  "internalType": "address",
                  "name": "account",
                  "type": "address"
                },
                {
                  "indexed": true,
                  "internalType": "address",
                  "name": "sender",
                  "type": "address"
                }
              ],
              "name": "RoleRevoked",
              "type": "event"
            },
            {
              "anonymous": false,
              "inputs": [
                {
                  "indexed": true,
                  "internalType": "address",
                  "name": "from",
                  "type": "address"
                },
                {
                  "indexed": true,
                  "internalType": "address",
                  "name": "to",
                  "type": "address"
                },
                {
                  "indexed": true,
                  "internalType": "uint256",
                  "name": "tokenId",
                  "type": "uint256"
                }
              ],
              "name": "Transfer",
              "type": "event"
            },
            {
              "anonymous": false,
              "inputs": [
                {
                  "indexed": false,
                  "internalType": "address",
                  "name": "account",
                  "type": "address"
                }
              ],
              "name": "Unpaused",
              "type": "event"
            },
            {
              "inputs": [],
              "name": "DEFAULT_ADMIN_ROLE",
              "outputs": [
                {
                  "internalType": "bytes32",
                  "name": "",
                  "type": "bytes32"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "address",
                  "name": "to",
                  "type": "address"
                },
                {
                  "internalType": "uint256",
                  "name": "tokenId",
                  "type": "uint256"
                }
              ],
              "name": "approve",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "address",
                  "name": "owner",
                  "type": "address"
                }
              ],
              "name": "balanceOf",
              "outputs": [
                {
                  "internalType": "uint256",
                  "name": "",
                  "type": "uint256"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "uint256",
                  "name": "tokenId",
                  "type": "uint256"
                }
              ],
              "name": "bindTaxTokenId",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "uint256",
                  "name": "tokenId",
                  "type": "uint256"
                }
              ],
              "name": "burn",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "uint256",
                  "name": "tokenId",
                  "type": "uint256"
                },
                {
                  "components": [
                    {
                      "internalType": "uint8",
                      "name": "v",
                      "type": "uint8"
                    },
                    {
                      "internalType": "bytes32",
                      "name": "r",
                      "type": "bytes32"
                    },
                    {
                      "internalType": "bytes32",
                      "name": "s",
                      "type": "bytes32"
                    },
                    {
                      "internalType": "uint256",
                      "name": "deadline",
                      "type": "uint256"
                    }
                  ],
                  "internalType": "struct DataTypes.EIP712Signature",
                  "name": "sig",
                  "type": "tuple"
                }
              ],
              "name": "burnWithSig",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "cap",
              "outputs": [
                {
                  "internalType": "uint16",
                  "name": "",
                  "type": "uint16"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "currency",
              "outputs": [
                {
                  "internalType": "address",
                  "name": "",
                  "type": "address"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "uint256",
                  "name": "tokenId",
                  "type": "uint256"
                }
              ],
              "name": "getApproved",
              "outputs": [
                {
                  "internalType": "address",
                  "name": "",
                  "type": "address"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "getDomainSeparator",
              "outputs": [
                {
                  "internalType": "bytes32",
                  "name": "",
                  "type": "bytes32"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "bytes32",
                  "name": "role",
                  "type": "bytes32"
                }
              ],
              "name": "getRoleAdmin",
              "outputs": [
                {
                  "internalType": "bytes32",
                  "name": "",
                  "type": "bytes32"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "bytes32",
                  "name": "role",
                  "type": "bytes32"
                },
                {
                  "internalType": "uint256",
                  "name": "index",
                  "type": "uint256"
                }
              ],
              "name": "getRoleMember",
              "outputs": [
                {
                  "internalType": "address",
                  "name": "",
                  "type": "address"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "bytes32",
                  "name": "role",
                  "type": "bytes32"
                }
              ],
              "name": "getRoleMemberCount",
              "outputs": [
                {
                  "internalType": "uint256",
                  "name": "",
                  "type": "uint256"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "int256",
                  "name": "sold",
                  "type": "int256"
                }
              ],
              "name": "getTargetSaleTime",
              "outputs": [
                {
                  "internalType": "int256",
                  "name": "",
                  "type": "int256"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "int256",
                  "name": "timeSinceStart",
                  "type": "int256"
                },
                {
                  "internalType": "uint256",
                  "name": "sold",
                  "type": "uint256"
                }
              ],
              "name": "getVRGDAPrice",
              "outputs": [
                {
                  "internalType": "uint256",
                  "name": "",
                  "type": "uint256"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "bytes32",
                  "name": "role",
                  "type": "bytes32"
                },
                {
                  "internalType": "address",
                  "name": "account",
                  "type": "address"
                }
              ],
              "name": "grantRole",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "bytes32",
                  "name": "role",
                  "type": "bytes32"
                },
                {
                  "internalType": "address",
                  "name": "account",
                  "type": "address"
                }
              ],
              "name": "hasRole",
              "outputs": [
                {
                  "internalType": "bool",
                  "name": "",
                  "type": "bool"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "identityHub",
              "outputs": [
                {
                  "internalType": "contract IIdentityHub",
                  "name": "",
                  "type": "address"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "address",
                  "name": "owner",
                  "type": "address"
                },
                {
                  "internalType": "address",
                  "name": "operator",
                  "type": "address"
                }
              ],
              "name": "isApprovedForAll",
              "outputs": [
                {
                  "internalType": "bool",
                  "name": "",
                  "type": "bool"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "string",
                  "name": "name_",
                  "type": "string"
                }
              ],
              "name": "mint",
              "outputs": [
                {
                  "internalType": "uint256",
                  "name": "id",
                  "type": "uint256"
                }
              ],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "mintMetaHubCoin",
              "outputs": [
                {
                  "internalType": "contract IMint",
                  "name": "metahubCoin",
                  "type": "address"
                },
                {
                  "internalType": "address",
                  "name": "LPTreasury",
                  "type": "address"
                },
                {
                  "internalType": "address",
                  "name": "alchemistTreasury",
                  "type": "address"
                },
                {
                  "internalType": "address",
                  "name": "XTreasury",
                  "type": "address"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "uint256",
                  "name": "tokenId_",
                  "type": "uint256"
                }
              ],
              "name": "name",
              "outputs": [
                {
                  "internalType": "string",
                  "name": "output",
                  "type": "string"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "name",
              "outputs": [
                {
                  "internalType": "string",
                  "name": "",
                  "type": "string"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "uint256",
                  "name": "tokenId",
                  "type": "uint256"
                }
              ],
              "name": "ownerOf",
              "outputs": [
                {
                  "internalType": "address",
                  "name": "",
                  "type": "address"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "pause",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "paused",
              "outputs": [
                {
                  "internalType": "bool",
                  "name": "",
                  "type": "bool"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "address",
                  "name": "spender",
                  "type": "address"
                },
                {
                  "internalType": "uint256",
                  "name": "tokenId",
                  "type": "uint256"
                },
                {
                  "components": [
                    {
                      "internalType": "uint8",
                      "name": "v",
                      "type": "uint8"
                    },
                    {
                      "internalType": "bytes32",
                      "name": "r",
                      "type": "bytes32"
                    },
                    {
                      "internalType": "bytes32",
                      "name": "s",
                      "type": "bytes32"
                    },
                    {
                      "internalType": "uint256",
                      "name": "deadline",
                      "type": "uint256"
                    }
                  ],
                  "internalType": "struct DataTypes.EIP712Signature",
                  "name": "sig",
                  "type": "tuple"
                }
              ],
              "name": "permit",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "address",
                  "name": "owner",
                  "type": "address"
                },
                {
                  "internalType": "address",
                  "name": "operator",
                  "type": "address"
                },
                {
                  "internalType": "bool",
                  "name": "approved",
                  "type": "bool"
                },
                {
                  "components": [
                    {
                      "internalType": "uint8",
                      "name": "v",
                      "type": "uint8"
                    },
                    {
                      "internalType": "bytes32",
                      "name": "r",
                      "type": "bytes32"
                    },
                    {
                      "internalType": "bytes32",
                      "name": "s",
                      "type": "bytes32"
                    },
                    {
                      "internalType": "uint256",
                      "name": "deadline",
                      "type": "uint256"
                    }
                  ],
                  "internalType": "struct DataTypes.EIP712Signature",
                  "name": "sig",
                  "type": "tuple"
                }
              ],
              "name": "permitForAll",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "bytes32",
                  "name": "role",
                  "type": "bytes32"
                },
                {
                  "internalType": "address",
                  "name": "account",
                  "type": "address"
                }
              ],
              "name": "renounceRole",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "bytes32",
                  "name": "role",
                  "type": "bytes32"
                },
                {
                  "internalType": "address",
                  "name": "account",
                  "type": "address"
                }
              ],
              "name": "revokeRole",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "safe",
              "outputs": [
                {
                  "internalType": "address",
                  "name": "",
                  "type": "address"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "address",
                  "name": "from",
                  "type": "address"
                },
                {
                  "internalType": "address",
                  "name": "to",
                  "type": "address"
                },
                {
                  "internalType": "uint256",
                  "name": "tokenId",
                  "type": "uint256"
                }
              ],
              "name": "safeTransferFrom",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "address",
                  "name": "from",
                  "type": "address"
                },
                {
                  "internalType": "address",
                  "name": "to",
                  "type": "address"
                },
                {
                  "internalType": "uint256",
                  "name": "tokenId",
                  "type": "uint256"
                },
                {
                  "internalType": "bytes",
                  "name": "data",
                  "type": "bytes"
                }
              ],
              "name": "safeTransferFrom",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "address",
                  "name": "operator",
                  "type": "address"
                },
                {
                  "internalType": "bool",
                  "name": "approved",
                  "type": "bool"
                }
              ],
              "name": "setApprovalForAll",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "contract ITaxHubBase",
                  "name": "newTaxHub",
                  "type": "address"
                }
              ],
              "name": "setTaxHub",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "contract ITokenURIHubRender",
                  "name": "newTokenURIHub",
                  "type": "address"
                }
              ],
              "name": "setTokenURIHub",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "address",
                  "name": "",
                  "type": "address"
                }
              ],
              "name": "sigNonces",
              "outputs": [
                {
                  "internalType": "uint256",
                  "name": "",
                  "type": "uint256"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "startTime",
              "outputs": [
                {
                  "internalType": "uint256",
                  "name": "",
                  "type": "uint256"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "bytes4",
                  "name": "interfaceId",
                  "type": "bytes4"
                }
              ],
              "name": "supportsInterface",
              "outputs": [
                {
                  "internalType": "bool",
                  "name": "",
                  "type": "bool"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "symbol",
              "outputs": [
                {
                  "internalType": "string",
                  "name": "",
                  "type": "string"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "targetPrice",
              "outputs": [
                {
                  "internalType": "int256",
                  "name": "",
                  "type": "int256"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "taxHub",
              "outputs": [
                {
                  "internalType": "contract ITaxHubBase",
                  "name": "",
                  "type": "address"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "taxTokenId",
              "outputs": [
                {
                  "internalType": "uint256",
                  "name": "",
                  "type": "uint256"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "timelock",
              "outputs": [
                {
                  "internalType": "contract TimelockController",
                  "name": "",
                  "type": "address"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "uint256",
                  "name": "index",
                  "type": "uint256"
                }
              ],
              "name": "tokenByIndex",
              "outputs": [
                {
                  "internalType": "uint256",
                  "name": "",
                  "type": "uint256"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "bytes32",
                  "name": "nameBytes32",
                  "type": "bytes32"
                }
              ],
              "name": "tokenIdByNameBytes32",
              "outputs": [
                {
                  "internalType": "uint256",
                  "name": "",
                  "type": "uint256"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "string",
                  "name": "name_",
                  "type": "string"
                }
              ],
              "name": "tokenIdOf",
              "outputs": [
                {
                  "internalType": "uint256",
                  "name": "",
                  "type": "uint256"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "address",
                  "name": "owner",
                  "type": "address"
                },
                {
                  "internalType": "uint256",
                  "name": "index",
                  "type": "uint256"
                }
              ],
              "name": "tokenOfOwnerByIndex",
              "outputs": [
                {
                  "internalType": "uint256",
                  "name": "",
                  "type": "uint256"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "uint256",
                  "name": "tokenId",
                  "type": "uint256"
                }
              ],
              "name": "tokenURI",
              "outputs": [
                {
                  "internalType": "string",
                  "name": "output",
                  "type": "string"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "string",
                  "name": "name_",
                  "type": "string"
                }
              ],
              "name": "tokenURIByName",
              "outputs": [
                {
                  "internalType": "string",
                  "name": "output",
                  "type": "string"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "tokenURIHub",
              "outputs": [
                {
                  "internalType": "contract ITokenURIHubRender",
                  "name": "",
                  "type": "address"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "totalSupply",
              "outputs": [
                {
                  "internalType": "uint256",
                  "name": "",
                  "type": "uint256"
                }
              ],
              "stateMutability": "view",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "address",
                  "name": "from",
                  "type": "address"
                },
                {
                  "internalType": "address",
                  "name": "to",
                  "type": "address"
                },
                {
                  "internalType": "uint256",
                  "name": "tokenId",
                  "type": "uint256"
                }
              ],
              "name": "transferFrom",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [
                {
                  "internalType": "bytes32",
                  "name": "role",
                  "type": "bytes32"
                },
                {
                  "internalType": "bytes32",
                  "name": "adminRole",
                  "type": "bytes32"
                }
              ],
              "name": "transferRoleAdmin",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            },
            {
              "inputs": [],
              "name": "unpause",
              "outputs": [],
              "stateMutability": "nonpayable",
              "type": "function"
            }
          ]
</code></pre>
</details>  

<font size=2 color=orange>Tips:内容很长请点击展开全部复制！(~完事记得关上太长了~)    
</font>  

![test4](/images/test/2023.02.02/348e72adf39397ce050096aa470f4dc.png)   
* 复制上面pass合约的地址
* 复制下拉框中全部的代码，放入 `ABI` 中
* 选择 `mint` 接口
* 给社区取名字（域名的顶级域名称表示）  
### 6.查询Pass NFT的TokenID。
---
困了 明天再继续
