# MemeChain JSON-RPC API Documentation

## Overview
This document provides a comprehensive reference for MemeChain's JSON-RPC API interface, detailing methods for interacting with blockchain data and transaction processing. The API follows JSON-RPC 2.0 specifications and supports core blockchain operations including:

* Transaction lifecycle management
* Block data retrieval
* Address/account operations
* Smart contract interactions
* Staking and investment mechanisms
* Vote assets
* Lock and unlock assets
* Network/node information queries

## Query class interface

### GetTransactionByHash

**Description**：

Get transaction information based on the transaction's hash

**Request**：

* id :Unique request identifier
* jsonRpc :  JSON-RPC version
* method Name of the called method of the called method
* params : Parameters:
  * txHash : Transaction hash

**Response**：

* Opaque request identifier
* jsonRpc  JSON-RPC version
* result 
  * code Return Status code
    * 0	    Success
    * -1    Transaction hash error
    * -2    Failed to parse transaction body
  * message Human-readable status description
  * tx transaction details (see transaction information description for details)

example

```json
//req
{
  "id":"1",
  "jsonRpc":"2.0",
  "params":{"txHash":"bfc73f1c66c7c552cbdb3d02cc1c434b1efaf35fd3916350b5d8a38f92c96fc7"}
}
//ack
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetTransactionByHash",
  "result": {
    "code": 0,
    "message": "success",
    "tx": {
      "consensus": 7,
      "gasTx": 0,
      "type": "Tx",
      "data": {
        "txInfo": {
          "lockAmount": 100000000000,
          "lockType": "lockNet"
        }
      },
      "identity": "0x85240c8dF5011d5967FA4566D3e2Ad5575A51856",
      "info": "",
      "time": 1724827704568873,
      "txHash": "0xbfc73f1c66c7c552cbdb3d02cc1c434b1efaf35fd3916350b5d8a38f92c96fc7",
      "txType": 9,
      "utxo": [
        {
          "assetType": "X",
          "gasUtxo": 0,
          "multiSigns": [
            {
              "pub": "xIVI+gfNGHAVrISn879D49+XV3HKT8kaHk7VnlAilvuQF67GYAeXqEoLapIjP0TBTcpsDHmZTqQUzjXVnJu0BQ==",
              "sign": "xIVI+gfNGHAVrISn879D49+XV3HKT8kaHk7VnlAilvuQF67GYAeXqEoLapIjP0TBTcpsDHmZTqQUzjXVnJu0BQ=="
            }
          ],
          "owner": [
            "0xffFd42e045737b11570B7981c2648ea532a10B23"
          ],
          "vin": {
            "preVout": {
              "hash": [
                "0x36b19c533a49ec05a06be9c99c4e1c2e1609f9679aa75989c8ae0999ca63562a"
              ]
            },
            "vinSigns": [
              {
                "pub": "MCowBQYDK2VwAyEAnVwyI7Xwk4lVNwi4j7ogCoHyy40isQmMumbM58JKTTU=",
                "sign": "jXugdh1gM05AT73xU5WYP6THqX7ghdi4heKe04XjdsJQ/QhR6DxwkA5SLUO//lFswiiWFMf6gf697uVewJ4MAw=="
              }
            ]
          },
          "vout": [
            {
              "addr": "lockVirtualStake",
              "value": 100000000000
            },
            {
              "addr": "0xffFd42e045737b11570B7981c2648ea532a10B23",
              "value": 9759599999665600
            },
            {
              "addr": "VirtualBurnGas",
              "value": 26100
            }
          ]
        }
      ],
      "verifySigns": [
        {
          "pub": "MCowBQYDK2VwAyEACE2DupNwSIpn854yGLj7QF/YHd6eAeLOhHYObzcbCTM=",
          "sign": "NTJntLI0ILj7hPFP1n5xmRj1eAOUKxEqec8cXLxGjjhJ74r8Qqn7fIwIsDbuQI8BGCD/D1Ikp9muLq/1eMACCw==",
          "addr": "0x85240c8dF5011d5967FA4566D3e2Ad5575A51856"
        }
      ]
    }
  }
}
```

### GetBlockByTransactionHash

**Description**：

Retrieve block information associated with a specific transaction hash.

**Request**：

* id          Unique request identifier
* jsonRpc     JSON-RPC version
* params      Parameters:
  * txHash    Transaction hash

**Response**：

* id          Unique request identifier
* jsonRpc     JSON-RPC version
* method      Name of the called method of the called method
* result      Return information
  * code      Return value number
    * 0	      Success
    * -1      Tx hash error
    * -2      Block hash error
    * -3      Block invert error
  * message   Human-readable status message
  * blockInfo Block information (see Block information description for details)

example

```json
//req
{
  "id":"1",
  "jsonRpc":"2.0",
  "params":{"txHash":"0x4505234713387c489827cc38a4209221bfe01fe65d688830b2f4f1871951b6e4"}
}
//ack
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetBlockByTransactionHash",
  "result": {
    "blockInfo": {
      "block": {
        "blockSigns": [
          {
            "pub": "MCowBQYDK2VwAyEAyxQqn3qeeAnatwu4h6I67eponm6VIdgAq8e9E/ttMso=",
            "sign": "xTmjJ3Eg+D5vqQmoh45tSqXKkQKzWsf5viXngTn16YMt18zhTsvFSzxHSpdxG1ghy6W39vT3PaiDjhOay/8NBA==",
            "addr": "0x35c89d9d466efd46A22E4e14ffB7f257278936a4"
          },
          {
            "pub": "MCowBQYDK2VwAyEAkqKb/VZksy3W+yTrX1br/7XxyEfUT8NxqtNkgWbElW0=",
            "sign": "ycNo4/cbDzN6N/yAMhqfuryLAkQ1Nt7oxGFdUabD7yUtXoEYoE7BetrsNpteFoyQH+Ojb2FrgsPMQfxhiTfDBw==",
            "addr": "0xf1a3c06f94a5Ee892a30d3Bfd66Af9A956fAbFD6"
          },
          {
            "pub": "MCowBQYDK2VwAyEA9Nb6YjtFFvxCXpqvtKsACleUe1/uV8scNE5k/tsgvhQ=",
            "sign": "vLpBEcidJPIJG73uRWK2Lcj58fsqlmgn+0p87pda+za6Vk45sn9tjiLzLKJrMs4rwWIQ9fkVjQWD53hji8EPDw==",
            "addr": "0x9afDc8688CDd18C17e8183263300d121f9deEB7D"
          },
          {
            "pub": "MCowBQYDK2VwAyEAWoIv4oyj1KvKTNSwc7y3nYBgnHzUEvXoTtV6/Ajuk9M=",
            "sign": "6KiQerwod6LD0q2/vWb8hWt6b1BWYLbrlz/wHgi9yGqixjWKtsoqkbe5lwdR5yHoualrahWuK7aFH8U0tSveAg==",
            "addr": "0x73eE2Fc25e8f9Fc0297B71B527352c2fA788f1b3"
          },
          {
            "pub": "MCowBQYDK2VwAyEAGQz8jDoEorTdZ6fQDuqCGqEqLZQpkZYzfBTa9y1+H/4=",
            "sign": "2V03ve+GbMjnSuREd4Uc5uF5ucQO1CNuIt8l8TMnl0sXMxsjFlxUQfmTJkflIgGe447Y6VV1Y/+qLadFx83MAA==",
            "addr": "0x5e8cd8c67783f70322B1b4ACbB0059808053C8d2"
          },
          {
            "pub": "MCowBQYDK2VwAyEAxC4xdTxCxU0pIiHRmu/ikDwPnS4TMmwRQbq88cT9Xpw=",
            "sign": "iW0rxmyuDem/o5dE2MnDXL9KxviprzP/ncjnTCkOSDeK3gY7g4+fCmnAcMgKE3lii+mman0a4Dg6NDfn1NocBg==",
            "addr": "0xC55A0d261bd7F2cDfaBba2a0e785Bf11eF1DC3B7"
          },
          {
            "pub": "MCowBQYDK2VwAyEAfWXv+y1GhWJXMYnxZV+0sD7GwANNQ7KRbxTjzzdskwU=",
            "sign": "sUInzXJlLuybtgzwAlTiRxJuf2HLMcEdiiGNBEb4SjFF8pSumJQQujG8pQpiwelppPtC9WfL1hVlpiLDKT+eAQ==",
            "addr": "0x04dc129B0Bb3F9B2ad2eD97407109DDF75a91EEb"
          }
        ],
        "bytes": 2034,
        "data": null,
        "hash": "0x34e49bf1e7ea404cbfce4c462f492d0965d8b92d815c21d3f58e29cc7e548438",
        "height": 5,
        "merkleRoot": "0x4505234713387c489827cc38a4209221bfe01fe65d688830b2f4f1871951b6e4",
        "prevHash": "0xbbb2bc3e5f11af6067a40cb99558b4346b4a5420b10b796e346de23744a71ca7",
        "time": 1726287221171952
      },
      "tx": [
        {
          "consensus": 7,
          "gasTx": 0,
          "type": "Tx",
          "identity": "0x35c89d9d466efd46A22E4e14ffB7f257278936a4",
          "info": "",
          "time": 1726287221171952,
          "txHash": "0x4505234713387c489827cc38a4209221bfe01fe65d688830b2f4f1871951b6e4",
          "txType": 1,
          "utxo": [
            {
              "assetType": "0x416ba3e59614072c3bbdfb4f194fe71d248a7d82b1727f2d4ca51f8b4aba1528",
              "gasUtxo": 0,
              "multiSigns": [
                {
                  "pub": "DO8FihR8vOTWxUjEG3LHcTkcFnZFyd/mWv/QX7cjIYGUF1MqCNQc8WIOmdu2VmiN4gRF9cQcARtq0QPDz8MGDQ==",
                  "sign": "DO8FihR8vOTWxUjEG3LHcTkcFnZFyd/mWv/QX7cjIYGUF1MqCNQc8WIOmdu2VmiN4gRF9cQcARtq0QPDz8MGDQ=="
                }
              ],
              "owner": [
                "0xffFd42e045737b11570B7981c2648ea532a10B23"
              ],
              "vin": {
                "preVout": {
                  "hash": [
                    "0xc87ebdb92895a2a3a81d10a2c5c64371b1f1ebc33da5d861d4efbfa7f35d4320"
                  ]
                },
                "vinSigns": [
                  {
                    "pub": "MCowBQYDK2VwAyEAnVwyI7Xwk4lVNwi4j7ogCoHyy40isQmMumbM58JKTTU=",
                    "sign": "IK0eU9QAdGKX1rVCzPuCoI83iTz7M+laAE7D6UAvSqLd0r8GLNqN+56QEkQsEfA8OQ7ONokhmAi+wkF5lioqDQ=="
                  }
                ]
              },
              "vout": [
                {
                  "addr": "0xc5CAf882D5B49F2b2b9D31400D4726E61BC8fBAB",
                  "value": 2000000000000
                },
                {
                  "addr": "0xc5b22F90279130e954bC1CbdFDf3772E8C2C0df0",
                  "value": 2000000000000
                },
                {
                  "addr": "0xc8bbA532f295EA2Ed02B4B51405F9129c17B5CB2",
                  "value": 2000000000000
                },
                {
                  "addr": "0xc9152625Abefeff3cf1211249d85Bae1744B68e5",
                  "value": 2000000000000
                },
                {
                  "addr": "0xd55b75566DEaD988205B01757938B2c985E2e335",
                  "value": 2000000000000
                },
                {
                  "addr": "0xda6DD96003bc6B8770857967de324Bc3b37C7506",
                  "value": 2000000000000
                },
                {
                  "addr": "0xf1a3c06f94a5Ee892a30d3Bfd66Af9A956fAbFD6",
                  "value": 2000000000000
                },
                {
                  "addr": "0xffFd42e045737b11570B7981c2648ea532a10B23",
                  "value": 9985999999959400
                },
                {
                  "addr": "VirtualBurnGas",
                  "value": 40600
                }
              ]
            }
          ],
          "verifySigns": [
            {
              "pub": "MCowBQYDK2VwAyEAyxQqn3qeeAnatwu4h6I67eponm6VIdgAq8e9E/ttMso=",
              "sign": "36ZEG2kZZ5wkTCzHq+oCJBIrkJYUt909ShKZILG24y5F256OX8nlk5AVi5Dn+7Vvm97CQkmDLVdEKyQksxq7BQ==",
              "addr": "0x35c89d9d466efd46A22E4e14ffB7f257278936a4"
            }
          ]
        }
      ]
    },
    "code": 0,
    "message": "success"
  }
}
```



### GetBlockByHash

**Description**：

Get block information based on block hash

**Request**：

* id          Unique request identifier
* jsonRpc     JSON-RPC version
* params      Parameters:
  * blockHash Block hash

**Response**：

* id            Unique request identifier
* jsonRpc       JSON-RPC version
* method        Name of the called method of the called method
* result        Return information
  * code        Return value number
    * 0	        Success
    * -1        Block hash error
  * message     Human-readable status message
  * blockInfo   Block information (see Block information description for details)

example

```json
//req
{
  "id":"1",
  "jsonRpc":"2.0",
  "params":{"blockHash":"0xb51f9199b387ce0b45c847c85f86fa3db3eb5e15b50b4a267dd9f582cd4bc256"}
}
//ack
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetBlockByHash",
  "result": {
    "blockInfo": {
      "block": {
        "blockSigns": [
          {
            "pub": "MCowBQYDK2VwAyEACE2DupNwSIpn854yGLj7QF/YHd6eAeLOhHYObzcbCTM=",
            "sign": "oKx5qKFORpeQ5XyrbR6bzPQyUFyB2W7iW9kVZ7QkFUK6KYpb+1Hc4asO8ra63C572FhXpBMvda5aF74TjA1ECg==",
            "addr": "0x85240c8dF5011d5967FA4566D3e2Ad5575A51856"
          },
          {
            "pub": "MCowBQYDK2VwAyEA8jzU4KuMjBgESW8u9aX5coT+KtfpcGWwAoRixNrjem4=",
            "sign": "y3RwfXf1OVzH3GJkIicRhdAev6N8NxSVniMf6/hLQ25TUBkBezig0Q8/IWVR8DWbfg2HqPCw0DpaIA4BHmJpDw==",
            "addr": "0x9Ed0009A37D251706c4f14a85f755eabaCE99Ae9"
          },
          {
            "pub": "MCowBQYDK2VwAyEAfuNxn5WIsxqDXkc57Vl2ZFsbAv50UEKMkzeP2Po1udU=",
            "sign": "BSx8AoB99luZEMPQtsVWDCBgo1JsxHh4cw1cVf91OBITpJWLHos7iYKZ2PTp1ZFbtF+98s1mrDq8UtH4E30pCA==",
            "addr": "0xd27384462Bfe9d37c8e27b732c2aBbcA99B2026f"
          },
          {
            "pub": "MCowBQYDK2VwAyEAIyogP9HbFhQLJPXWTJvr7oacfOj7V7jbwr+tWuLUpeo=",
            "sign": "oZSfjyABTAmYMs8JDeH9BGcsxQ3ih9VnDSgyj4LTYIWw+wtoQS6lWW01Hh4r3E3NCicwGaYHeOtVa0S65Kr6AQ==",
            "addr": "0x066F1A3f2E6C25a21B1a8B342E8CEA91Df585835"
          },
          {
            "pub": "MCowBQYDK2VwAyEAKblncGE2av+phdWRpUGHta3wagpb+xMdnZ3HBy1sTsM=",
            "sign": "hHw9F2rO+LwXRYsLOUk4MAidRp0esVEU+iRuOSIjvods6Df37yscTOmqj5xsTPB2FBbT2jknObpceaUrdRv+Aw==",
            "addr": "0x3aeeFE155376a47E63bB93fE4e95e67aF42B68eC"
          },
          {
            "pub": "MCowBQYDK2VwAyEANI0XsAkIjo1T9QSBucwrNMklWOohtZccqub4OWUNrWU=",
            "sign": "g0+kMIf5ekUL4imH/A0XeOLQxHoQuVzRVfoBSotNlYx1KgcARhUNVXx7ysxrh27lif1wTG0RwCNliISFEsJfAA==",
            "addr": "0x5F4c7cFD9B2095c947B9be84F6A57D08e44eF791"
          },
          {
            "pub": "MCowBQYDK2VwAyEAbALWvBTB+PQv2StB5NEYON6WVj1eYwHxGfI0G/UFFmk=",
            "sign": "zcw8ob5dNOBV8InDEe1xkcJc5CnxZJYEwBNfHsbFUYi7/RYhmA4AO8SwFRAavc6i36TEJ3FhkKAERSwK8C+mCQ==",
            "addr": "0x277Ff39E8176A582A392265ca619bdb6477674a5"
          }
        ],
        "bytes": 1765,
        "data": null,
        "hash": "0xb51f9199b387ce0b45c847c85f86fa3db3eb5e15b50b4a267dd9f582cd4bc256",
        "height": 65,
        "merkleRoot": "0xbfc73f1c66c7c552cbdb3d02cc1c434b1efaf35fd3916350b5d8a38f92c96fc7",
        "prevHash": "0xb03385ae8fce992887c56f38966636a7e31cc273b599a2e4197a31878a7fcaf5",
        "time": 1724827704568873
      },
      "tx": [
        {
          "consensus": 7,
          "gasTx": 0,
          "type": "Tx",
          "data": {
            "txInfo": {
              "lockAmount": 100000000000,
              "lockType": "lockNet"
            }
          },
          "identity": "0x85240c8dF5011d5967FA4566D3e2Ad5575A51856",
          "info": "",
          "time": 1724827704568873,
          "txHash": "0xbfc73f1c66c7c552cbdb3d02cc1c434b1efaf35fd3916350b5d8a38f92c96fc7",
          "txType": 9,
          "utxo": [
            {
              "assetType": "X",
              "gasUtxo": 0,
              "multiSigns": [
                {
                  "pub": "xIVI+gfNGHAVrISn879D49+XV3HKT8kaHk7VnlAilvuQF67GYAeXqEoLapIjP0TBTcpsDHmZTqQUzjXVnJu0BQ==",
                  "sign": "xIVI+gfNGHAVrISn879D49+XV3HKT8kaHk7VnlAilvuQF67GYAeXqEoLapIjP0TBTcpsDHmZTqQUzjXVnJu0BQ=="
                }
              ],
              "owner": [
                "0xffFd42e045737b11570B7981c2648ea532a10B23"
              ],
              "vin": {
                "preVout": {
                  "hash": [
                    "0x36b19c533a49ec05a06be9c99c4e1c2e1609f9679aa75989c8ae0999ca63562a"
                  ]
                },
                "vinSigns": [
                  {
                    "pub": "MCowBQYDK2VwAyEAnVwyI7Xwk4lVNwi4j7ogCoHyy40isQmMumbM58JKTTU=",
                    "sign": "jXugdh1gM05AT73xU5WYP6THqX7ghdi4heKe04XjdsJQ/QhR6DxwkA5SLUO//lFswiiWFMf6gf697uVewJ4MAw=="
                  }
                ]
              },
              "vout": [
                {
                  "addr": "lockVirtualStake",
                  "value": 100000000000
                },
                {
                  "addr": "0xffFd42e045737b11570B7981c2648ea532a10B23",
                  "value": 9759599999665600
                },
                {
                  "addr": "VirtualBurnGas",
                  "value": 26100
                }
              ]
            }
          ],
          "verifySigns": [
            {
              "pub": "MCowBQYDK2VwAyEACE2DupNwSIpn854yGLj7QF/YHd6eAeLOhHYObzcbCTM=",
              "sign": "NTJntLI0ILj7hPFP1n5xmRj1eAOUKxEqec8cXLxGjjhJ74r8Qqn7fIwIsDbuQI8BGCD/D1Ikp9muLq/1eMACCw==",
              "addr": "0x85240c8dF5011d5967FA4566D3e2Ad5575A51856"
            }
          ]
        }
      ]
    },
    "code": 0,
    "message": "success"
  }
}
```

### GetBlockByHeight

**Description**：

Get block information based on block height

**Request**：

* id              Unique request identifier
* jsonRpc         JSON-RPC version
* params          Parameters:
  * beginHeight   Starting block height
  * endHeight     End block height
  * If endHeight > top, endHeight = top, and the difference between beginHeight and endHeight is 100 at most

**Response**：

