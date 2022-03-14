## Website
https://ethernaut.openzeppelin.com/

## Completed
0. Hello Ethernaut
1. Fallback

## Other useful sites:

https://www.pauric.blog/How-To-Hack-Ethereum-Contracts-The-Easy-Way/
https://trufflesuite.com/docs/truffle/getting-started/interacting-with-your-contracts

## Other Notes:

player is you
get the balance using
```
getBalance(player)
```

interact with the `contract`

(await contract.contributions(player)).toString();
await contract.contribute.sendTransaction({value: toWei(.0009)})

contract is a truffle object. can do fallback methods using

contract.sendTransction({value: 50000000});
