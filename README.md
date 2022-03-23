IOTA - python
===
###### tags: `區塊鏈`

```
主旨： Iota python 套件範例
更新日期： 2022-02-25
版本： V1
作者： Ya-Sheng Chen (Rock)
```

---
## IOTA簡介
`IOTA` 是第三代公開無權限(permissionless) 分散式帳本， 其網路所使用的為有向無環圖（ Directed Acyclic Graph， 簡稱 ） ， IOTA 稱呼此 DAG 為「`Tangle`」

### 開發理念
無需交易費、 速度更快、 更具擴充性的交易平台， 更在於加強物聯網（ Internet of Things），紀錄和執行物聯網生態中不同設備間的資料傳輸， 提供一個人類和電腦可以交換資料的特殊網絡。

### IOTA不是區塊鏈
團隊運用分散式帳本技術， 針對物聯網打造了創新的 Tangle 網路， 與區塊鏈一樣意圖創立一個去中心化的世界，`Tangle`是`IOTA` 開發團隊基於有向無環圖（DAG） 技術所打造的去中心化網路系統， Tangle 並不是區
塊鏈， 因為 `Tangle` 的世界中既沒有鏈， 沒有區塊， 也沒有礦工。

### IOTA 特點
● 擴展性 (Scalability)
● 去中心化 (Decentralisation)
● 無交易手續費 (No transaction fees)
● 抵抗量子計算 (Quantum computing protection)

---
## 透過Python iota client 套件將資訊上鏈
### 安裝

1. 依自己Python版本, 下載官方 [python-client](https://nightly.link/iotaledger/iota.rs/workflows/python_binding_publish/dev) 套件.zip檔案，並解壓縮至您的project 資料夾
2. 進入您需要安裝套件的python 環境
    - `cd ./Document/project/iota_test`
    - `source ./venv/bin/activite`
3. 安裝套件
    - `pip install iota_client_python-0.2.0_alpha.3-cp38-abi3-linux_x86_64.whl`
4. 完成
    - 檢視安裝套件是否完成 `pip list` 
```
Package                    Version
-------------------------- -------
iota-client-python           0.2.0a3
```

### 使用
#### 載入套件
```
import iota_client
```
#### init 連線
##### 使用預設或自定義連線
```
# 預設
client = iota_client.Client()

# 自定義<option>
client = iota_client.Client(network='devnet',
                            nodes_name_password=[['https://api.lb-1.h.chrysalis-devnet.iota.cafe']])
```
- `net_type` = [deafult=`"devnet"`, `"mainnet"`] # 主網與測試網
- `node_addr`= 預設測試網址`https://api.lb-1.h.chrysalis-devnet.iota.cafe `進行算力並上傳交易使用的節點地址。

#### 取得節點資訊
```
client.get_info()
```
**response**
```
{
   "nodeinfo":{
      "name":"HORNET",
      "version":"0.6.0-alpha",
      "is_healthy":true,
      "network_id":"testnet7",
      "bech32_hrp":"atoi",
      "min_pow_score":4000.0,
      "messages_per_second":27.3,
      "referenced_messages_per_second":34.5,
      "referenced_rate":126.37362637362637,
      "latest_milestone_timestamp":1618133322,
      "latest_milestone_index":33602,
      "confirmed_milestone_index":33602,
      "pruning_index":16086,
      "features":[
         "PoW"
      ]
   },
   "url":"https://api.hornet-0.testnet.chrysalis2.com"
}
```
#### 節點是否正常運作
```
client.get_health()
>> True
```

#### 傳送zero_value_transaction 無費用交易
- index \<str>   = 為你的資訊設定index名稱，之後可透過此index 於 區塊鏈瀏覽器查詢這筆資訊
- data_str \<str>= 需要上傳的資訊
```
idx_name = "Rock_1"
mssg     = "hello world 1"

# sending message
result   = client.message(index=idx_name, data_str=mssg)
```

#### 完成
- 可於 [iota tangle explorer](https://explorer.iota.org/mainnet) 查詢 透過切換 [`mainnet`,`devnet`] 查詢主網或測試網上的上鏈資訊

<img src="https://i.imgur.com/8jAgU5y.png">
<img src="https://i.imgur.com/K5NCakB.png">

#### 完整code
```
import iota_client

try:
    # init connect
    client = iota_client.Client()

    # check node health
    is_health = client.get_health()
    if not is_health:
        raise ValueError('node is not healthy, please check node is on, or change node address')
    
    # prepare index and mssg
    for i in range(2):
        idx_name = f'Rock' 
        mssg     = f'hello world {i}'
        
        # send message
        client.message(index=idx_name, data_str=mssg)
        
except ValueError as ve:
    print(ve)

except Exception as e:
    print(e)
```


---
## reference
### IOTA 介紹
- [gitbook](https://iotazh.gitbook.io/iota--guidebook/tangle/iota)
- [Tangle 白皮書.md](https://hackmd.io/@blockchain/rkpoORY4W/%2Fs%2FryriSgvAW?type=book#Tangle-%E7%99%BD%E7%9A%AE%E6%9B%B8)
- [IOTA 簡介筆記.md](https://hackmd.io/@VXrni9wISJq-vtB64ThjYw/Sy9ChM1If?type=view)

###  develop resurce
- **IOTA 1.5** `Chrysalis`
    - [IOTA REST API Doc](https://editor.swagger.io/?url=https://raw.githubusercontent.com/rufsam/protocol-rfcs/master/text/0026-rest-api/0026-rest-api.yaml)
    - [iota-client](https://wiki.iota.org/chrysalis-docs/libraries/client)
    - [iota-client-python-api-reference](https://wiki.iota.org/iota.rs/libraries/python/api_reference)
    - [iota-client-python-example](https://wiki.iota.org/iota.rs/libraries/python/api_reference)
    - [iota-client-python-send-address](https://wiki.iota.org/iota.rs/libraries/python/api_reference)
    - [iota-client-python-github-param](https://github.com/iotaledger/iota.rs/tree/dev/bindings/python)

- ~~**IOTA 1.0**~~
    - [~~legacy-python clien library get started~~](https://legacy.docs.iota.works/docs/core/1.0/getting-started/get-started-python)
    - [~~Pyota github~~](https://github.com/iotaledger/iota.py)
    - [~~Pyota Doc .pdf~~](https://buildmedia.readthedocs.org/media/pdf/pyota/latest/pyota.pdf)

### infomation
[networks intro](https://legacy.docs.iota.works/docs/getting-started/1.1/networks/overview)

### node

- ~~**IOTA 1.0**~~
    - [~~iri full node~~](https://iri-playbook.readthedocs.io/en/master/introduction.html)

- **hornet\<full node>**
    - [iota hornet-wiki](https://wiki.iota.org/hornet/welcome)
    - [安裝 hornet](https://wiki.iota.org/hornet/getting_started/using_docker)
- **Chronicle\<permanode>**
    - [scylladb-for permanode](https://www.scylladb.com/2020/08/13/iota-using-scylla-for-distributed-storage-of-the-tangle/)
    - [scylladb -install with docker](https://www.scylladb.com/download/?platform=docker#open-source)
    - [IOTA use scylla distributed storage of the tangle](https://www.scylladb.com/2020/08/13/iota-using-scylla-for-distributed-storage-of-the-tangle/)
---

