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
https://bitcoin.org/en/developer-reference

### List Balances
```
bitcoin-cli listreceivedbyaddress 0 true
```

### Dump Private Key
```
bitcoin-cli dumpprivkey "myaddress"
```

https://bitkey.io/
