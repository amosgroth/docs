# How to Recover Your Umbrel Jam Wallet

This guide will show you how to recover your [Jam](https://github.com/joinmarket-webui/jam) wallet that you somehow have lost on your [Umbrel](https://github.com/getumbrel/umbrel) server. You will be guided through different recovery scenarios, depending on what has happened (e. g. hard drive failure) - or more precisely - what you have at hand (e. g. seed phrase).

<p align="center"><strong>⚠️ Jam and Umbrel are beta software, they can fail at any time. Your hardware can also fail at any time.<br/>Write down your seed phrase(s) and wallet password right after installation so you don't have to worry about losing funds! ⚠️</strong></p>

## Prerequisites
It is crucial to know that Umbrel and Jam don't share the same wallet. What you do with and have in your Umbrel wallet is completely apart from your Jam wallet. Jam is only using Umbrels Bitcoin Node app, creates and uses its own wallet with its own funds. As said above, it is therefore a must to not only write down your Umbrel seed phrase right after you have installed your Umbrel server, you also need to write down your Jam seed phrase right after installing the Jam plugin on your Umbrel. If you have done that, no need to worry. Please note that **this guide is written for Umbrel 0.5 and above**. Let's go!

## Recovery with both Seeds
This is the best case scenario. You have _both_ - your Umbrel _and_ your Jam seed phrase - at hand. To recover your Umbrel Bitcoin funds, you will need to do the following:
1. [Install Umbrel](https://github.com/getumbrel/umbrel#installing-umbrel)
2. Install Bitcoin Node from the [Umbrel App Store](https://github.com/getumbrel/umbrel#umbrel-app-store) and wait until it is 100% synched
3. Install Lightning Node from the App Store, let it fully synch
4. Open the Lightning Node app and [recover your Umbrel funds with your Umbrel seed phrase](https://twitter.com/umbrel/status/1562099972547690501)

OK, cool. You should have recovered your old Umbrel server and wallet successfully. You should be able to see and access your funds again. If not, checkout the [Umbrel Community](https://community.getumbrel.com) where you can find more detailed instructions and support. Let's see how you can recover your Jam wallet now:
1. Install Jam from the Umbrel App Store
2. Connect to your Umbrel via SSH
3. Go into the Jam Docker container
4. Use the [_wallet-tool.py_](https://jamdocs.org/FAQ/#can-i-import-an-existing-wallet) script with your Jam seed phrase

So here is an essential version of what you will need to type and see in your terminal (replace "zoo..." with your personal Jam seed phrase):
```
user@device  % ssh umbrel@umbrel.local
umbrel@umbrel.local's password: 
umbrel@umbrel:~/ $ docker exec -it jam_web_1 bash
root@33025215bd28:/src/scripts# cd ..
root@33025215bd28:/src# python3 scripts/wallet-tool.py recover --gap-limit=200 --recoversync
User data location: /root/.joinmarket/
Input mnemonic recovery phrase: zoo zoo zoo zoo zoo zoo zoo zoo zoo zoo zoo wrong
Input mnemonic extension, leave blank if there isnt one: 
Enter new passphrase to encrypt wallet: 
Reenter new passphrase to encrypt wallet: 
Input wallet file name (default: wallet.jmdat): recover.jmdat
Would you like this wallet to support fidelity bonds? write 'n' if you don't know what this is (y/n): y
Write down this wallet recovery mnemonic

zoo zoo zoo zoo zoo zoo zoo zoo zoo zoo zoo wrong

Recovered wallet OK
```

Now - when opening your Jam app on Umbrel in your browser - you should see your recovered wallet and be able to open and use it. If you don't see your wallet at all, you probably forgot adding the _.jmdat_ while naming the recovered wallet. If you don't see transactions and funds, you might have to adjust the [_--gap-limit_](https://blog.blockonomics.co/bitcoin-what-is-this-gap-limit-4f098e52d7e1) parameter with the recovery tool. Or you need to do a...

## Rescan with Umbrels Bitcoin Node App
You probably need to [rescan](https://developer.bitcoin.org/reference/rpc/rescanblockchain.html) the blockchain on your Umbrel if you had to reinstall or resynch the Bitcoin Node before recovering your Jam wallet. This can be done with the [_bitcoin-cli_](https://bitcoin.org/en/bitcoin-core/features/user-interface#cli) on your Umbrel but can take a long time if you rescan the whole blockchain. If you know roughly when you created (and lost) your old Jam wallet that you want to recover, you can pass an optional start/end block height to avoid needlessly rescanning the whole blockchain. This is how you do a rescan on Umbrel:
1. Connect to your Umbrel via SSH
2. Find the specific [block height(s) by time](https://timeinblocks.com)
3. Use the _bitcoin-cli_ to start the rescan 

So here is an essential version of what you will need to type and see in your terminal. Note that you can also skip the _stop_height_ parameter in order to scan from a specific block height to now:
```
user@device  % ssh umbrel@umbrel.local
umbrel@umbrel.local's password: 
umbrel@umbrel:~ $ ./umbrel/scripts/app compose bitcoin exec bitcoind bitcoin-cli rescanblockchain 510110 510114
{
  "start_height": 510110,
  "stop_height": 510114
}
```
