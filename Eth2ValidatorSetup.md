### Setting Up Ethereum 2.0 Validator

Update System
```
$ sudo apt update && sudo apt upgrade
$ sudo apt dist-upgrade && sudo apt autoremove
```
Prepare the Validator Deposit Data
    - Get Göerli ETH (https://faucet.goerli.mudit.blog/)
    - Generate the validator keys. Each key is a validator account
    - Fund the validator account(s) (32 Göerli ETH per account)
    - Wait for your validator account(s) to become active
    
go to https://github.com/ethereum/eth2.0-deposit-cli/releases
```
wget https://github.com/ethereum/eth2.0-deposit-cli/releases/download/v0.2.1/eth2deposit-cli-v0.2.1-linux-amd64.tar.gz
tar -xvf eth2deposit-cli-v0.2.1-linux-amd64.tar.gz

cd eth2deposit
./deposit --num_validators 1 --chain medalla
```
Save the Key somewhere safe (Note.txt in home directory)

Go to launchpad https://medalla.launchpad.ethereum.org/

Transfer the 32 ETH to the deposit.json file generated in eth2 deposit