* id              Unique request identifier
* jsonRpc         JSON-RPC version
* method          Name of the called method of the called method
* result          Return information
  * code          Status code: 
    * 0	          Success
    * -1          Block height error, beginHeight < endHeight
    * -2          The height of the request does not exceed 100
    * -3          Database abnormal, Get block hashes by block height error
    * -4          Database abnormal, Get block by block hash error
    * -5          Database abnormal, Get block top error
  * message       Human-readable status
  * blocks        Array of block objects (see Block information description for details)

example

```json
//req
{
  "id":"1",
  "jsonRpc":"2.0",
  "params":{"beginHeight":"10", "endHeight":"20"}
}
//ack
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetBlockByHeight",
  "result": {
    "blocks": [
      {
        "block": {
          "blockSigns": [
            {
              "pub": "MCowBQYDK2VwAyEAJPmMLCjSAjBx9GY2JAtmsSR9IuSDI1lN1m4yhUvxOEM=",
              "sign": "+3RAHn0u6TGjDYavjS/Td+mtTzctxyCi9z+0tLkqYenmJ8XWmTjb1QeYpF5hsqYL9Q9JRl/xNeZHyweK89arDA==",
              "addr": "0xE8a1A99432658958B6F3065977fe39192d91ecF6"
            },
            {
              "pub": "MCowBQYDK2VwAyEAbALWvBTB+PQv2StB5NEYON6WVj1eYwHxGfI0G/UFFmk=",
              "sign": "k4s5ucxeFUutQhOdos6zGlIkbW5HHg294aHPnfBzFMTpcv0hiDvcdREICjol1JjdZy9CQkQugDGjFeDrtA7VCQ==",
              "addr": "0x277Ff39E8176A582A392265ca619bdb6477674a5"
            },
            {
              "pub": "MCowBQYDK2VwAyEA6zMDRvZ82ObZCpVFw2+47ejYrLquImR1oI3skXZRtiY=",
              "sign": "JW+A2V0wbdmX5ZXnFE37fDMTLcFwKg8tLU8nI2Cz6FMm37zNhbarloPws41Mavw+ms5KC93h4x/CHAKrAyVTCw==",
              "addr": "0xCe3efA4FE6b044FB985736C62ABFDF435CC9AfCF"
            },
            {
              "pub": "MCowBQYDK2VwAyEA6Q6C8O9jkTtbPEHYnwIyBsx85/DEVnq640FmXXniTlE=",
              "sign": "2tCSQk+OHaWZXJ/Px9ql8id21a9pW6h6+/K4QZRfWYmaOBCpVK7AMhfcOmLN/P8AdrcYGSwfBDxWO+ryB0CUDA==",
              "addr": "0x690e0814a282f02Db36078f2B794777595bEDe89"
            },
            {
              "pub": "MCowBQYDK2VwAyEAgNYIcBwelxAzk/0Y2zHKIouw/Hgp7PyezmODMynlPtA=",
              "sign": "wd16hITmuuSYBa2yUoXnX9p5j9WkFQhZCPclL+dh2Fmreb0tOwx4N/rJ1OzT8a4c/zpWaxef3x/zVrLEiFEjAw==",
              "addr": "0xD9ECEec8420a0c053b70511f5f150EbD44358F3d"
            },
            {
              "pub": "MCowBQYDK2VwAyEAjV7zlpaeW3frrfwVoJgRZ+t2afDrVcWJnJtbOOvjX4k=",
              "sign": "nMEGg/v7rVNaRJur6dtNfMi30/rsEtygadHa4h0c92vZoa6uPiV+vko6haA8s4fo9h3/Zx9TLqdKwLe7fUPTCg==",
              "addr": "0x7E6A499159814eB3e3b1139afA2a7E4C9E883cce"
            },
            {
              "pub": "MCowBQYDK2VwAyEAfmL01bATzcX8LbZPBQ4haaWHfcNqaNnlVrsnk8+LTJI=",
              "sign": "YgOyUQx2LVSmEQrZgVF4t4weOUS7xMWmc9QHRqnrGzUYuEvJX/JBJLtxIBJKqjdKYOB1Sg0h6a5tHKL93rJ9DA==",
              "addr": "0xcaB8d5526b63BaF381Bc7a64eAF8690D16011BC4"
            }
          ],
          "bytes": 1932,
          "data": null,
          "hash": "0xbd804875a98343ad652ce7ad2252c06bbaa50410c156a588d0b4b43a7a8a4360",
          "height": 10,
          "merkleRoot": "0x311fa442700603cacb38018e0ce7f1f43224879905c5ea80aabd236267fc9451",
          "prevHash": "0x02c305a51b1a9201ed5a68513fe8bcd83f29f87ac452b3c708e0984e32c237b0",
          "time": 1724814849728314
        },
        "tx": [
          {
            "consensus": 7,
            "gasTx": 0,
            "type": "Tx",
            "identity": "0xE8a1A99432658958B6F3065977fe39192d91ecF6",
            "info": "",
            "time": 1724814849728314,
            "txHash": "0x311fa442700603cacb38018e0ce7f1f43224879905c5ea80aabd236267fc9451",
            "txType": 1,
            "utxo": [
              {
                "assetType":"5e7c785de771a3130587872bc4381b15c1b2d38a6c101796c67535af5c5471f0",
                "gasUtxo": 0,
                "multiSigns": [
                  {
                    "pub": "wmgFvHyr83tY0QO6Zg4kf/7JTLL3aKwSL8mxmulD4uerOnigthuyye6AuYOF7CgVQhl64Gg36PbTfd9W7QSHCw==",
                    "sign": "wmgFvHyr83tY0QO6Zg4kf/7JTLL3aKwSL8mxmulD4uerOnigthuyye6AuYOF7CgVQhl64Gg36PbTfd9W7QSHCw=="
                  }
                ],
                "owner": [
                  "0xffFd42e045737b11570B7981c2648ea532a10B23"
                ],
                "vin": {
                  "preVout": {
                    "hash": [
                      "0x54b87606b3ae037ecd5d76cd5e496bc489ad602931ec5f6a7722e93c91e96e5c"
                    ]
                  },
                  "vinSigns": [
                    {
                      "pub": "MCowBQYDK2VwAyEAnVwyI7Xwk4lVNwi4j7ogCoHyy40isQmMumbM58JKTTU=",
                      "sign": "19Mh06xHGee+J3lZFxLVL3k3xlEzGP4c8dfPxbsgaUCP/0jQodfxkeK8q8D2GkFA64ApYQT/qg3Fy9Igvc59Dw=="
                    }
                  ]
                },
                "vout": [
                  {
                    "addr": "0x690e0814a282f02Db36078f2B794777595bEDe89",
                    "value": 1200000000000
                  },
                  {
                    "addr": "0x746CADE61c69a2af24CEf4928a523E616c84b36E",
                    "value": 1200000000000
                  },
                  {
                    "addr": "0x79bb919D80AccbF3b7a62E5E2E841B2837B6D882",
                    "value": 1200000000000
                  },
                  {
                    "addr": "0x7E6A499159814eB3e3b1139afA2a7E4C9E883cce",
                    "value": 1200000000000
                  },
                  {
                    "addr": "0x7f3928315606DA72868848f1F0f6154461F1cBA2",
                    "value": 1200000000000
                  },
                  {
                    "addr": "0xffFd42e045737b11570B7981c2648ea532a10B23",
                    "value": 9981999999898600
                  },
                  {
                    "addr": "VirtualBurnGas",
                    "value": 33800
                  }
                ]
              }
            ],
            "verifySigns": [
              {
                "pub": "MCowBQYDK2VwAyEAJPmMLCjSAjBx9GY2JAtmsSR9IuSDI1lN1m4yhUvxOEM=",
                "sign": "8nvcAC6dWFfZIOswHpTWj2cw7/dsZ/BWd16PtIhRH1+GT4R1TGpI3Y+LZ0xg1u/vLGiiYtQhL/dY167A8KtPDw==",
                "addr": "0xE8a1A99432658958B6F3065977fe39192d91ecF6"
              }
            ]
          }
        ]
      },
      {
        "block": {
          "blockSigns": [
            {
              "pub": "MCowBQYDK2VwAyEAlCT0eYlIC0N086DOdxf1JV4KIAdrMPk9edmgVSvFtEs=",
              "sign": "PbEvCF/iZqbcaHWC4kT7cyvTxnVNCTV9D7c0IBcssDil1u6g3wd7KRMZuiCmW4FMOeU1KepWYLlrMNY9V0G6CA==",
              "addr": "0x00380ecf01085A4D877B9C83Bf7da715661057a5"
            },
            {
              "pub": "MCowBQYDK2VwAyEAVlvNx7mZLV1Nz/YnT+bhALXC/GR7XN7su3/izWBWhx8=",
              "sign": "I1ZAC0ozRItpy101deuPHqcCpkh9w8sSoC3yOXSGcQvbNg3ygWEurC3JGV85HCvh7Soixtt9JG37jTYLA8wpBg==",
              "addr": "0xE68A90e2af411b20a9CF421adF6531AaEfD404F8"
            },
            {
              "pub": "MCowBQYDK2VwAyEA6zMDRvZ82ObZCpVFw2+47ejYrLquImR1oI3skXZRtiY=",
              "sign": "LK7aRfFshdFhCq+f6B3mB7cnKM9+GdxSNUVO72pg3qwvnZgHjyY69EmOCRYl4n7jTsou9DK/dRo0P9S6XDNDCw==",
              "addr": "0xCe3efA4FE6b044FB985736C62ABFDF435CC9AfCF"
            },
            {
              "pub": "MCowBQYDK2VwAyEA2F7rPz4YMNeQl5Gx4mAFM/+23eg2C0O8mHYf6FdtuR0=",
              "sign": "FEEgsOGBtctp05OL5O9Yyti1QGbbzQ5oNEwDOLW4H0ANATlc5t7ARqKLeO84mPO84sXZT4rtD8GRUXr2JzYpBQ==",
              "addr": "0x82b79db0f26524f34c67e736a7BB0611Db702930"
            },
            {
              "pub": "MCowBQYDK2VwAyEAJPmMLCjSAjBx9GY2JAtmsSR9IuSDI1lN1m4yhUvxOEM=",
              "sign": "QQWAfuXu7qYMYOA+/v5ZuLRiASjWG+rCZPK+b7M6oR86XJlkX7AowjIpMoU3VKcrj40H34VtEekvAscvIb2mCg==",
              "addr": "0xE8a1A99432658958B6F3065977fe39192d91ecF6"
            },
            {
              "pub": "MCowBQYDK2VwAyEAiQR7rUhgYA1Eb1YXJJXLRSVaX/46aYvYilNidVD3DDs=",
              "sign": "Ndgb/dqyBEUESrORxJDPOEEFKYP3I7gJ6FPec+Ock0psSWhquNie5NyNV+IGp+6bCOC7hIIuQFUMhwWVZJ3rCA==",
              "addr": "0xC2ee63B5169D2cdbc1BBB5CfC1f15051A8549B5e"
            },
            {
              "pub": "MCowBQYDK2VwAyEA6Q6C8O9jkTtbPEHYnwIyBsx85/DEVnq640FmXXniTlE=",
              "sign": "L0r36sdK9V/LGl3qvOVzuF5Ae/FIKms93Bbkzi2tVDmU9NUHM81AMmQiP2xvYcF9Qr7Se3HHIrgh/qseDmJhBA==",
              "addr": "0x690e0814a282f02Db36078f2B794777595bEDe89"
            }
          ],
          "bytes": 1932,
          "data": null,
          "hash": "0x6124e62c2d36c3cb63f2fdd9d07bb7de8b989ee1079680fdcf35bd65bd307825",
          "height": 11,
          "merkleRoot": "0xc844ffc0f4cd2e8c3d64c875ce709340b856eabb3baa61ef85db6614ed53abb0",
          "prevhash": "0xbd804875a98343ad652ce7ad2252c06bbaa50410c156a588d0b4b43a7a8a4360",
          "time": 1724814857464488
        },
        "tx": [
          {
            "consensus": 7,
            "GasTx": 0,
            "Type": "Tx",
            "identity": "0x00380ecf01085A4D877B9C83Bf7da715661057a5",
            "info": "",
            "time": 1724814857464488,
            "txHash": "0xc844ffc0f4cd2e8c3d64c875ce709340b856eabb3baa61ef85db6614ed53abb0",
            "txType": 1,
            "utxo": [
              {
                "assetType": "0x416ba3e59614072c3bbdfb4f194fe71d248a7d82b1727f2d4ca51f8b4aba1528",
                "gasUtxo": 0,
                "multiSigns": [
                  {
                    "pub": "xb2RNPl3GJ3nfr8Fsthl7jKaCBEPwYn/hz9aFOSQwuhNl/XVm45YI31btHFBSnM3scLCnn73nCUOIF3WD4jwCg==",
                    "sign": "xb2RNPl3GJ3nfr8Fsthl7jKaCBEPwYn/hz9aFOSQwuhNl/XVm45YI31btHFBSnM3scLCnn73nCUOIF3WD4jwCg=="
                  }
                ],
                "owner": [
                  "0xffFd42e045737b11570B7981c2648ea532a10B23"
                ],
                "vin": {
                  "preVout": {
                    "hash": [
                      "0x9258ed48fc0e4d63d1e99ce7d6dea5cad80dd273a32bef2b4ddfc4031b1ddcf3"
                    ]
                  },
                  "vinSigns": [
                    {
                      "pub": "MCowBQYDK2VwAyEAnVwyI7Xwk4lVNwi4j7ogCoHyy40isQmMumbM58JKTTU=",
                      "sign": "BcCAUie3/f4pR9qC/qAGZ1oQeqG3U75MLiPmgp/eCGT4IN46a/Ca2X7IjeiGI6hyK2H7/X12z3LPgd6dE+SrDw=="
                    }
                  ]
                },
                "vout": [
                  {
                    "addr": "0x690e0814a282f02Db36078f2B794777595bEDe89",
                    "value": 1200000000000
                  },
                  {
                    "addr": "0x746CADE61c69a2af24CEf4928a523E616c84b36E",
                    "value": 1200000000000
                  },
                  {
                    "addr": "0x79bb919D80AccbF3b7a62E5E2E841B2837B6D882",
                    "value": 1200000000000
                  },
                  {
                    "addr": "0x7E6A499159814eB3e3b1139afA2a7E4C9E883cce",
                    "value": 1200000000000
                  },
                  {
                    "addr": "0x7f3928315606DA72868848f1F0f6154461F1cBA2",
                    "value": 1200000000000
                  },
                  {
                    "addr": "0xffFd42e045737b11570B7981c2648ea532a10B23",
                    "value": 9981999999898600
                  },
                  {
                    "addr": "VirtualBurnGas",
                    "value": 33800
                  }
                ]
              }
            ],
            "verifySigns": [
              {
                "pub": "MCowBQYDK2VwAyEAlCT0eYlIC0N086DOdxf1JV4KIAdrMPk9edmgVSvFtEs=",
                "sign": "NB+Z095i7ctP7kwjtBPmqkH3e4T6tFMW8xXiMyCfpF6zlAVZfxxrxqleZHeDvwzYkKXxcC96d1ZFiOQIR+PYBg==",
                "addr": "0x00380ecf01085A4D877B9C83Bf7da715661057a5"
              }
            ]
          }
        ]
      },
      {
        "block": {
          "blockSigns": [
            {
              "pub": "MCowBQYDK2VwAyEAKblncGE2av+phdWRpUGHta3wagpb+xMdnZ3HBy1sTsM=",
              "sign": "oic8leQoCg5SCde5THO0InvNJMyprZiADPG9BJTi69tnzHkgVXAhwwVtY+i8PZBOE/+vzY3/3GImVQM/ByHNDA==",
              "addr": "0x3aeeFE155376a47E63bB93fE4e95e67aF42B68eC"
            },
            {
              "pub": "MCowBQYDK2VwAyEADD94/vLoo/SLRuWomnmvignrER/7wX+HDCoBMCXT9hM=",
              "sign": "LynnYAA1IHGl6VDsWXvxFEnWZ5ukDo1E2n5RbIiNEvWSj7TPfWQRcON/A3dCZFmxVTxDsL8TDWzoPhczM0CmCw==",
              "addr": "0x746CADE61c69a2af24CEf4928a523E616c84b36E"
            },
            {
              "pub": "MCowBQYDK2VwAyEACE2DupNwSIpn854yGLj7QF/YHd6eAeLOhHYObzcbCTM=",
              "sign": "vdEDCb2crS/0NMmAmFCHxrWcu1sqjthfWmqhVTZIoIFwnyuqpBMh3UOnsTKnCA6e4edgWq1k953bOy7Dw/QbBQ==",
              "addr": "0x85240c8dF5011d5967FA4566D3e2Ad5575A51856"
            },
            {
              "pub": "MCowBQYDK2VwAyEAw+WS2EacRYHJfOulc7OGvkR2LN/im1BrepT51IM/l74=",
              "sign": "cZmtNiDHWFWUKZcAJchxdrrqSSHa745kQk5pCdxwnuecLzlaVDje3XZLjd2c+gw6TapZCSmoRCeodhwcujagAw==",
              "addr": "0x8DABa2e48009a713B419bD31051f5708fEd2672E"
            },
            {
              "pub": "MCowBQYDK2VwAyEATcB9j/WO1+oUQdrk0iD3BkcnbgQQS/dCxDgAkfMGIGo=",
              "sign": "FyZIobk1azEBiQLt2c/d3G2RQDl4UZdOlfs4okmQoi9lEk3gk/ZHhhWy1gl2pIdnOkKv/5aAwCVYI7OamZmPCg==",
              "addr": "0x22618D827b657C3A3Aa322CEa63275cD9cf5620B"
            },
            {
              "pub": "MCowBQYDK2VwAyEAIyogP9HbFhQLJPXWTJvr7oacfOj7V7jbwr+tWuLUpeo=",
              "sign": "hv9Afdacp4hQKjItMn6dT9Jn/3wkiqSr1e1iKwO7OtclsbvoeI60eIhSSn8ERurx7hx0fEfl3FRpGsXE0lIDDg==",
              "addr": "0x066F1A3f2E6C25a21B1a8B342E8CEA91Df585835"
            },
            {
              "pub": "MCowBQYDK2VwAyEAJPmMLCjSAjBx9GY2JAtmsSR9IuSDI1lN1m4yhUvxOEM=",
              "sign": "UWP62p8zleLgoEvAs8jHZu+yRt03LJaDRXUX8YsRIrmvNmrFm3Qg+gfZ2MOZGnJWGK4/d6F4+3YfL/5Y+i9hCQ==",
              "addr": "0xE8a1A99432658958B6F3065977fe39192d91ecF6"
            }
          ],
          "bytes": 1932,
          "data": null,
          "hash": "0x8cc1071fd61c9992fb0897739c8ae464e1cf404f8046682b17a2600d7e36152a",
          "height": 12,
          "merkleRoot": "0x6c472a4c621f481941abae6a60db7bfdc0406ebbd0c21a13b1e6cfba59ff73e1",
          "prevHash": "0x6124e62c2d36c3cb63f2fdd9d07bb7de8b989ee1079680fdcf35bd65bd307825",
          "time": 1724814882100984
        },
        "tx": [
          {
            "consensus": 7,
            "gasTx": 0,
            "type": "Tx",
            "identity": "0x3aeeFE155376a47E63bB93fE4e95e67aF42B68eC",
            "info": "",
            "time": 1724814882100984,
            "txHash": "0x6c472a4c621f481941abae6a60db7bfdc0406ebbd0c21a13b1e6cfba59ff73e1",
            "txType": 1,
            "utxo": [
              {
                "assetType": "X",
                "gasUtxo": 0,
                "multiSigns": [
                  {
                    "pub": "Iuh2bSBKrarIbz3rbiuW1VIP9W7p9tk7QOsGcvIhkKW0aELqWE0nqk8jWv9YaT//PXPRhKDhpR/v2YCn1YmjCA==",
                    "sign": "Iuh2bSBKrarIbz3rbiuW1VIP9W7p9tk7QOsGcvIhkKW0aELqWE0nqk8jWv9YaT//PXPRhKDhpR/v2YCn1YmjCA=="
                  }
                ],
                "owner": [
                  "0xffFd42e045737b11570B7981c2648ea532a10B23"
                ],
                "vin": {
                  "preVout": {
                    "hash": [
                      "0x0006ac2efc60edeb71f12c720b9dde07841bdbb2930a22f6f9d5ad64f76138cc"
                    ]
                  },
                  "vinSigns": [
                    {
                      "pub": "MCowBQYDK2VwAyEAnVwyI7Xwk4lVNwi4j7ogCoHyy40isQmMumbM58JKTTU=",
                      "sign": "5Bec0R/u/KZDnSmyxBH5RoDxKKiEdtf2hL1fGeFIvg0vs1sBmXKIALu08Gx2eoDKQO+wp4PLxJDVNMSO4f+tDw=="
                    }
                  ]
                },
                "vout": [
                  {
                    "addr": "0x82b79db0f26524f34c67e736a7BB0611Db702930",
                    "value": 1200000000000
                  },
                  {
                    "addr": "0x85240c8dF5011d5967FA4566D3e2Ad5575A51856",
                    "value": 1200000000000
                  },
                  {
                    "addr": "0x8897DE435e9276a0683ADBb4E62d6C9DdCd261DE",
                    "value": 1200000000000
                  },
                  {
                    "addr": "0x8DABa2e48009a713B419bD31051f5708fEd2672E",
                    "value": 1200000000000
                  },
                  {
                    "addr": "0x9Ed0009A37D251706c4f14a85f755eabaCE99Ae9",
                    "value": 1200000000000
                  },
                  {
                    "addr": "0xffFd42e045737b11570B7981c2648ea532a10B23",
                    "value": 9974899999803900
                  },
                  {
                    "addr": "VirtualBurnGas",
                    "value": 33800
                  }
                ]
              }
            ],
            "verifySigns": [
              {
                "pub": "MCowBQYDK2VwAyEAKblncGE2av+phdWRpUGHta3wagpb+xMdnZ3HBy1sTsM=",
                "sign": "1OX7Nhecxr23Hnsyb+nwlXMwRSnDer3nLp3hTTPqrAbClzs6uFqHDLr7dHLdPhc/sfEonnerlTLYSvwvh2kyAA==",
                "addr": "0x3aeeFE155376a47E63bB93fE4e95e67aF42B68eC"
              }
            ]
          }
        ]
      }
    ],
    "code": 0,
    "message": "success"
  }
}
```

