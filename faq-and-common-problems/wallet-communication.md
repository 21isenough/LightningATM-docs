---
description: >-
  This section will answer some questions in regards to how the ATM communicates
  with the wallets that you connect it to. We'll be looking into API calls and
  what actually happens "under the hood".
---

# Wallet Communication

## 🔈How the ATM "talks"

When someone uses the LightningATM, they insert a certain amount of coins into the ATM and expect bitcoin / satoshis back for it \(from now on, I'll just simply write "satoshis", the smallest denomination of one bitcoin\). The ATM must therefore be connected to a Lightning Wallet ⚡ from which it sends satoshis to the person who has inserted the coins.

To ATM doesn't have any satoshis "on it". It will always have to "communicate" to a Lightning Wallet over a network and tell the wallet to send the satoshis. This communication is happening over an API \([Application Programming Interface](https://www.freecodecamp.org/news/what-is-an-api-in-english-please-b880a3214a82/)\) of a Lightning Wallet.

APIs can be talked to in various ways. Most often the ATM will talk to them through a URL. Almost all API communication also requires a username and a password 🔑 .

1. The API might be accessed at [https://my-lightning-wallet.com/api](https://my-lightning-wallet.com/api)
2. To prove that the ATM is allowed to use this API, it will have to provide a username and a password

It's therefore clear that we have to store this information \(URL, username and password\) on the ATM. The easiest way to do this, is by encoding all that information into a QR code and showing it to the camera of the ATM \([as explained here](https://docs.lightningatm.me/lightningatm-setup/wallet-setup/lnd_btcpay#connecting-to-the-atm)\).

The ATM will then read the content of the QR code and store those three pieces of information in a configuration file. From then on, it uses that information to talk to that Lightning Wallet to facilitate payouts and other communication like requesting the current state of the Lightning Wallet such as "balance" or "channel information".

## 🖥 API endpoint, usernames and passwords

Let's take a closer look at the kind of information that is needed to talk to the API of a Lightning Wallet. Be aware that these pieces of information come in various shapes and encodings.

The URL to access an API might contain an IP address or a domain and can have a multitude of different paths \(called "API endpoints"\). Some examples:

* [https://my-lightning-wallet.com/api/payinvoice](https://my-lightning-wallet.com/api/payinvoice)
* [https://api.my-lightning-wallet.com/v1/channelbalance](https://api.my-lightning-wallet.com/v1/channelbalance)
* [https://localhost:8080/v1/payments](https://localhost:8080/v1/payments)
* [https://btcpayserver.mydomain.me/v1/balance/blockchain](https://btcpayserver.mydomain.me/v1/balance/blockchain)

The URL to which your ATM will be talking to, depends on the software of the Lightning Wallet and the location where the wallet is "run" or operated \(maybe a LND Lightning Node/Wallet on a [RaspiBlitz](https://github.com/rootzoll/raspiblitz) or a [BTCPayServer](https://github.com/btcpayserver/btcpayserver-docker)\).

The username and password might need to be supplied as you're used to it from logging into websites but could as well be encoded in a [hexadecimal](https://www.lifewire.com/what-is-hexadecimal-2625897) or [base64](https://base64.guru/learn/what-is-base64) string.

## 👩💻 Talking to an API in practice

Now, let's get a little bit more practical and actually talk to an API. For this example, I'll be using the API of the Lntxbot because it is available to everyone with Telegram no their phone and can easily be followed along \(more information on how to install Lntxbot can [be found here](https://docs.lightningatm.me/lightningatm-setup/wallet-setup/lntxbot#installing-lntxbot)\).

First, let's find out what the URL, username and password of the API is, so we can talk to it. Send the command `/lightningatm` to your Lntxbot and you will get back a QR code and some text. The text comes back in the following format:

* &lt;username:password&gt;@&lt;url\_of\_lntxbot&gt;

### &lt;username:password&gt;

You won't be able to distinguish here between username and password because it has already been encoded in the base64 format. However, before that, it was actually a separate username and password.

If you type `/bluewallet` into your Lntxbot, you will get to see your username and password \(don't get confused about the command "bluewallet", this is just because Lntxbots API is compatible with a piece of software from bluewallet called [LndHUB](https://bluewallet.io/lndhub/).

The 5 digit number between `lndhub://` an the `:` is your username. The long string between the `:` and the `@` symbol is your password.

Let's take the username and the password and convert it into the base64 string from the `/lightningatm` command and we'll see that they match. Log into your Raspberry Pi and execute the following command:

```text
echo -ne "<username:password>" | base64 --wrap 0
```

Now you can go back to the result that you've gotten from the `/lightningatm` command and you will see that this result is the same. You just manually encoded your username and password in base64 with the above command.

### &lt;url\_of\_lntxbot&gt;

What follows after the `@` symbol from the `/bluewallet` command is the base URL. This URL needs to be appended with the API endpoint that we want to call. This might be `/balance` or `/payinvoice` depending on the action that we want to execute.

We will now request the balance from our Lntxbot through the command line with the `/balance` endpoint. Your base URL is most likely `https://lntxbot.bigsun.xyz` so the final URL the we want to call is `https://lntxbot.bigsun.xyz/balance`.

We are going to do that with the command line tool called `cURL` \(client for URLs\). Not only do we need to call the correct URL but we also have to supply the username and password. Username and password will be sent in the base64 encoded format \(as you've done above and can get from the `/lightningatm` command\). It will be sent in what is called the [http header](https://www.geeksforgeeks.org/http-headers/) of this request.

```text
curl -H "Authorization: Basic <BASE64_ENCODED_PASS_AND_USERNAME>" https://lntxbot.bigsun.xyz/balance
```

This command will make a request to the URL at the end and supply your username and password in the http header and back comes - your current balance in the Lntxbot \(in json format\).

## Summary

You've just manually done a HTTP request to an API endpoint and supplied your username and password as a base64 encoded string in the header of the request. Bravo 🥳🎉 .

And that is all the ATM really does when it comes to "talking with Lightning Wallets ⚡ ". Different wallets have different APIs and therefore different URLs and endpoints. Some might want the username and password to be sent in base64 or HEX encoding. In the case of LND the "username and password" takes the form of a `cookie` that is called a `macaroon` and has to be sent in its HEX format \[\(more info here\)\([https://github.com/lightningnetwork/lnd/blob/master/docs/macaroons.md\#macaroon-delegation](https://github.com/lightningnetwork/lnd/blob/master/docs/macaroons.md#macaroon-delegation)\)\].

As mentioned above: When you show the QR code with your wallet information to the ATMs camera and it scans it, it will use that information later in various API calls as you or others interact with the ATM. It stores these details in the configuration file of your ATM, which you can take a look at when you run the command `nano ~/.lightningATM/config.ini`.

Happy satoshi buying!! 💰 

{% hint style="info" %}
Take a look at the source code of the ATM where we request the balance for the ATM in python rather than through the command line here: [Requesting Lntxbot balance in python](https://github.com/21isenough/LightningATM/blob/a35a0a128f016620a27b2c03b7539439fc396fdf/lntxbot.py#L80)
{% endhint %}

