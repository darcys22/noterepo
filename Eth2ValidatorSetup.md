# Setting Up Ethereum 2.0 Validator

### Update System
```
$ sudo apt update && sudo apt upgrade
$ sudo apt dist-upgrade && sudo apt autoremove
```
### Prepare the Validator Deposit Data
- Get Göerli ETH (https://faucet.goerli.mudit.blog/)
- Generate the validator keys. Each key is a validator account
- Fund the validator account(s) (32 Göerli ETH per account)
- Wait for your validator account(s) to become active
    
#### go to https://github.com/ethereum/eth2.0-deposit-cli/releases
Pick the most recent release to download
```
wget https://github.com/ethereum/eth2.0-deposit-cli/releases/download/v0.2.1/eth2deposit-cli-v0.2.1-linux-amd64.tar.gz
tar -xvf eth2deposit-cli-v0.2.1-linux-amd64.tar.gz

cd eth2deposit
./deposit --num_validators 1 --chain medalla
```
Save the Key somewhere safe (Note.txt in home directory)

#### Go to launchpad https://medalla.launchpad.ethereum.org/

Transfer the 32 ETH to the deposit.json file generated in eth2 deposit

### Configure the Beacon Node

We will run the beacon node as a service so if the system restarts the process will automatically start back up again.
Setup Accounts and Directories

Create an account for the beacon node to run under. This type of account can’t log into the server.
```
$ sudo useradd --no-create-home --shell /bin/false lighthousebeacon
```
Create the data directory for the Lighthouse beacon node database. Use the -p option to create the full path.
```
$ sudo mkdir -p /var/lib/lighthouse/beacon-node
```
Set directory permissions. The lighthousebeacon account needs permission to modify the database directory. The -R means recursive.
```
$ sudo chown -R lighthousebeacon:lighthousebeacon /var/lib/lighthouse/beacon-node
```
Next, copy the newly compiled lighthouse binary to the /usr/local/bin directory. We will run it from there. Note: You will need to do this step each time you pull/build a new version of the lighthouse binary.
```
$ sudo cp /$HOME/.cargo/bin/lighthouse /usr/local/bin
```
#### Create and Configure the Service

Create a systemd service file to store the service config.
```
$ sudo nano /etc/systemd/system/lighthousebeacon.service
```
Paste the following into the file.
```
[Unit]
Description=Lighthouse Beacon Node
Wants=network-online.target
After=network-online.target

[Service]
Type=simple
User=lighthousebeacon
Group=lighthousebeacon
Restart=always
RestartSec=5
ExecStart=/usr/local/bin/lighthouse beacon_node --datadir /var/lib/lighthouse/beacon-node --testnet medalla --http --eth1-endpoint http://127.0.0.1:8545 --graffiti "<yourPOAPstring>"

[Install]
WantedBy=multi-user.target
```
Replace <yourPOAPstring> with your Lighthouse POAP participation medal value for a special NFT prize! E.g. --graffiti "abcdefg12345saf"

The --eth1-endpoint flag defines the endpoint of the Eth1 node. If you installed one locally the value is http://127.0.0.1:8545. If you’re using a third party change the value to point to the external endpoint address.

The beacon_node subcommand tells the lighthouse binary that we want to run the beacon node.

The --datadir flag is where we are going to save our beacon node database.

Reload systemd to reflect the changes.
```
$ sudo systemctl daemon-reload
```
Note: If you are running a local Eth1 node (see Step 3) you should wait until it fully syncs before starting the beacon chain service. Check progress here: `sudo journalctl -f -u geth.service`

Start the service and check to make sure it’s running correctly.
```
$ sudo systemctl start lighthousebeacon
$ sudo systemctl status lighthousebeacon
```

Enable the beacon-chain service to automatically start on reboot.
```
$ sudo systemctl enable lighthousebeacon
```
The beacon-chain will begin to sync. It may take several hours for the node to fully sync. You can check the progress by running the journal command. Press Ctrl+C to quit.
```
$ sudo journalctl -f -u lighthousebeacon.service
```

### Create the Validator Wallet

The validator wallet is created by importing the keystore-m JSON files from the previous step.

First create a directory to store the validator wallet and give the current user permissions to access it. Change <yourusername> to your logged in username.
```
$ sudo mkdir -p /var/lib/lighthouse/validator
$ sudo chown -R <yourusername>:<yourusername> /var/lib/lighthouse/validator
```
Next, run the wallet creation process. As mentioned at the end of Step 7 the account validator import expects the keystore-m JSON keys to be in the directory HOME/eth2.0-deposit-cli/validator_keys.
```
$ cd lighthouse
$ lighthouse account validator import --directory $HOME/eth2.0-deposit-cli/validator_keys --validator-dir /var/lib/lighthouse/validator
```
The --validator-dir flag specifies the location to output the wallet data.

You will be asked to provide the password for each key, one-by-one. Be sure to provide the password each time because the validator will be running as a service, and it needs to persist the password in a file to access the key. This may change in future as it’s not very secure.

Output should look like:
```
Keystore found at "/home/<yourusername>/eth2.0-deposit-cli/validator_keys_lighthouse/keystore-m_12381_3600_28_0_0-1596123077.json":- Public key: 0x963b95a66d952053adc6d8ce4cce2f13315d1ca063ff51278ad6b49b090665d887f70e9a398d837fe4b40ee225b761df
 - UUID: 902a84a1-2536-4346-c619-dd8b19cb1398If you enter the password it will be stored as plain-text in validator_definitions.yml so that it is not required each time the validator client starts.Enter the keystore password, or press enter to omit it:Password is correct.Successfully imported keystore.
Successfully updated validator_definitions.yml.

Once you do this for each keystore-m JSON file you should get a successful message.

Successfully imported 40 validators (0 skipped).WARNING: DO NOT USE THE ORIGINAL KEYSTORES TO VALIDATE WITH ANOTHER CLIENT, OR YOU WILL GET SLASHED.
```
That’s it! Now that the validator wallet is configured we will set up the validator itself to run as a service.

### Configure the Validator
#### Setup Accounts and Directories

We will run the validator as a service so if the system restarts the process will automatically start back up again.

Create an account for the validator service to run under. This type of account can’t log into the server.
```
$ sudo useradd --no-create-home --shell /bin/false lighthousevalidator
```
We created the data directory for the validator in the previous step: /var/lib/lighthouse/validator. Now set directory permissions so the lighthousevalidator account can modify the validator account data directory.
```
$ sudo chown -R lighthousevalidator:lighthousevalidator /var/lib/lighthouse/validator
```
#### Create and Configure the Service

Create a systemd service file to store the service config.
```
$ sudo nano /etc/systemd/system/lighthousevalidator.service
```
Paste the following into the file.
```
[Unit]
Description=Lighthouse Validator
Wants=network-online.target
After=network-online.target

[Service]
Type=simple
User=lighthousevalidator
Group=lighthousevalidator
Restart=always
RestartSec=5
ExecStart=/usr/local/bin/lighthouse validator_client --datadir /var/lib/lighthouse/validator

[Install]
WantedBy=multi-user.target
```
We use the same lighthouse binary located in /usr/local/bin but this time we apply the validator_client subcommand, instructing it to run the validator.

The --datadir flag is where we are going to save our validator database.

Reload systemd to reflect the changes.
```
$ sudo systemctl daemon-reload
```
Start the service and check to make sure it’s running correctly.
```
$ sudo systemctl start lighthousevalidator
$ sudo systemctl status lighthousevalidator
```

If you did everything right, it should say active (running) in green text. If not then go back and repeat the steps to fix the problem. Press Q to quit.

Enable the validator service to automatically start on reboot.
```
$ sudo systemctl enable lighthousevalidator
```
You can check the progress by running the journal command. Press Ctrl+C to quit.
```
$ sudo journalctl -f -u lighthousevalidator.service
```
The validator will enable the validator keys in the validator wallet and confirm the connection to the beacon node. If the testnet genesis hasn’t begun yet it will tell us how much time is remaining.
```
Aug 03 05:42:50 ETH-STAKER-002 lighthouse[61599]: Aug 03 05:42:50                                                                                                         .560 INFO Initialized validators                  enabled: 40, di                                                                                                         sabled: 0
Aug 03 05:42:50 ETH-STAKER-002 lighthouse[61599]: Aug 03 05:42:50                                                                                                         .590 INFO Connected to beacon node                version: Lighth                                                                                                         ouse/v0.1.2-unstable/x86_64-linux
Aug 03 05:42:50 ETH-STAKER-002 lighthouse[61599]: Aug 03 05:42:50                                                                                                         .599 INFO Starting node prior to genesis          seconds_to_wait                                                                                                         : 112637
```
It may take hours or even days to activate the validator account(s) on the testnet once the beacon chain has actually started processing.

You can check the status of your validator(s) via beaconcha.in. Simply do a search for your validator public key(s). It may be a while before they appear on the site.

That’s it. We have a functioning beacon chain and validator. Congratulations: you are awesome!