### ConfirmTransaction

Verify if a transaction has been confirmed and included in a block.

**Request**

- txhash Transaction hash
- Transaction height

**Response**：

- code          Return value number
  - 0           Success
  - -1          Nodelist size is empty
  - -2          FilterHeightNodeList size is empty
  - -3          CreateWait error
  - -4          AddResNode error
  - -5          WaitData error
  - -6          susSize node list is empty
  - -7          The amount received was too small to verify transaction on-chain
  - -8          tx Parse error

- message       Human-readable description of the result 
- tx            Detailed transaction data
- percent       Percentage of nodes that have confirmed the transaction
- sendsize      Total number of nodes polled for consensus
- receivedsize  Number of valid consensus responses received from nodes

```json
{
  "id":"1",
  "jsonRpc":"2.0",
  "params":{
      "txhash":"64e91e7fa9ce873a1891806ae1adcc0af98d38ff78660c8408ad9caa81c67495",
      "height": "500"
    }
}
```

```json
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "ConfirmTransaction",
  "result": {
    "code": 0,
    "message": "success",
    "percent": "1.000000",
    "receivedSize": "27",
    "sendSize": "34",
    "tx": {
      "consensus": 7,
      "type": "Tx",
      "data": {
        "txInfo": {
          "bonusAddr": "0xFFFc74b51BC5e75527fE5970D04355958dd3657C",
          "investAmount": 1000000000000,
          "investType": "normal"
        }
      },
      "identity": "0x0796B6DB27e5eb1e9F8Bd2c4d03191C902D22F0f",
      "time": 1716775934685374,
      "txHash": "0x64e91e7fa9ce873a1891806ae1adcc0af98d38ff78660c8408ad9caa81c67495",
      "txType": 4,
      "utxo": {
        "multiSigns": [
          {
            "pub": "Hv7Z7SrYgnK9WGI0qZJJkCcDBVG5mYZlAN2fe0RsdEEIY3i9iAbRK+JtT+hxrv1+pWJeR3IdT/81Mx6TlAkkAg==",
            "sign": "Hv7Z7SrYgnK9WGI0qZJJkCcDBVG5mYZlAN2fe0RsdEEIY3i9iAbRK+JtT+hxrv1+pWJeR3IdT/81Mx6TlAkkAg=="
          }
        ],
        "owner": [
          "0xFFFc74b51BC5e75527fE5970D04355958dd3657C"
        ],
        "vin": {
          "preVout": {
            "hash": [
              "0x7dd57386b958cb7ad02170bd5c190e369c1694f596d524d2b2bfa5e1a55c253b"
            ]
          },
          "vinSigns": [
            {
              "pub": "MCowBQYDK2VwAyEA+X/pIfbC/gTA+iuG5yoLn6AH90PFdko5gWfURmCYC90=",
              "sign": "eArBhLH2J24CjgE6SnPMV1/p+5Uqyuh2QwCwD7ldeqpJ63hPpcQ0n9CiNXh8CNPeKJNufduL1WjfDvqHymiZBA=="
            }
          ]
        },
        "vout": [
          {
            "addr": "VirtualInvest",
            "value": 1000000000000
          },
          {
            "addr": "0xFFFc74b51BC5e75527fE5970D04355958dd3657C",
            "value": 6998899999939100
          },
          {
            "addr": "VirtualBurnGas",
            "value": 32400
          }
        ]
      },
      "verifySigns": [
        {
          "pub": "MCowBQYDK2VwAyEAHDoLfSX+ygmvSICr/1Q/UnfLlPFkAQBB4oPZne/SoVo=",
          "sign": "bCoIyAR1qH5LDHpX5Y5E5OqZogQo0EDDPnihTaPDHV5jQdT9AEadCo/+uhRMOi7l9XlwxhrCcxesnfJDXbQmCg==",
          "addr": "0x0796B6DB27e5eb1e9F8Bd2c4d03191C902D22F0f"
        },
        {
          "pub": "MCowBQYDK2VwAyEABK13LqOyxq7skjywUZwpTTLVXU3yPMSClL0u9xI5+hg=",
          "sign": "",
          "addr": "0x2eb2F635320c3Dbf29eadD35E894c13EE3F20bd5"
        },
        {
          "pub": "MCowBQYDK2VwAyEANFAhkjOUKAp0RbqjjiDetKQjcwQTXLRpL0Vh7uz3Sm0=",
          "sign": "",
          "addr": "0x3b5AF36c2F269c4eA5ADffd12d65818A9cd94Dc2"
        },
        {
          "pub": "MCowBQYDK2VwAyEAl0V//ZTw/56RkIUtrEzyXIbPm0nQ+XjB2QEDZR+KbT4=",
          "sign": "",
          "addr": "0x3CA9403151e5E7ad6072c9CF29237A3BB61eFaF3"
        },
        {
          "pub": "MCowBQYDK2VwAyEAtLhQrLNMMCWqjBzgy3cf/eRC7ypLgZgg7inzrFP4vyY=",
          "sign": "",
          "addr": "0x0a887Ad7a0a383e8fF9E1CB2433712e53C26AF95"
        },
        {
          "pub": "MCowBQYDK2VwAyEAr8qDQ8MYYxD26OVtzmLshwDH44rbtFcxp+n7YMsvit8=",
          "sign": "",
          "addr": "0x3812aE1f4a85A937340e882e4285f2CdaaCbC21F"
        },
        {
          "pub": "MCowBQYDK2VwAyEACPZP4VDg6AE4zXC3GN0et49O0wxAQ5bNfgqDulRc+vk=",
          "sign": "",
          "addr": "0x244125ddD7A63479F3A5DA8bC36682EdaFfdc92d"
        },
        {
          "pub": "MCowBQYDK2VwAyEAdTGsapuDIoqcgqXHYKJgNPuTkwhZ6EYGi9ORPXV7krQ=",
          "sign": "",
          "addr": "0xca3B60adeEf20337427b0d4Fa6E62920ea81a855"
        },
        {
          "pub": "MCowBQYDK2VwAyEAh6RFUhVdsoE3MehHfFNlj4tWgyzLo+8F6SIPbW7zIYw=",
          "sign": "",
          "addr": "0x28bA6E30cB0d9372a18c80552eE11DFe47883FAd"
        },
        {
          "pub": "MCowBQYDK2VwAyEAZVRP0epGewUhFeh7p6tvzX3Rhn4BSB/7Exjqr8hW5yk=",
          "sign": "",
          "addr": "0xd57730E2CE30d412cea04689C9cDE2f0846df169"
        },
        {
          "pub": "MCowBQYDK2VwAyEANkIfPzXigAr1hfIIh4qaJ7bG0jrC7a5F1FUR39kBnoE=",
          "sign": "",
          "addr": "0x08C08F389c8255c0B4d1C5e337C811D02F220B6e"
        },
        {
          "pub": "MCowBQYDK2VwAyEAQ05ytVs7kiZxfN2f6PUT9XpjfASpuMxoDNTJkzmimew=",
          "sign": "",
          "addr": "0xbBE3F8cf409A4554AC4dC3307B0198967E68258F"
        },
        {
          "pub": "MCowBQYDK2VwAyEAE9q3hlengBKro4iPMtj+F3RGyoJ7DdyToMzBSFvv2f8=",
          "sign": "",
          "addr": "0x1A2a22101480Cd3c0f966e0399cc5f4150B0EbF7"
        }
      ]
    },
    "txHash": "0x64e91e7fa9ce873a1891806ae1adcc0af98d38ff78660c8408ad9caa81c67495"
  }
}
```

### GetAllStakeNodeList

Retrieve a list of nodes that have staked assets to participate in the network consensus or services.

**Request**

- none

**Response**

- code      Return value number
  - 0       Success
  - -1      peerlist is empty
- message   Human-readable status of the operation
- version   Version of the protocol or API being used
- list      List of nodes that have staked assets to participate in the network.
- addr      Blockchain address of the node
- ip Node   IP address and port of the node
- identity  Public key of the node's account
- logo node Logo
- name node Human-readable name of the node 

```json
{
  "id":"1",
  "jsonRpc":"2.0",
  "params":{}
}
```

```json
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetAllStakeNodeList",
  "result": {
    "code": 0,
    "list": {
      "list": [
        {
          "addr": "0x01921896D8AAC12B19BC8413135907AB5aE82326",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAnkb8f/5s/LsQXNlU7/SDXR2sPf8IZZrbZ9v2HmYJffk=",
          "ip": "192.168.1.86",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x0796B6DB27e5eb1e9F8Bd2c4d03191C902D22F0f",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAHDoLfSX+ygmvSICr/1Q/UnfLlPFkAQBB4oPZne/SoVo=",
          "ip": "192.168.1.118",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x08C08F389c8255c0B4d1C5e337C811D02F220B6e",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEANkIfPzXigAr1hfIIh4qaJ7bG0jrC7a5F1FUR39kBnoE=",
          "ip": "192.168.1.99",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x0a887Ad7a0a383e8fF9E1CB2433712e53C26AF95",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAtLhQrLNMMCWqjBzgy3cf/eRC7ypLgZgg7inzrFP4vyY=",
          "ip": "192.168.1.95",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x0aFeBC02da4d5111d05d425e74e822B032274f2b",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAd2sNbj9c8IKcU8zzC2qWrGkwwFkZSQTtkvrgkxCzpTE=",
          "ip": "192.168.1.100",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x1A2a22101480Cd3c0f966e0399cc5f4150B0EbF7",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAE9q3hlengBKro4iPMtj+F3RGyoJ7DdyToMzBSFvv2f8=",
          "ip": "192.168.1.104",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x1CD6855FB33190754b122f8aBad737791BaB3F0a",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAF/4cPYBHTbG05HVOwUSmM/0wWPdrf7UbB1VO2ZfDuK0=",
          "ip": "192.168.1.61",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x244125ddD7A63479F3A5DA8bC36682EdaFfdc92d",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEACPZP4VDg6AE4zXC3GN0et49O0wxAQ5bNfgqDulRc+vk=",
          "ip": "192.168.1.102",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x28bA6E30cB0d9372a18c80552eE11DFe47883FAd",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAh6RFUhVdsoE3MehHfFNlj4tWgyzLo+8F6SIPbW7zIYw=",
          "ip": "192.168.1.116",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x2eb2F635320c3Dbf29eadD35E894c13EE3F20bd5",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEABK13LqOyxq7skjywUZwpTTLVXU3yPMSClL0u9xI5+hg=",
          "ip": "192.168.1.103",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x3292FEAbea61A76cf59Fa917b9DCcC937Ca489eE",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAz7Y+YE+zTAZO26NcyvbWFpwPOYS18kyofL9pitE73G0=",
          "ip": "192.168.1.117",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x372b320ECA35F86A28249E3e309545A44270DD7D",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAJJnp6slecl6UN0fjGiWya9a37N0iwUW1gQBS3Sh0qvU=",
          "ip": "192.168.1.101",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x3812aE1f4a85A937340e882e4285f2CdaaCbC21F",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAr8qDQ8MYYxD26OVtzmLshwDH44rbtFcxp+n7YMsvit8=",
          "ip": "192.168.1.96",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x3CA9403151e5E7ad6072c9CF29237A3BB61eFaF3",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAl0V//ZTw/56RkIUtrEzyXIbPm0nQ+XjB2QEDZR+KbT4=",
          "ip": "192.168.1.98",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x3b5AF36c2F269c4eA5ADffd12d65818A9cd94Dc2",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEANFAhkjOUKAp0RbqjjiDetKQjcwQTXLRpL0Vh7uz3Sm0=",
          "ip": "192.168.1.119",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x69b34b7538DeB6913f2b9f59Cbc8610059442e5A",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEApiP9nArs1ZDRXH3k89VuRReOlgNufYsF939nC3pBsqg=",
          "ip": "192.168.1.35",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x6a72ad3e9762d67D45a311954CdC6ad4693203a9",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAQjLIZj6+3TH2mSye+RS2HqN5W1+cGSg63ghfEOvBDnc=",
          "ip": "192.168.1.81",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x79c80a68Cc851d9A2aBF16c32eBAaC866C4Fced9",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAawp+8tDyeSREnNHrEaeBs6B9AeclJOlrAkeWMijTPww=",
          "ip": "192.168.1.114",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x855052fa258B463AEAd1E5abD55F2ffbCBb3F022",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAwigpWZg9E0DRbbbNuE4PDHT7MJ9XIH2hh5yADHNa6jw=",
          "ip": "192.168.1.89",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x8C33DF5ca4a4de15B53316dc3db60Ae4A7e09734",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEApakW/x/DvV7BBRmhbQzkxhj7xbS0Xr5JN4tSEigWshA=",
          "ip": "192.168.1.105",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x8F66e288547032026dd1ddFb992ff7eEcD9261f0",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAbA5Gq2olxI11gecRsyYYmaecJN0ht74mB2fLNWb3TcQ=",
          "ip": "192.168.1.115",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x8fFb06c288C30F3e62b31d6c5FD34328A964774a",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAner1iR+SqRLmN0lLWB0+su0Quh0XpNDTmm9PWWODirI=",
          "ip": "192.168.1.111",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x9234e37d86AE7De3Dd0Ac57AF815b54551873504",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAcUcydwF7CSr9bjBiUbd3drV+WMd4yd8xFL7HWGA4FTw=",
          "ip": "192.168.1.113",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x93E70Da36F35934C704ca9f2d2CF5cbc3Cba5988",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEARRkX0aksdpaxlbCExPkiaYaga6T/i2/iJyPGRTTNDm8=",
          "ip": "192.168.1.91",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0xB6AE1C10C5547ed1D6ba50d74cc92214E17b5111",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAkHwtzRc4cHtDid6kE/hqO/h6bPlU+cG5ZigBEwOGD2Y=",
          "ip": "192.168.1.88",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0xD82a5740De434f67b64946ba5939dfECc594Bcc1",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAB13mSe2XJ46JzM6WC3sOh7dh5TlMaDevNUlX7b4tuu8=",
          "ip": "192.168.1.109",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0xE2EBF3781D7eFeCbf242a5510AAb60985E045F17",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAktscT7UBR2sjjapjsIjA00bR5vg3I62vPu1HcXQkzrM=",
          "ip": "192.168.1.108",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0xFFFc74b51BC5e75527fE5970D04355958dd3657C",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEA+X/pIfbC/gTA+iuG5yoLn6AH90PFdko5gWfURmCYC90=",
          "ip": "192.168.1.87",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0xadc2A709EC1413eCcEB4d115E50BD9ebBA35E3Ce",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAYc23TU7Tw6L9QcUXNM6FuS5kEzTTQEfX15dR9+n251Y=",
          "ip": "192.168.1.93",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0xbBE3F8cf409A4554AC4dC3307B0198967E68258F",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAQ05ytVs7kiZxfN2f6PUT9XpjfASpuMxoDNTJkzmimew=",
          "ip": "192.168.1.90",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0xc6C621E6BA9Ad2FA2E81998006e0f4Ff45c34b65",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEALUncL09pHgayYIMkZS+hbq5t61CIHG0juNkcbAo9abE=",
          "ip": "192.168.1.106",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0xca3B60adeEf20337427b0d4Fa6E62920ea81a855",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAdTGsapuDIoqcgqXHYKJgNPuTkwhZ6EYGi9ORPXV7krQ=",
          "ip": "192.168.1.97",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0xd56d950d5a79d7906269f87FEa9d1FE48Cb577E7",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAAXU9Om/NJRE0T7lo3L1b/QMcd6cBmGRW1/Y4jX2xiHQ=",
          "ip": "192.168.1.60",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0xd57730E2CE30d412cea04689C9cDE2f0846df169",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAZVRP0epGewUhFeh7p6tvzX3Rhn4BSB/7Exjqr8hW5yk=",
          "ip": "192.168.1.110",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0xdaAfa89eafe616EEa5Aa219d93bC8b1C0299Cc9E",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEAbrU2gaKp26A8Tmn7S0bMTTBJ5BrnLCv450l6oU+ixZM=",
          "ip": "192.168.1.107",
          "version": "1_1.0.0_d"
        },
        {
          "addr": "0x5c8bf650F93d82A7131C2FeA01Ec2bFB3C61A03B",
          "height": "590",
          "identity": "MCowBQYDK2VwAyEASFAPKN8n+Nqn2RcJX8XCgyx1sveBLZ/f5tn5JpM2Xxs=",
          "ip": "123.121.14.187",
          "version": "1_1.0.0_d"
        }
      ],
      "message": "success",
      "version": "1_1.0.0_d"
    },
    "message": "success"
  }
}
```

### GetBonusInfo

Retrieve node signature statistics and reward eligibility details.

**Request**

- none

**Response**

- code
  - 0      Success
  - -1     DB get sign addr failed!
- message  Human-readable status
- address  Node address
- count    Number of valid signatures submitted
- time     UNIX timestamp of the last update 

```json
{
  "id":"1",
  "jsonRpc":"2.0",
  "params":{}
}
```

