## Monero

### Generating Wallet

This guide assumes you have already initialized your Ledger wallet and thus generated a 24 word mnemonic seed.

You need to install the Ledger Monero app. In addition, you may have to add some udev-rules.

Your Ledger needs to be plugged in and the Ledger Monero app should be running.

Either your daemon (monerod) should be running and preferably be fully synced or you should connect to a remote node.

Now that we're sufficiently prepared, let's start!

1) Go to the directory where monero-wallet-cli and monerod are located.

2) Open a new terminal.

3) Now type:
```
./monero-wallet-cli --generate-from-device <new-wallet-name> --subaddress-lookahead 3:200
```

Note that is simply a placeholder for the actual wallet name. If you, for instance, want to name your wallet MoneroWallet, the command would be as follows:

```
./monero-wallet-cli --generate-from-device MoneroWallet --subaddress-lookahead 3:200
```

The CLI will, after executing aforementioned command, prompt your for a password. Make sure to set a strong password and confirm it thereafter.

The Ledger will ask whether you want to export the private view key or not. First and foremost, your funds cannot be compromised with merely the private view key. Exporting the private view key enables the client (on the computer - Monero v0.15.0.1) to scan blocks looking for transactions that belong to your wallet / address. If this option is not utilized, the device (Ledger) will scan blocks, which will be significantly slower. There is, however, one caveat. That is, if your system gets compromised, the adversary will potentially be able to compromise your private view key as well, which is detrimental to privacy. This is virtually impossible when the private view key is not exported.

You may have to hit confirm twice before it proceeds.

Your Ledger Monero wallet will now be generated. Note that this may take up to 5-10 minutes. Furthermore, there will be no immediate feedback in the CLI nor on the Ledger.

monero-wallet-cli will start refreshing. Wait until it has fully refreshed.

Congratulations, you can now use your Ledger Monero wallet in conjunction with the CLI.

### A few final notes:

I'd strongly advise to test the full process first. That is, send a small amount to the wallet and subsequently restore it (using aforementioned guide) to verify that you can recover the wallet. Note that, upon recreating / restoring the wallet, you ought to append the --restore-height flag (with a block height before the height of your first transaction to the wallet) to the command in step 3 (Windows), step 5 (Mac OS X), or step 3 (Linux). More information about the restore height and how to approximate it can be found here.

If you use a remote node, append the --daemon-address host:port flag to the command in step 3 (Windows), step 5 (Mac OS X), or step 3 (Linux).

If desired, you can manually tweak the --subaddress-lookahead value. The first value is the number of accounts and the second value is the number of subaddresses per account. Thus, if you, for instance, want to pregenerate 5 accounts with 100 subaddresses each, use --subaddress-lookahead 5:100. Bear in mind that, the more subaddresses you pregenerate, the longer it takes for the Ledger to create your wallet.

You only have to use the --generate-from-device flag once (i.e. upon wallet creation). Thereafter, you'd basically use it similar to how you normally use the CLI. That is:

[1] Make sure your Ledger is plugged in and the Monero app is running.

[2] Open monero-wallet-cli

[3] Enter the wallet name of your Ledger Monero wallet.

[4] Enter the password to open the wallet.

If the Ledger wallet files are not in the same directory as monero-wallet-cli, you ought to open monero-wallet-cli with the --wallet-file /path/to/wallet.keys/file flag. Alternatively, you can copy the Ledger wallet files to the same directory as monero-wallet-cli.

#### It's imperative that the closing process of your Ledger Monero wallet is done in this specific consecutive order:

[1] Exit monero-wallet-cli by typing exit

[2] Exit the Ledger Monero app.

[3] Unplug the Ledger device.
