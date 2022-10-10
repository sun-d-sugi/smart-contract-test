# smart-contract-test

### ①Dockerインストール

### ②truffleイメージ取得
```
docker pull trufflesuite/ganache-cli:latest
```

### ③コンテナ実行
```
docker run -v /Users/daisuke.sugimoto/Project/NFT/SmartContract:/usr/src/SmartContract -it -d --name test_truffle trufflesuite/ganache-cli /bin/bash

docker container ls
```

### ④truffleインストール
```
docker container exec -it test_truffle /bin/ash

npm install -g truffle
```

### ⑤Truffleプロジェクト作成
```
cd /usr/src/SmartContract
truffle init
```

### ⑥Truffle Config設定
truffle-config.jsを編集

```
module.exports = {
    networks: {
      development: {
         host: "127.0.0.1",     // Localhost (default: none)
         port: 7545,            // Standard Ethereum port (default: none)
         network_id: "*",       // Any network (default: none)
      }
    }
}
```

### ⑦Ganacheインストール
https://www.trufflesuite.com/ganache

### ⑧Ganacheワークスペース設定
https://qiita.com/romorimori/items/155bb1f5e4cced629ce8

### ⑨HelloWorldコントラクト作成
```
truffle create contract HelloWorld
```

contracts/HelloWorld.solを編集
```
pragma solidity ^0.5.0;

contract HelloWorld {
  string defaultMessage;
  constructor() public {
    defaultMessage = 'Hello World';
  }
  function getMessage() public view returns(string memory){
    return defaultMessage;
  }
}
```

### ⑩コンパイル
```
truffle compile
```

### ⑪マイグレーションファイル作成

migrations/15xxxxxxxx_hello_world.jsを編集

```
const HelloWorld = artifacts.require("HelloWorld");
module.exports = function(_deployer) {
  // Use deployer to state migration tasks.
  _deployer.deploy(HelloWorld)
};
```

### ⑫デプロイ
```
truffle migrate
```