```json
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetBonusInfo",
  "result": {
    "code": 0,
    "info": {
      "addrCount": [
        {
          "address": "0xCA66A76E2a279050EF6b57797ac53199379abB9F",
          "count": 3
        },
        {
          "address": "0xdaAfa89eafe616EEa5Aa219d93bC8b1C0299Cc9E",
          "count": 4
        },
        {
          "address": "0x5c8bf650F93d82A7131C2FeA01Ec2bFB3C61A03B",
          "count": 4
        },
        {
          "address": "0xca3B60adeEf20337427b0d4Fa6E62920ea81a855",
          "count": 2
        },
        {
          "address": "0xadc2A709EC1413eCcEB4d115E50BD9ebBA35E3Ce",
          "count": 3
        },
        {
          "address": "0x0796B6DB27e5eb1e9F8Bd2c4d03191C902D22F0f",
          "count": 4
        },
        {
          "address": "0x8C33DF5ca4a4de15B53316dc3db60Ae4A7e09734",
          "count": 3
        },
        {
          "address": "0x116058AcF188BB96F9Da1317Bd11fD737E4f8Cd2",
          "count": 4
        },
        {
          "address": "0x3812aE1f4a85A937340e882e4285f2CdaaCbC21F",
          "count": 2
        },
        {
          "address": "0x3CA9403151e5E7ad6072c9CF29237A3BB61eFaF3",
          "count": 3
        },
        {
          "address": "0x855052fa258B463AEAd1E5abD55F2ffbCBb3F022",
          "count": 5
        },
        {
          "address": "0x01921896D8AAC12B19BC8413135907AB5aE82326",
          "count": 5
        },
        {
          "address": "0xd57730E2CE30d412cea04689C9cDE2f0846df169",
          "count": 13
        },
        {
          "address": "0x0aFeBC02da4d5111d05d425e74e822B032274f2b",
          "count": 4
        },
        {
          "address": "0xbBE3F8cf409A4554AC4dC3307B0198967E68258F",
          "count": 8
        },
        {
          "address": "0x93E70Da36F35934C704ca9f2d2CF5cbc3Cba5988",
          "count": 6
        },
        {
          "address": "0x28bA6E30cB0d9372a18c80552eE11DFe47883FAd",
          "count": 1
        },
        {
          "address": "0xFFFc74b51BC5e75527fE5970D04355958dd3657C",
          "count": 10
        },
        {
          "address": "0xB6AE1C10C5547ed1D6ba50d74cc92214E17b5111",
          "count": 10
        },
        {
          "address": "0x3292FEAbea61A76cf59Fa917b9DCcC937Ca489eE",
          "count": 8
        },
        {
          "address": "0x9234e37d86AE7De3Dd0Ac57AF815b54551873504",
          "count": 6
        },
        {
          "address": "0x372b320ECA35F86A28249E3e309545A44270DD7D",
          "count": 9
        },
        {
          "address": "0x79c80a68Cc851d9A2aBF16c32eBAaC866C4Fced9",
          "count": 5
        },
        {
          "address": "0x8fFb06c288C30F3e62b31d6c5FD34328A964774a",
          "count": 7
        },
        {
          "address": "0xc6C621E6BA9Ad2FA2E81998006e0f4Ff45c34b65",
          "count": 15
        },
        {
          "address": "0xE2EBF3781D7eFeCbf242a5510AAb60985E045F17",
          "count": 3
        },
        {
          "address": "0x3b5AF36c2F269c4eA5ADffd12d65818A9cd94Dc2",
          "count": 6
        },
        {
          "address": "0x244125ddD7A63479F3A5DA8bC36682EdaFfdc92d",
          "count": 5
        },
        {
          "address": "0x8F66e288547032026dd1ddFb992ff7eEcD9261f0",
          "count": 7
        },
        {
          "address": "0x2eb2F635320c3Dbf29eadD35E894c13EE3F20bd5",
          "count": 5
        },
        {
          "address": "0xD82a5740De434f67b64946ba5939dfECc594Bcc1",
          "count": 10
        },
        {
          "address": "0x0a887Ad7a0a383e8fF9E1CB2433712e53C26AF95",
          "count": 2
        }
      ],
      "time": "1717113600000000"
    },
    "message": "message"
  }
}
```

### GetStakeUtxo

Retrieve staking UTXO (Unspent Transaction Output) details for a specific address.

**Request**

- fromaddr address

**Response**

- code
  -  0    Success
  - -1    fromaddr not stake!
- message Human-readable status
- utxo    UTXO details at the time of staking:
- value   Staked amount

```json
{
  "id":"1",
  "jsonRpc":"2.0",
  "params":{"fromAddr":"5c8bf650F93d82A7131C2FeA01Ec2bFB3C61A03B"}
}
```

```json
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetAllStakeNodeList",
  "result": {
    "code": 0,
    "message": "",
    "utxos": {
      "827022b125d2b60e9ed40a1e7bfa6874b90bb6dbccd515824cb353f0ab3397c6": 100000000000
    }
  }
}
```

### GetDivestUtxo

Retrieve uninvested or divested UTXOs (Unspent Transaction Outputs) between two addresses.

**Request**

- fromAddr investor
- toAddr investee

Status code: 

- code
  - 0     Success 
  - -1    The address has no investment in anyone
- message Human-readable status
- utxos   List of uninvested/divested UTXOs:

```json
{
  "id":"1",
  "jsonRpc":"2.0",
  "params":{
    "fromAddr":"5c8bf650F93d82A7131C2FeA01Ec2bFB3C61A03B",
    "toAddr":"5c8bf650F93d82A7131C2FeA01Ec2bFB3C61A03B"
  }
}
```

```json
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetAllStakeNodeList",
  "result": {
    "code": 0,
    "message": "success",
    "utxos": {
      "utxo": [
        "17c62bacc4db9eee7a9b4596894dbf6a17754319fc8b24204fd4e7519a3f4457"
      ]
    }
  }
}
```



### GetBalance

**Description**：

Retrieves the asset balance of a specified blockchain address.

**Request**：

* id Unique request identifier
* jsonRpc  JSON-RPC version
* params Parameters:
  * addr  Address to query
  * asset Asset type identifier 
  

**Response**：

* id          Unique request identifier
* jsonRpc     JSON-RPC version
* method      Name of the API method called
* result      Return information
  * code      Status code: 
     0  	    Success
    -1        address is invalid
    -2        search balance failed
  * message   Human-readable status message
  * balance   Account balance in smallest unit
  * addr      Address that was queried
  * assetType Type of asset queried 

**example**:

```json
//req
{
    "id": "1",
    "jsonRpc": "2.0",
    "params": {
        "addr": "0xffFd42e045737b11570B7981c2648ea532a10B23",
        "assetType": "X"
    }
}
//ack
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetBalance",
  "result": {
    "addr": "0xffFd42e045737b11570B7981c2648ea532a10B23",
    "assetType": "X",
    "balance": "9759699999691700",
    "code": 0,
    "message": "success"
  }
}
```



### GetBlockHeight

**Description**：

Retrieves the current height of the blockchain (latest confirmed block number).

**Request**：

* id       Unique request identifier
* jsonRpc  JSON-RPC version

**Response**：

* id          Unique request identifier
* jsonRpc     JSON-RPC version
* method      Echoes the Name of the called method
* result      Result payload:
  * code      Status code:
    -  0      Success
    -  -1     GetBlockTop error
  * message   Human-readable status message
  * top       Latest block height 

**example**:

```json
//req
{
    "id":"1",
    "jsonRpc":"2.0",
}
//ack
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetBlockHeight",
  "result": {
    "code": 0,
    "message": "success",
    "height": "590"
  }
}
```



### GetVersion

**Description**：

Retrieves version information of the client, network protocol, database, and configuration.

**Request**：

* id       Unique request identifier
* jsonRpc  JSON-RPC version

**Response**：

* id                Unique request identifier
* jsonRpc           JSON-RPC version
* method            Name of the called method of the called method
* result            Version details:
  * code            Status code    
    -  0  	        Success
  * message         Human-readable status message
  * clientVersion   Client software version
  * netVersion      Network protocol version
  * configVersion   Configuration schema version 
  * dbVersion       Database schema version

**example**:

```json
//req
{
    "id":"1",
    "jsonRpc":"2.0",
}
//ack
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetVersion",
  "result": {
    "clientVersion": "1_1.0.0_d",
    "code": 0,
    "configVersion": "1.0.0",
    "dbVersion": "1_1.0.0_d",
    "message": "success",
    "netVersion": "1"
  }
}
```



### GetBlockTransactionCountByHash

**Description**：

Returns the number of transactions in a block that matches the hash of a given block

**Request**：

* id            Unique request identifier
* jsonRpc       JSON-RPC version
* params        Parameters:
  * blockHash   Block hash

**Response**：

* id            Unique request identifier
* jsonRpc       JSON-RPC version
* method        Name of the called method of the called method
* result        Return information
  * code        Status code
    *   0  	    Success
    *  -1       GetBlockByBlockHash error
    *  -2       block parse string fail
  * message     Human-readable status message
  * txCount     Number of transactions in the block for a specified block hash

**example**:

```json
//req
{
    "id":"1",
    "jsonRpc":"2.0",
    "params":{"blockHash":"0x12e52383dc0fedc40bdab13fc1afd851d7123facf030f90163c03f87411650f1"}
}
//ack
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetBlockTransactionCountByHash",
  "result": {
    "code": 0,
    "message": "success",
    "txCount": "1"
  }
}
```







### GetAccounts

**Description**：

Returns a list of addresses owned by the client

**Request**：

* id       Unique request identifier
* jsonRpc  JSON-RPC version

**Response**：

* id              Unique request identifier
* jsonRpc         JSON-RPC version
* method          Name of the called method of the called method
* result          Return information
  * code          Status code: 
    - 0  	        Success
  * message       Human-readable status message
  * acccountList  List of addresses owned by the client

**example**: 

```json
//req
{
    "id":"1",
    "jsonRpc":"2.0",
}
//ack
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetAccounts",
  "result": {
    "acccountLists": [
      "0x6a72ad3e9762d67D45a311954CdC6ad4693203a9",
      "0x87dE53fdC1e5AA53eB9Cb839C2EF664Cab0f4C01",
      "0x9d394DFB4475Eaef15A27396568e5028f13C3F85",
      "0xD4c60A4866BeE49e0642feC293ee8560C237b758",
      "0xf535227CCA5487776e666374c839de8b7005892B"
    ],
    "code": 0,
    "message": "success"
  }
}
```



### GetChainId

**Description**：

Return chain ID

**Request**：

* id           Unique request identifier
* jsonRpc      JSON-RPC version

  

**Response**：

* id           Unique request identifier
* jsonRpc      JSON-RPC version
* method       Name of the called method of the called method
* result       Return information
  * code       Status code: 
    -  0  	   Success
  * message    Human-readable status message
  * chainId    Chain ID

**example**:

```json
//req
{
    "id":"1",
    "jsonRpc":"2.0",
}
//ack
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetChainId",
  "result": {
    "chainId": "0x1080c0ce",
    "code": 0,
    "message": "success"
  }
}
```



### GetNodeList

**Description**：

Retrieves the list of peer nodes currently connected to the client.

**Request**：

* id          Unique request identifier
* jsonRpc     JSON-RPC version

  

**Response**：

* id          Unique request identifier
* jsonRpc     JSON-RPC version
* method      Name of the called method of the called method
* result      Return information
  * code      Status code: 
    -  0  	  Success
  * message   Human-readable status message
  * peers     List of connected peer nodes
  * size      Total number of connected peers



```json
//req
{
    "id":"1",
    "jsonRpc":"2.0",
}
//ack
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetNodeList",
  "result": {
    "code": 0,
    "message": "success",
    "peers": [
      {
        "addr": "0x0aFeBC02da4d5111d05d425e74e822B032274f2b", //account addresses
        "fd": 16,  		//fd。
        "pulse": "3",		//heart beats
        "height": 2499,  	//node cuurent height
        "ip": "192.168.1.100", 	//remote ip
        "ip_l": "192.168.1.81", 	//local ip
        "kind": 1,    		// connection type
        "name": "",    		//node name
        "logo": "",   		//node logo
        "port": 55302, 		//local port
        "port_l": 20619, 	//remote port
        "version": "1_1.0.0_d" 	//client version
      },
      {
        "addr": "0xd57730E2CE30d412cea04689C9cDE2f0846df169",
        "fd": 17,
        "pulse": 3,
        "height": 2499,
        "ip": "192.168.1.110",
        "ip_l": "192.168.1.81",
        "kind": 1,
        "name": "",
         "logo": "",
        "port": 36874,
        "port_l": 20619,
        "version": "1_1.0.0_d"
      }
    ],
    "size": 2
  }
}
```

### GetYield‌Info

Retrieves the current annualized yield/interest rate information.

**Request**

- jsonRpc     2.0,  
- id:         Unique request id,  
- method:     GetYieldInfo

**Response**

- code        Return value number
  - -1：      The annualizedRate is greater than the threshold
- annualizedRate 

example：

```json
//req
{
    "id" : "1",
    "jsonRpc": "2.0",
}
//ack
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetYield‌Info",
  "result": {
    "code": 0,
    "message": "success",
    "currentAPR" : "0.16"
    }
}
```

### GetInvestAddrsBybonusAddr

**Description**：

Retrieves investment details associated with a specified bonus address.
Maximum Investment Limit: 6,500,000,000 (65000 * 100000000) base units.

**Request**：

* id        Unique request identifier
* jsonRpc   JSON-RPC version
* params    Parameters:
  * addr    Bonus address to query

**Response**：

* id        Unique request identifier
* jsonRpc   JSON-RPC version
* method    Name of the called method (echoed from request)
* result    Response payload:
* code Status code: 
  * 0	      Success
  * -1      Database abnormal, Get invest addrs by node failed!
  * -2      The account number to be invested have been invested by 999 people
  * -3      Database abnormal, Get bonus addr invest utxos by bonusAddr failed
  * -4      Database abnormal, Get transaction by hash failed
  * -5      Failed to parse transaction body
* message   Human-readable status
* info      Investment details: array of objects with:
  
  ```json
  //req
  {
    "id":"1",
    "jsonRpc":"2.0",
    "params":{"addr":"0xadc2A709EC1413eCcEB4d115E50BD9ebBA35E3Ce"}
  }
  //ack
  {
    "id": "1",
    "jsonRpc": "2.0",
    "method": "GetInvestAddrsBybonusAddr",
    "result": {
      "code": 0,
      "info": {
        "746CADE61c69a2af24CEf4928a523E616c84b36E": [
          [
            "5e7c785de771a3130587872bc4381b15c1b2d38a6c101796c67535af5c5471f0",
            "500000000000"
          ],
          [
            "0x416ba3e59614072c3bbdfb4f194fe71d248a7d82b1727f2d4ca51f8b4aba1528",
            "500000000000"
          ]
        ],
        "AbA56968eA57C630B22A21ff791458cF253cA6aE": [
          [
            "X",
            "1000000000000"
          ]
        ],
        "Ce3efA4FE6b044FB985736C62ABFDF435CC9AfCF": [
          [
            "5e7c785de771a3130587872bc4381b15c1b2d38a6c101796c67535af5c5471f0",
            "100000000000"
          ],
          [
            "0x416ba3e59614072c3bbdfb4f194fe71d248a7d82b1727f2d4ca51f8b4aba1528",
            "100000000000"
          ]
        ],
        "D9ECEec8420a0c053b70511f5f150EbD44358F3d": [
          [
            "5e7c785de771a3130587872bc4381b15c1b2d38a6c101796c67535af5c5471f0",
            "200000000000"
          ],
          [
            "0x416ba3e59614072c3bbdfb4f194fe71d248a7d82b1727f2d4ca51f8b4aba1528",
            "300000000000"
          ]
        ]
      },
      "message": "success"
    }
  }
  ```
  

### GetbonusAddrByInvestAddr

**Description**：

Retrieves the bonus address and asset type associated with an investor address.

**Request**：

* id           Unique request identifier
* jsonRpc      JSON-RPC version
* params       Parameters:
  * addr       Address to check

**Response**：

* id           Unique request identifier
* jsonRpc      JSON-RPC version
* method       Name of the called method of the called method
* result       Return information
  * code       Status code: 
    * 0	       Success
    * -1       Get bonus addr error
    * -2       Get assetType error
  * assetType  Type of asset invested in
  * bonusAddr  Address receiving the investment rewards

example：

```json
//req
{
  "id":"1",
  "jsonRpc":"2.0",
  "params":{"addr":"0x9D69D2774Ecbf6F36c0d8250892aFAD68EB35919"}
}
//ack
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetbonusAddrByInvestAddr",
  "result": {
    "assetType": "0xe71da6a3a2052f20d425aaecc6c9b65e3aa42ddd47a9f6d5c0448b7881ef43ab",
    "bonusAddr": "0x9D69D2774Ecbf6F36c0d8250892aFAD68EB35919",
    "code": 0,
    "message": "success"
  }
}
```

### GetAddrType

**Description**：

Checks the current state of a blockchain address to determine if it has active investments, staking (pledges), or locked assets.

**Request**：

* id         Unique request identifier
* jsonRpc    JSON-RPC version
* params     Parameters:
  * addr     Address to check

**Response**：

* id         Unique request identifier
* jsonRpc    JSON-RPC version
* method     Name of the called method of the called method
* result     Return information
  * code     Status code: 
    *  0	   Success
    * -1     Get can be revoke asset type error
  * isInvested  
  * isLocked  
  * isStaked  

example：

```json
//req
{
  "id":"1",
  "jsonRpc":"2.0",
  "params":{"addr":"0x9D69D2774Ecbf6F36c0d8250892aFAD68EB35919"}
}
//ack
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetAddrType",
  "result": {
    "code": 0,
    "isInvested": true,
    "isLocked": true,
    "isStaked": true,
    "message": "success"
  }
}
```

## Transaction correlation

The process of sending transactions from the current account is as follows:

1. Determine the time difference between this transaction and the previous transaction sent on this account. On the APP side, after calling the two interfaces for sending transactions, parse the contents returned by the two interfaces and cache the transaction information locally. The txJson structure returned by the ConfirmTransaction interface contains transaction time and gas information, and the txJson returned by the CreateCallContractTransaction interface also contains transaction time and gas information. Meanwhile, the content returned by the SendMessage or SendContractMessage interface includes txhash.

2. It is necessary to determine whether the code in the "Status code:  result" of the interface is 0 to confirm whether the interface call is normal. Only when the code of the interface call is 0 can the next interface call be made.

3. All transaction interfaces use the Post request method, and the data format in the request body is JSON.。

* If the time difference is within 30 seconds, it is necessary to determine whether the previous transaction has been Successfully recorded on the blockchain. If it has been Successfully recorded, send the current transaction; if not, prompt the user that the operation is too frequent.。
* If the time difference is greater than or equal to 30 seconds, directly send this transaction.。

Determine whether the transaction has been Successfully added to the blockchain.

1. First, obtain the node height. Call the GetBlockHeight interface to retrieve the value of the "height" field in the returned result, which represents the node height.
2. After calling the ConfirmTransaction interface again, the value of the height field should be set to the value of the height field returned by the GetBlockHeight interface. The Txhash field should be set to the txhash value returned by the SendMessage or SendContractMessage interface when the current account sent the previous transaction. The ConfirmTransaction interface returns that the percent value field is greater than or equal to 0.8, which indicates that the transaction has been Successfully added to the blockchain.。

## Send MeMeChain transactions

First, invoke the transaction interfaces such as CreateTransaction, and then sign all the contents returned by the CreateTransaction interface. The signature method is to call the Sig method in the library, and then call the /SendMessage interface. The /SendMessage interface is invoked to request the Parameters: which is the JSON string returned by calling the sigTx method.

### SendMessage

**Description**：

For the interfaces such as CreateTransaction, CreateStakeTransaction, CreateUnStakeTransaction, CreateInvestTransaction, CreateDisInvestTransaction, CreateBouns, etc., after the invocation is completed, sign the transaction using the signature SDK tool and then send it to the node through the SendMessage interface to complete the transaction sending. Whether to be on-chain is determined by using the ConfirmTransaction interface.

**Request**：

The Status code:  of the SDK tool signature interface that is invoked for the data returned by interfaces such as CreateTransaction

**Response**：

No. After calling this interface, you can check whether it has been linked by viewing the result.

**example**:

```json
//The data obtained after signing the data returned by CreateTransaction
{
    "id": "",
    "jsonRpc": "",
    "result": {
        "code": "",
        "gas": "20200",
        "height": "600",
        "message": "",
        "time": "1717148047269517",
        "txJson": "{\"time\":\"1717148047269517\",\"identity\":\"2eb2F635320c3Dbf29eadD35E894c13EE3F20bd5\",\"utxo\":{\"owner\":[\"cED97dA085527Fe7e1772CA59Aa1e64A78143128\"],\"vin\":[{\"prevOut\":[{\"hash\":\"3f1342e96e426e2905021ad991787131ec70d31298646b1e80da9d912eeff274\"}],\"vinSigns\":{\"sign\":\"ApxL8NDgh9YYDuUXpdbsbVv0cEAr3HyXmr2TICkD4mfuDIZqVlZJNUmaPAKHCs5kkn7JnZx7r12+CpnnR4ZpAg==\",\"pub\":\"MCowBQYDK2VwAyEA89VSBQU7d4uL+jvqAKeCRbgYz2tzk/Rf8DNRhB0sLbg=\"}}],\"vout\":[{\"value\":\"1350000000\",\"addr\":\"06BA76F46631d4F344d1344303895001F1E3Af29\"},{\"value\":\"1982446992477\",\"addr\":\"cED97dA085527Fe7e1772CA59Aa1e64A78143128\"},{\"value\":\"20200\",\"addr\":\"VirtualBurnGas\"}],\"multiSigns\":[{\"sign\":\"WCoFsLKML69x1rSpQc7pwbnd+GMfZ0Ce3wTPg96Rdb1v7ezFw9KuEBXwvGecTz264pVZB6T8hzgJIx26GuKVAA==\",\"pub\":\"MCowBQYDK2VwAyEA89VSBQU7d4uL+jvqAKeCRbgYz2tzk/Rf8DNRhB0sLbg=\"}]},\"type\":\"tx\",\"consensus\":7,\"txType\":1}",
        "txType": "1",
        "vrfJson": "{\"vrfdata\":{\"hash\":\"6cf89d80c98eecd9138caca4f55d7ad0fda2aed9d8e68dd4642543ae3ee056d6\"},\"vrfSigns\":{\"sign\":\"u5dNZ16Rd77B4nLd8gAcKTwz+GxeHH1HIlcGennGbPaKgIFXUkmFzS/EnVxRC4nmSfESAdWyMEmj4pKBhwuqAg==\",\"pub\":\"MCowBQYDK2VwAyEAcUcydwF7CSr9bjBiUbd3drV+WMd4yd8xFL7HWGA4FTw=\"}}"
    }
}
```

