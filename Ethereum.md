## Ethereum

Running Geth Node
https://medium.com/better-programming/run-an-ethereum-node-on-linux-late-2019-b37a1d35800e

#### Start geth to sync
```
geth --cache 2048
```

#### Attach console to running instance of geth
```
geth attach
```

#### Show sync status
From within geth console
```
eth.syncing
```

Run script from geth console to continuously update the time remaining on sync
```
var lastPercentage = 0;var lastBlocksToGo = 0;var timeInterval = 10000;
setInterval(function(){
    var percentage = eth.syncing.currentBlock/eth.syncing.highestBlock*100;
    var percentagePerTime = percentage - lastPercentage;
    var blocksToGo = eth.syncing.highestBlock - eth.syncing.currentBlock;
    var bps = (lastBlocksToGo - blocksToGo) / (timeInterval / 1000)
    var etas = 100 / percentagePerTime * (timeInterval / 1000)

    var etaM = parseInt(etas/60,10);
    console.log(parseInt(percentage,10)+'% ETA: '+etaM+' minutes @ '+bps+'bps');

    lastPercentage = percentage;lastBlocksToGo = blocksToGo;
},timeInterval);
```
