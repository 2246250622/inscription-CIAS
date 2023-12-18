# Celestia(tia) 公鏈銘文 cias mint 腳本

## 代碼參考 [qzz0518/coss](https://github.com/qzz0518/coss)

### Step 1: 安裝

```
git clone https://github.com/sfter/cias-mint
yarn install
cp .env.example .env
```

### Step 2: 配置環境變數

在腳本原始碼目錄下修改 .env 文件

『`bash
# rpc配置, 可以從 https://atomscan.com/directory/celestia 找到自己喜歡的節點伺服器
NODE_URL=https://public-celestia-rpc.numia.xyz
# NODE_URL=https://celestia-rpc.mesa.newmetric.xyz

# 主錢包（資金錢包）私鑰, 用於轉移給其它真正用來 Mint 的錢包
PRIVATE_KEY=

# 產生錢包配置,按需配置
# 產生多少 Mint 錢包
NUM_OF_WALLETS=5
# 真正 Mint 的錢包文件，所有產生的錢包都在這個文件裡
WALLET_JSON_FILE=wallets.json

# celestia配置（可以不用動）
CHAIN_SYMBOL=celestia
TOKEN_DENOM=utia
TOKEN_DECIMAL=1000000

# 從主錢包（資金錢包）轉多少個 TIA 到 每個真正 Mint 的錢包
TOKEN_TRANSFER_AMOUNT=2

# gas 配置, 按需修改
GAS_PRICE=10000
GAS_LIMIT=100000

# mint配置, 一定要根據官方參數配置
MINT_AMOUNT=10000
# 銘文代幣名稱
TICK=cias
# 協定類型
PROTOCOL=cia-20

# 每個錢包 mint 次數
MINT_TIMES=10

```

### Step 3: 批量產生 Mint 錢包

『`bash
node wallet_gen.js
```

### Step 4: 從主錢包（資金錢包）批量轉帳到 Mint 錢包

『`bash
node transfer.js
```

### Step 5: 執行 Mint 程式開始 Mint

『`bash
node mint.js
```

### 特別說明
如果 keplr 錢包導不出私鑰，可以用以下方法來做
> - 先把 .env 檔配置好，PRIVATE_KEY 留空。
>
>
> - 使用 node wallet_gen.js 產生錢包
>
>
> - 開啟目前目錄下的 wallet.json 文件
>
>
> - 選擇其中任一個錢包做為主錢包。
>
>
> - 打開 keplr 錢包，向你在上面第4步選擇的錢包地址轉一些 $TIA 進去。
>
>
> - 將上面第4步驟選擇的錢包位址配置到 .env 檔案裡的 PRIVATE_KEY 欄位。
>
>
> - 執行 node transfer.js 將會從上面第4步選擇的錢包向其它 Mint 的錢包批量轉帳。
>
>
> - 執行 node mint.js 開始批次 Mint，完成 OK。