### SendContractMessage

**Description**：

For interfaces such as CreatecallContractTransaction and CreateDeployContractTransaction, after the invocation is completed, sign the transaction using the signature SDK tool and then send it to the node through the SendContractMessage interface to complete the transaction sending. Whether to be on-chain is determined by using the ConfirmTransaction interface.
**Request**：

The Status code:  of the SDK tool signature interface that is invoked for the data returned by interfaces such as CreateDeployContractTransaction

**Response**：

No. After calling this interface, you can check whether it has been linked by viewing the result.

**example**：

```json
//req
{
    "id": "",
    "jsonRpc": "",
    "result": {
        "code": "",
        "contractJs": "{\"version\":\"1_1.0.0_d\",\"txMsgReq\":{\"version\":\"1_1.0.0_d\",\"txMsgInfo\":{\"nodeHeight\":\"601\",\"contractStorageList\":[\"A8B8Ae6F84709fF80E08aD9d26575c161aCC95f1\"]},\"vrfInfo\":{\"vrfdata\":{\"hash\":\"dea1b44a641928d6a09db9a3d9da274abe4ef13eb23833213144a5b46c612136\"},\"vrfSigns\":{\"pub\":\"MCowBQYDK2VwAyEASFAPKN8n+Nqn2RcJX8XCgyx1sveBLZ/f5tn5JpM2Xxs=\"}}}}",
        "message": "",
        "txJson": "{\"time\":\"1717148103333839\",\"identity\":\"2eb2F635320c3Dbf29eadD35E894c13EE3F20bd5\",\"utxo\":{\"owner\":[\"cED97dA085527Fe7e1772CA59Aa1e64A78143128\"],\"vin\":[{\"prevOut\":[{\"hash\":\"dea1b44a641928d6a09db9a3d9da274abe4ef13eb23833213144a5b46c612136\"}],\"vinSigns\":{\"sign\":\"3o82Rq7taGO+VRtrhtxWOVPAolo/pVxuNXEBdklDpDVd8tJcTjNrnmaMFixdav2wCyvCb+AFOd02ryPI4JV1Cw==\",\"pub\":\"MCowBQYDK2VwAyEA89VSBQU7d4uL+jvqAKeCRbgYz2tzk/Rf8DNRhB0sLbg=\"}}],\"vout\":[{\"value\":\"480\",\"addr\":\"VirtualDeployContractBurnGas\"},{\"value\":\"1982446498797\",\"addr\":\"cED97dA085527Fe7e1772CA59Aa1e64A78143128\"},{\"value\":\"493200\",\"addr\":\"VirtualBurnGas\"}],\"multiSigns\":[{\"sign\":\"YVcOA5gZhVNaQx7eoduw4lOI4d1HNtPRWEUoMzDK6D2UnZXDbRziXV66XiaRxKOzXF3kF/N4j8PEe5CMjkf3BQ==\",\"pub\":\"MCowBQYDK2VwAyEA89VSBQU7d4uL+jvqAKeCRbgYz2tzk/Rf8DNRhB0sLbg=\"}]},\"type\":\"tx\",\"consensus\":7,\"txType\":7,\"data\":\"{\\\"txInfo\\\":{\\\"blockPrevRandao\\\":4406,\\\"blockTimeStamp\\\":1717148110,\\\"input\\\":\\\"608060405234801561001057600080fd5b506108b3806100206000396000f3fe608060405234801561001057600080fd5b50600436106100575760003560e01c80630483a7f61461005c5780631629614e1461008c57806327e235e3146100a85780637ad9ad7c146100d8578063afc58189146100f4575b600080fd5b610076600480360381019061007191906105a8565b610110565b60405161008391906106d7565b60405180910390f35b6100a660048036038101906100a19190610615565b610128565b005b6100c260048036038101906100bd91906105a8565b6102a7565b6040516100cf91906106d7565b60405180910390f35b6100f260048036038101906100ed91906105d5565b6102bf565b005b61010e60048036038101906101099190610615565b61037d565b005b60016020528060005260406000206000915090505481565b80806000803373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff1681526020019081526020016000205410156101aa576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016101a1906106b7565b60405180910390fd5b816000803373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008282546101f89190610759565b9250508190555081600160003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020600082825461024e9190610703565b925050819055503373ffffffffffffffffffffffffffffffffffffffff167f3a14c6aa3e15c61c97825b026647b989a91e18aa33b689769475a298922480428360405161029b91906106d7565b60405180910390a25050565b60006020528060005260406000206000915090505481565b806000808473ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020600082825461030d9190610703565b925050819055508173ffffffffffffffffffffffffffffffffffffffff163373ffffffffffffffffffffffffffffffffffffffff167f322d0c4befd4c2dd440740b711488a1638fd7d8eeb25f9dacede84083db428c98360405161037191906106d7565b60405180910390a35050565b6000600160003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020541415610400576040517f08c379a00000000000000000000000000000000000000000000000000000000081526004016103f790610697565b60405180910390fd5b80600160003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff168152602001908152602001600020541015610482576040517f08c379a000000000000000000000000000000000000000000000000000000000815260040161047990610697565b60405180910390fd5b806000803373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008282546104d09190610703565b9250508190555080600160003373ffffffffffffffffffffffffffffffffffffffff1673ffffffffffffffffffffffffffffffffffffffff16815260200190815260200160002060008282546105269190610759565b925050819055503373ffffffffffffffffffffffffffffffffffffffff167f867b353f032680758428983522443995b88120a470e436b962c6a9d0d8940af78260405161057391906106d7565b60405180910390a250565b60008135905061058d8161084f565b92915050565b6000813590506105a281610866565b92915050565b6000602082840312156105be576105bd6107f8565b5b60006105cc8482850161057e565b91505092915050565b600080604083850312156105ec576105eb6107f8565b5b60006105fa8582860161057e565b925050602061060b85828601610593565b9150509250929050565b60006020828403121561062b5761062a6107f8565b5b600061063984828501610593565b91505092915050565b600061064f6011836106f2565b915061065a826107fd565b602082019050919050565b60006106726014836106f2565b915061067d82610826565b602082019050919050565b610691816107bf565b82525050565b600060208201905081810360008301526106b081610642565b9050919050565b600060208201905081810360008301526106d081610665565b9050919050565b60006020820190506106ec6000830184610688565b92915050565b600082825260208201905092915050565b600061070e826107bf565b9150610719836107bf565b9250827fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff0382111561074e5761074d6107c9565b5b828201905092915050565b6000610764826107bf565b915061076f836107bf565b925082821015610782576107816107c9565b5b828203905092915050565b60006107988261079f565b9050919050565b600073ffffffffffffffffffffffffffffffffffffffff82169050919050565b6000819050919050565b7f4e487b7100000000000000000000000000000000000000000000000000000000600052601160045260246000fd5b600080fd5b7f4e6f206c6f636b65642062616c616e6365000000000000000000000000000000600082015250565b7f496e73756666696369656e742062616c616e6365000000000000000000000000600082015250565b6108588161078d565b811461086357600080fd5b50565b61086f816107bf565b811461087a57600080fd5b5056fea264697066735822122067e67aed3152cf78a07c4f8842540cf5803e421699b10fbf8f66c015550b0ed464736f6c63430008070033\\\",\\\"recipient\\\":\\\"A8B8Ae6F84709fF80E08aD9d26575c161aCC95f1\\\",\\\"sender\\\":\\\"cED97dA085527Fe7e1772CA59Aa1e64A78143128\\\",\\\"version\\\":0,\\\"virtualMachine\\\":0}}\"}"
    }
}
```

### CreateTransaction

Creates a standard transaction between two addresses.

**Request**

- gasAssets          Select the currency type for paying gas fees
  - gasFromAddr      Gas Fee Payment Address
  - gasType          Select the currency type
- id                 Unique request identifier
- jsonRpc            JSON-RPC version
- method             Name of the called method of the called method 
- params             Parameters:
  - isFindUtxo       Whether to search the current status of UTXO across the entire network  
  - isGasAssets      Use other assets to pay for gas
- txAsset            Transaction asset information
  - assetType        Transfer asset type hash
  - fromAddr         Sender's blockchain address
  - toAddrAmount     Recipient's blockchain address  and transfer amount
    - toAddr         Recipient's blockchain address  
    - value          Transfer amount 

```json
{
    "gasAssets": {
        "gasFromAddr": "e9E6f91783ADf09cE6FCEbB2A852E953286b1032",
        "gasType": "e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc"
    },
    "id": "",
    "jsonRpc": "",
    "method": "",
    "params": {
        "isFindUtxo": false,
        "isGasAssets": false,
        "txInfo": ""
    },
    "txAsset": [
        {
            "assetType": "e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc",
            "fromAddr": [
                "e9E6f91783ADf09cE6FCEbB2A852E953286b1032"
            ],
            "toAddrAmount": [
                {
                    "addr": "7C81161348F21cf77A011fAB74cf7ee0cdCC2347",
                    "value": 1000000000
                }
            ]
        }
    ]
}
```

**Response**
- id                   Unique request identifier
- jsonRpc              JSON-RPC version
- method               Name of the called method of the called method 
- result               Response data:
  - code               Return value number
    -  0:              success
    - -1:              db get top failed
    - -2:              Check parameters failed
    - -3:              to addr is empty
    - -4:              To address is not  address
    - -5:              from address is same with toaddr
    - -6:              Value is zero
    - -7:              The information entered exceeds the specified length
    - -8:              FindUtxo failed
    - -9:              Utxo is empty
    - -10:             Tx owner is empty
    - -11:             Generate Gas failed
    - -12:             The total cost  is  total less than the cost
    - -13:             Check parameters failed! The error code is ret
    - -14:             FindUtxo failed! The error code is
    - -15:             Utxo is empty
    - -16:             Tx owner is empty
    - -17:             Find packager failed
    - -18:             utxo is using
  - gas:               Computed gas fee in atomic units
  - height:            Current blockchain height when transaction was created
  - message            Status code:  information (see code error Return information for details)
  - time:              UNIX timestamp of transaction creation
  - txJson:            Raw transaction data in JSON format
  - txType:            Transaction type
  - vrfJson:           Verifiable Random Function (VRF) parameters for transaction validation

```json
{
    "id": "",
    "jsonRpc": "",
    "method": "CreateTransaction",
    "result": {
        "code": 0,
        "gas": "20200",
        "height": "259",
        "message": "success",
        "time": "1743560774393802",
        "txJson": "{\"time\":\"1743560774393802\",\"identity\":\"A0409Fb7d5f77488f538253E7701EE711E90ADB0\",\"type\":\"Tx\",\"consensus\":7,\"txType\":1,\"utxos\":[{\"owner\":[\"e9E6f91783ADf09cE6FCEbB2A852E953286b1032\"],\"vin\":[{\"prevOut\":[{\"hash\":\"0053f7530a5d4113ac999d6ca6b3dbc22ef316d7727f627e33d4bcf2e7bb63ce\"}]}],\"vout\":[{\"value\":\"1000000000\",\"addr\":\"7C81161348F21cf77A011fAB74cf7ee0cdCC2347\"},{\"value\":\"9998999919000\",\"addr\":\"e9E6f91783ADf09cE6FCEbB2A852E953286b1032\"},{\"value\":\"20200\",\"addr\":\"VirtualBurnGas\"}],\"assetType\":\"e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc\"}]}",
        "txType": "1",
        "vrfJson": "{}"
    }
}
```

### CreateDeployContractTransaction

Creates a transaction to deploy a smart contract to the blockchain.

**Request**
- id                   Unique request identifier
- jsonRpc              JSON-RPC version
- method               Name of the called method of the called method 
- params               Parameters:
  - addr               Blockchain address initiating the deployment 
  - contract           Compiled bytecode of the smart contract 
  - data               Initialization data for the contract 
  - gasAssets          Use other assets to pay for gas
  - info               Metadata describing the contract
  - isFindUtxo         Whether to search the current status of UTXO across the entire network  
  - nContractType      Type of contract (default: 0 for standard contracts)
  - isGasAssets        Use other assets to pay for gas
  - pubStr             Base58-encoded public key of the deployer address
  - txInfo             Optional description/memo

```json
{
    "id": "",
    "jsonRpc": "",
    "method": "",
    "params": {
        "addr": "0x7C81161348F21cf77A011fAB74cf7ee0cdCC2347",
        "contract": "608060405234801562000010575f80fd5b5060405162000c0838038062000c08833981016040819052620000339162000156565b5f62000040858262000267565b5060016200004f848262000267565b506002805460ff191660ff93909316929092179091556003819055335f81815260046020526040902091909155600680546001600160a01b0319169091179055506200032f9050565b634e487b7160e01b5f52604160045260245ffd5b5f82601f830112620000bc575f80fd5b81516001600160401b0380821115620000d957620000d962000098565b604051601f8301601f19908116603f0116810190828211818310171562000104576200010462000098565b8160405283815260209250868385880101111562000120575f80fd5b5f91505b8382101562000143578582018301518183018401529082019062000124565b5f93810190920192909252949350505050565b5f805f80608085870312156200016a575f80fd5b84516001600160401b038082111562000181575f80fd5b6200018f88838901620000ac565b95506020870151915080821115620001a5575f80fd5b50620001b487828801620000ac565b935050604085015160ff81168114620001cb575f80fd5b6060959095015193969295505050565b600181811c90821680620001f057607f821691505b6020821081036200020f57634e487b7160e01b5f52602260045260245ffd5b50919050565b601f82111562000262575f81815260208120601f850160051c810160208610156200023d5750805b601f850160051c820191505b818110156200025e5782815560010162000249565b5050505b505050565b81516001600160401b0381111562000283576200028362000098565b6200029b81620002948454620001db565b8462000215565b602080601f831160018114620002d1575f8415620002b95750858301515b5f19600386901b1c1916600185901b1785556200025e565b5f85815260208120601f198616915b828110156200030157888601518255948401946001909101908401620002e0565b50858210156200031f57878501515f19600388901b60f8161c191681555b5050505050600190811b01905550565b6108cb806200033d5f395ff3fe608060405234801561000f575f80fd5b50600436106100e5575f3560e01c806370a0823111610088578063a9059cbb11610063578063a9059cbb146101d5578063c4e41b22146101e8578063dd62ed3e146101f0578063f0141d841461021a575f80fd5b806370a08231146101835780638da5cb5b146101a257806395d89b41146101cd575f80fd5b806318160ddd116100c357806318160ddd1461011757806323b872dd1461012e578063313ce5671461015157806340c10f1914610170575f80fd5b806306fdde03146100e9578063150704011461010757806317d7de7c1461010f575b5f80fd5b6100f1610225565b6040516100fe91906106dd565b60405180910390f35b6100f16102b0565b6100f1610340565b61012060035481565b6040519081526020016100fe565b61014161013c366004610743565b61034e565b60405190151581526020016100fe565b60025461015e9060ff1681565b60405160ff90911681526020016100fe565b61014161017e36600461077c565b61040c565b6101206101913660046107a4565b60046020525f908152604090205481565b6006546101b5906001600160a01b031681565b6040516001600160a01b0390911681526020016100fe565b6100f1610547565b6101416101e336600461077c565b610554565b600354610120565b6101206101fe3660046107c4565b600560209081525f928352604080842090915290825290205481565b60025460ff1661015e565b5f8054610231906107f5565b80601f016020809104026020016040519081016040528092919081815260200182805461025d906107f5565b80156102a85780601f1061027f576101008083540402835291602001916102a8565b820191905f5260205f20905b81548152906001019060200180831161028b57829003601f168201915b505050505081565b6060600180546102bf906107f5565b80601f01602080910402602001604051908101604052809291908181526020018280546102eb906107f5565b80156103365780601f1061030d57610100808354040283529160200191610336565b820191905f5260205f20905b81548152906001019060200180831161031957829003601f168201915b5050505050905090565b60605f80546102bf906107f5565b5f336001600160a01b038516146103c05760405162461bcd60e51b815260206004820152602b60248201527f596f752063616e206f6e6c79207472616e736665722066726f6d20796f75722060448201526a6f776e206164647265737360a81b60648201526084015b60405180910390fd5b6001600160a01b0384165f908152600460205260409020548211156103f75760405162461bcd60e51b81526004016103b79061082d565b610402848484610596565b5060019392505050565b6006545f906001600160a01b031633146104765760405162461bcd60e51b815260206004820152602560248201527f4f6e6c7920746865206f776e65722063616e2063616c6c20746869732066756e60448201526431ba34b7b760d91b60648201526084016103b7565b61047f836106c1565b6104bd5760405162461bcd60e51b815260206004820152600f60248201526e496e76616c6964206164647265737360881b60448201526064016103b7565b8160035f8282546104ce919061086f565b90915550506001600160a01b0383165f90815260046020526040812080548492906104fa90849061086f565b90915550506040518281526001600160a01b038416907f0f6798a560793a54c3bcfe86a93cde1e73087d944c0ea20544137d41213968859060200160405180910390a25060015b92915050565b60018054610231906107f5565b335f908152600460205260408120548211156105825760405162461bcd60e51b81526004016103b79061082d565b61058d338484610596565b50600192915050565b6001600160a01b0382166105de5760405162461bcd60e51b815260206004820152600f60248201526e496e76616c6964206164647265737360881b60448201526064016103b7565b6001600160a01b0383165f908152600460205260409020548111156106155760405162461bcd60e51b81526004016103b79061082d565b6001600160a01b0383165f908152600460205260408120805483929061063c908490610882565b90915550506001600160a01b0382165f908152600460205260408120805483929061066890849061086f565b92505081905550816001600160a01b0316836001600160a01b03167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef836040516106b491815260200190565b60405180910390a3505050565b5f6001600160a01b0382166106d757505f919050565b503b1590565b5f6020808352835180828501525f5b81811015610708578581018301518582016040015282016106ec565b505f604082860101526040601f19601f8301168501019250505092915050565b80356001600160a01b038116811461073e575f80fd5b919050565b5f805f60608486031215610755575f80fd5b61075e84610728565b925061076c60208501610728565b9150604084013590509250925092565b5f806040838503121561078d575f80fd5b61079683610728565b946020939093013593505050565b5f602082840312156107b4575f80fd5b6107bd82610728565b9392505050565b5f80604083850312156107d5575f80fd5b6107de83610728565b91506107ec60208401610728565b90509250929050565b600181811c9082168061080957607f821691505b60208210810361082757634e487b7160e01b5f52602260045260245ffd5b50919050565b602080825260149082015273496e73756666696369656e742062616c616e636560601b604082015260600190565b634e487b7160e01b5f52601160045260245ffd5b808201808211156105415761054161085b565b818103818111156105415761054161085b56fea2646970667358221220b93f8b1333aeda6203f8e1897846afb1399a3187c112bd1b3f6528b80b952f2164736f6c63430008140033",
        "data": "0x000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000000000000000000000000000000c0000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000001610000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000016100000000000000000000000000000000000000000000000000000000000000",
        "gasAssets": [
            "0x7C81161348F21cf77A011fAB74cf7ee0cdCC2347",
            "e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc"
        ],
        "info": "[]",
        "isFindUtxo": false,
        "nContractType": "0",
        "pubStr": "MCowBQYDK2VwAyEA+3NUeOwuiK70qXhpnzSZ8LKgOVmnX98mqcUi3O3MtNw=",
        "txInfo": "info"
    }
}
```

**Response**
- id                    Unique request identifier
- jsonRpc               JSON-RPC version
- method                Name of the called method of the called method 
- result                Response data:
  - code                Return value number
    -  0                Success
    - -1:               Input addr error
    - -2:               Created a deal height failed
    - -3:               The information entered exceeds the specified length
    - -4:               Get contractaddress failed
    - -5:               nContractType Invalid
    - -6:               Get CanBeRevoke AssetType fail
    - -300              Call contract error(Determine whether the balance is insufficient   according to the output error message )
    - -2004             The main network currency balance is insufficient
    - -13114            The main network currency balance is insufficient
    - -13116            Reward is less than gas
    - -13117            The main network currency balance is insufficient
  - contractJs          Finalized contract details 
  - message             Status code:  information (see code error Return information for details)
  - txJson              Signed transaction ready for broadcasting

