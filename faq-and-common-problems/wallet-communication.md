---
description: >-
  This section will answer some questions in regards to how the ATM communicates
  with the wallets that you connect it to. We'll be looking into API calls and
  what actually happens "under the hood".
---

# Wallet Communication

## How the ATM "talks"

When someone uses the LightningATM, they will insert a certain amount of coins into the ATM and expect bitcoin / satoshis back for it (from now on, I'll just simply write "satoshis", the smallest denomination of one bitcoin). The ATM must therefore be connected to a Lightning Wallet from which it sends satoshis to the person who has inserted the coins.

To ATM doesn't have any satoshis "on it". It will always have to "communicate" to a Lightning Wallet over a network and tell the wallet to send the satoshis. This communication is happening over an API ([Application Programming Interface](https://www.freecodecamp.org/news/what-is-an-api-in-english-please-b880a3214a82/)) of a Lightning Wallet.

APIs can be talked to in various ways. Most often the ATM will talk to them through a URL. Almost all API communication also requires a username and a password.

1. The API might be accessed at https://my-lightning-wallet.com/api
2. To prove that the ATM is allowed to use this API, it will have to provide a username and a password

It's therefore clear that we have to store this information (URL, username and password) on the ATM. The easiest way to do this is by encoding all that information into a QR code and showing it to the camera of the ATM ([as explained here](https://docs.lightningatm.me/lightningatm-setup/wallet-setup/lnd_btcpay#connecting-to-the-atm)).

The ATM will then read the content of the QR code and store those three pieces of information in a configuration file. From then on, it uses that information to talk to that Lightning Wallet to facilitate payouts and other communication like requesting the current state of the Lightning Wallet such as "balance" or "channel information".

## API endpoint, usernames and passwords

Let's take a closer look at the kind of information that is needed to talk to the API of a Lightning Wallet. Be aware that these pieces of information come in various shapes and encodings.

The URL to access an API might contain an IP address or a domain and can have a multitude of different paths (call "API endpoints"). Some examples:

* https://my-lightning-wallet.com/api/payinvoice
* https://api.my-lightning-wallet.com/v1/channelbalance
* https://localhost:8080/v1/payments
* https://btcpayserver.mydomain.me/v1/balance/blockchain

The URL to which your ATM will be talking to, depends on the software of the Lightning Wallet and the location where the wallet is "run" or operated (maybe a LND Lightning Node/Wallet on a [RaspiBlitz](https://github.com/rootzoll/raspiblitz) or a [BTCPayServer](https://github.com/btcpayserver/btcpayserver-docker)).

The username and password might need to be supplied as you're used to it from logging into websites but could as well be encoded in a [hexadecimal](https://www.lifewire.com/what-is-hexadecimal-2625897) or [base64](https://base64.guru/learn/what-is-base64) string.

## Talking to an API in practice

Now, let's get a little bit more practical and actually talk to an API. For this example, I'll be using the API of the Lntxbot because it is available to everyone with a Telegram account and can easily be followed along (more information on how to install Lntxbot can [be found here](https://docs.lightningatm.me/lightningatm-setup/wallet-setup/lntxbot#installing-lntxbot)).

First, let's find out what the URL, username and password of the API is, so we can talk to it. Send the command `/lightningatm` to your Lntxbot and you will get back a QR code and some text. The text comes back in the following format:

* username:password@url_of_lntxbot

### username:password
You won't be able to distinguish here between username and password because it has already been encoded in the base64 format. However, before that, it was actually a separate username and password.

If you type `/bluewallet`into your Lntxbot, you will get to see your username and password (don't get confused about the command "bluewallet", this is just because Lntxbot uses a piece of software from bluewallet called [LndHUB](https://bluewallet.io/lndhub/) for the accounting).

The 5 digit number between `lndhub://` an the colon is your username. The long string between the colon and the `@` symbol is your password. What follows after the `@` symbol is the base URL.

Let's take the username and the password and convert it into the base64 string from the `/lightningatm` command and we'll see that they match. Log into your Raspberry Pi and execute the following command:

```text
echo -ne "password:password" | base64 --wrap 0
```







&lt; &gt;
lndhub://42546:04d16c4cd379e82dc46591daafa494ca40b76f51815b5a39d8b0db9e3eee003b@https://lntxbot.bigsun.xyz



{% hint style="info" %}
Make sure, you have finished the hardware video part 3, before you attempt to setup your wallet \([https://www.youtube.com/watch?v=A9JKUQvvmYM](https://www.youtube.com/watch?v=A9JKUQvvmYM)\)
{% endhint %}



###
