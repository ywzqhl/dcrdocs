# The Paymetheus Windows Wallet

This guide assumes you have already set up a Paymetheus wallet using [this guide](paymetheus.md).

---

## Overview

The overview tab gives a quick summary of your total DCR (spendable and locked), number of accounts and transactions as well as a list
of recent account activity.  

![Overview tab](/img/Paymetheus-overview.png)  

---

## Accounts   

The accounts tab shows you the accounts in your wallet and allows you to add new ones.
Accounts in Decred work just like bank accounts.
They allow you to keep separate records of your DCR. This feature is most
useful for those who run businesses and wish to keep separate accounts for
tax records for example. Transferring DCR across accounts will create a
transaction on the blockchain.  

![Overview tab](/img/Paymetheus-accounts.png)  

---

## Scripts

Currently only used for PoS mining in a pool. As of version 0.8.0
script setup has been automated. See the Purchase Tickets section below for more information.
It will be used for more advanced features in the future.  

![Scripts tab](/img/Paymetheus-import-script.png)  

---

## Create Transaction

This tab is how you send funds to another address. Simply copy the receiver's
address into the text box and type in the amount of Decred you wish to send.
The estimated fee will be listed as well. You can click the '+' button to
send Decred to multiple addresses in the one transaction if you wish.  

![Create transaction tab](/img/Paymetheus-send.png)  

---

## Purchase Tickets tab

Paymetheus is able to buy tickets for Proof of Stake mining by using its manual ticket
purchasing features. Note that Paymetheus can only *purchase* tickets, it can't do the
actual voting. For that you will either need to setup [solo PoS](/mining/proof-of-stake.md)
or use a PoS [stake pool](/mining/proof-of-stake.md#list-of-stakepools).

> To join the pool, provide a public key address which can be used to generate a
> 1-of-2 multisignature script. The multisignature script will be generated by
> the pool and returned to you along with a P2SH address to give voting rights to.  

Don't worry if you didn't understand that quote. What it means is that you create
an address that can be accessed by two wallets. Only one wallet needs to be available
to use the address. This means that the pool can vote on your behalf and you can vote
using your own wallet if the pool stops working.  

It DOES NOT give the pool access to your funds. All you are doing is granting voting
rights to the pool. The pool does not touch your funds.

Official stake pools are [listed here](/mining/proof-of-stake.md#list-of-stakepools).
All stake pools run the same basic code, but may differ in the amount of redundancy available.
More redundancy equals less chance of missed votes (although all pools will have missed votes
as many missed votes are caused by PoW miners (sometimes they will find a solution to the blocks
so quickly that votes haven't had time to propagate around the network). In order to ensure one pool
does't become too large, it is recommended that you join a smaller pool. While a pool can't access your funds,
they CAN choose to vote against your wishes. Doing so would have them blacklisted pretty quickly, but
keeping individual pool sizes low means that any rogue operators would have a hard time affecting
the outcome of any vote. By spreading tickets around pools, it makes the network even more decentralized.

![Creating voting account](/img/Paymetheus-create-voting-account.png)

There's a fair bit of information here, so we'll go through each of the options.

* **Ticket difficulty** - The current price of a ticket.
* **Blocks until retarget** - When this reaches 0, a new ticket price is calculated.
* **Source account** - This is the account that will purchase the tickets and receive the reward.
* **Tickets to purchase** - The number of tickets to purchase.
* **Ticket fee (DCR/kB)** - Tickets are entered into the voting pool by order of their fee. In times of high demand,
                        you will need to increase this value in order to have your tickets accepted.
                        You can view current ticket fees [here](https://www.dcrstats.com).
* **Split fee (DCR/kB)** - Paymetheus uses a "split" transaction to avoid blocking your balance, splitting the
                       exact amount needed for the ticket from the balance in your wallet. The "split" transaction
                       needs to be confirmed at least once before you can reuse your balance. This can block your
                       whole balance for several minutes while this confirmation occurs. Without the split, you
                       would have to wait for the confirmation of the ticket transaction, which could take several hours.
                       This can be left at 0.01. It does not affect your chances of buying tickets or voting with them.

* **Expiry (blocks)** - Often ticket fees will increase during a window and you may be stopped out by higher fees. By setting an expiry, tickets that are not mined by the given block height are cancelled so you can try again with higher fees if you wish. If this is empty, they will not expire until the end of the window.

* **Stake pool preference** - Automate setup with PoS pools. See below for more information.
* **Voting address** - The Decred address that will do the voting. Solo and custom pool miners only.
* **Pool fee address** - For those using a custom pool.
* **Pool fees (%)** - For those using a custom pool.

![Purchasing tickets](/img/Paymetheus-ticket-purchasing.png)  

To easily set up ticket purchasing for a stake pool, click the 'Manage pools button'. If you haven't already,
you'll need to register with a stake pool (see above). Once you've registered, log in, look for your API key, and copy it.
Select the pool you just registered with from the drop down. Paste the key into the 'API key' box and click 'Save'.
You should see a bunch of letters and numbers appear in the bottom box. Click 'Close'. You can now purchase
tickets by clicking the 'Purchase' button!

![Manage stake pools](/img/Paymetheus-manage-stake-pool.png)

NOTE: While you can purchase tickets using Paymetheus, it cannot vote for you so you must either use a pool
or run your own voting wallet which needs to be online 24/7. If you would prefer to solo mine,
check the [dcrd Setup Guide](/getting-started/user-guides/dcrd-setup.md), [dcrwallet Setup Guide](/getting-started/user-guides/dcrd-setup.md) and [PoS Mining Guide](/mining/proof-of-stake.md) for more information.

---

## Request Payment

This is where you can generate wallet addresses to give to other people so they can
send you DCR. Simply choose the account you want funds to go to and press Generate Address.
Copy the address (it's the top line that starts with Ds) and share that with the other person.
Decred addresses can be used as many times as you want, but for privacy reasons it's best
to generate a new one for each transaction. There's around 1.4E48 (that's 14 followed by 47 zeroes)
addresses available so you don't need to worry about running out.

![Request Payment](/img/Paymetheus-receive.png)  

---

## Transaction History

This tab shows a list of all transactions that have occurred. The transaction hash can be used with the
[block explorer](/getting-started/using-the-block-explorer.md) to see more information about the transaction.  

![Transaction History](/img/Paymetheus-transactions.png)  

---

## Stake Mining

This tab shows some statistics on the PoS network:  

Item                         | Description
:-----------------------------:|:------------------------------------------------------------:
Number of live tickets       | The total number of tickets that are eligible for voting across the network
Number of tickets in mempool | The total number of tickets waiting to enter the voting pool
Ticket difficulty            | The cost of a ticket (refunded on ticket vote/expiry)
Owned tickets in mempool     | The number of your tickets in the mempool
Owned live tickets           | The number of your tickets that are eligible for voting
Owned immature tickets       | Number of tickets waiting to mature before going live (256 blocks, ~17 hours)
Tickets missed               | Tickets that missed a vote either because the voting wallet or stake pool was offline or the PoW miner didn't mine it properly
Tickets revoked              | Tickets that missed a vote and have had the ticket price refunded (minus the ticket fee), should be the same as tickets missed
Tickets voted                | Lifetime tickets voted by this wallet
Total subsidy earned         | Lifetime DCR subsidy earned by this wallet