```json
{
    "id": "",
    "jsonRpc": "",
    "method": "CreateDeployContractTransaction",
    "result": {
        "code": 0,
        "contractJs": "{\"version\":\"1_1.0.0_d\",\"txMsgReq\":{\"version\":\"1_1.0.0_d\",\"txMsgInfo\":{\"nodeHeight\":\"262\",\"txUtxoHeight\":\"262\",\"contractStorageList\":[\"cD38e9D64Bb5F4983B27932F355bbF699483F858\"]}}}",
        "message": "success",
        "txJson": "{\"time\":\"1743564369847935\",\"identity\":\"3Ab2973755533Fb6C429F1ecaC263c9fb3d6F433\",\"type\":\"tx\",\"consensus\":7,\"txType\":7,\"data\":\"{\\\"txInfo\\\":{\\\"blockPrevRandao\\\":4777,\\\"blockTimeStamp\\\":1743564370,\\\"input\\\":\\\"608060405234801562000010575f80fd5b5060405162000c0838038062000c08833981016040819052620000339162000156565b5f62000040858262000267565b5060016200004f848262000267565b506002805460ff191660ff93909316929092179091556003819055335f81815260046020526040902091909155600680546001600160a01b0319169091179055506200032f9050565b634e487b7160e01b5f52604160045260245ffd5b5f82601f830112620000bc575f80fd5b81516001600160401b0380821115620000d957620000d962000098565b604051601f8301601f19908116603f0116810190828211818310171562000104576200010462000098565b8160405283815260209250868385880101111562000120575f80fd5b5f91505b8382101562000143578582018301518183018401529082019062000124565b5f93810190920192909252949350505050565b5f805f80608085870312156200016a575f80fd5b84516001600160401b038082111562000181575f80fd5b6200018f88838901620000ac565b95506020870151915080821115620001a5575f80fd5b50620001b487828801620000ac565b935050604085015160ff81168114620001cb575f80fd5b6060959095015193969295505050565b600181811c90821680620001f057607f821691505b6020821081036200020f57634e487b7160e01b5f52602260045260245ffd5b50919050565b601f82111562000262575f81815260208120601f850160051c810160208610156200023d5750805b601f850160051c820191505b818110156200025e5782815560010162000249565b5050505b505050565b81516001600160401b0381111562000283576200028362000098565b6200029b81620002948454620001db565b8462000215565b602080601f831160018114620002d1575f8415620002b95750858301515b5f19600386901b1c1916600185901b1785556200025e565b5f85815260208120601f198616915b828110156200030157888601518255948401946001909101908401620002e0565b50858210156200031f57878501515f19600388901b60f8161c191681555b5050505050600190811b01905550565b6108cb806200033d5f395ff3fe608060405234801561000f575f80fd5b50600436106100e5575f3560e01c806370a0823111610088578063a9059cbb11610063578063a9059cbb146101d5578063c4e41b22146101e8578063dd62ed3e146101f0578063f0141d841461021a575f80fd5b806370a08231146101835780638da5cb5b146101a257806395d89b41146101cd575f80fd5b806318160ddd116100c357806318160ddd1461011757806323b872dd1461012e578063313ce5671461015157806340c10f1914610170575f80fd5b806306fdde03146100e9578063150704011461010757806317d7de7c1461010f575b5f80fd5b6100f1610225565b6040516100fe91906106dd565b60405180910390f35b6100f16102b0565b6100f1610340565b61012060035481565b6040519081526020016100fe565b61014161013c366004610743565b61034e565b60405190151581526020016100fe565b60025461015e9060ff1681565b60405160ff90911681526020016100fe565b61014161017e36600461077c565b61040c565b6101206101913660046107a4565b60046020525f908152604090205481565b6006546101b5906001600160a01b031681565b6040516001600160a01b0390911681526020016100fe565b6100f1610547565b6101416101e336600461077c565b610554565b600354610120565b6101206101fe3660046107c4565b600560209081525f928352604080842090915290825290205481565b60025460ff1661015e565b5f8054610231906107f5565b80601f016020809104026020016040519081016040528092919081815260200182805461025d906107f5565b80156102a85780601f1061027f576101008083540402835291602001916102a8565b820191905f5260205f20905b81548152906001019060200180831161028b57829003601f168201915b505050505081565b6060600180546102bf906107f5565b80601f01602080910402602001604051908101604052809291908181526020018280546102eb906107f5565b80156103365780601f1061030d57610100808354040283529160200191610336565b820191905f5260205f20905b81548152906001019060200180831161031957829003601f168201915b5050505050905090565b60605f80546102bf906107f5565b5f336001600160a01b038516146103c05760405162461bcd60e51b815260206004820152602b60248201527f596f752063616e206f6e6c79207472616e736665722066726f6d20796f75722060448201526a6f776e206164647265737360a81b60648201526084015b60405180910390fd5b6001600160a01b0384165f908152600460205260409020548211156103f75760405162461bcd60e51b81526004016103b79061082d565b610402848484610596565b5060019392505050565b6006545f906001600160a01b031633146104765760405162461bcd60e51b815260206004820152602560248201527f4f6e6c7920746865206f776e65722063616e2063616c6c20746869732066756e60448201526431ba34b7b760d91b60648201526084016103b7565b61047f836106c1565b6104bd5760405162461bcd60e51b815260206004820152600f60248201526e496e76616c6964206164647265737360881b60448201526064016103b7565b8160035f8282546104ce919061086f565b90915550506001600160a01b0383165f90815260046020526040812080548492906104fa90849061086f565b90915550506040518281526001600160a01b038416907f0f6798a560793a54c3bcfe86a93cde1e73087d944c0ea20544137d41213968859060200160405180910390a25060015b92915050565b60018054610231906107f5565b335f908152600460205260408120548211156105825760405162461bcd60e51b81526004016103b79061082d565b61058d338484610596565b50600192915050565b6001600160a01b0382166105de5760405162461bcd60e51b815260206004820152600f60248201526e496e76616c6964206164647265737360881b60448201526064016103b7565b6001600160a01b0383165f908152600460205260409020548111156106155760405162461bcd60e51b81526004016103b79061082d565b6001600160a01b0383165f908152600460205260408120805483929061063c908490610882565b90915550506001600160a01b0382165f908152600460205260408120805483929061066890849061086f565b92505081905550816001600160a01b0316836001600160a01b03167fddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef836040516106b491815260200190565b60405180910390a3505050565b5f6001600160a01b0382166106d757505f919050565b503b1590565b5f6020808352835180828501525f5b81811015610708578581018301518582016040015282016106ec565b505f604082860101526040601f19601f8301168501019250505092915050565b80356001600160a01b038116811461073e575f80fd5b919050565b5f805f60608486031215610755575f80fd5b61075e84610728565b925061076c60208501610728565b9150604084013590509250925092565b5f806040838503121561078d575f80fd5b61079683610728565b946020939093013593505050565b5f602082840312156107b4575f80fd5b6107bd82610728565b9392505050565b5f80604083850312156107d5575f80fd5b6107de83610728565b91506107ec60208401610728565b90509250929050565b600181811c9082168061080957607f821691505b60208210810361082757634e487b7160e01b5f52602260045260245ffd5b50919050565b602080825260149082015273496e73756666696369656e742062616c616e636560601b604082015260600190565b634e487b7160e01b5f52601160045260245ffd5b808201808211156105415761054161085b565b818103818111156105415761054161085b56fea2646970667358221220b93f8b1333aeda6203f8e1897846afb1399a3187c112bd1b3f6528b80b952f2164736f6c63430008140033000000000000000000000000000000000000000000000000000000000000008000000000000000000000000000000000000000000000000000000000000000c0000000000000000000000000000000000000000000000000000000000000000100000000000000000000000000000000000000000000000000000000000000010000000000000000000000000000000000000000000000000000000000000001610000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000016100000000000000000000000000000000000000000000000000000000000000\\\",\\\"recipient\\\":\\\"cD38e9D64Bb5F4983B27932F355bbF699483F858\\\",\\\"sender\\\":\\\"7C81161348F21cf77A011fAB74cf7ee0cdCC2347\\\",\\\"version\\\":0,\\\"virtualMachine\\\":0}}\",\"info\":\"aW5mbw==\",\"utxos\":[{\"owner\":[\"7C81161348F21cf77A011fAB74cf7ee0cdCC2347\"],\"vin\":[{\"prevOut\":[{\"hash\":\"7617d504ef6ec1436f81b1a3af71eff78afcbcd429ca1c3aa483cbe8975bed65\"}]}],\"vout\":[{\"value\":\"9980988089112\",\"addr\":\"7C81161348F21cf77A011fAB74cf7ee0cdCC2347\"},{\"value\":\"841255\",\"addr\":\"VirtualBurnGas\"}],\"assetType\":\"e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc\",\"gasUtxo\":\"1\"}],\"gasTx\":1}"
    }
}

```

### CreateCallContractTransaction

Creates a transaction to execute a function on a deployed smart contract.

**Request**
- id                 Unique request identifier
- jsonRpc            JSON-RPC version
- method             Name of the called method of the called method 
- params             Parameters:
  - addr             Blockchain address initiating the contract call
  - args             Arguments for the contract function (ABI-encoded hex strings)
  - contractAddress  Address of the deployed smart contract to interact with
  - deployer         Address that originally deployed the contract
  - deployUtxo       Transaction hash of the contract deployment
  - gasAssets        Select the currency type for paying gas fees
  - isFindUtxo       Whether to search the current status of UTXO across the entire network  
  - isToChain        Whether the transaction must be on-chain validated (true/false)
  - money            Native currency amount to send with the call
  - pubStr           Base64-encoded public key of the caller address
  - tip              Optional priority fee (tip)
  - txInfo           Contract ABI and function metadata


```json
{
    "id": "1",
    "jsonRpc": "",
    "method": "",
    "params": {
        "addr": "7C81161348F21cf77A011fAB74cf7ee0cdCC2347",
        "args": "18160ddd",
        "contractAddress": "0x0384c3a2222E5a176de4Ac7f97B3F111C35390e0",
        "deployer": "7C81161348F21cf77A011fAB74cf7ee0cdCC2347",
        "deployutxo": "0x0fffb9853b2c2a1a0f0017e31b604bc9a378dbb24eaeff275d2fb44b04590521",
        "gasAssets": [
            "7C81161348F21cf77A011fAB74cf7ee0cdCC2347",
            "e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc"
        ],
        "isFindUtxo": false,
        "istochain": "true",
        "money": "0",
        "pubstr": "MCowBQYDK2VwAyEA+3NUeOwuiK70qXhpnzSZ8LKgOVmnX98mqcUi3O3MtNw=",
        "tip": "0",
        "txInfo": "info"
    }
}
```

**Response**
- id              Unique request identifier
- jsonRpc         JSON-RPC version
- method          Name of the called method of the called method 
- result          Response data:
- code Return value number
  - 0             Success
  - -1:           from addr error
  - -2:           to addr error
  - -4:           money regex match error
  - -5：          db get top failed
  - -6：          The information entered exceeds the specified length
  - -7：          get contract transaction failed
  - -8：          contract transaction parse failed
  - -9：          Get CanBeRevoke AssetType fail
  - -10：         VmType is not EVM
  - -300          Contract execution failed (judging whether the balance is insufficient according to the output error message)
  - -2004         The main network currency balance is insufficient
  - -13114        The main network currency balance is insufficient
  - -13116        Reward is less than gas
  - -13117        The main network currency balance is insufficient
- contractJs      Post-execution contract state and logs
- message         Status code:  information (see the error Return information corresponding to code for details, omitted content is an internal error)
- txJson          Signed transaction ready for broadcasting
- 
```json
{
    "id": "1",
    "jsonRpc": "",
    "method": "CreateCallContractTransaction",
    "result": {
        "code": 0,
        "contractJs": "{\"version\":\"1_1.0.0_d\",\"txMsgReq\":{\"version\":\"1_1.0.0_d\",\"txMsgInfo\":{\"nodeHeight\":\"267\",\"txUtxoHeight\":\"267\",\"contractStorageList\":[\"0384c3a2222E5a176de4Ac7f97B3F111C35390e0\",\"0384c3a2222E5a176de4Ac7f97B3F111C35390e0\"]}}}",
        "message": "success",
        "txJson": "{\"time\":\"1743572180758433\",\"identity\":\"E2Daa42525026Ed5bDe70D4F5C2e53eF2AEd8248\",\"type\":\"Tx\",\"consensus\":7,\"txType\":8,\"data\":\"{\\\"txInfo\\\":{\\\"blockPrevRandao\\\":4748,\\\"blockTimestamp\\\":1743572180,\\\"contractDeployer\\\":\\\"7C81161348F21cf77A011fAB74cf7ee0cdCC2347\\\",\\\"input\\\":\\\"18160ddd\\\",\\\"output\\\":\\\"000000000000000000000000000000000000000000000000000000000000006f\\\",\\\"recipient\\\":\\\"0384c3a2222E5a176de4Ac7f97B3F111C35390e0\\\",\\\"sender\\\":\\\"7C81161348F21cf77A011fAB74cf7ee0cdCC2347\\\",\\\"transfer\\\":0,\\\"version\\\":0,\\\"virtualMachine\\\":0}}\",\"info\":\"aW5mbw==\",\"utxos\":[{\"owner\":[\"7C81161348F21cf77A011fAB74cf7ee0cdCC2347\"],\"vin\":[{\"prevOut\":[{\"hash\":\"261f96acc7ccf1d6d5f7fd288ec4a6df0d803fa76373b14485bbe6b5e9d90f7d\"}]}],\"vout\":[{\"value\":\"9980984751486\",\"addr\":\"7C81161348F21cf77A011fAB74cf7ee0cdCC2347\"},{\"value\":\"57084\",\"addr\":\"VirtualBurnGas\"}],\"assetType\":\"e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc\",\"gasUtxo\":\"1\"}],\"gasTx\":1}"
    }
}

```

### CreateStakeTransaction

Creates a staking transaction to participate in network consensus or delegated services.

**Request**:
- id                 Unique request identifier
- jsonRpc            JSON-RPC version
- method             Name of the called method of the called method 
- params             Parameters:
  - pledgeType       Type of staking: 0 = Validator node, 1 = Delegated staking
  - commissionRate   Commission rate for delegated staking
  - fromAddr         Staker's blockchain address
  - gasAssets        Select the currency type for paying gas fees
  - isFindUtxo       Whether to search the current status of UTXO across the entire network  
  - isGasAssets      Use other assets to pay for gas
  - stakeAmount      Amount to stake in atomic units
  - txInfo           Optional transaction description

```json
{
    "id": "",
    "jsonRpc": "",
    "method": "",
    "params": {
        "pledgeType": "0",
        "commissionRate": "5",
        "fromAddr": "0x7C81161348F21cf77A011fAB74cf7ee0cdCC2347",
        "gasAssets": [
            "7C81161348F21cf77A011fAB74cf7ee0cdCC2347",
            "e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc"
        ],
        "isFindUtxo": false,
        "isGasAssets": false,
        "stakeAmount": "100000",
        "txInfo": ""
    }
}
```
**Response**：
- id           Unique request identifier
- jsonRpc      JSON-RPC version
- method       Name of the called method of the called method 
- result       Response data:
  - code       Return value number
    -  0：     success
    - -1：     input pumping percentage error
    - -2：     Failed to get the current highest block height
    - -3：     Check parameters failed
    - -4：     From address invlaid
    - -5：     Stake amount is zero
    - -6：     The pledge amount must be greater than Minimum pledge value
    - -7：     Unknown stake type
    - -8：     There has been a pledge transaction before !
    - -9：     The information entered exceeds the specified length
    - -10：    FindUtxo failed
    - -11：    Utxo is empty
    - -12：    Tx owner is invalid
    - -13：    The commission ratio is not in the range
    - -14：    The gas charge cannot be 0
    - -15：    The total amount is less than gas
    - -16：    Check parameters failed
    - -17：    FindUtxo failed
    - -18：    Utxo is empty
    - -19：   Tx owner is empty
    - -20：    Failed to get the packager
    - -21：    Get Can BeRevoke AssetType fail
  - gas        Gas cost in atomic units
  - height     Current blockchain height when transaction was created
  - message    Status code:  message
  - time       UNIX timestamp of transaction creation
  - txJson     Unsigned staking transaction ready for broadcast
  - txType     Transaction type
  - vrfJson    Verifiable Random Json (VRF) parameters for validation

```json
{
    "id": "",
    "jsonRpc": "",
    "method": "CreateStakeTransaction",
    "result": {
        "code": 0,
        "gas": "28300",
        "height": "261",
        "message": "success",
        "time": "1743562886429830",
        "txJson": "{\"time\":\"1743562886429830\",\"identity\":\"4FA2d1Baab2a8c9285b1E8dFa05364B3780e41d4\",\"type\":\"Tx\",\"consensus\":7,\"txType\":2,\"data\":\"{\\\"txInfo\\\":{\\\"commissionRate\\\":0.05,\\\"stakeAmount\\\":10000000000000,\\\"stakeType\\\":\\\"Net\\\"}}\",\"utxos\":[{\"owner\":[\"7C81161348F21cf77A011fAB74cf7ee0cdCC2347\"],\"vin\":[{\"prevOut\":[{\"hash\":\"748bbd15f7a03d848a21b24af822302c4079fdacbb173727b52b20e8a08eb7a5\"}]}],\"vout\":[{\"value\":\"10000000000000\",\"addr\":\"VirtualStake\"},{\"value\":\"9980988930367\",\"addr\":\"7C81161348F21cf77A011fAB74cf7ee0cdCC2347\"},{\"value\":\"28300\",\"addr\":\"VirtualBurnGas\"}],\"assetType\":\"e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc\"}]}",
        "txType": "1",
        "vrfJson": "{}"
    }
}
```



### CreateUnStakeTransaction

Creates a transaction to unstake (withdraw) previously locked assets from a UTXO.

**Request**:
- id                 Unique request identifier
- jsonRpc            JSON-RPC version
- method             Name of the called method of the called method 
- params             Parameters:
  - fromAddr         Sender's blockchain address
  - gasAssets        Asset type and address for gas payment
  - isFindUtxo       Whether to search the current status of UTXO across the entire network  
  - isGasAssets      Use other assets to pay for gas
  - txInfo           Optional description/memo
  - utxoHash         UTXO hash to unstake from


```json
{
    "id": "",
    "jsonRpc": "",
    "method": "",
    "params": {
        "fromAddr": "0x7C81161348F21cf77A011fAB74cf7ee0cdCC2347",
        "gasAssets": [
            "0x7C81161348F21cf77A011fAB74cf7ee0cdCC2347",
            "e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc"
        ],
        "isFindUtxo": false,
        "isgasAssets": false,
        "txInfo": "",
        "utxoHash": "e4015855a1a23492dcb7b8e0aed956cd3ab5245cd08591fcad533777e8936128"
    }
}
```
**Response**：
- id          Unique request identifier
- jsonRpc     JSON-RPC version
- method      Name of the called method of the called method 
- result      Response data: 
  - code      Return value number
    -  0：    success
    - -1：    Failed to get the current highest block height
    - -2：    Check parameters failed
    - -3：    FromAddr is not normal addr.
    - -4：    FindUtxo failed
    - -5：    Utxo is empty
    - -6：    Tx owner is empty
    - -7：    The information entered exceeds the specified length
    - -8：    The gas charge cannot be 0
    - -9：    The total amount is less than expend
    - -10：   Check parameters failed
    - -11：   FindUtxo failed
    - -12：   Utxo is empty
    - -13：   Tx owner is empty
    - -14：   GetBlockPackager error
    - -15：   Get Can BeRevoke AssetType fail
    - -101：  Get all stake address failed
    - -102：  The account number has not staked assets
    - -103：  Get stake utxo from address failed
    - -104：  The utxo to be de staked is not in the staked utxo
    - -105：  The staked utxo is not more than 30 days
    - -106：  Stake tx not found
    - -107：  Failed to parse transaction body
    - -108：  Stake value is zero
  - gas       Gas cost in atomic units
  - height    Blockchain height when transaction was created
  - message   Status code:  message
  - time      UNIX timestamp of transaction creation
  - txJson    Unstake transaction ready for broadcast
  - txType    Transaction type
  - vrfJson   Verifiable Random Function (VRF) parameters for transaction validation
  - 
