# How to Recover Your Umbrel Jam Wallet

This guide will show you how to recover your [Jam](https://github.com/joinmarket-webui/jam) wallet that you somehow have lost on your [Umbrel](https://github.com/getumbrel/umbrel) server. You will be guided through different recovery scenarios, depending on what has happened (e. g. hard drive failure) - or more precisely - what you have at hand (e. g. seed phrase).

<p align="center"><strong>⚠️ Jam and Umbrel are beta software, they can fail at any time. Your hardware can also fail at any time.<br/>Write down your seed phrase(s) right after installation so you don't have to worry about losing funds! ⚠️</strong></p>

## Prerequisites
It is crucial to know that Umbrel and Jam don't share the same wallet. What you do with and have in your Umbrel wallet is completely apart from your Jam wallet. Jam is only using Umbrels Bitcoin Core app, creates and uses its own wallet with its own funds. As said above, it is therefore a must to not only write down your Umbrel seed phrase right after you have installed your Umbrel server, you also need to write down your Jam seed phrase right after installing the Jam plugin on your Umbrel. If you have done that, no need to worry. Please note that this guide is written for _Umbrel 0.5 and above_. Let's go!

## Recovery with both Seeds
This is the best case scenario. You have _both_ - your Umbrel _and_ your Jam seed phrase - at hand. To recover your Umbrel Bitcoin funds, you will need to do the following:
* [Install Umbrel](https://github.com/getumbrel/umbrel#installing-umbrel)
* Install Bitcoin Core from the [Umbrel App Store](https://github.com/getumbrel/umbrel#umbrel-app-store) and wait until it is 100% synched
* Install Lightning Node from the App Store, let it fully synch
* Open the Lightning Node app and [recover your Umbrel funds with your Umbrel seed phrase](https://twitter.com/umbrel/status/1562099972547690501)

OK, cool. You should have recovered your old Umbrel server and wallet successfully. You should be able to see and access your funds again. If not, checkout the [Umbrel Community](https://community.getumbrel.com) where you can find more detailed instructions and support. Let's see how you can recover your Jam wallet now:
* Install Jam from the Umbrel App Store
* [](https://jamdocs.org/FAQ/#can-i-import-an-existing-wallet)
