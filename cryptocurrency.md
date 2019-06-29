# ZCash 
### Run Daemon inside systemd
```
zcashd -daemon -bind=[::]:8233
```

### Check the state of the blockchain
```
zcash-cli getblockchaininfo > blockchain
```

# Bitcoin Core 
https://bitcoin.org/en/developer-reference#block-versions

### list balances
```
bitcoin-cli listreceivedbyaddress 0 true
```