```json
{
    "id": "",
    "jsonRpc": "",
    "method": "CreateUnStakeTransaction",
    "result": {
        "code": 0,
        "gas": "45700",
        "height": "260",
        "message": "success",
        "time": "1743562471443339",
        "txJson": "{\"time\":\"1743562471443339\",\"identity\":\"8dcCa6EFFF82E9Ea9868f730ef91d1e688322561\",\"type\":\"tx\",\"consensus\":7,\"txType\":3,\"data\":\"{\\\"txInfo\\\":{\\\"unstakeUtxo\\\":\\\"e4015855a1a23492dcb7b8e0aed956cd3ab5245cd08591fcad533777e8936128\\\"}}\",\"utxos\":[{\"owner\":[\"7C81161348F21cf77A011fAB74cf7ee0cdCC2347\",\"7C81161348F21cf77A011fAB74cf7ee0cdCC2347\"],\"vin\":[{\"prevOut\":[{\"hash\":\"e4015855a1a23492dcb7b8e0aed956cd3ab5245cd08591fcad533777e8936128\",\"n\":1}]},{\"prevOut\":[{\"hash\":\"44b364a4b69c460049754ad65a39725c64e5ade03433e0c80779eb468801cb8e\"},{\"hash\":\"b6c7640039ae98a5f2b0eeedd95bcff6fe43f5d91c88edb6c5a9dc996875d220\"}],\"sequence\":1}],\"vout\":[{\"value\":\"10000000000000\",\"addr\":\"7C81161348F21cf77A011fAB74cf7ee0cdCC2347\"},{\"value\":\"9980988958667\",\"addr\":\"7C81161348F21cf77A011fAB74cf7ee0cdCC2347\"},{\"value\":\"45700\",\"addr\":\"VirtualBurnGas\"}],\"assetType\":\"e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc\"}]}",
        "txType": "1",
        "vrfJson": "{}"
    }
}

### CreateInvestTransaction

Creates a transaction to invest assets into a designated node or protocol.

**Request**:
- id                Unique request identifier
- jsonRpc           JSON-RPC version
- method            Name of the called method of the called method 
- params            Parameters:
  - assetType       Transfer asset type hash
  - fromAddr        Investor's blockchain address
  - gasAssets       Select the currency type for paying gas fees
  - investAmount    Investment amount 
  - investType      Type of investment
  - isFindUtxo      Whether to search the current status of UTXO across the entire network
  - isGasAssets     Use other assets to pay for gas
  - toAddr          Investee's blockchain address
  - txInfo          Optional description/metadata for the transaction

```json
{
    "id": "",
    "jsonrpc": "",
    "method": "",
    "params": {
        "assetType": "e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc",
        "fromAddr": "0x9573b641A035a6dA6333890317B54A7DFd17622f",
        "gasAssets": [
            "0x9573b641A035a6dA6333890317B54A7DFd17622f",
            "e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc"
        ],
        "investAmount": "700000",
        "investType": "0",
        "isFindUtxo": false,
        "isGasAssets": false,
        "toAddr": "0x9573b641A035a6dA6333890317B54A7DFd17622f",
        "txInfo": ""
    }
}
```
**Response**：
- id            Unique request identifier
- jsonRpc       JSON-RPC version
- method        Name of the called method of the called method 
- result        Response data:
  - code        Return value number
    -  0：      success
    - -1：      Failed to get the current highest block height
    - -2：      Check parameters failed
    - -3：      The initiator address is incorrect
    - -4：      The receiver address is incorrect
    - -5：      investment amount less 35
    - -6：      Unknown invest type
    - -7：      The information entered exceeds the specified length
    - -8：      FindUtxo failed
    - -9：      Utxo is empty
    - -10：     Tx owner is empty
    - -11：     gas cannot be 0
    - -12：     The total amount is less than expend
    - -13：     Check parameters failed
    - -14：     FindUtxo failed
    - -15：     Utxo is empty
    - -16：     Tx owner is empty
    - -17：     GetBlockPackager error
    - -101：    The investor have already invested in a node
    - -102：    The investment amount is less than 35
    - -103：    The account to be invested has not spent 500 to access the Internet
    - -104：    Get invest addrs by node failed
    - -105：    The account number to be invested have been invested by 9999 people
    - -106：    GetBonusAddrInvestAddrUtxoByBonusAddr failed
    - -107：    GetTransactionByHash failed
    - -108：    Failed to parse transaction body
    - -109：    The total amount invested in a single node will be more than 3500000
    - -110：    The asset type is Vote
  - gas         Gas cost in atomic units
  - height      Blockchain height when transaction was created
  - message     Status code:  message
  - time        UNIX timestamp of transaction creation
  - txJson      Investment transaction ready for broadcast
  - txType      Transaction type
  - vrfJson     Verifiable Random Function (VRF) parameters for transaction validation
```json
{
    "id": "",
    "jsonrpc": "",
    "method": "CreateInvestTransaction",
    "result": {
        "code": 0,
        "gas": "32100",
        "height": "270",
        "message": "success",
        "time": "1743572900452768",
        "txJson": "{\"time\":\"1743572900452768\",\"identity\":\"34D57041e90E17e3D880b90E1E93c93347D63918\",\"type\":\"Tx\",\"consensus\":7,\"txType\":4,\"data\":\"{\\\"TxInfo\\\":{\\\"BonusAddr\\\":\\\"9573b641A035a6dA6333890317B54A7DFd17622f\\\",\\\"InvestAmount\\\":70000000000000,\\\"InvestType\\\":\\\"Normal\\\"}}\",\"utxos\":[{\"owner\":[\"9573b641A035a6dA6333890317B54A7DFd17622f\"],\"vin\":[{\"prevOut\":[{\"hash\":\"b2344b1587f1ee92f98d6261d71f9c20e8722187b9fde898c2f97097a531aed5\"}]}],\"vout\":[{\"value\":\"70000000000000\",\"addr\":\"VirtualInvest\"},{\"value\":\"19999999939600\",\"addr\":\"9573b641A035a6dA6333890317B54A7DFd17622f\"},{\"value\":\"32100\",\"addr\":\"VirtualBurnGas\"}],\"assetType\":\"e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc\"}]}",
        "txType": "1",
        "vrfJson": "{}"
    }
}
```



### CreateDivestTransaction

Creates a transaction to divest (withdraw) assets from a previously invested node .
**Request**:
- id                Unique request identifier
- jsonRpc           JSON-RPC version
- method            Name of the called method of the called method 
- params            Parameters:
  - assetType       Transfer asset type hash
  - fromAddr        Investor's blockchain address
  - gasAssets       Select the currency type for paying gas fees
  - utxoHash        UTXO hash to divest from
  - isFindUtxo      Whether to search the current status of UTXO across the entire network
  - isGasAssets     Use other assets to pay for gas
  - toAddr          Investee's blockchain address
  - txInfo          Optional description/metadata for the transaction

```json
{
    "id": "",
    "jsonrpc": "",
    "method": "",
    "params": {
        "assetType": "e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc",
        "fromAddr": "0x9573b641A035a6dA6333890317B54A7DFd17622f",
        "gasAssets": [
            "0x9573b641A035a6dA6333890317B54A7DFd17622f",
            "e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc"
        ],
        "utxoHash": "0xdb2caaf71ff57ec954e67cabede4a4b2207fd8645e684e66983eaefea63f4e2a",
        "isFindUtxo": false,
        "isGasAssets": false,
        "toAddr": "0x9573b641A035a6dA6333890317B54A7DFd17622f",
        "txInfo": ""
    }
}
```
**Response**：
- id            Unique request identifier
- jsonRpc       JSON-RPC version
- method        Name of the called method of the called method 
- code          Return value number
  -  0：        success
  - -1：        Failed to get the current highest block height
  - -2：        Check parameters failed 
  - -3：        FromAddr is not normal addr.
  - -4：        To address is not normal addr.
  - -5：        The information entered exceeds the specified length
  - -6：        FindUtxo failed
  - -7：        Utxo is empty
  - -8：        Tx owner is empty
  - -9：        gas cannot be 0
  - -10：       The total amount is less than expend
  - -11：       Check parameters failed
  - -12：       FindUtxo failed
  - -13：       Utxo is empty
  - -14：       Tx owner is empty
  - -15：       GetBlockPackager error
  - -101：      GetBonusAddrByInvestAddr failed
  - -102：      The account has not invested assets to node
  - -103：      GetBonusAddrInvestAddrUtxoByBonusAddr failed
  - -104：      The utxo to divest is not in the utxos that have been invested
  - -105：      The invested utxo is not more than 1 day
  - -106：      Invest tx not found
  - -107：      Failed to parse transaction body
  - -108：      The node to be divested is not invested
  - -109：      The invested value is zero
  - -110：      The asset type is vote
- gas           Gas cost in atomic units
- height        Blockchain height when transaction was created
- message       Status code:  message
- time          UNIX timestamp of transaction creation 
- txJson        Divestment transaction ready for broadcast
- txType        Transaction type
- vrfJson       Verifiable Random Function (VRF) parameters for transaction validation

```json
{
    "id": "",
    "jsonrpc": "",
    "method": "CreateDivestTransaction",
    "result": {
        "code": 0,
        "gas": "32100",
        "height": "270",
        "message": "success",
        "time": "1743572900452768",
        "txJson": "{\"time\":\"1743572900452768\",\"identity\":\"34D57041e90E17e3D880b90E1E93c93347D63918\",\"type\":\"tx\",\"consensus\":7,\"txType\":4,\"data\":\"{\\\"txInfo\\\":{\\\"bonusAddr\\\":\\\"9573b641A035a6dA6333890317B54A7DFd17622f\\\",\\\"DisinvestUtxo\\\":0xdb2caaf71ff57ec954e67cabede4a4b2207fd8645e684e66983eaefea63f4e2a,}}\",\"utxos\":[{\"owner\":[\"9573b641A035a6dA6333890317B54A7DFd17622f\"],\"vin\":[{\"prevOut\":[{\"hash\":\"b2344b1587f1ee92f98d6261d71f9c20e8722187b9fde898c2f97097a531aed5\"}]}],\"vout\":[{\"value\":\"70000000000000\",\"addr\":\"VirtualInvest\"},{\"value\":\"19999999939600\",\"addr\":\"9573b641A035a6dA6333890317B54A7DFd17622f\"},{\"value\":\"32100\",\"addr\":\"VirtualBurnGas\"}],\"assetType\":\"e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc\"}]}",
        "txType": "1",
        "vrfJson": "{}"
    }
}

```



### CreateBonusTransaction

Creates a transaction to claim staking or investment rewards for a specified address.

**Request**:
- id                 Unique request identifier
- jsonRpc            JSON-RPC version
- method             Name of the called method of the called method 
- params             Parameters:
  - addr             Address eligible for bonus claims
  - assetType        Transfer asset type hash
  - gasAssets         Use other assets to pay for gas
  - isFindUtxo          Whether to search the current status of UTXO across the entire network
  - isGasAssets         Use other assets to pay for gas
  - txInfo              Optional description/metadata for the transaction
```json
{
    "id": "",
    "jsonrpc": "",
    "method": "",
    "params": {
        "addr": "4FA2d1Baab2a8c9285b1E8dFa05364B3780e41d4",
        "assetType": "e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc",
        "gasAssets": [
            "4FA2d1Baab2a8c9285b1E8dFa05364B3780e41d4",
            "e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc"
        ],
        "isFindUtxo": false,
        "isGasAssets": true,
        "txInfo": ""
    }
}
```

**Response**：
- id            Unique request identifier
- jsonRpc       JSON-RPC version
- method        Name of the called method of the called method 
- result        Response data:  
  - code        Return value number
    -  0：      success
    - -1：      Failed to get the current highest block height
    - -2：      Description Failed to obtain the balance of type X from the database based on the current type
    - -3：      Description Failed to obtain the jump asset type
    - -4：      Check parameters failed
    - -5：      The bouns address is incorrect
    - -6：      The information entered exceeds the specified length
    - -7：      Failed to obtain the amount claimed by the investor
    - -8：      FindUtxo failed
    - -9：      Utxo is zero
    - -10：     Tx owner is empty
    - -11：     GetCommissionPercentage error
    - -12：     The gas charge cannot be 0
    - -13：     The total cost = {} is less than the cost
    - -14：     The claim amount is 0
    - -15：     Extra Gas Trade Check parameters failed
    - -16：     Extra Gas Trade FindUtxo failed
    - -17:      Utxo is empty
    - -18:      Tx owner is empty
    - -19：     GetBlockPackager fail
    - -101:     The bouns time is not within the prescribed limits
    - -102:     Incorrect time
    - -103:     GetBonusUtxoByPeriod fail
    - -104:     GetTransactionByHash fail
    - -105:     Failed to parse transaction body
    - -106:     GetBonusUtxoByPeriod fail
    - -107:     VerifyBonusAddr fail
    - -108:     The bouns address is not pledged
  - gas         Gas cost in atomic units
  - height      Current blockchain height when transaction was created
  - message     Status code:  message
  - time        UNIX timestamp of transaction creation 
  - txJson      Reward claim transaction ready for broadcast
  - txType      Transaction type
  - vrfJson     Verifiable Random Function (VRF) parameters for transaction validation
```json
{
    "id": "",
    "jsonrpc": "",
    "method": "CreateBounsTransaction",
    "result": {
        "code": 0,
        "gas": "25800",
        "height": "273",
        "message": "success",
        "time": "1743682444422900",
        "txJson": "{\"time\":\"1743682444422900\",\"identity\":\"752027C61E8F285F30798cb5f7D0e63861f27dDd\",\"type\":\"tx\",\"consensus\":7,\"txType\":99,\"data\":\"{\\\"TxInfo\\\":{\\\"bonusAddrList\\\":3,\\\"bonusAmount\\\":42498630136}}\",\"utxos\":[{\"owner\":[\"4FA2d1Baab2a8c9285b1E8dFa05364B3780e41d4\"],\"vin\":[{\"prevOut\":[{\"hash\":\"c2d755a6ad2cd6e69f1348fd5b357987163f8fad351d879ae484f29dd0aba989\"}]}],\"vout\":[{\"value\":\"27624109588\",\"addr\":\"4FA2d1Baab2a8c9285b1E8dFa05364B3780e41d4\"},{\"value\":\"14874520548\",\"addr\":\"4FA2d1Baab2a8c9285b1E8dFa05364B3780e41d4\"},{\"addr\":\"VirtualBurnGas\"}],\"assetType\":\"Vote\"},{\"owner\":[\"4FA2d1Baab2a8c9285b1E8dFa05364B3780e41d4\"],\"vin\":[{\"prevOut\":[{\"hash\":\"c2d755a6ad2cd6e69f1348fd5b357987163f8fad351d879ae484f29dd0aba989\"}]}],\"vout\":[{\"value\":\"9999999913400\",\"addr\":\"4FA2d1Baab2a8c9285b1E8dFa05364B3780e41d4\"},{\"value\":\"25800\",\"addr\":\"VirtualBurnGas\"}],\"assetType\":\"e9107b1f5a2ee7d6ed2ef8d42aea6429cf9b52d550650bfb3487123763cfa4fc\",\"gasUtxo\":\"1\"}],\"gasTx\":1}",
        "txType": "1",
        "vrfJson": "{}"
    }
}
```

## Co-governing agreement

### GetAllAssertType

**Description**

Retrieves a list of all supported asset types on the blockchain network.

**Request**

* id            Unique request identifier
* jsonRpc       JSON-RPC version

**Response**

- id            Unique request identifier
- jsonRpc       JSON-RPC version
- method        Echoed method name 
- result        Return information
  - code        Return value number
    - 0	        Success
    - -1        Get asset type error
  - assertType  List of asset types
```json
req:
{
    "id":"1",
    "jsonRpc":"2.0"
}

ack:
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetAllAssertType",
  "result": {
    "assertType": [
      "0x44b90ac31b70805ced1f6c7884c0b8eb24b78b63689c6d3b19f42fbf11b28b6b",
      "0x416ba3e59614072c3bbdfb4f194fe71d248a7d82b1727f2d4ca51f8b4aba1528",
      "0xd3e8eba0d3eeae87c17c9ab2d4e42fa436374e111b631f71824e7a08ce2b03e8"
    ],
    "code": 0,
    "message": "success"
  }
}
```

------

### GetAssertTypeInfo

**Description**

Retrieves detailed information about active and revoked governance proposals.

**Request**

* id            Unique request identifier
* jsonRpc       JSON-RPC version
* params
  * assetType   Asset type

**Response**

- id                        Unique request identifier
- jsonRpc                   JSON-RPC version
- method                    Name of the called method of the called method
- result                    Return information
  - code                    Return value number
    - 0	                    Success
    - -1                    Get asset info error
    - -2                    Get revoke tx hash error
    - -3                    Get revoke proposal info error
- proposalInfo              Proposalinfo (in JSON format)
  - beginTime               Proposal start Time Timestamp (subtle)
  - endTime                 Proposal end time Timestamp (subtle)
  - contractAddr            Indicates the contract address
  - exchangeRate            Asset conversion rate
  - expirationDate          Expiration date (currently reserved field)
  - name                    Asset name (Base64)
  - canBeStake              Whether the current asset can be pledged (whether it is an S asset) 1: can be  pledged 0: can not be pledged
  - minVoteNum              Specifies the minimum number of votes
  - identifier              Unique proposal ID
  - title                   Human-readable proposal title
  - version                 Contract version
- revokeProposalInfo        Information about the withdrawal proposal (in JSON format)
  - beginTime               Revoking proposal start Time timestamp (subtle)
  - endTime                 End time of withdrawal proposal timestamp (subtle)
  - proposalHash            ProposalHash
  - revokeProposalHash      Transaction hash of the revocation action
  - minVoteNum              Specifies the minimum number of votes
  - version                 Version

```json
req:
{
    "id":"1",
    "jsonRpc":"2.0",
    "params":{"assetType":"0c23a6a11119065dc9bd32197bda6aab58abf8f1519bddb4d8009f01da9830ee"}
}
ack:
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetAssertTypeInfo",
  "result": {
    "code": 0,
    "message": "success",
    "proposalInfo": "{\"beginTime\":1740990051747766,\"canBeStake\":0,\"contractAddr\":\"0x5f2ECcfd8dBA119832464ce93777ec770A4A617b\",\"endTime\":1740990771747766,\"exchangeRate\":\"1\",\"expirationDate\":18446744073709551615,\"identifier\":\"MTEx\",\"minVoteNum\":1,\"name\":\"Qg==\",\"title\":\"MTE=\",\"version\":0}",
    "revokeProposalInfo": [
      "{\"beginTime\":1741141725928616,\"endTime\":1741142445928616,\"minVoteNum\":4,\"proposalHash\":\"0x0c23a6a11119065dc9bd32197bda6aab58abf8f1519bddb4d8009f01da9830ee\",\"revokeProposalHash\":\"0x8028ec7742c3f7e7cbcf4e3deabc095770df6300a424d8cc44caaae2b582af07\",\"version\":0}"
    ]
  }
}
```

------

### GetVoteTxHash

**Description**

Retrieves all voting transaction hashes associated with a governance proposal or its revocation.

**Request**

* id Unique request identifier
* jsonRpc  JSON-RPC version
* params
  * hash  Proposal type hash or revocation proposal type hash

**Response**

- id          Unique request identifier
- jsonRpc     JSON-RPC version
- method      Name of the called method of the called method
- result      Return information
  - code      Return value number
    - 0	      Success
    - -1      Get vote tx hash error

```json
req:
{
    "id":"1",
    "jsonRpc":"2.0",
    "params":{"hash":"0x416ba3e59614072c3bbdfb4f194fe71d248a7d82b1727f2d4ca51f8b4aba1528"}
}
ack:
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetVoteTxHash",
  "result": {
    "code": 0,
    "message": "success",
    "txHashs": [
      "0x414a16d5316448ea36775412defd79ec870150803575e0c53e12a11bc1c25d05"
    ]
  }
}
```

------

### GetVoteAddrs

**Description**

Retrieves all voting addresses for/against a governance proposal or revocation proposal.

**Request**

* id        Unique request identifier
* jsonRpc   JSON-RPC version
* params
  * hash    Proposal type hash or revocation proposal type hash

**Response**

- id              Unique request identifier
- jsonRpc         JSON-RPC version
- method          Name of the called method of the called method
- result          Return information
  - code          Return value number
    - 0	          Success
    - -1          Get approve addrs error
    - -2          Get against addrs error
  - againstAddrs  Address to vote against
  - approveAddrs  Indicates the yes vote address

```json
req:
{
    "id":"1",
    "jsonRpc":"2.0",
    "params":{"hash":"0x416ba3e59614072c3bbdfb4f194fe71d248a7d82b1727f2d4ca51f8b4aba1528"}
}
ack:
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetVoteAddrs",
  "result": {
    "againstAddrs": [],
    "approveAddrs": [
      "0xffFd42e045737b11570B7981c2648ea532a10B23"
    ],
    "code": 0,
    "message": "success"
  }
}
```

------

### CreateLockTransaction

**Description**

Creates a transaction to lock a specified amount of assets (default: 1000 units) at a blockchain address.

**Request**：

* id                    Unique request identifier
* jsonRpc               JSON-RPC version
* params                Parameters:
  * lockType            Lock type The default value is 0
  * fromAddr            Indicates the lock address
  * isFindUtxo          Whether to query Utxo
  * isGasAssets         Use other assets to pay for gas
  * address             Contract address of the gas payment asset
  * lockAmount          Specifies the lockout amount
  * txInfo              Optional description/metadata for the transaction

**Response**：

* id          Unique request identifier
* jsonRpc     JSON-RPC version
* method      Name of the called method of the called method
* result      Return information
  - code      Return value number
    - 0	      Success
    - -1      db get top failed!
    - -2      Check parameters failed!
    - -3      From address invlaid
    - -4      The pledge amount error
    - -5      Unknown lock type! 
    - -6      The information entered exceeds the specified length
    - -7      There has been a lock transaction before !
    - -8      FindUtxo failed
    - -9      Utxo is empty
    - -10     Tx owner is invalid!
    - -11     gas = 0 !
    - -12     The total cost is less than the cost
    - -13     Check parameters failed
    - -14     FindUtxo failed
    - -15     Gas utxo is empty
    - -16     Tx owner is empty!
    - -17     Failed to get the packager
    - -18     LockAmount format error
  - height    Current blockchain height when transaction was created
  - time      UNIX timestamp of transaction creation
  - txJson    Transaction ready for broadcast

```json
req:
{
    "id": "",
    "jsonRpc": "",
    "params": {
        "lockType": "0",
        "fromAddr": "0x3CD050678178A3029E7436A661694237589AF868",
        "gasAssets": [
            "0x3CD050678178A3029E7436A661694237589AF868",
            "6f1eee7e83bed73cfe2cd9533c1fc795a4ee344984a0372479fab7635c44889a"
        ],
        "isFindUtxo": false,
        "isGasAssets": true,
        "lockAmount": "1000",
        "txInfo": ""
    }
}
ack:
{
  "id": "",
  "jsonRpc": "",
  "method": "CreateLockTransaction",
  "result": {
    "code": 0,
    "gas": "",
    "height": "1046",
    "message": "success",
    "time": "1741081616280062",
    "txJson": "{\"time\":\"1741081616280062\",\"identity\":\"3CD050678178A3029E7436A661694237589AF868\",\"type\":\"tx\",\"consensus\":7,\"txType\":9,\"data\":\"{\\\"txInfo\\\":{\\\"lockAmount\\\":100000000000,\\\"lockType\\\":\\\"lockNet\\\"}}\",\"utxos\":[{\"owner\":[\"3CD050678178A3029E7436A661694237589AF868\"],\"vin\":[{\"prevOut\":[{\"hash\":\"9056df2e966eaee88499effc3d5976c6a4534a23335daf81c2b9501d26be47b1\"}]}],\"vout\":[{\"value\":\"100000000000\",\"addr\":\"lockVirtualStake\"},{\"value\":\"32575342465\",\"addr\":\"3CD050678178A3029E7436A661694237589AF868\"},{\"addr\":\"VirtualBurnGas\"}],\"assetType\":\"X\"},{\"owner\":[\"3CD050678178A3029E7436A661694237589AF868\"],\"vin\":[{\"prevOut\":[{\"hash\":\"f6bf68016abb9927be848021ce8e0eccefa2bde96ae062896fee682dd0a46820\"}]}],\"vout\":[{\"value\":\"80001999907200\",\"addr\":\"3CD050678178A3029E7436A661694237589AF868\"},{\"value\":\"26000\",\"addr\":\"VirtualBurnGas\"}],\"assetType\":\"6f1eee7e83bed73cfe2cd9533c1fc795a4ee344984a0372479fab7635c44889a\",\"gasUtxo\":\"1\"}],\"gasTx\":1}",
    "txType": "1",
    "vrfJson": "{}"
  }
}
```

------

### GetLockUtxo

**Description**

Retrieves locked UTXOs (Unspent Transaction Outputs) associated with a specified blockchain address.

**Request**

* id          Unique request identifier
* jsonRpc     JSON-RPC version
* params      Parameters:
  * fromAddr  Address to check

**Response**

- id        nique request identifier
- jsonRpc   JSON-RPC version
- method    Name of the called method of the called method
- result    Return information
  - code    Return value number
    - 0	    Success
    - -1    fromaddr not lock!
    - -2    get transaction error
    - -3    parse transaction error
  - utxos   Locked utxo hash and locked amount 

```json
req:
{
    "id": "1",
    "jsonRpc": "2.0",
    "params": {
        "fromAddr": "0xffFd42e045737b11570B7981c2648ea532a10B23"
    }
}
ack:
{
  "id": "1",
  "jsonRpc": "2.0",
  "method": "GetLockUtxo",
  "result": {
    "code": 0,
    "message": "success",
    "utxos": [
      "70da8e27db29177361514726446b5689ad318ba926530958e777ac5657ec5236",
      100000000000
    ]
  }
}
```

------

### CreateUnLockTransaction

**Description**：

Creates a transaction to unlock previously locked assets for a specified address.

**Request**：

* id                  Unique request identifier
* jsonRpc             JSON-RPC version
* params              Parameters:
  * fromAddr          Indicates the lock address
  * utxoHash          The utxo when unlocked
  * isFindUtxo        Whether to query Utxo
  * isGasAssets        Use other assets to pay for gas
  * gasAssets          Asset type and address for gas payment
  * txInfo            Optional description/metadata for the transaction

**Response**：

* id                  Unique request identifier
* jsonRpc             JSON-RPC version
* method              Name of the called method of the called method
* result              Return information
  - code              Return value number
    - 0	              Success
    - -1              db get top failed!
    - -2              The information entered exceeds the specified length
    - -3              Check parameters failed
    - -4              FromAddr is not normal  addr
    - -5              FromAddr is not qualified to unlock
    - -6              FindUtxo failed
    - -7              Utxo is empty
    - -8              Tx owner is empty
    - -9              gas = 0
    - -10             The total cost  is less than the cost
    - -11             Check parameters failed
    - -12             FindUtxo failed
    - -13             Utxo is empty
    - -14             Tx owner is empty
    - -15             GetBlockPackager error
  - height            Current blockchain height when transaction was created
  - time              UNIX timestamp of transaction creation
  - txJson            Unlock transaction ready for broadcast:

```json
req:
{
    "id": "1",
    "jsonRpc": "2,0",
    "method": "",
    "params": {
        "fromAddr": "0x3CD050678178A3029E7436A661694237589AF868",
        "gasAssets": [
            "0x3CD050678178A3029E7436A661694237589AF868",
            "6f1eee7e83bed73cfe2cd9533c1fc795a4ee344984a0372479fab7635c44889a"
        ],
        "isFindUtxo": false,
        "isGasAssets": false,
        "txInfo": "",
        "utxoHash": "8d9253fb2ecfe3e8ff698de172a396739d70208fb07ad7bf9e0b0385ed987bf5"
    }
}

ack:
{
  "id": "1",
  "jsonRpc": "2,0",
  "method": "CreateUnLockTransaction",
  "result": {
    "code": 0,
    "gas": "",
    "height": "1070",
    "message": "success",
    "time": "1741154556596941",
    "txJson": "{\"time\":\"1741154556596941\",\"identity\":\"C776F881bC6c6763821f3e3b3c1E2625B522ee0d\",\"type\":\"tx\",\"consensus\":7,\"txType\":10,\"data\":\"{\\\"txInfo\\\":{\\\"unLockUtxo\\\":\\\"8d9253fb2ecfe3e8ff698de172a396739d70208fb07ad7bf9e0b0385ed987bf5\\\"}}\",\"utxos\":[{\"owner\":[\"3CD050678178A3029E7436A661694237589AF868\",\"3CD050678178A3029E7436A661694237589AF868\"],\"vin\":[{\"prevOut\":[{\"hash\":\"8d9253fb2ecfe3e8ff698de172a396739d70208fb07ad7bf9e0b0385ed987bf5\",\"n\":1}]},{\"prevOut\":[{\"hash\":\"8d9253fb2ecfe3e8ff698de172a396739d70208fb07ad7bf9e0b0385ed987bf5\"}],\"sequence\":1}],\"vout\":[{\"value\":\"10000000000\",\"addr\":\"3CD050678178A3029E7436A661694237589AF868\"},{\"value\":\"32575237865\",\"addr\":\"3CD050678178A3029E7436A661694237589AF868\"},{\"value\":\"39200\",\"addr\":\"VirtualBurnGas\"}],\"assetType\":\"X\"}]}",
    "txType": "1",
    "vrfJson": "{}"
  }
}
```

------

### CreateVoteTransaction

**Description**：

Creates a transaction to vote for/against a governance proposal or its revocation.

**Request**：

* id                  Unique request identifier
* jsonRpc             JSON-RPC version
* params              Parameters:
  * fromAddr          Voting address
  * gasAssets    Address and asset name of gasAssets to pay gas
  * isFindUtxo        Whether to query Utxo
  * pollType          Indicates that 0 indicates no and 1 indicates yes
  * voteHash          Proposal type or revocation proposal type hash
  * voteTxType        Voting type 11: Proposal type 12: Revoke proposal type
  * txInfo            Optional description/metadata for the transaction

**Response**：

* id                  Unique request identifier
* jsonRpc             JSON-RPC version
* method              Name of the called method of the called method
* result              Return information
  - code              Return value number
    - 0	              Success
    - -1              db get top failed!
    - -2              The information entered exceeds the specified length
    - -3              FromAddr is not normal addr
    - -4              Check parameters failed
    - -5              FromAddr is not qualified to unlock
    - -6              Check vote tx info error
    - -7              FindUtxo failed!
    - -8              Utxo is empty
    - -9              Tx owner is empty
    - -10             gas = 0
    - -11             The total cost is less than the cost
    - -12             Find block packager error
  - height            Current blockchain height when transaction was created
  - time              UNIX timestamp of transaction creation
  - txJson            Vote transaction ready for broadcast

```json
req:
{
    "id": "",
    "jsonRpc": "",
    "method": "",
    "params": {
        "fromAddr": "0x3CD050678178A3029E7436A661694237589AF868",
        "gasAssets": [
            "0x3CD050678178A3029E7436A661694237589AF868",
            "556fc975c75073a7a76acc4990d0b68d79f97af971674ccb9b2d46d61d76ae1b"
        ],
        "isFindUtxo": false,
        "pollType": "1",
        "txInfo": "",
        "voteHash": "6df465a89c945f1a2ca5b429c8a2f3e656920c26d39026e122a01ecf9de998c6",
        "voteTxType": "11"
    }
}

ack:
{
  "id": "",
  "jsonRpc": "",
  "method": "CreateVoteTransaction",
  "result": {
    "code": 0,
    "gas": "",
    "height": "1070",
    "message": "success",
    "time": "",
    "txJson": "{\"time\":\"1741154374038148\",\"identity\":\"C776F881bC6c6763821f3e3b3c1E2625B522ee0d\",\"type\":\"tx\",\"consensus\":7,\"txType\":13,\"data\":\"{\\\"txInfo\\\":{\\\"voteHash\\\":\\\"6df465a89c945f1a2ca5b429c8a2f3e656920c26d39026e122a01ecf9de998c6\\\",\\\"voteTxType\\\":11,\\\"voteType\\\":1}}\",\"utxos\":[{\"owner\":[\"3CD050678178A3029E7436A661694237589AF868\"],\"vin\":[{\"prevOut\":[{\"hash\":\"6367c45ba4c30b72acd493e36c863547e80b131cda2473f3c956f3b34d2eea8a\"}]}],\"vout\":[{\"value\":\"29999936200\",\"addr\":\"3CD050678178A3029E7436A661694237589AF868\"},{\"value\":\"28700\",\"addr\":\"VirtualBurnGas\"}],\"assetType\":\"556fc975c75073a7a76acc4990d0b68d79f97af971674ccb9b2d46d61d76ae1b\",\"gasUtxo\":\"1\"}],\"gasTx\":1}",
    "txType": "1",
    "vrfJson": "{}"
  }
}
```

------

### CreateFundTransaction

**Description**：

Creates a transaction to claim gas fee rewards from the network treasury.

**Request**：

* id            Unique request identifier
* jsonRpc       JSON-RPC version
* method        Name of the called method of the called method
* params        Parameters:
  * fromAddr    get fund address
  * isFindUtxo  Is or not inquired Utxo
  * txInfo      Optional description/metadata for the transaction

```json
req:
{
    "id": "1",
    "jsonRpc": "2.0",
    "method": "CreateFundTransaction",
    "params": {
        "fromAddr": "0x3CD050678178A3029E7436A661694237589AF868",
        "isFindUtxo": false,
        "txInfo": ""
    }
}
```
**Response**：

* id            Unique request identifier
* jsonRpc       JSON-RPC version
* method        Name of the called method of the called method
* result        Return information
  - code        Return value number
    - 0	        Success
    - -1        db get top failed!
    - -2        The information entered exceeds the specified length
    - -3        Default is not normal  addr.
    - -4        Get available asset fail!
    - -5        GetGasamountbyTimeType error!
    - -6        Nodes are not eligible to claim treasury
    - -7        Sign Utxo fail!
    - -8        Utxo is empty
    - -9        Tx owner is empty
    - -10       gas = 0
    - -11       The total cost is less than the cost
    - -12       Find block packager error
    - -13       GetIdentityNodes fail!!! ret
    - -99       Verify bonus address fail
  - height      Current blockchain height when transaction was created
  - time        UNIX timestamp of transaction creation
  - txJson      Treasury claim transaction:

```json
ack:
{
  "id": "",
  "jsonRpc": "",
  "method": "CreateFundTransaction",
  "result": {
    "code": 0,
    "gas": "",
    "height": "1070",
    "message": "success",
    "time": "",
    "txJson": "{\"time\":\"1741154374038148\",\"identity\":\"C776F881bC6c6763821f3e3b3c1E2625B522ee0d\",\"type\":\"tx\",\"consensus\":7,\"txType\":13,\"data\":\"{\\\"txInfo\\\":{\\\"treasuryLockedAmount\\\":\\\"31000\\\",\\\"treasuryPackageAmount\\\":23,}}\",\"utxos\":[{\"owner\":[\"3CD050678178A3029E7436A661694237589AF868\"],\"vin\":[{\"prevOut\":[{\"hash\":\"6367c45ba4c30b72acd493e36c863547e80b131cda2473f3c956f3b34d2eea8a\"}]}],\"vout\":[{\"value\":\"29999936200\",\"addr\":\"3CD050678178A3029E7436A661694237589AF868\"},{\"value\":\"28700\",\"addr\":\"VirtualBurnGas\"}],\"assetType\":\"556fc975c75073a7a76acc4990d0b68d79f97af971674ccb9b2d46d61d76ae1b\",\"gasUtxo\":\"1\"}],\"gasTx\":1}",
    "txType": "1",
    "vrfJson": "{}"
  }
}
```

# Blockchain Data Structure Specification

## Transaction Schema

- `consensus`: Number of validating nodes confirming the transaction
- `identity`: Block packer/validator address
- `timestamp`: Transaction creation time (Unix epoch)
- `transaction` Hash (txHash)**: Unique transaction identifier (hex string)
- `type: Default value `"Tx"` (base transaction type)
- `utxo`
  - ​`multiSigns`: Transaction Multisignature
    - `pub`: Base64-encoded public key
    - `sign`: Base64-encoded cryptographic signature
  - `owner`: Transaction initiator address
  - `vin`:
    - `preVout`: Reference to spent UTXO
      - `hash`: Source transaction hash
  - `vinSigns`: Input validation signature
    - `pub`: Base64-encoded public key
    - `sign`: Base64-encoded signature
- `vout`:
  - `addr`: Recipient address
  - `value`: Transferred amount in atomic units (string format)
- ​`verifySigns`:
  - `pub`: Base64-encoded validator public key
  - `sign`: Base64-encoded validation signature
  - `addr`: Validator node address
- `txType`: Transaction type 
| Code | Type            | Description                           |
| ---- | --------------- | ------------------------------------- |
| 0    | Unknown         | Undefined transaction type            |
| 1    | Transfer        | Asset transfer between accounts       |
| 2    | Stake           | Asset locking for network consensus   |
| 3    | Unstake         | Release of staked assets              |
| 4    | Invest          | Capital allocation to nodes/protocols |
| 5    | Divest          | Withdrawal of invested capital        |
| 7    | ContractDeploy  | Smart contract deployment             |
| 8    | ContractExecute | Smart contract interaction            |
| 99   | TreasuryClaim   | Network reward distribution claim     |
- `data`
#### Stake Transaction
- `txInfo`:Stake transaction information
  - `commissionRate`: Validator fee percentage (float)
  - `stakeAmount`: Locked amount in atomic units
  - `stakeType`: Staking mechanism (Default: `net`)

#### Unstake Transaction
- `txInfo`:Unstake transaction information
  - `unstakeUtxo`: Reference to locked UTXO being released

#### Investment Transaction
- `txInfo`:Invested transaction information
  - `bonusAddr`: Target node/protocol address
  - `investAmount`: Invested capital in atomic units
  - `investType`: Investment category (Default: `normal`)

#### Divest Transaction
- `txInfo`:Invested transaction information
- `bonusAddr`: Address designated to receive investment returns
- `disinvestUtxo`: UTXO associated with disinvestment transactions

#### Bonus Transaction
- `txInfo` Applies for transaction information
- `bonusAddrList`: List of addresses eligible to claim protocol rewards
- `bonusAmount`: Total reward amount available for claim in atomic units

#### Contract Deployment Transaction 
- `txInfo` Applies for transaction information
- `blockPrevRandao`: Cryptographic random seed from transaction inputs
- `blockTimeStamp`: Deployment timestamp 
- `input`: Contract bytecode (hex string)
- `recipient`: Contract deployment address
- `sender`: Transaction initiator address
- `version`: Contract version identifier
- `virtualMachine`: Execution environment (`0`=EVM, `1`=WASM)

#### Contract Execution Transaction
- `txInfo` Applies for transaction information
- `blockPrevRandao`: Cryptographic random seed from transaction inputs
- `blockTimeStamp`: Execution timestamp 
- `contractDeployer`: Deployment contract address
- `donation`: Optional gratuity to contract deployer
- `input`: Parameters for executing thcontract
- `recipient`: Message sender
- `sender`: Transaction initiator address
- `transfer`: Value transferred with contract call
- `version`: Contract version identifier
- `virtualMachine`: Execution environment (`0`=EVM, `1`=WASM)

## Block Schema

- ​**blockSigns**:
  - `pub`: Base64-encoded validator public key
  - `sign`: Base64-encoded block signature
  - `addr`: Signing validator address
- ​**bytes**: Block size in bytes
- ​**hash**: Unique block identifier (hex string)
- ​**height**: Sequential block number
- ​**merkleRoot**: Hash of all transactions (hex string)
- ​**prevhash**: Parent block reference (hex string)

- ​**tx**: Parent block reference (hex string): Indicate transaction information
- **data**
  - `Deployment Contract`
    - `creation`: Child contracts created during deployment
    - `dependentCTx`: Required predecessor transactions
    - `output`: Finalized contract bytecode
    - `preHash`: Contract state hash pre-deployment
    - `storage`: Initial contract storage state

  - `Execution Contract`
    - `destruction`: Contracts terminated during execution
    - `output`: Execution result payload
    - `preHash`: Contract state hash pre-execution
    - `storage`: Finalized contract storage state    
    - 'log'
      - `creator`: Indicates the contract address for generating logs
      - `data`: Data
      - `topics`: topics
    - `output`: Indicates the output of the contract
    - `preHash`: Indicates the pre-hash of the contract
    - `storage`: storage